# Ajax和Comet
Ajax：Asynchronous JavaScript + XML. 使能够想服务器请求额外的数据而无需卸载页面。
XHR: XMLHttpRequset对象
异步方式从服务器取得更多信息，使用XHR对象取得新数据，再通过DOM将新数据插入到页面中。

## XMLHttpRequest对象
可以用过XHR构造函数新创建一个XHR对象：
```JavaScript
var xhr = new XMLHttpRequest();
```

### XHR的用法
第一个方法是`open()`，它接受3个参数：要发送的请求的类型(get，post等)，请求的URL和表示是否异步发送请求的bool。
```JavaScript
xhr.open("get", "url", false);
```
`open()`不是真正发送请求，而只是启动一个请求以备发送。要发送请求要调用`send()`函数：
```JavaScript
xhr.send(null);
```
send()接受一个参数，即要发送的数据，这上面的get请求中不需要发送数据，所以为null。
由于以上的请求是同步的，所以会等到服务器响应之后再继续执行。收到响应后，响应的数据的会自动填充XHR对象的属性：
* responseText: 座位响应主体返回的文本
* responseXML: 如果响应的内容类型是： text／xml 或者 application／xml，这个属性中保存包涵响应数据的XML DOM文档。
* status: 响应的HTTP状态
* statusText: HTTP状态说明
`接受响应后`：
* 先检查status属性：将200作为成功标志。304代表请求的资源并没有被修改(也表示成功)，可以直接使用缓存版本。
#### 如果是`异步`请求，则要借助readyState属性判断请求状态：
* 0: 为初始化，需调用open()
* 1: 启动。已经低哦啊用open(),但是没有send()
* 2: 已调用send但是还没有响应。
* 3: 已经接收到部分响应数据
* 4: 接受全部，可以使用。

readyState的值每改变一次都会触发一次readystatechange事件。
```JavaScript
var xhr = createXHR();
xhr.onreadystatechange = function() {
    if (xhr.readyState == 4) {
        if ((xhr.status >= 200 && xhr.status <300) || xhr.status) {
            alert(xhr.responseText);
        } else {
            alert();
        }
    }
};
xhr.open("get", "e.txt", true);
xhr.send(null);
```
因为不是所有浏览器都支持DOM2级，所以不一定有readystatechange事件，所以设置了这个事件。

#### 取消异步请求使用`abort()`

### HTTP头部信息
每个HTTP请求和响应都会带有相应的头部信息。
放松请求时，会发送以下头部信息：
* Accept: 浏览器能够处理的内容类型
* Accept-Charset: 浏览器能够显示的字符集
* Accept-Encoding: 浏览器能够处理的压缩编码
* Accept-Language: 浏览器当前设置的语言
* Connection: 浏览器与服务器之间连接的类型
* Cookie: 当前页面设置的任何Cookie
* Host: 发出请求的页面所在的域
* Referer: 发出请求的页面的URI
* User-Agent: 浏览器的用户代理字符串

可以用`setRequestHeader(name，value)`来设置自定义的请求头部信息。`必须要在open()之后且send()之前调用`。
对应setRequestHeader，在得到响应时，可以通过`getRequestHeader()`来获得相应的头部信息，如果不传参，默认获得全部头部信息。

### GET请求
最常用于向服务器查询某些信息，必要时可以将字符串参数追加到URL的末尾（`必需要用encodeURICOmponent()进行编码`）以便将信息发送到服务器。

```JavaScript
function addURLParam(url, name, value) {
    url += (url.indexOf("?")) == -1 ? "?" : "&";
    url += encodeURICOmponent(name) + "=" + encodeURICOmponent(value);
    return url;
}
```
### POST请求
向服务器发送应该被保存的数据。

## XMLHttpRequest 2级

### FormData类型
FormData为序列化表单以及创建与表单格式相同的数据提供了便利。
```JavaScript
var data = new FormData();
data.append("name", "Benny");
```
append接受键值对参数。
可以用xhr.send()发送form对象
```JavaScript
var XHR = new XMLHttpRequest();
xhr.open("post", "postexample", true);
xhr.send(new FormData(form));
```
### 超时设定
```JavaScript
xhr.timeout = 1000;
xhr.ontime = function() {

};
```
不知道是否支持IE8意外的浏览器

