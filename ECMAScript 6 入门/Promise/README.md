# Promise
所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。

## 特点
* 对象的状态不受外界影响
```javascript
Promise对象代表一个异步操作，有三种状态：Pending（进行中）、Resolved（已完成，又称 Fulfilled）和Rejected（已失败）.
```
* 一旦状态改变，就不会再变，任何时候都可以得到这个结果
```javascript
Promise对象的状态改变，只有两种可能：从Pending变为Resolved和从Pending变为Rejected。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果。
如果改变已经发生了，你再对Promise对象添加回调函数，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。
```

## 基本用法
ES6规定，Promise对象是一个构造函数，用来生成Promise实例。
```javascript
var promise = new Promise(function (resolve, reject) {
    if (success...) {
        resolve(value);
    } else {
        reject(error);
    }
})
Promise构造函数接受一个函数作为参数，该函数的两个参数分别是resolve和reject。它们是两个函数，由JavaScript引擎提供，不用自己部署。
```

* resolve函数的作用是，将Promise对象的状态从“未完成”变为“成功”（即从Pending变为Resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去.
* reject函数的作用是，将Promise对象的状态从“未完成”变为“失败”（即从Pending变为Rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

### then方法
Promise实例生成以后，可以用then方法分别指定Resolved状态和Reject状态的回调函数。
```javascript
promise.then(function(value) {
    //success
}, function (error) {
    //fail
});
```

### 例子
Promise新建后就会立即执行!!!
```javascript
let promise = new Promise(function(resolve, reject) {
  console.log('Promise');
  resolve();
});

promise.then(function() {
  console.log('Resolved.');
});

console.log('Hi!');

// Promise
// Hi!
// Resolved
```
如果调用resolve函数和reject函数时带有参数，那么它们的参数会被传递给回调函数。reject函数的参数通常是Error对象的实例，表示抛出的错误；
resolve函数的参数除了正常的值以外，还可能是另一个Promise实例，表示异步操作的结果有可能是一个值，也有可能是另一个异步操作。


## Promise.prototype.then()
Promise实例具有then方法，也就是说，then方法是定义在原型对象Promise.prototype上的。
它的作用是为Promise实例添加状态改变时的回调函数。
then方法的第一个参数是Resolved状态的回调函数，第二个参数（可选）是Rejected状态的回调函数。
`then方法返回的是一个新的Promise实例,因此可以采用链式写法，即then方法后面再调用另一个then方法。`