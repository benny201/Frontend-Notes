#imooc入门篇

## 基本操作
* document.write()
* alert()
* confirm(): 消息确认框
* prompt(): 消息输入框
* body中加入button监听

```html
<body>
    <input name="button" type="button" onClick="rec()" value="点击我!" />
</body>
```
* window.open([URL], [窗口名称], [参数字符串])
```html
[窗口名称]: "_top"、"_blank"、"_self"具有特殊意义的名称。
       		_blank：在新窗口显示目标网页
       		_self：在当前窗口显示目标网页
       		_top：框架网页中在上部窗口中显示目标网页

[[参数字符串]]:
	top/left/width/height/menubar/toolbar/scrollbar/status
```

* 例子：

```JavaScript
window.open('http://www.imooc.com','_top','width=300,height=200,menubar=no,toolbar=yes, status=no,scrollbars=yes')
```
* window.close() / object.close()

* 测试:

```JavaScript
<html>
 <head>
  <title> new document </title>  
  <meta http-equiv="Content-Type" content="text/html; charset=gbk"/>   
  <script type="text/javascript">  
    
    // 新窗口打开时弹出确认框，是否打开
    function openWindow() {
        var isOpen = confirm("是否打开");
        if (isOpen) {
            var website = prompt("输入网址", "http://www.imooc.com/")
            window.open('website', '_blank', 'width = 400, height = 500, toolbar = no, menubar = no');
        }
    }
    // 通过输入对话框，确定打开的网址，默认为 http：//www.imooc.com/

    //打开的窗口要求，宽400像素，高500像素，无菜单栏、无工具栏。
    
    
  </script> 
 </head> 
 <body> 
	  <input type="button" value="新窗口打开网站" onclick="openWindow()" /> 
 </body>
</html>
```

## DOM
* document.getElementById(“id”)
* Object.innerHTML: 提取html
* Object.style.property=new style: 提取样式
```JavaScript
 var mychar= document.getElementById("con");
    mychar.style.color = "red";
    mychar.style.fontSize = "30px"
    mychar.style.backgroundColor = "green"
```     
* Object.style.display = value: 显示／隐藏内容
* object.className = classname: 设置CSS的样式类