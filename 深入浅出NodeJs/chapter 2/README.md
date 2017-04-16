# 模块机制

## 1.CommonJS规范
CommonJS对模块的定义十分简单，主要分为模块引用，模块定义和模块标识3个部分。
### 模块引用
```javascript
var math = require('math');
```

### 模块定义
在模块中上下文提供`require()`方法来引入外部模块。上下文提供了`exports`对象用于导出当前模块的方法和变量。
还存在一个`module`对象，代表模块自身，而exports是module的属性。
在Node中，一个文件就是一个模块，`将方法挂载在exports对象上作为属性即可以定义导出`。

```javascript
exports.add = funtion() {};
```

### 模块标识
模块标识就是传递给require()方法的参数，`必须符合小驼峰命名的字符串`或者以.或者..开头的相对路径或者局定路径，可以没有后缀js。


## 2.Node的模块实现
在Node中引入模块，需要经历3个步骤：
* 路径分析
* 文件定位
* 编译执行
Node中的模块分为两类：
* Node提供的`核心模块`
* 用户编写的`文件模块`
* 核心模块在Node源码编译过程中部分已经被肢解加载斤内存，所以引用过程中文件定位和编译执行这两个步骤可以忽略。
文件模块则是在运行时动态加载，需要完整的路径分析文件定位编译执行过程，速度较慢。

### 优先从缓存加载
Node对引入过的模块进行缓存，减少二次引入时的开销，Node会缓存编译和执行之后的对象。
require引用优先加载缓存。

### 模块编译
每个文件模块都是一个对象：
```javascript
function module(id, parent) {
    this.id = id;
    this.exports = {};
    this.parent =parent;
    if (parent && parent.children) {
        parent.children.push(this);
    }

    this.filename = null;
    this.loaded = false;
    this.children = [];

}
```
每个编译成功的模块都会将其文件路径作为索引缓存在Module._cache对象上，以提高二次引入的性能。
`根据不同的文件扩展名，Node会调用不同的读取方式。`
* JS文件
`为了避免污染全局变量，Node在编译的过程中对获取的JS文件内容进行了头尾包装`:
```javascript
(function (exports, require, module, __filename, __dirname) {
    //code
});
包装之后用`runInThisContext()`方法进行执行，返回一个function对象。
以这样的方式进行了作用域隔离。
```

* C++
调用`process.dlopen()`方法进行加载和执行。

* JSON
利用fs模块进行同步读区JSON文件，在用JSON.parse()得到对象。

## 3.核心模块
C/C++编写的模块放到src目录下，JS编写的放在lib目录下。

### JS核心模块编译过程
* 转存为C++代码
通过js2c.py工具。
将所有内置的JavaScript代码转换成C++里面的数组。
* 编译JS核心模块
也要经历头尾包装的过程，然后才知性和导出exports对象。
通过process.binding('native')取出，并且缓存到`NativeModule._cache`对象上.

### C++核心模块编译过程
`内建模块`：纯C／C++编写的部分，buffer，crypto，evals，fs，os等。

### 核心模块的引入流程
见图：
![]()

### 编写核心模块
p36 － p37，还需细读

## 4.C/C++扩展模块
C/C++扩展模块属于文件模块一类。
JS具有一些弱点，例如位运算，因为JS中只有double类型，所以需要转成int型再进行，非常慢，但是C++就不用。
C／C＋＋模块的会先预编译成`.node文件`，然后调用`process.dlopen()`来加载执行。

![]()

### 前提条件
* GYP项目生成工具
```javascript
生成各个平台下的项目文件。
```
* V8引擎C++库
```javascript
实现js和C++的互相调用。
```
* libuv库
```javascript
实现跨平台的核心，是跨平台的一层封装，通过它去调用一些底层操作，封装了时间循环，文件操作等功能。
```
* Node内部库
* 其他库

### 编写
与核心模块的区别是无须将源代码编译进Node，而是通过dlopen()方法动态加载。

### 编译
写好`bingding.gyp`文件，然后调用`node-gyp configure`创建build目录，再之后执行`node-gyp build`生成`.node`文件。

### 加载
需要加载`.node`文件：
```javascript
var hello = require(',.build/Release/hello.node');
```
对于.node文件Node将会调用process.dlopen（）方法进行加载。
![]()

## 5.模块调用栈
JS核心模块主要扮演的职责有两类：
* 作为C++内建模块的封装层和桥接层,供文件模块调用。
* 纯粹的功能模块，不跟底层打交道，但是十分重要。






