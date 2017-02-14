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

## node类型
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
### nodeName和nodeValue
* 对于元素节点，nodeName永远是标签名，nodeValue为null

### 节点关系
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


