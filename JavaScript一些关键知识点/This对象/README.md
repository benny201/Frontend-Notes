# This/call/apply/bind

## 怎么才会绑定this?
### 将函数赋予对象的属性时，this会绑定这个对象
```JavaScript
function test() {
  ///
};

var object;
object.method  = test();
```
### 通过new新创建的函数赋给一个对象时
```JavaScript
function test(){
　　　　this.x = 1;
　　}
var o = new test();
```

### bind可以改变this的指向
bind()方法会创建一个新函数，称为绑定函数，当调用这个绑定函数时，绑定函数会以创建它时传入 bind()方法的第一个参数作为 this，传入 bind() 方法的第二个以及以后的参数加上绑定函数运行时本身的参数按照顺序作为原函数的参数来调用原函数。
```JavaSCript
var bar = function(){
console.log(this.x);
}
var foo = {
x:3
}
bar(); // undefined
var func = bar.bind(foo);
func(); // 3
```
这里我们创建了一个新的函数 func，当使用 bind() 创建一个绑定函数之后，它被执行的时候，它的 this 会被设置成 foo ， 而不是像我们调用 bar() 时的全局作用域。

### 使用函数对象apply()改变调用对象
apply()是函数对象的一个方法，它的作用是`改变函数的调用对象`，它的第一个参数就表示改变后的调用这个函数的对象。
因此，this指的就是这第一个参数。
如果第一个参数为空，则是全局this。


### 同理call()也可以改掉调用对象
用法与apply()大致相同，但是也有一些区别




## call() 和 apply() 的区别
对于 apply、call 二者而言，作用完全一样，只是接受参数的方式不太一样。
JavaScript 中，某个函数的参数数量是不固定的，因此要说适用条件的话，当你的参数是明确知道数量时用 call 。

```JavaScript
func.call(this, arg1, arg2);
func.apply(this, [arg1, arg2]/array);
```
正确运用apply：
```JavaScript
function log(msg)　{
  console.log(msg);
}
log(1);    //1
log(1,2);    //1

而使用apply可以解决参数不确定的问题：
function log(){
  console.log.apply(console, arguments);
};
log(1);    //1
log(1,2);    //1 2
```


