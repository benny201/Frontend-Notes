# JavaScript - 引用类型

## 对象
* 万物皆对象 : )
* object.propertyName
* objext.methodName()

## Date类型
* var date = new Date();
* methods
```javaScript
1. get/setDate()
2. get/setFullYear()
3. get/setYear()
4. get/setMonth()
5. get/setHours()
6. get/setMinutes()
7. get/setSeconds
8. get/setTime()
```
* 按照毫秒计算 60 * 60 * 1000

## RegExp类型

### 基本语法
* var expression = / pattern / flags;
```JavaScript
1. g: global: 并非在找到第一个字符串后停止
2. i: case-insensitive
3. m: multiline多行查找
```
### 符号
```java
{}[]\^$?*+.
```
### 实例属性
* index
* lastIndex
* test(): true/false

### 调用
```JavaScript
var pattern1 = new RegExp("at", "i");
var patter2 = /at/i;
text = "asff"
var match = pattern.exc(text);
```

## Funtion类型

### 构造方法
* Function x(a)
* var fun = function(a);
* 第二种不推荐，因为解析两次代码，第一次：解析常规ECMAScript 第二次：解析传入构造函数的字符串

### 没有重载
* 可以把函数名想象为指针
* 如果重名函数，后面会覆盖前面

### 函数声明
* 以下代码可以执行
```JavaScript
alert(sum(a));
function sum(a) {
	
}
```
* 因为解析器会有一个function declaration hoisting的过程，读取并将函数声明添加到执行环境中，升到源代码树的顶部.

### 函数的嵌套
* 函数中可以返回一个完整的函数
```JavaScript
function sum() {
	return function(a,b) {
		return a;
	}
} 
```
* 递归
* 去除递归中的函数名耦合可以调用arguments.callee()代替原函数名进行递归.

### this & caller & callee
* caller: 返回调用者
* callee: 返回自身
* arguments.callee.caller

### arguments对象
* 每个函数都有自己的一个arguments对象，它包括了函数所要调用的参数。

### apply()/call()
* 每个函数都继承了apply()/call()
* call要列出所有的参数，不能用arguments

### bind()
* this值会绑定到bind的对象
```JavaScript
var o = {color : "red"};
fuction sayColor () {alert(this.color)};
var ob = sayColor.bind(o);


output: red;
```


### 基本包装类型
* new出来的对象和自动创建的基本包装类型对象的生存期不同。
* new出来的对象在执行流离开当前作用域之前移植都保存在内存中。
* 但是，自动创建的类型, 仅有执行代码的瞬间的生存期，会自动执行以下操作：
```JavaScript
var s1 = "hello World"

1)创建一个实例： new String（"hello World"） 
2)然后删除：null
3)下次调用s1时会再次创建对象
```
* 所以不能够给自动创建的对象加任何属性，因为下次调用的时候就没了！！！！！！
* var obj = new Object("任何类型");

### 可以用基本包装类型创建对象
* Boolean
* Number
```JavaScript
1.toFixed(num): 显示几个小数
2.toExponential(num): 显示几个指数
```
* String
```JavaScript
1. charAt()
2. charCodeAt(): 字符编码
3. concat()
4. substring()/slice()/substr(start,length)
5. indexOf(str, start index)
6. lastIndexOf()
7. trim(): 删除前后空格
```


### 单体内置对象
* Global对象: 不属于任何其他对象的属性和方法，最终都是他的属性和方法。
```JavaScript
isFinite()/parseInt()/......

1. encodeURI(): 进行URI(Uniform Resource Indentifiers, 通用资源标识符), 不会URI特用的符号进行编码。
2. encodeURIComponent() :会对所有非标准字符进行编码
3. eval()： ECMAScript解析器
```

* window对象，在全局作用域中声明的所有变量和函数，都是window对象的属性.
* Math对象
























