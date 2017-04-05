# BOM

## window对象
window是所有对象，变量，函数的Global对象
### 全局作用域
全局作用域的变量函数都会变成window对象的方法和属性
```JavaScript
var age = 29;
alert(window.age);
```
* this.age = window.age
* 但是如果是普通变量，不能直接delete
```JavaScript
var d = 0;
delete window.d; -> false;
alert(d); -> 0;

因为var语句自动定义了一个configurable的特性为false；
```
### 窗口关系及框架
to be continued

### 窗口位置
* screenLeft: 窗口位于屏幕左边。
* screenTop
```JavaScript
var leftPos = (typeof window.screenLeft == "number") ? screenLeft : window.screenX;
这事先判断浏览器是否支持screeLeft，如果不支持泽调用screenX／Y
```
* moveTo(x,y): 将窗口移动到具体坐标值，左上角为（0，0）
* moveBy(x,y): 接受的参数为水平和垂直方向上的像素值
```JavaScript
window.moveTo(0,100);
```
### 窗口大小
获取大小
* innerWidth/innerHeight: 页面试图区大小
* outerWidth/outerHeight: 浏览器窗口本身的尺寸
* document.documentElement.clientWidth/document.documentElement.clientHeight: 标准模式下
* document.body,width/height: 混杂模式下
* 移动浏览器中只能用document.documentElement.clientWidth/document.documentElement.clientHeight
调整窗口大小
* resizeTo(x,y): 新宽度和新高度
* resizeBy(defX,defY)：新旧窗口的宽差和高差

### 导航和弹出窗口
```JavaScript
window.open(url, "target", "atrribute", "是否取代浏览器历史记录中当前大家页面／true or false"): 具有四个参数, 第四个参数只在不打开新窗口的时候使用
```
* atrribute: "width=300,height=30,etc"
```JavaScript
var win = window.open("www.dasdsadsa");
win.close();
win.resizeTo();
win.moveTo();
```
* 检测新开的窗口是否被屏蔽
```JavaScript
var blocked = false;
try{
    var win = window.open("http://www.baidu.com");
    if (win == null) {
        blocked = true;
    }

} catch(ex) {
    blocked = true;
}
```
### 间歇调用和超时调用

* setTimeout("", time);
```JavaScript
var timeout = setTimeout(function(){
    alert("a");
}, 1000);
```
* setTimeout()返回一个超时调用ID，可以用ID调用clearTimeout取消
```JavaScript
timeout.clearTimeout();
```
* setInterval()间歇调用
* 同样会返回一个ID，并且可以用clearInterval()取消

### 系统对话框
* alert()
* confirm()会返回一个boolean值
```JavaScript
if(confirm("nice?")) {
    alert(yes);
} else {
    alert(no);
}
```
* prompt("文本提示", "默认值")：输入文本的对话框，若是选择ok则返回文本。

## location对象
BOM对象之一，提供当前窗口中加载的文档有关的信息，还提供一些导航功能。
**location对象及时window对象的属性，也是document对象的属性**
location的是体育帅哥也许不够如下:
* hash
* host
* hostname
* href
* pathname
* port：返回端口
* protocol：返回协议
* search: 查询字符串

### 查询字符串的写法
```JavaScript
function get() {
    var qs = (location.search.length > 0 ? location.search.substring(1) : "");
    var args[];
    var items = qs.length ? qs.split("&") : [];
    var item = null, name = null, value = null;
    var i = 0, len = item.length;
    for(i = 0; i < len; i++) {
        item = items[i].split("&");
        name = decodeURIComponent(item[0]);
        value = decodeURIComponent(item[1]);

        if (name.length) {
            args[name] = value;
        }
    }
}
```

### 位置操作
* 通过location.assign("URL")可以带打开一个新的URL并且产生一条记录。
* 通过改变location的属性改变现有的URL
```JavaScript
location.hash = "#section" -> "http://www.baidu.com/#section"
```

* 通过replace()定向一个新的URL，但是用户不能返回前一个页面.
* 通过reload()重新加载当前页面
```JavaScript
location.reload(): 有可能从缓存中加载（若页面无改变）
location.reload(true): 强制从服务器中重新加载
```

## navigator对象
主要用于检测显示网页的浏览器类型
### 检测插件plugins
可以用plugins数组来检测，对于**非IE**浏览器可行，新版IE是否支持有待查实
plugins数组的中每一项都含有
* name: 插件名字
* description: 插件的描述
* filename: 插件的文件名
* length: 插件缩处理的MIME类型数量
```JavaScript
function hasPlugin(name) {
    name = name.toLowerCase();
    for (var i = 0; i <navigator.plugins.length; i++) {
        if (navigator.plugins[i].toLowerCase().indexOf(name) > -1) {
            return ture;
        }
    }

    return false;
}
```
IE中是以COM对象的方式实现插件的，而COM对象使用的唯一标识符来标识，所以检测IE中的插件必须首先知道其标识符。
然后使用IE转悠的ActiveXObject类型。
```JavaScript
以flash为例子
function hasPlugin() {
    try{
        new ActiveXObject(name);
        return true;
    } catch(ex) {
        return false;
    }
}

alert(hasPlugin("ShockwaveFlash.ShockwaveFlash"));
```
## screen对象
编程用处不大，用来表明客户端的能力，其中包括浏览器窗口外部的显示器信息等。
## history对象
history对象上保存着用户上网的历史记录。但是开发人员无法得知用户浏览过的URL。
* 使用go()方法可以在用户的历史记录中任意跳转。
```JavaScript
history.go(1); 前进一页
history.go(-1); 后退一页
history.go(2); 前进两页
```
* go()方法还可以接受字符串参数，表示跳转到最近打开的对应URL
```JavaScript
history.go("http://www.baidu.com")
```
* 可以用back(),forward()代替


