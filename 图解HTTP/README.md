# 图解HTTP

## 1. 代理／网关／隧道
都是通信数据转发程序， 配合服务器工作。

### 代理
基本行为：接受客户端的请求转发到其他服务器。
转发时附加`via首部字段`。
使用理由： `缓存技术`。
两种代理：
* 缓存代理：把请求数据缓存到代理服务器上，相同请求不用再转发。
* 透明代理：不对报文作修改则透明，反之不透明。

### 网关
基本行为：可以与转发的服务器使用非HTTP协议。
理由：可以提高与客户端通信里的安全。


### 隧道
基本行为：本身不解析HTTP请求，意在添加SSL等安全协议，确保客户端与服务器的安全通信。


### 缓存
缓存是指代理服务器或者客户端保存资源副本。
`优点`：利用缓存可以减少服务器的访问。

## 2. 首部字段
格式： `首部字段名`:`字段值`


### 为Cookie服务的首部字段
Cookie工作机制：用户识别以及状态管理
* Set-Cookie: 开始状态管理所使用的Cookie信息, 响应首部字段
```
1. Name = value: 必选，赋予Cookie名称和值。
2. expires ＝ Data： 有效期
3. path ＝ PATH： 将服务器上的文件目录作为Cookie的适用对象。
4. domain ＝ 域名： 作为COokie适用对象的域名。
5. Secure： 仅在HTTPS安全通信时才发送Cookie
6. HttpOnly： 加以限制，不能被JavaScript访问，主要防止跨站脚本攻击(Cross-site scripting, XSS), 但是并非为此而开发。

例子：Set-Cookie: name=value; Secure; HttpOnly
```

* Cookie: 服务器受到的Cookie信息，请求首部字段
```
首部Cookie字段的意义：告知服务器， 当客户端想获得HTTP状态管理支持时，就会在请求中包含从服务器接收到的Cookie。

Cookie: status = enable;
```

## 3.HTTPS
HTTP缺点：
* 通信使用明文，会被窃听
* 不验证通信方身份
* 不保证报文完整性

### 通信加密
通过SSL(Secure Socket Layer安全套接层)和TLS(Transport Layer Security安全层传输协议)，加密HTTP通信内容。
先通过SSL建立安全通信线路，再进行HTTP通信。
HTTPS并非是应用层的新协议，只是HTTP通信接口部分用SSL和TSL协议代替。
```
从：HTTP直接和TCP通信
到：HTTP首先与SSL通信，再由SSL与TCP通信。
```
SSL的加密方法：
```
采用公共密钥加密(Public－key cryptography)。
加密算法是公开的，但是密钥是私有的，加密和解密都需要密钥。
```
HTTPS采用混合加密机制：共享密钥加密 ＋ 公共密钥加密。



### 内容加密
即是把HTTP报文中所含的内容进行加密处理。

### 验证请求的客户端身份
不验证的话谁都可以请求。

查明对方证书。
```
SSL不仅提供了加密处理，还使用了一种叫证书的手段，可用于确定方。证书由第三方机构颁发。
```

### 确保内容完整
有可能收到的HTTP响应已经是被窜改的，如中间人攻击(Man-in-the-Middle attack, MITM).

如何防止？
```

```



*
*
