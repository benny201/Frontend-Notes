#JSON
## 对象
JSON对象与JavaScript字面量稍有不同：
* 字面量
```JavaScript
var person = {
    name: "benny",
    age: 29
}
```
* JSON
```JSON
{
    "name" : "benny",
    "age": 29
}

* JSON的属性要加双引号

## 解析与序列化
JSON流行的原因主要是可以把JSON数据解析为有用的JavaScript对象。

### JSON对象
早期解析JSON使用eval()函数，可以返回JavaScript对象和数组。
JSON对象有两个方法：stringify()和parse()
* stringify(): 把JavaScript对象序列化为JSON字符串,不包含任何空格或者缩进
```JavaScript
var book ＝ {};

var jsonText = JSON.stringify(book);
```
* parse(): 把JSON字符串解析为JavaScript对象
```JavaScript
jsonText = {};

var book = JSON.parse(jsonText);
```
### 序列化选项
JSON.stringify()函数
* stringify()另外还接受两个参数，其中一个是过滤器，可以是一个函数：
```JavaScript
var jsonText = JSON.stringify(book, ["title", "edition"]);
以上告诉结果只接受title和edition的结果
```
* 另一个参数是是否保留缩进，以及缩进形式(但是不超过10长度)
```JavaScript
var jsonText = JSON.stringify(book, null, 4);
```
还可以在对象中设置一个toJSON方法。stringify()的序列化顺序：
* 如果存在toJSON()方法而且能通过它去的有效的值，则调用该方法。否则，返回对象本身。
* 如果提过了第二个参数，应用这个函数过滤器，传入函数过滤器的值是第一步返回的值。
* 对第二部返回的每个值进行序列化
* 如果提供了第三个参数，执行相应的格式化


### 解析选项
可以通过一个过滤器进行反编译


