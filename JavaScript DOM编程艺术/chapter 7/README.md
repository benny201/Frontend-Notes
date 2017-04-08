# chpater 7

## 一些传统的方法

### document.write
document.write()可以将字符串插入到文档里。
但是document.write()的兼容性差，最好不要去使用。

### innerHTML属性
这个属性不适W3C DOM标准的组成，但是已经包含到HTML5中。
`innerHTML属性可以用来读写某给定元素里的HTML内容。`
innerHTML属性不会获取元素里面的细节，一旦使用了innerHTML属性，他的全部内容都会被`替换`。
DOM操作可以替换innerHTML属性。

## DOM方法
用DOM方法改变DOM节点树上的内容，如setAttribute方法并没有改变文档的物理内容：`如果用编辑器而不是浏览器去浏览内容，是不会看到变化的`。

### createElement
把一个元素节点加入一个元素节点中，需要经历两个步骤:
* 创建一个新的元素
```javascript
document.createELement(nodeName)
```
* 把这个元素插入节点树


### appendChild方法
上面的createElement并没有链接到文档中。把新创建的节点插入某个文档的节点树最简单的方法是让这个新节点成为文档某个现有节点的子节点。
所用的方法就是：`parent.appendChild(childNode)`
所以总结来说就是:
```javascript
var newNode = document.createELement("p");
document.getElementById("testdiv").appendChild(newNode);
```

### createTextNode
以上已经插入了一个P元素节点，但是需要增加文本的时候，还需要创建一个文本节点。
要使用`createTextNode`去创建一个文本节点。
例如：
```javascript
var textnode = document.createTextNode("text");
```

### insertBefore()
DOM提供了名为`insertBefore()`方法，这个方法是将一个新元素插入到现有的元素之前。
```javascript
element.insertBefore(newELement, targerElement)
```
### insertAfter()
自定义的一个函数，DOM没有提供
```javascript
function insertAfter(newELement, targerElement) {
    var parent = newELement.parentNode;
    //先检查是不是最后一个儿子，如果是直接插入
    if (parent.lastChild === targerElement) {
        parent.appendChild(newELement);
    } else {
        //如果不是，则插入到下个兄弟与目标element之间
        parent.insertBefore(newELement, targerElement.nextSibling);
    }
}
```
## Ajax
Ajax主要优势就是对页面的请求以异步的方式发送到服务器，服务器不会用整个页面来响应请求，它会在后台处理请求。

### 兼容IE7之前版本
IE7+都支持原生的XHR对象了，只有IE5之前的比较麻烦,IE7之前借助了一个MSXML来创建XHR对象。
```javascript
function  getHTTPObject() {
    if (typeof XMLHttpRequest == "undefined") {
        try {
            return new ActiveXObject("Msxml2.XMLHTTP.6.0");
        } catch(e) {

        }
        try {
            return new ActiveXObject("Msxml2.XMLHTTP.3.0");
        } catch(e) {

        }
        try {
            return new ActiveXObject("Msxml2.XMLHTTP");
        } catch(e) {

        }
    }
}
```

### onreadystatechange/readyState
* readyState: 0-4, 4表示完成
* xhr.status >= 200 && xhr.status < 300 || xhr.status ==304

### Hijax
渐进增强的使用Ajax