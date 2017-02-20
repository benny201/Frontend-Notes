# 事件
JavaScript 与 HTML之间的交互式通过事件实现的。事件就是文档或者浏览器窗口中发生的一些特定的交互瞬间。
## 事件流
事件流描述的是从页面接受事件的顺序。
### 事件冒泡 event bubbling
事件开始时由最具体的元素接受，然后逐级向上传播到较为不具体的节点（文档）。
### 事件捕获 event capturing
不太具体的几点应该更早接收到事件，而最具体的节点应该最后接收到事件。
事件捕获的用意在于再事件到达预定目标之前捕获它。
### DOM事件流
DOM2级事件规定的事件流包括三个阶段：事件捕获阶段，处于目标阶段和事件冒泡阶段。
* 捕获阶段到目标元素的父节点就停止了。
* 处于目标阶段，事件在目标上发生。
* 在事件冒泡阶段可以对事件做出响应。
高版本的浏览器会在捕获阶段出发事件对象上的事件。

##事件处理程序
事件是用户或者浏览器自身执行的某种动作。响应某个事件的函数就是事件处理程序（或者监听器）。以'on'开头。
* example
```JavaScript
<input type="button" name="click me" onclick="try{showMessage();} catch(ex){}">
在html中指定事件处理程序，有两个缺点。
1. 时差问题： 函数在按钮下方定义，还没解析函数就按按钮，就会报错。
2. 扩展事件处理程序的作用域链在不同浏览器中会导致不同结果
```

### DOM0级事件处理程序

将一个函数赋值给一个事件处理程序属性。
```JavaScript
var btn = document.getElementById("myBtn");
myBtn.onclick = function() {
    alert("clicked")
 }
 ```
 删除事件处理程序
 ```JavaScript
 btn.onclick = null;
 ```

 ### DOM2级事件处理程序
 DOM2级定义了两个方法：
 * addEventListener()
 * removeEventListener()
 * 都接受3个参数：要处理的事件名(没有on)，事件处理函数，boolean参数（true：在捕获阶段调用函数，false：在冒泡阶段调用函数）
 * 大多数情况下，将事件处理程序添加到事件流的冒泡阶段，可以兼容各种浏览器。
DOM2级方法添加事件处理程序的主要好处是可以添加多个事件处理程序。
```JavaScript
btn.addEventListener("click", function(){}, false);
btn.addEventListener("click", function(){}, false);
```
用removeEventListener()删除监听器时，所有的参数都要对应相同。

### IE事件处理程序
IE中的两个方法：
* attachEvent()
* detachEvent()
* 都接收两个参数：事件处理程序名称， 事件处理函数。
```JavaScript
var btn = document.getElementById("myBtn");
myBtn.attachEvent("onclick", function(){});
```
IE中的监听器与DOM0级的主要区别在于事件处理程序的作用域：
* DOM0级事件处理程序会在其所属元素的作用域内运行
* IE的则会在全局作用域中运行。
IE中监听器与DOM2级的相同与区别：
#### 共同点
* 都可以为一个元素添加多个事件处理程序
#### 区别
* DOM2级在一个元素多个事件处理程序的情况下，是按照书写顺序执行事件的。
* IE中则是从最后的开始处理。

### 跨浏览器的事件处理程序
创建一个EventUtil的对象，其中含有addHandler()和removeHandler()的方法。
```JavaScript
var EventUtil = {
    addHandler: function(element, type, handler) {
        if (element.addEventListener) {
            element.addEventListener(type, handler, false);
        } else if (element.attachEvent) {
            element.attachEvent("on"+type, handler);
        } else {
            element["on" + type] = handler;
        }
    }

    removeHandler: function(element, type, handler) {
        if (element.addEventListener) {
            element.removeEventListener(type, handler, false);
        } else if (element.attachEvent) {
            element.detachEvent("on"+type, handler);
        } else {
            element["on" + type] = null;
        }
    }
}
```

## 事件对象
出发DOM上的某个事件时，会产生一个事件对象event，这个对象中包含着所有与事件有关的信息。

### DOM中的事件对象
兼容DOM的浏览器会将一个event对象传入到事件处理程序中。
event对象的一些属性：
* type: event的类型
* cancelable
* currentTarget: 事件处理程序当前正在处理事件的那个元素
* target:事件的目标
* stopPropagation()
* ...

#### this、currentTarget和target
在事件处理程序内部，对象this始终等于currentTarget的值，而target则只包含事件的实际目标。
如果直接将事件处理程序指定给了目标函数，this，currentTraget和target包涵相同的值。

#### type
event.type结合switch可以处理多个动作
```JavaScript
var handler = function(event) {
    switch(event.type) {
        case "click":
    }
}

btn.onclick = handler;
```
#### preventDefault()/cancelable
```JavaScript
link.onclick = function(event) {
    event.preventDefault();
}

只有cancelable设置为true才能用preventDefault()去去笑默认行为
```

#### stopPropagation()
立刻停止事件在DOM层次中传播，即取消进一步的事件捕获或冒泡。
**举个栗子**：
```JavaScript
var btn = document.getElementById("myBtn");
btn.onclick = function(event) {
    event.stopPropagation();
}

document.body.onclick = function(event) {
    alert();
}

在btn处停止了onclick的冒泡，所以body上的onclick动作就不会被处理了。
```

#### eventPhase
该属性可以查出事件流在哪个阶段：
* 1: 事件处于捕获阶段
* 2: 事件出狱目标阶段
* 3: 事件处于冒泡阶段


