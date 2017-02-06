# chapter6 - 面向对象的程序设计

## 理解对象
* 创建对象嘴简单的方式：
```JavaScript
var obj = new Object();
obj.name = xxx;
obj.age = 111;
```
* 首选对象字面量方式：
```JavaScript
var person = {
	name: "a",
	age: 20

	sayNanme: function() {
		alert(this.name);
	}
}
```



## 两种属性attribute
### 数据属性
```JavaScript
4个描述其行为的特性:
1. Configurable: 能否重新定义／删除／修改为访问器属性 
2. Enumerable: 能否通过for－in循环返回属性
3. Writeable: 能否修改属性的值
4. Value: 读取和写入时都调用这个属性

通过对象的Object.defineProperty()去定义这个四个属性（如果用改方法创建***新的属性***，全部属性默认为false）：

example：

var person = ();
Object.defineProperty(person, "name", {
	writable: false,
	value:"benny"
});
```
### 访问器属性
```JavaScript
4个特性：
1. Configurable: 如果不是新属性，就是默认true
2. Enumerable:同上
3. Get: 读取属性时调用
4. Set: 设置属性时调用

Example:

var book = {
	_name: "benny", （！！！在属性前的下划线表明该属性只能通过对象方法访问）
	price: 100
}


Object.defineProperty(book, "_name", {
	get: function() {
		return this._name;
	}
	set: function(newValue) {
		this._name = "Jenny";
		this.price = 101;  ( !!! 通过设置一个属性的值可以导致其他属性发生变化)
	}
})
```
* 只有setter就说明只写不能读，只有getter则反之。

* Object.defineProperties(): 一次性定义多个属性
* Objeact.getOwnPropertyDescriptor(): 获取属性
```JavaScript
var des = Object.getOwnPropertyDescriptor(book, "name");
alert(des.value);
```
## 创建对象

### 工厂模式Factory Pattern
* 通过function创建对象
```JavaScript
function crateObj(name, age, job) {
	var o = new Object();
	o.name = name;
	o.age = age;
	o.job = job;

	return o
} 
```
* 工厂模式的优点：解决创建多个相似对象的问题
* 工厂模式的缺点：没解决识别一个对象的类型

### 构造函数模式
* 不显式的创建对象
* 直接将属性和方法赋给了this对象
* 没有return语句
```JavaScript
function Person(name, age, job) {
	this.name = name;
	this.age = age;
	this.job = job;
	this.sayName(){
		return this.name;
	}
}

调用：var person = new Person(name, age, job);(必须用new！！！！！！)

经历了以下步骤：
1: 创建了一个新对象
2: 将够早对象的作用域付给新对象，this指向新对象
3: 执行构造函数中的代码：添加新属性
4: 返回新对象
```
* 解决了识别对象类型的问题：
```JavaScript
构造属性验证： person.contrcutor == Person
instanceOf:  person instanceOf Person / person insatanceOf Object -> true
```

### 原型模式 （待续）
### 构造函数模式＋原型模式
### 动态原型模式
### 寄生构造函数模式
### 稳妥构造函数模式

## 继承
### 继承一般分为两种方式：
* 接口继承和实现继承
* ECMAScript中只有实现继承

### 原型链
* 例子 : 用父类构造方法构造新对象并赋给instance.prototype原型
```JavaScript
fuction super() {
	
}

function sub() {
	
}

//继承
sub.prototype = new super()
var test = new sub();
test可以跳用sup的方法.
```
* 不能用对象字面量创建原型方法，不然会重写原型链。
* 原型链的问题：引用类型的原型属性会被所有实例共享，所以要再构造函数中定义属性。
```JavaScript
function sup() {
	this.colors = {"red", "blue", "green"};
}

function sub() {
}

sub.prototype = new sup();

var test = new sub();
test.colors.push("black");

alert(test.colors) -> "red", "blue", "green", "black"

var test2 = new sup();
alert(test2.colors) -> "red", "blue", "green", "black"
```