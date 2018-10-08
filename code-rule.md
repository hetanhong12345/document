##  HTML 代码规范
* HTML文件必须加上 DOCTYPE 声明，并统一使用 HTML5 的文档声明：
```html
<!DOCTYPE html>
```
* 统一使用 “UTF-8” 编码
```html
<meta charset="UTF-8">
```

* 所有具有开始标签和结束标签的元素都要写上起止标签，某些允许省略开始标签或和束标签的元素亦都要写上。


_推荐:_
```html
<div>
    <h1>我是h1标题</h1>
    <p>我是一段文字，我有始有终，浏览器能正确解析</p>
</div>
	

```
  

_不推荐:_
```html
<div>
    <h1>我是h1标题</h1>
    <p>我是一段文字，我有始无终，浏览器亦能正确解析
</div>

```
* HTML标签名、类名、标签属性和大部分属性值统一用小写
  
_推荐：_
```html
<div class="demo"></div>
```
_不推荐：_
```html
<div class="DEMO"></div>
	
<DIV CLASS="DEMO"></DIV>
```

* 元素属性值使用双引号语法
* 元素属性值可以写上的都写上
_推荐：_
```html
<input type="text">
	
<input type="radio" name="name" checked="checked" >
```
_不推荐：_
```html
<input type=text>	
<input type='text'>
	
<input type="radio" name="name" checked >
```
* 特殊字符引用
* 在 HTML 中不能使用小于号 “<” 和大于号 “>”特殊字符，浏览器会将它们作为标签解析，若要正确显示，在 HTML 源代码中使用字符实体
_推荐：_

```html

<a href="#">more&gt;&gt;</a>

```
_不推荐：_
```html
<a href="#">more>></a>

```
* 统一使用四个空格进行代码缩进，使得各编辑器表现一致（各编辑器有相关配置）

```html
<div class="jdc">
    <a href="#"></a>
</div>
```

* 元素嵌套规范，每个块状元素独立一行，内联元素可选

_推荐：_
```html
<div>
    <h1></h1>
    <p></p>
</div>	
```
_不推荐：_
```html
<div>
    <h1></h1><p></p>
</div>	
```

* 段落元素与标题元素只能嵌套内联元素

_推荐：_
```html
<h1><span></span></h1>
<p><span></span><span></span></p>
```
_不推荐：_
```html
<h1><div></div></h1>
<p><div></div><div></div></p>
```
### 单行注释
* 一般用于简单的描述，如某些状态描述、属性描述等
* 注释内容前后各一个空格字符，注释位于要注释代码的上面，单独占一行

```html
<!-- Comment Text -->
<div>...</div>
```
### 模块注释
* 一般用于描述模块的名称以及模块开始与结束的位置
* 注释内容前后各一个空格字符，<!-- S Comment Text --> 表示模块开始，<!-- E Comment Text --> 表示模块结束，模块与模块之间相隔一行
```html
<!-- S Comment Text A -->	
<div class="mod-a">
    ...
</div>
<!-- E Comment Text A -->
	
<!-- S Comment Text B -->	
<div class="mod-b">
    ...
</div>
<!-- E Comment Text B -->
```

### 文件模板
* html5 标准模板
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<title>HTML5标准模版</title>
</head>
<body>
	
</body>
</html>
```
* 移动端模板
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, shrink-to-fit=no" >
<meta name="format-detection" content="telephone=no" >
<title>移动端HTML模版</title>
	

</head>
<body>
</body>
</html>
```

* pc端模板
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="keywords" content="your keywords">
<meta name="description" content="your description">
<meta name="author" content="author,email address">
<meta name="robots" content="index,follow">
<meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">
<meta name="renderer" content="ie-stand">
<title>PC端HTML模版</title>

</head>
<body>
</body>
</html>
```
## css/less 规范
* 样式文件必须写上 @charset 规则，并且一定要在样式文件的第一行首个字符位置开始写，编码名用 “UTF-8”
```less
@charset "UTF-8";
.ipalfish{}
```
* 统一使用展开格式书写样式
* 样式书写一般有两种：一种是紧凑格式 (Compact)
```less
@charset "UTF-8";
.ipalfish{ display: block;width: 50px;}
```
* 一种是展开格式（Expanded）

```less
@charset "UTF-8";
.ipalfish{
    display: block;
    width: 50px;
}
```
* 推荐使用展开式

* 样式选择器，属性名，属性值关键字全部使用小写字母书写，属性字符串允许使用大小写。
```less
/* 推荐 */
.ipalfish{
	display:block;
}
	
