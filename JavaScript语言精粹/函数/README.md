# 函数
在JavaScript中，函数就是对象。对象是key－value对的集合，并拥有一个连到原型的对象的隐藏连接。
* 对象字面量产生的对象连接到Object.prototype中
* 函数对象连接到Function.prototype中

## 函数字面量
如下：
```JavaScript
var add = function() {

}
```
可以省略函数名，即为匿名函数。

## 调用
调用函数时，除了声音时定义的形式参数，每个函数海接收两个附加的参数： this，arguments(array－like，只有一个length属性)。
当实际参数arguments的个数与形式参数的个数不匹配的时候不会导致运行错误：
```
如果实际参数过多，超出的将会被忽略；
如果实际参数过少，缺失的将会被替代位undefined；
```

一共有四种调用模式：
* 方法调用模式
```
当方法时对象里的一个属性时：
myObject.increament()；
```
* 函数调用模式
```
add(3,4);
缺点是，调用时，函数内部的this是指向全局的，这是一个缺陷。
```
* 构造器调用模式
```
在一个函数前面带上new来调用。这种调用方法会将创建一个隐藏连接到该函数的prototype成员的新对象，
同时this将会绑定到新对象上。
这种属于构造函数，但是不推荐。
```
* call／apply调用模式
```
apply调用可以构建一个参数数组调用，并且可以绑定this
```

## 参数
当函数被调用时，会得到一个arguments数组。
通过它，函数可以访问所有它被调用时传递给它的参数列表。
这样，可以编写一个无须制定参数个数的函数。
```JavaScript
var sum = function() {
    var i , sum = 0;
    for (i = 0; i < arguments.length; i++) {
        sum += arguments[i];
    }
    return sum;
};

document.writeln(sum(4,8,15,16,23,42)); -> 108
```


## 返回
没有返回值，则返回undefined.

## 异常
用try……catch来抛出一个exception对象，其中有两个属性：
* name: 异常类型
* message: 异常描述

```JavaScript
try {
    xxx
} catch(e) {
    document.write(e.name + '' + e.message);
}
```


## 给类型增加方法
可以给基本类型：Object\number\array\string\boolean\Function...增加类型一边对所有对象可用。
```JavaScript
Object.prototype.method = function () {};
```

## 递归
历遍所有的DOM节点,并对每个点进行一个function deal(){}的处理
```JavaScript
var traversal = function (node, deal) {
    deal(node);
    node = node.firstChild;
    while (node) {
        traversal(node,deal);
        node = node.nextSibling;
    }
}
```

## 闭包
函数可以访问它呗创建时所处的上下文环境－>`闭包`；
```JavaScript
var quo = function (status) {
    return {
        get_status:function() {
            return status;
        }
    }
}

var myQuo = quo("amazed");

此时myQuo获得了一个quo()返回的get_status方法的一个新对象，
但是这个时候myQuo.get_status()方法仍然可以访问quo对象中的status属性，
这个属性不是一个复制！！！而是就是他的本身！！！！

```
另外一种能说明`内部函数拥有外部函数的变量，比外部函数自己还有更长的生命周期`的情况：
设置一个setTimeOut()去延时调用内部函数，此时外部函数已经结束，
但是内部函数还能够访问道外部函数的变量。
由于这个原因，还可以用另外一个例子来说明：
`内部函数拥有外部函数的变量，比外部函数自己还有更长的生命周期｀ 以及 `调用的变量不是复制，而就是它的本身！`
```JavaScript
var add_the_handlers = function (nodes) {
    var i;
    for (i = 0; i < nodes.length; i++) {
        nodes[i].onclick = function () {
            alert(i);
        }
    }
};
这种情况下，输出的全是最后一个i，因为这里绑定是变量i，而不是构造时变量i的值。
```
解决方案：
```JavaScript
var add_the_handler = function(nodes) {
    var i;
    for (i = 0; i < nodes.length; i++) {
        nodes[i].onclick = function(i) {
            return function(i) {
                alert(i);
            }
        }(i)
    }
}
```

## 回调
实现不连续事件处理。
```JavaScript
func(request, function(){});
```

## 模块
模块是一个提供接口，却隐藏状态与实现的函数或者对象。
对于：运行完一个函数，然后需要保存一定状态，可以不放在全局变量中，而用闭包来实现。
其实就是对应着类c语言中的私有变量和私有函数,让数据更加安全。
```JavaScript
String.method('deentity', function () {
    //私有变量
    var entity = {};

    //返回一个可以访问私有变量的函数
    return function() {
        ......
    }
//此处是立刻执行，立刻返回给deentity。
}())；

调用：deentity（）；
```






