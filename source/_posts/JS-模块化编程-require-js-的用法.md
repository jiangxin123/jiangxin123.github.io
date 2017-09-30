---
title: JS 模块化编程 require.js 的用法
date: 2017-08-30 13:43:00
tags: 
	- js 
	- require.js
---
## 什么是RequireJS?
>RequireJS 是一个JavaScript模块加载器。它非常适合在浏览器中使用, 但它也可以用在其他脚本环境, 就像 Rhino and Node. 使用RequireJS加载模块化脚本将提高代码的加载速度和质量。
## 为什么用RequireJS?

 1. 异步“加载”。我们知道，通常网站都会把script脚本的放在html的最后，这样就可以避免浏览器执行js带来的页面阻塞。使用RequireJS，会在相关的js加载后执行回调函数，这个过程是异步的，所以它不会阻塞页面。
 2. 按需加载。通过RequireJS，你可以在需要加载js逻辑的时候再加载对应 的js模块，这样避免了在初始化网页的时候发生大量的请求和数据传输，或许对于一些人来说，某些模块可能他根本就不需要，那就显得没有必要。
 3. 更加方便的模块依赖管理。相信你曾经一定遇到过因为script标签顺序问题而导致依赖关系发生错误，这个函数未定义，那个变量undefine之类的。通过RequireJS的机制，你能确保在所有的依赖模块都加载以后再执行相关的文件，所以可以起到依赖管理的作用。
 4. 更加高效的版本管理。想一想，如果你还是用的script脚本引入的方式来引入一个jQuery2.x的文件，然后你有100个页面都是这么引用的，那当你想换成jQuery3.x，那你就不得不去改这100个页面。但是如果你的requireJS有在config中做jQuery的path映射，那你只需要改一处地方即可。
 5. 当然还有一些诸如cdn加载不到js文件，可以请求本地文件等其它的优点，这里就不一一列举了。


<!--more-->
## require.js的加载
使用require.js的第一步，是先去官方网站下载最新版本。
下载后，假定把它放在js子目录下面，就可以加载了。

```
<script src="js/require.js"></script>
```
加载require.js以后，下一步就要加载我们自己的代码了。假定我们自己的代码文件是main.js，也放在js目录下面。那么，只需要写成下面这样就行了：

```
<script src="js/require.js" data-main="js/main"></script>
```
data-main属性的作用是，指定网页程序的主模块。在上例中，就是js目录下面的main.js，这个文件会第一个被require.js加载。由于require.js默认的文件后缀名是js，所以可以把main.js简写成main。

## 主模块的写法
上一节的main.js，我把它称为"主模块"，意思是整个网页的入口代码。它有点像C语言的main()函数，所有代码都从这儿开始运行。
下面就来看，怎么写main.js。

```
// main.js
require(['moduleA', 'moduleB', 'moduleC'], function (moduleA, moduleB, moduleC){
　　// some code here
});
```
require()函数接受两个参数。第一个参数是一个数组，表示所依赖的模块，上例就是['moduleA', 'moduleB', 'moduleC']，即主模块依赖这三个模块；第二个参数是一个回调函数，当前面指定的模块都加载成功后，它将被调用。加载的模块会以参数形式传入该函数，从而在回调函数内部就可以使用这些模块。
require()异步加载moduleA，moduleB和moduleC，浏览器不会失去响应；它指定的回调函数，只有前面的模块都加载成功后，才会运行，解决了依赖性的问题。
下面，我们看一个实际的例子。
假定主模块依赖jquery、underscore和backbone这三个模块，main.js就可以这样写：

```
require(['jquery', 'underscore', 'backbone'], function ($, _, Backbone){
　　// some code here
});

```
## 模块的加载
上一节最后的示例中，主模块的依赖模块是['jquery', 'underscore', 'backbone']。默认情况下，require.js假定这三个模块与main.js在同一个目录，文件名分别为jquery.js，underscore.js和backbone.js，然后自动加载。
使用require.config()方法，我们可以对模块的加载行为进行自定义。require.config()就写在主模块（main.js）的头部。参数就是一个对象，这个对象的paths属性指定各个模块的加载路径。

```
　　require.config({
　　　　paths: {
　　　　　　"jquery": "jquery.min",
　　　　　　"underscore": "underscore.min",
　　　　　　"backbone": "backbone.min"
　　　　}
　　});
```
上面的代码给出了三个模块的文件名，路径默认与main.js在同一个目录（js子目录）。如果这些模块在其他目录，比如js/lib目录，则有两种写法。一种是逐一指定路径。

```
　　require.config({
　　　　paths: {
　　　　　　"jquery": "lib/jquery.min",
　　　　　　"underscore": "lib/underscore.min",
　　　　　　"backbone": "lib/backbone.min"
　　　　}
　　});
```
另一种则是直接改变基目录（baseUrl）。

```
　　require.config({
　　　　baseUrl: "js/lib",
　　　　paths: {
　　　　　　"jquery": "jquery.min",
　　　　　　"underscore": "underscore.min",
　　　　　　"backbone": "backbone.min"
　　　　}
　　});
```
## AMD模块的写法

require.js加载的模块，采用AMD规范。也就是说，模块必须按照AMD的规定来写。
具体来说，就是模块必须采用特定的define()函数来定义。如果一个模块不依赖其他模块，那么可以直接定义在define()函数之中。
假定现在有一个math.js文件，它定义了一个math模块。那么，math.js就要这样写：

```
　　// math.js
　　define(function (){
　　　　var add = function (x,y){
　　　　　　return x+y;
　　　　};
　　　　return {
　　　　　　add: add
　　　　};
　　});
```
加载方法如下：

```
　　// main.js
　　require(['math'], function (math){
　　　　alert(math.add(1,1));
　　});
```
如果这个模块还依赖其他模块，那么define()函数的第一个参数，必须是一个数组，指明该模块的依赖性。

```
　　define(['myLib'], function(myLib){
　　　　function foo(){
　　　　　　myLib.doSomething();
　　　　}
　　　　return {
　　　　　　foo : foo
　　　　};
　　});
```
当require()函数加载上面这个模块的时候，就会先加载myLib.js文件

## 加载非规范的模块
理论上，require.js加载的模块，必须是按照AMD规范、用define()函数定义的模块。但是实际上，虽然已经有一部分流行的函数库（比如jQuery）符合AMD规范，更多的库并不符合。那么，require.js是否能够加载非规范的模块呢？
回答是可以的。
这样的模块在用require()加载之前，要先用require.config()方法，定义它们的一些特征。
举例来说，underscore和backbone这两个库，都没有采用AMD规范编写。如果要加载它们的话，必须先定义它们的特征。

```
　　require.config({
　　　　shim: {

　　　　　　'underscore':{
　　　　　　　　exports: '_'
　　　　　　},
　　　　　　'backbone': {
　　　　　　　　deps: ['underscore', 'jquery'],
　　　　　　　　exports: 'Backbone'
　　　　　　}
　　　　}
　　});
```
require.config()接受一个配置对象，这个对象除了有前面说过的paths属性之外，还有一个shim属性，专门用来配置不兼容的模块。具体来说，每个模块要定义（1）exports值（输出的变量名），表明这个模块外部调用时的名称；（2）deps数组，表明该模块的依赖性。
比如，jQuery的插件可以这样定义：

```
　　shim: {
　　　　'jquery.scroll': {
　　　　　　deps: ['jquery'],
　　　　　　exports: 'jQuery.fn.scroll'
　　　　}
　　}
```