/* 不推荐 */
.IPALFISH{
	DISPLAY:BLOCK;
}
```

* 统一使用四个空格进行代码缩进，使得各编辑器表现一致（各编辑器有相关配置）
* 每个属性声明末尾都要加分号；
```less
.ipalfish {
    width: 100%;
    height: 100%;
}
```
* 属性值十六进制数值能用简写的尽量用简写
```less
/* 推荐 */
.ipalfish {
    color: #fff;
}
/* 不推荐 */
.ipalfish {
    color: #ffffff;
}
```
* 不要为 0 指明单位
```less
/* 推荐 */
.ipalfish {
    margin: 0;
}
/* 不推荐 */
.ipalfish {
     margin: 0rem;
}
```
* 不需要为浏览器添加前缀
```less
/* 推荐 */
.ipalfish {
   
    border-radius: 10px;
}
/* 不推荐 */
.ipalfish {
    -webkit-border-radius: 10px;
    -moz-border-radius: 10px;
    -o-border-radius: 10px;
    -ms-border-radius: 10px;
    border-radius: 10px;
}
```
* 可复用属性尽量抽离为页面变量，易于统一维护

```less
@color-text: #333; //主标题
@color-text-secondary: #666; // 内容
@color-text-gray:#999; // 副标题
@color-split: #d8d8d8; //分割线的颜色

```
### 单行注释
* 注释内容第一个字符和最后一个字符都是一个空格字符，单独占一行，行与行之间相隔一行

```less
/* Comment Text */
.palfish{}

/* Comment Text */
.palfish{}

```
### 模块注释
* 注释内容第一个字符和最后一个字符都是一个空格字符，/* 与 模块信息描述占一行，多个横线分隔符-与*/占一行，行与行之间相隔两行

```less
/* Module A
---------------------------------------------------------------- */
.mod-a {}


/* Module B
---------------------------------------------------------------- */
.mod-b {}

```

### 文件信息注释
* 在样式文件编码声明 @charset 语句下面注明页面名称、作者、创建日期等信息

```less
@charset "UTF-8";
/**
 * @desc File Info
 * @author Author Name
 * @date 2015-10-10
 */

```

## 命名规范
### 目录命名

* 项目文件夹：projectname
* 样式文件夹：css/less
* 脚本文件夹：js
* 样式类图片文件夹：images
* 容器文件夹：containers
* 组件文件夹：components
### 图片命名
   
模块+功能，比如
   
login-password.png

### `**html/css/less文件命名（强制）**`

* 确保文件命名总是以字母开头而不是数字，且字母一律小写，以-连接且不带其他标点符号，如：
```
login.html
personal-center.html

login.less
personal-center.less
```

### `**className 命名（强制）**`
* 模块+功能 （中间用横线链接，不可出现大写字母）
```less
.login{
    .text-center{
     ...
    }
}
```

## javascript规范

### `**命名（强制）**`
* 类、组件、全局变量、常量、构造函数使用大驼峰式命名法：单字的首字母大写，例如：Swiper、Message
* 函数、方法、变量使用小驼峰式命名法：第一个单字以小写字母开始；第二个单字的首字母大写，例如：dispatch、lastName

### 注释
```
/**
 * @method
 * @param  参数
 * @returns 返回值
 * @desc 函数功能
 */
function doSomething(value, message){
    ...
    return '返回对象'
}
```
### `**引用（强制）**`
* const 和 let 都是块级作用域，var 是函数级作用域
* 对所有不可变引用都使用 const，不要使用 var
***


```js
// bad
var A = 1
var B = 2
// good
const A = 1
const B = 2

```
* 如果引用是可变动的，则使用 let

```js
// bad
var count = 1
if (count < 10) {
  count += 1
}
// good
let count = 1
if (count < 10) {
  count += 1
}

```
### 对象
* 请使用字面量值创建对象
```js

