# chaoter 5: 作用域闭包

## 1. 什么是闭包
当函数可以记住并访问所在的词法作用域时，就产生了闭包，即使函数是在当前词法作用域之外执行。

### 这个是闭包吗？
```javascript
function foo() {
    var a = 2;
    function bar() {
        console.log(a);
    }

    bar();
}

foo();
```
技术上来说，也许是。但是按照上面的定义来说，不是。

### 这个是一个清晰的闭包
```javascript
function foo() {
    var a = 2;
    function bar() {
        console.log(a);
    }

    return bar;
}

var baz = foo();
baz();
```
在这个例子中bar函数在自己定义的词法作用域意外的地方执行。
无论通过何种手段将内部函数传递到所在的词法作用域以外,它都会持有对原始定义作用 域的引用,无论在何处执行这个函数都会使用闭包。

### 只要使用了回调函数，实际上就是实用闭包。

## 2. 模块
用闭包来创建模块：
```javascript
function module() {
    function doSomthing() {};
    function doAnouter() {};
    return {
        doSomthing: doSomthing,
        doAnouter: doAnouter
    };
}
```

### ES6中的模块
* export
* export default
* import X from 'xxx'
