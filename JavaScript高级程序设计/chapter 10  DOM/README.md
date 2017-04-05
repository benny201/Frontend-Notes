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

### Element类型
用语表现XML或HTML元素，具有一下特征：
```JavaScript
nodeType = 1,
nodeName = tag name,
nodeValue = null,
parentValue = Document or ELement
```
tag的名字可以通过，tagName或者nodeName来获取，但是HTML获取的名字始终为大写！
#### HTML元素
HTML元素都是HTMLElement类型的, 具有以下特性值, 可修改:
```JavaScript
div.id / className / title(鼠标移到对象时会显示) / lang / dir(文字方向 rtl or ltr)
div.id = "new" ,etc...
```
#### 获取特性
除了以上直接通过element访问特性的方法，还有就是用getAttribute("Attribute Name"), 不区分大小写，不存在时会返回null:
```JavaScript
var div = document.getElementById("id");
div.getAttribute("id")
```
#### 设置特性
用setAttribute("name", "new attribute"),特性名会转换成小写。**推荐用该方法设置特性** :
```JavaScript
div.setAttribute("class", "newClass");
```
#### 删除特性
用removeAttribute("name"),完全删除。

#### attributes属性
Element类型时使用atrributes属性的唯一一个DOM节点类型。attribute属性中包含一个NamedNodeMap，与NodeList类似。
每一个特性都由一个Attr节点表示，每个节点都保存在NamedNodeMap中，具有以下方法：
* getNamedItem(name) : 返回nodeName为name的节点
* removeNamedItem(name) : 从列表中移除节点,(返回值是被删除的节点)
* setNamedItem(node) ： 添加节点
* item(pos) ; 返回节点

可以通过两种方法访问特性：
```JavaScript
var id = element.attributes.getNamrItem("id").nodeValue; or
var id = element.attributes["id"].nodeValue;
还可以设置新特性：
element.attributes["id"].nodeValue = "someOtherId";
```

#### 创建元素
使用document.createElement().HTML中不区分大小，XML则区分大小写。
```JavaScript
var div = document.createElement("div");
div.id = "newDIv";
这样设置只是设置了值，并未加到文档树上，应该继续使用appendChild(),insertBefore(),replaceChild()
document.body.appendChild();
```
document.createELement()中还可以传入完整的标签！
还有一些创建表单的重要内容，（p268 － p269）

### Text类型
文本节点，包含了纯文本内容，不包含html代码，具有以下特征
* nodeType = 3
* nodeName = "#text"
* nodeValue = 文本值
* parentNode = Element
* 没有子节点
可以通过nodeValue属性或者data属性访问text节点中的文本，以下方法可以操作文本
* appendData()
* deleteData(offset, count)
* insertData(offset, text)
* replaceData(offset, count, text)
* splitData(offset)
* substringData(offset, count)
还可以通过data.length，nodeValue.length或者Text.length去访问文本长度

#### 创建文本节点
使用document.createTextNode()创建新文本节点，创建新文本节点的同时会设置为ownerDocument属性，不过没有加到文档树中就看不到。
```JavaScript
var element = document.createElement("div");
element.className = "message";

var textNode = document.createTextNode("Hello world");
element.appendChild(textNode);

document.body.appendChild(element);
```

####规范文本节点
一个元素一般只有一个文本子节点，不过在某些情况下也可能包含多个文本子节点，如果加入两个文本点，文本节点会连起来显示，没有空格。
为了繁殖文本节点混乱，需要规范化。
在父元素上使用normalize()方法可以讲所有的文本节点合并成一个节点。

#### 分割文本节点
与normalize()相反，splitText(offset)将一个文本节点分成两个文本同胞。

### Comment类型
DOM中的注释通过Comment类型来表示。Comment节点具有下列特征:
* nodeType = 8
* nodeName = "#comment"
* nodeValue = 注释的内容
* parentNode  = Document or ELement
* 没有子节点

### Attr类型
元素的特性在DOM中以Attr类型来表示，浏览器中可以访问Atrr类型的构造函数和圆形。特性就是存在于元素的atrributes属性中的节点，特性节点具有以下特性:
* nodeType = 2
* nodeName 为特性的名字
* nodeValue = 特性的值
* parentNode = null

## DOM操作技术

### 动态脚本
#### 通过添加tag来动态加入脚本
```JavaScript
function loadScript(url) {
    var script = document.createElement("script");
    script.type = "text/javascript";
    script.src = url;
    document.body.appendChild(script);
}
```
#### 直接嵌入代码块的形式
IE将script这个元素视为一个特殊元素，不能访问起子节点，所以不能加一个text子节点
```JavaScript
function loadScriptString(code) {
    var script = document.createElement("script");
    script.type = "text/javascript";
    try{
        script.appendChild(document.createTextNode(code))
    } catch(ex) {
        script.text = code;
    }
    document.body.appendChild(script);
}
```
### 动态样式
一般的CSS样式要加到head下才能保证浏览器中的行为一致。添加CSS样式的方法与script类似
```HTML
<link rel="stylesheet" type="text/css" href="style.css">
```
#### 添加CSS文件
```JavaScript
var link = document.createElement("link");
link.rel = "stylesheet";
link.type = "text/css";
link.href = "style.css";
var head = document.getElementByTagName("head")[0];
head.appendChild(link);
```
#### 添加CSS代码
考虑到IE也是讲Style元素作为一个特殊元素，不能访问其子节点，所以：
```JavaScript
function loadStyleString(code) {
    var style = document.createElement("style");
    style.type = "text/css";
    try {
        style.appendChild(document.createTextNode(css));
    } catch(ex) {
        style.stylesheet.cssText = css;
    }
    var head = document.getElementByTagName("head")[0];
    head.appendChild(style);
}
```
### 操作表格
table元素是HTML中最复杂的结构之一。具体操作参考p282

## 总结
DOM是语言中立的API，用语访问和操作HTML和XML文档。DOM1级将HTML和XML文档形象地看作一个层次化的节点树，然后使用JavaScript操作它。
























