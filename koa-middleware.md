## koa-middleware

### 中间件

* middleware 称之为中间件，是 Koa 中一个非常重要的概念，利用中间件，可以很方便的处理用户的请求，比如log，bodyparser；
* 中间件格式为一个高阶函数，外部的函数接收一个 options 参数，这样方便中间件提供一些配置信息；
* 内部函数是一个async函数，接收两个参数ctx，next；
* ctx为请求上下文，next将请求扔给下一个中间件处理。

### 常见的koa中间件实例

```js

// log info 
const log =(level='debug')=>{
    return async (ctx,next) => {
       console.debug(`request url is ${ctx.url}`);
       next()
        
    };
};

// 404 not found
const page404 = () => {
    return async (ctx) => {
        ctx.body = {code: 404, msg: 'not found'};
    }
};

```

### 使用中间件

```js
const Koa = require('koa');
const app = new Koa();
app.use(log('debug'));
app.use(page404())

```
* koa 实例有如下属性 

```js

constructor() {
    super();

    this.proxy = false;
    this.middleware = []; //存放中间件的数组
    this.subdomainOffset = 2;
    this.env = process.env.NODE_ENV || 'development';
    this.context = Object.create(context);
    this.request = Object.create(request);
    this.response = Object.create(response);
  }

```
* app.use 将async function 添加到 middleware数组中 

```js
use(fn) {
   
    this.middleware.push(fn); //添加到 middleware数组中
    return this;
  }
 ``` 
 
 * 通过函数 compose 将中间件组合起来，并且将请求交给第一个中间件处理
 
 ```js
 
 
 function compose (middleware) {
  


  return function (context, next) {
    // last called middleware #
    let index = -1
    return dispatch(0) // 将请求交给第一个中间件处理
    function dispatch (i) {
      if (i <= index) 
      // 如果同一个中间件 多次调用 next ，抛出错误
      return Promise.reject(new Error('next() called multiple times'))
      
      index = i
      let fn = middleware[i]
      if (i === middleware.length) fn = next
      if (!fn) return Promise.resolve() // 所有中间件都处理完毕 ，返回。
      try {
        return Promise.resolve(fn(context, function next () {
          return dispatch(i + 1) // 当前中间件处理完后 ，交给下一个中间件处理
        }))
      } catch (err) {
        return Promise.reject(err)
      }
    }
  }
}
 
 ```
 
 ## koa-router
 
 ### 基本特性
 
 * router 数据格式
 
 ```js
 function Router(opts) {
  ...
  this.methods = this.opts.methods || [
    'HEAD',
    'OPTIONS',
    'GET',
    'PUT',
    'PATCH',
    'POST',
    'DELETE'
  ];
  this.stack = []; // ？？
};
```
 * 路由名称根据URL生成
 * 路由名称支持正则
 
 * router.register注册请求
 
 ```js
 Router.prototype.register = function (path, methods, middleware, opts) {
  opts = opts || {};

  var router = this;
  var stack = this.stack;
  ...

  // create route
  var route = new Layer(path, methods, middleware, {
   ...
  });

  ...

  stack.push(route); //将route 存入stack中

  return route;
};
 
 ```
 * 使用router.get,  router.post等方式注册路由
 * router.get,router.post,router.all都将调用router.register

 
 ```js
 router.post('/login', async (ctx ,next) => {
    console.log('login');
    return next();
});
 ```
 
 * 通过compose方法将所有子路由的stack组合成 router.routes()
 
 ```js
 Router.prototype.routes = Router.prototype.middleware = function () {
  var router = this;

  var dispatch = function dispatch(ctx, next) {
    ...

    layerChain = matchedLayers.reduce(function(memo, layer) {
      memo.push(function(ctx, next) {
        ctx.captures = layer.captures(path, ctx.captures);
        ctx.params = layer.params(path, ctx.captures, ctx.params);
        ctx.routerName = layer.name;
        return next();
      });
      return memo.concat(layer.stack); //将多个子router的 stack 合并
    }, []);

    return compose(layerChain)(ctx, next); // 组合函数 ，返回router注册的第一个方法
  };

  dispatch.router = this;

  return dispatch;
};
 
 ```
 * router.allowedMethods(),检查请求方法是否允许
 
 ```js
 Router.prototype.allowedMethods = function (options) {
  options = options || {};
  var implemented = this.methods;

  return function allowedMethods(ctx, next) {
    return next().then(function() {
        var allowed = {};
        ...
        // 请求方法不被允许
        if (!~implemented.indexOf(ctx.method)) {
          ...
          ctx.status = 501;
          ctx.set('Allow', allowedArr.join(', '));
      }
    });
  };
};
 
 ```

 * 支持路由嵌套
 
 ```js
 const router = new Router();
 const user = new Router();
 const trade = new Router();
 // user router
 user.post('/login', async (ctx ,next) => {
    console.log('login');
    return next();
});

// trade router
trade.post('/recharge', async (ctx) => {
    ctx.body = 'ok';
});

// root router
 router.use('/user', user.routes(), user.allowedMethods());
 router.use('/trade', trade.routes(), trade.allowedMethods());
 
 ```
 * 路由中间件
 
 ```js
 
  const app = new Koa();
  
  // 挂在跟路由中间件
  app.use(router.routes()).use(router.allowedMethods());
  
 ``` 