// bad
const A = new Object()
// good
const A = {}

```

* 别使用保留字作为对象的键值
```js
// bad
const A = {
  default: {},  // default 是保留字
  common: {}
}
// good
const A = {
  defaults: {},
  common: {}
}

```

* 请使用对象方法的简写方式

```js

// bad
const Item = {
  value: 1,
  addValue: function (val) {
    return Item.value + val
  }
}
// good
const Item = {
  value: 1,
  addValue(val) {
    return Item.value + val
  }
}
```
* 请使用对象属性值的简写方式

```js
let job = 'FrontEnd'
// bad
const Item = {
  job: job
}
// good
const Item = {
  job
}
```
* 对象属性值的简写方式要和声明式的方式分组

```js
let job = 'FrontEnd'
let department = 'JDC'
// bad
const Item = {
  sex: 'male',
  job,
  age: 25,
  department
}
// good
const Item = {
  job,
  department,
  sex: 'male',
  age: 25
}
```

* 请使用字面量值创建数组
```js
// bad
let Items = new Array()
// good
let items = []
```
* 向数组中添加元素时，请使用 push 方法
```js
let items = []
// bad
items[items.length] = 'test'
// good
items.push('test')

```
* 使用拓展运算符 ... 复制数组

```js
// bad
let items = []
let itemsCopy = []
let len = items.length
let i
// bad
for (i = 0; i < len; i++) {
  itemsCopy[i] = items[i]
}
// good
itemsCopy = [...items]
```
* 使用数组的 map 等方法时，请使用 return 声明，如果是单一声明语句的情况，可省略 return
```js
// good
[1, 2, 3].map(x => {
  let y = x + 1
  return x * y
})
// good
[1, 2, 3].map(x => x + 1)




```
* 当需要使用对象的多个属性时，请使用解构赋值
```js
// bad
function getFullName (user) {
  let firstName = user.firstName
  let lastName = user.lastName
  return `${firstName} ${lastName}`
}
// good
function getFullName (user) {
  let { firstName, lastName } = user
  return `${firstName} ${lastName}`
}
// better
function getFullName ({ firstName, lastName }) {
  return `${firstName} ${lastName}`
}
```

* 当需要使用数组的多个值时，请同样使用解构赋值
```js
let arr = [1, 2, 3, 4]
// bad
let first = arr[0]
let second = arr[1]
// good
let [first, second] = arr

```


* 字符串统一使用单引号的形式 ''

```js
// bad
let department = "JDC"
// good
let department = 'JDC'
```

* 程序化生成字符串时，请使用模板字符串
```js
let test = 'test'
// bad
let str = ['a', 'b', test].join()
// bad
let str = 'a' + 'b' + test
// good
let str = `ab${test}`
```


* 不要使用 arguments，可以选择使用 ...
```js
// bad
function test () {
  let args = Array.prototype.slice.call(arguments)
  return args.join('')
}
// good
function test (...args) {
  return args.join('')
}
```

* 使用 class，避免直接操作 prototype
```js
// bad
function Queue (contents = []) {
  this.queue = [..contents]
}
Queue.prototype.pop = function () {
  const value = this.queue[0]
  this.queue.splice(0, 1)
  return value
}
// good
class Queue {
  constructor (contents = []) {
    this.queue = [...contents]
  }
  pop () {
    const value = this._queue[0]
    this.queue.splice(0, 1)
    return value
  }
}
```
* 使用标准的 ES6 模块语法 import 和 export

```js
// bad
import * as Util from './util'

// good
import Util from './util'

```

* 声明变量时，请使用 const、let 关键字，如果没有写关键字，变量就会暴露在全局上下文中，这样很可能会和现有变量冲突，另外，也很难明确该变量的作用域是什么。这里推荐使用 const 来声明变量，我们需要避免全局命名空间的污染。

```js
// bad
MyDemo = new Demo()
// good
const MyDemo = new Demo()

```




* 多个if else 条件分支请使用return

``` js

// bad
if(conditionOne){
    doSomething();
}else if(conditionTwo){
    doElse();
}else{
    doOther()
}

// good 
if(conditionOne){
    doSomething();
    return;
}
if(conditionTwo){
    doElse();
    return;
}
doOther()

```