### IE中的事件对象
获取IE中的对象方法不同取决于你用哪种方法添加事件处理程序。
* 使用DOM0级添加事件处理程序
```JavaScript
var event = window.event;
alert(event.type)

IE中的type与DOM中的type相同
```
* 使用attachEvent()添加
```JavaScript
对同一个对象，利用：
btn.attachEvent("onclick", function(event) {
    alert(event.type);
});
```
* 如果是通过HTML特性指定的事件处理程序, 可以直接用event的变量来访问。

#### IE对象属性
* cancelBubble: 与stopPropagation（）相同
* returnValue: preventDefault（）
* srcElement: 事件的目标

```JavaScript
btn.onclick = function() {
    alert(window.event.srcElement === this); //true
};
btn.attachEvent("onclick", function(event) {
    alert(event.srcElement === this); //false
});
```

### 跨浏览器的事件对象操作
* P360

## 事件类型
* UI事件
* 焦点事件
* 鼠标事件
* 滚轮事件
* 文本事件
* 键盘事件
* 合成事件

### UI事件
UI事件指的是不一定与用户操作有关的事件

#### load事件
当页面完全加载完之后，就会触发load事件。－> onload
* 第一种方式：
```JavaScript
EventUtil.addHandler(window, "load", function(event) {
    alert("");
});

兼容DOM的浏览器会将event.target = document
IE不会为它设置srcElement信息
```
* 第二种方式：
为`<body>`添加一个onload特性
```JavaScript
<body onload="alert()">
```
一般来说window上面发生的任何事件都可以在`<body>`元素中通过相应的特性来指定，因为在HTML中无法访问window元素。－>为了向后兼容。
但推荐JavaScript形式。

* 在`<img>`元素上也可以指定load特性，但是如果是想创建一个新img并且要求图片加载后出现提示，那么要`先加入load事件，再设置src`。
因为在创建新节点的时候，即使没将img加入DOM树，只要赋予了src，就开始下载。

* `<script>` 和 `<link>`节点也支持onload

#### unload事件
这个事件在文档呗完全卸载后触发： `用户从一个页面切换到另一个页面`

#### resize事件
当浏览器呗调整到一个新的高度或者宽度时，就会触发resize事件。
这个事件也在window上面触发，因此可以通过JavaScript或者`<body>`元素虹的onresize特性来指定。

#### scorll事件
文档滚动期间被触发。
* 混杂模式中，可以通过`<body>`的scrollLeft或者scrollRight来监控
* 在标准模式中，除Safari之外，可视通过`<html>`元素来反映这一变化，Safari仍然基于`<body>`

```JavaScript
EventUtil.addHandler(window, "scorll", function(){
    if (document.compatMode == "CSS1Compat") {
        //标准模式
    } else {
        //混杂模式
    }
});
```
### 焦点事件
焦点事件会在页面元素获得或者失去焦点时触发。利用document.hasFocus() & document.activeElement可以知晓用户行踪。

#### blur失焦事件
不冒泡事件
#### focus事件
不冒泡事件
#### focusin
冒泡事件。等价于focus
### 鼠标与滚轮事件
* click: 单击鼠标
* dbclick: 双击鼠标
* mousedown: 任意鼠标按键
* mouseenter: 光标首次移动到元素范围内／不冒泡
* mouseleave: 光标移开／不冒泡
* mousemove: 元素内移动反复触发
* mouseout:
* mouseup: 用户释放鼠标按钮时触发。
click和dbclick事件发生有一定的顺序：
1. mousedown
2. mouseup
3. click
4. mousedown
5. mouseup
6. click
7. dbclick
检测浏览器是否支持以上DOM2级事件：
```JavaScript
var isSupported = document.implementation.hasFeature("MouseEvents", "2.0");
```
同理，检测DOM3级事件（应该用MouseEvent）：
```JavaScript
var isSupported = document.implementation.hasFeature("MouseEvent", "3.0");
```
#### 客户区坐标位置
在浏览器视口中，对象中的clientX和clientY保存了鼠标指针的位置。
```JavaScript
var div = document.getElementById("myDiv");

EventUtil.addHandler(div, "click", function(event) {
    event = EventUtil.getEvent(event);
    alert(event.clientX + event.clientY);
});
```

#### 页面坐标位置
pageX和pageY记录的是事件对象的位置。非视口的左边和定边计算。
在页面没有滚动的情况下，pageX和pageY的值等于clientX和clientY的值。

#### 屏幕坐标位置
整个屏幕的位置。screenX和screenY。

#### 修改键
shiftKey, ctrlKey, altKey 和 metaKey 这些属性都是布尔值。相应的键按下则为true。
可以配合click事件用。

####
####
####
####
####

## 内存和性能
事件处理程序数量影响了页面的整体运行性能。
每个函数都是对象，会占用内存，所以对象越多，性能越差。

### 事件委托
事件处理程序过多，解决方案是`事件委托`。
事件委托利用了事件冒泡，指定一个事件处理程序就可以管理某一类型的所有事件。
```JavaScript
var list = document.getElementById("myLinks");
EventUtil.addHandler(list, "click", function(event) {
    event = EventUtil.getEvent(event);
    var target = EventUtil.getEvent(event);

    switch(target.id) {
        case "":

        case "":

        case "":

    }
});
```

click, mouseup, mousedown, keydown, keyup 和 keypress