## 进度事件
以下6个进度事件针对XHR事件
* loadstart: 接受到相应数据的第一个字节时触发
* progress: 接受期间不断触发
* error: 请求错误时
* abort: 调用abort()时
* load: 在接收到完整的响应数据时
* loadend: 通信完成或者error／abort／load事件后触发
```JavaScript
xhr.onload = function() {
    if (xhr.status >= 200 && xhr.status < 300 || xhr.status == 304) {
        //success
    }
}
```
### progress事件
```JavaScript
xhr.onprogress = function(event) {
    if (event.lengthComputable == true) {
        event.position;
        event.totalSize;
    }
}
```

progress事件会接受一个event对象，有三个属性：
* lengthComputable: 进度信息是否可读
* position: 已接收字节数
* totalSize: 根据content－length响应头部确定的语气字节数。


## 跨域源资源共享
默认情况下，XHR对象只能访问与包含它的页面位于一个域中的资源（安全策略）。
CORS定义了访问跨源资源时，浏览器与服务器应该如何沟通。
基本思想：使用自定义Http头部让浏览器与服务器进行沟通，从而决定请求或响应的成功和失败。
比如发送请求时，附加一个Origin头部(源信息包含协议，域名，端口)：
```JavaScript
Origin: http://www.nczonline.net
如果服务器认为这个请求可以接受，则返回：
Access-Control-Allow-Origin: http://www.nczonline.net
```

### IE中的CORS
IE中是XDR对象，XDomainRequst。与XHR类似。
与XHR不同点：
* cookie不会随请求发送，也不会随响应返回。
* 只能设置请求头部信息中的content－type
* 不能访问响应头部的信息。
* 只只吃get和post请求
调用方法也是先open再send，open()只接受请求类型和url，一定是异步的。
不能访问readyState，只能是：
* 响应有效触发load事件
* 失败就会触发error事件
可以设置timeout和对应的timeout事件
在`POST`请求时可以设置`contentType`。

### 其他浏览器的CORS
就用XHR就可以了。但是为了区别同源请求和跨源请求，本地资源最好使用相对URL，远程资源使用绝对URL。

### Preflighted Requests

### 带凭证的请求
默认情况下，跨源请求不提供凭证的请求，但可以设置`withCredentials : true`来要求发送凭证。
如果服务器接受带凭证的请求会用HTTP头部来响应：
```JavaScript
Access-Control-Allow-Credentials: true
```

### 跨浏览器的CORS
检查XdomainRequest对象和withCredentials属性。

```JavaScript
function createCORS(method, url) {
    var xhr = new XMLHttpRequest();
    if ("withCredentials" in xhr) {
        xhr.open(method, url, true);
    } else if (typeof XDomianRequest != "undefined") {
        xhr = new XDomianRequest();
        xhr.open(method, url);
    } else {
        xhr = null;
    }
}
```
## 其他跨域技术
利用DOM中能够执行跨域请求的功能。

### 图片PING
使用`<img>`，因为网页可以从任何网页加载图像，可以用于跨域。但是图片PING得不到任何具体的数据，但是可以监听load和error事件。
只要请求完成，就能得到通知。请求从设置src属性那一刻开始。
```JavaScript
var img = new Image();
img.onload = img.onerror = function() {
    alert();
}
img.src = "";
```
图片PING最常用于跟踪用语点击页面或动态广告曝光次数。但是只能发送`get`请求, 无法访问服务器的响应文本。

### JSONP
JSONP stands for JSON with padding ： 包含在函数调用中的JSON，例如：
```JavaScript
callback({"name" : "benny"})
```
在页面上引入不同域上的js脚本文件却是可以的，jsonp正是利用这个特性来实现的。jsonp的原理就很清楚了，通过script标签引入一个js文件，这个js文件载入成功后会执行我们在url参数中指定的函数，并且会把我们需要的json数据作为参数传入。所以jsonp是需要服务器端的页面进行相应的配合的。

### Comet(也叫服务器推送)
Ajax饰从页面向服务器请求数据的技术，Comet是一种服务器从页面推送数据的技术。
实现Comet的两种方式：
* 长轮询
* HTTP流

短轮询：定时向服务器发送请求，看有没有更新数据。
长轮询即： 发送请求，然后服务器一只保持打开，直到有数据可发送，页面打开阶段持续不断。
