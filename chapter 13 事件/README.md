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




