# chapter 10 DOM
DOM: document obejct model.
针对HTML以及XML所产生的一个API.

## IE中的DOM
IE中的DOM都是COM的形式来实现的，所以与原声JS对象行为并不一致。
### COM
The Component Object Model. 定义了对象在单个应用程序内部或多个应用程序之间的行为方式。

## 节点层次
DOM可以讲任何HTML或者XML描绘成一个由多节点构成的结构，以及节点之间的层次关系。
### 文档元素
文档元素师文档的最外层元素。
* HTML始终是<html>
* XML中没有与定义元素，因此任何元素都能成为文档元素。

### node类型
JS中所有节点类型都继承自Node类型。每个节点都有一个nodetype属性用语表明节点的类型。
节点的类型一共有12种,**每一种都有对应的数值**，书本**P248**。**但是在IE中不能访问Node类型!!!**.
```JavaScript
if (someNode.nodeType == Node.ELEMENT_NODE) {
    alert("Node is an element");
}
为了兼容性，最好用数值表示类型，适用于IE!!!
if (someNode.nodeType == 1) {
    alert("Node is an element");
}
```
#### nodeName和nodeValue
* 对于元素节点，nodeName永远是标签名，nodeValue为null

#### 节点关系
* 每个节点都有一个**childNode**属性，其中保存一个**NodeList**对象。DOM的改变会动态改变NodeList对象。
* NodeList虽然不是array实例，但是有length，可以用方括号语法访问。
* 还可以用**item()**来访问NodeList
```JavaScript
var firstChild = someNode.childNodes[0];
var fisrtChild = someNode.childNodes.item(1);
```
* 讲NodeList对象转换数组
```JavaScript
function convertToArray(nodes) {
    var array = null;
    try {
        array = Array.prototype.slice.call(nodes,0);//针对非IE浏览器
    } catch(ex) {
        array = new Array();
        for (var i = 0; i < nodes.length; i++) {
            array.push(nodes[i]);
        }
    }
    return array;
}
```
* 节点还有**parentNode**, **previousSibling**, **nextSibling**, **firstChild**, **lastChild**
* 还有一个试用的方法：hasChildNodes()，若有child返回true
* 可以通过**owenerDocument**访问文档节点。

#### 操作节点
* appendChild(): 会返回新增节点
```JavaScript
var returnNode = someNode.appendCHild(newNode);
alert(returnNode == newNode); -> true
alert(someNode.lastChild == newNode); -> true
```
* insertBefore(newNode, 参考位置的node) 与 appendChild() 相反
* replaceChild(newNode, oldNode);
* removeChild(): 移除的节点仍然归文档所有，但是在文档中没有了自己的位置。
* 以上方法都必须先得到父节点
* cloneNode(boolean)
```JavaScript
cloneNode(true): 深复制，复制节点并且整个子节点树
cloneNode(false): 浅复制，只复制该节点
！！！复制并不会复制DOM节点种的JavaScript属性，例如事件处理程序之类，只会复制特性。
```
* normalize(): 找到空文本节点，删除；找到连续两个文本节点，合并。


### Document类型
Document类型表示文档，HTMLDocument继承自Document类型，而document对象是HTMLDocument的一个实例，表示整个HTML页面。
document对象是window对象的一个属性，Document节点只有一个儿子，**html**。
```JavaScript
Document节点有下列特征：
nodeType ＝ 9；
nodeName ＝ #document；
nodeValue = null;
parentNode = null;
ownerDocument = null;

获取html元素：
document.documentElement = document.childNodes[0] = document.firstChild;
```
* document.body 获取body元素
* document.doctype

#### 文档信息
* document.titleL获取标题信息
* 设置title
```JavaScript
document.title = "new page title";
```
* document.URL 获取本网页完整url
* document.domain 只获取域名
* 将两个页面的domain设成一致才能使两个页面互相通信，访问互相的JavaScript对象

#### 查找元素
获取元素的引用，Document类型提供了三个方法：
* getElementById(): 区分大小写
* getElementsByTagName()：获取的对象类似NodeLists，可以用方括号访问也可以用item()，namedItem("itemname")来获取相应的item, "*" 表示全部
* getElementsByName(): 返回所有name特性一样的元素，返回一个HTMLCollection

#### 特殊集合
* document.anchors : 返回所有带name特性的<a>元素
* document.links: 带href的<a>
* document.images: <img>

#### 一致性检测
用document.implementation中的hasFeature("function", "version")来检测
```JavaScript
var hasXMLDOM = document.implementation.hasFeature("XML", "1.0");
```
#### 文档写入
有四个方法：write(), writeln(), open(), close();

###






