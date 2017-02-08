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

## 闭包
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

