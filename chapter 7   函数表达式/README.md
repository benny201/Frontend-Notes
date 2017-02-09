# chapter 7 函数表达式

##  函数表达式的特征
* 重要的特征: function declaration hoisting（函数声明提升）

```JavaScript
say();
function say(){
	
}
```
* 两种创建函数的方法

```JavaScript
1. function say(){}; 命名函数
2. var name = funtion(){}; : 匿名函数anonymous function
```
## 递归
* 利用arguments.callee解决递归问题，arguments.callee是指向正在执行的函数的指针
* 或者使用命名函数的形式来解决

```JavaScript
严格模式下，不能调用arguments.callee，所以只能通过命名函数来解决：

var fac = (function f(num) {
	if (num < 1) {
		return 1;
	} else {
		return num * f(num - 1);
	}
});

这种情况下即使将fac赋给其他变量，函数的名字仍然有效。
```

## 闭包 Closure
* 闭包指的是有权访问另一个函数作用域中的变量的函数。

```JavaScript

function create(propertyName) {
	return function(a, b) {
		var obj = a[propertyname];
		......
	}
}

内部函数的作用域中包含了外部函数的作用域，所以能调用外部函数的参数。
```
* 某个函数变调用的时候会创建一个执行环境（execution context）以及作用域链。

```JavaScript
以这个例子：
function compare(v1, v2) {
    if(v1 > v2) {
        return 1;
    }
}

var res = compare(1,2);
```
* 然后使用arguments和其他命名参数的值来初始化函数的**活动对象**, 即arguments，v1，v2，全局环境的变量对象始终存在，而活动对象只能在函数执行的过程存在 

### 闭包与变量 
* 闭包具有副作用

```JavaScript
function create() {
    var res = new Array();
    for (var i = 0; i < 10; i++) {
        res[i] = function(){
            return i;
        }
    }
    return res;
}
```
* 表面上没个函数都返回索引i的值，但是其实没个都返回10，因为当create()被调用时，产生的活动对象中会存有一个索引值i，然而每个res［i］的元素都指向同一个i，所以当结束之后，全部都是10.

* 改进此缺点

```JavaScript
res[i] = function(num) {
    return function(){
        return num
    }
}(i);
每次返回res［i］时没有用i来赋值，而是重新设定了一个num，每个函数都有一个num的副本
```

### this对象
* 全局中this指向window
* 调用函数时，活动对象会生成this和argument，搜索变量的时候只会搜索函数内部而不会访问外部函数，所以不可能拿到外部函数的this，所以此时返回this，仍是全局的this

```JavaScript
var name = "windows"

var object = {
    var name = "obj";
    getName:function(){
        return function(){
            return this.name;
        }
    }
}

alert(object.getName()) ---> windows

在函数内部加一个var that = this;获取本object的this可解决这个问题；
```

### 内存泄漏
* IE9之前一些回收机制导致的内存泄漏

```JavaScript
function ass() {
    ver element = document.getElementById("someElement");
    element.onclick = function() {
        alert(element.id);
    };
}
``` 
* 事实上这样html元素并没有被回收，因为匿名函数在调用时会保留一份ass（）函数的活动对象的引用，所以只要这个函数在，ass（）的引用数永远都是1，所以导致了内存泄漏。
* 解决这个问题要消除循环饮用，还要给对象赋null

```JavaScript
var id = element.id;
......
element = null;
```
## 模仿块级作用域
* JavaScript没有块级作用域，作用域：scope
* JavaScript不会提示后续声明重复变量。
* 使用匿名函数可以模仿块级作用域

```JavaScript
(function(){})();
```
## 私有变量
* 函数内部定义的变量，外部不能访问，但是闭包可以通过作用链来访问这些变量。
* 通过闭包来创建特权方法

### 静态私有变量
* **初始化一个未经声明的变量，总会创建一个全局变量**
* 使用闭包和私有变量一个明显的不足之处是影响查找速度

```JavaScript
(function() {
    var name = "";
    Person = function(value) {
        name = value;
    }
    
    Person.peo
})
```


 
 


