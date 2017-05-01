# chapter 4: 提升
神奇的提升。
* 情况1：
```javascript
a = 2;
var a;
console.log(a); -> 2
```
* 情况2：
```javascript
console.log(a); -> undefined.
var a = 2;
```

## 1.从编译器开始解析
首先在解释JS代码前，先对其进行编译。编译阶段中的一部分工作就是找到所有的声明，然后用合适的作用域将它们关联起来。
所以，`变量和函数`在内的所有声明都会在任何代码被执行前首先被处理。

###对于变量
```javascript
var a = 2;
这个不是一个声明，而是两个。 var a 和 a ＝ 2.第一个声明在编译阶段进行。第二个在执行阶段进行。
```

### 对于函数
以下这种可以正确执行：
```javascript
foo();
function foo () {

};
```
但是对于这种匿名函数，则会出现`TypeError`异常。
```javascript
foo();
var foo = function (){};
```

`注意：每个作用域都会进行提升操作。`
换句话来说，先有蛋后有鸡。

还有一种情况：
```javascript
foo(); // TypeError
bar(); // ReferenceError
var foo = function bar() { // ...
};
```

## 2.
