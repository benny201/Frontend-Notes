# javaScipt进阶篇笔记

## 事件
* 事件是可以被 JavaScript 侦测到的行为.
* 网页中的每个元素都可以产生某些可以触发 JavaScript 函数或程序的事件.
```JavaScript
onclick: 鼠标单击事件
onmouseover: 鼠标经过事件
onmouseout: 鼠标移开事件
onchange: 文本框内容改变事件：失焦时才调用
oninput: 文本框内容改变事件：输入时调用
onfocus: 光标聚焦
onblur: 光标离开
onload: 网页导入
onunload: 关闭网页: winodw.unload
```

## 对象
* 万物皆对象 : )
* object.propertyName
* objext.methodName()

### Date()
* var date = new Date();
* methods
```javaScript
1. get/setDate()
2. get/setFullYear()
3. get/setYear()
4. get/setMonth()
5. get/setHours()
6. get/setMinutes()
7. get/setSeconds
8. get/setTime()
```
* 按照毫秒计算 60 * 60 * 1000

### String
* 类似Java
* indexOf/split/length/substring/substr()...

### Math
* ceil：向上取整
* floor: 向下取整
* round: 四舍五入
* random()

### Array
* concat: 连接
* join: 讲数组转化成字符串并且添加自定义分隔符
* pop = shift/push/reverse/
* splice（start，end）： 选取
* unshit: 向数组头添加新对象并返回长度

## BOM

### 计算器
* setTimeout()/clearTimeout() : 指定延时后执行代码／清除延时
* setInterval()/clearInterval() : 每隔指定时间执行代码／取消设置

