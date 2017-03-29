# chapter 3
DOM: Document Object Model

## DOM中的"O"
JavaScript语言里对象可以分为三种类型：
* 用户定义对象(user-defined obejct)：自定义
* 内建对象(native obejct)：Array, Math, Date
* 宿主对象(host object)：由浏览器提供的对象

## DOM中的"M"
DOM把一份文档表示为一棵树。

## 节点
DOM tree是由node构成的集合。

### 元素节点
DOM的原子是元素节点(element node)。例如: body、p、ul元素之类
html是根元素

### 文本节点
例如P tag中包含的文本就是文本节点(text node)。

### 属性节点
各种tag中的属性就是属性节点(attribute node)。

### 获取元素
有3种DOM方法可以获取元素节点：通过ID，通过标签名字，通过类名字：
* document.getElementById
* doucment.getElementsByTagName
```javascript
返回一个对象数组，包含所有的对应的tag name，通过历遍数组来操作。
```
* document.getElementsByClassName(start node, className)
```javascript
可以通过类名来搜索元素。接受两个参数：1. 开始搜索的node，2. 类名
e.g.
var node = document.getElementById("hello");
var classNode = document.getElementsById(node, "className");
```

## 获取和设置属性

### getAttribute
不属于document对象，只能通过元素节点调用。
```javascript
document.getElementById("id").getAttribute("title");
```
若不存在则返回null


### setAttribute("atrribute", value)
如果attribute存在的话会覆盖原值，如果不存在则会新创建一个attribute。
通过setAttribute做出的修改不会反映在文档源代码里。
因为：先还在文档的静态内容，再动态刷新，动态刷新不影响文档的静态内容。