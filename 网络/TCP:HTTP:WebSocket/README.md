# TCP/HTTP/SPDY/WebSocket

## HTTP的不足
* HTTP的连接问题，HTTP客户端和服务器之间的交互是采用请求/应答模式，在客户端请求时，会建立一个HTTP连接，然后发送请求消息，服务端给出应答消息，然后连接就关闭了。（后来的HTTP1.1支持持久连接）
* 因为TCP连接的建立过程是有开销的，如果使用了SSL/TLS开销就更大.
* HTTP消息头问题，现在的客户端会发送大量的HTTP消息头，由于一个网页可能需要50-100个请求，就会有相当大的消息头的数据量。
* HTTP通信方式问题，HTTP的请求/应答方式的会话都是客户端发起的，缺乏服务器通知客户端的机制，在需要通知的场景，如聊天室，游戏，客户端应用需要不断地轮询服务器。

## SPDY
SPDY并不是一种用于替代HTTP的协议，而是对HTTP协议的增强。新协议的功能包括数据流的多路复用、请求优先级以及HTTP报头压缩

### 优点
* 多路复用，一个TCP连接上同时跑多个HTTP请求。请求可设定优先级
* 去除不需要的HTTP头，压缩HTTP头，以减少需要的网络带宽
* 使用了SSL作为传输协议提供数据安全
* 对传输的数据使用gzip进行压缩
* 提供服务方发起通信，并向客户端推送数据的机制

## websocket
WebSocket则提供使用一个TCP连接进行双向通讯的机制，包括网络协议和API，以取代网页和服务器采用HTTP轮询进行双向通讯的机制。

本质上来说，WebSocket是不限于HTTP协议的，但是由于现存大量的HTTP基础设施，代理，过滤，身份认证等等，WebSocket借用HTTP和HTTPS的端口。

WebSocket连接除了建立和关闭时的握手，数据传输和HTTP没丁点关系了。

### websocket和SPDY的关系
* 补充关系，二者侧重点不同。SPDY更侧重于给Web页面的加载提速，而WebSocket更强调为Web应用提供一种双向的通讯机制以及API。
* 竞争关系，二者解决的问题有交集，比如在服务器推送上SPDY和WebSocket都提供了方案。
* 承载关系，试想，如果SPDY的标准化早于WebSocket，WebSocket完全可以侧重于API，利用SPDY的帧机制和多路复用机制实现该API。 Google提出草案，说WebSocket可以跑在SPDY之上。WebSocket的连接建立在SPDY的流之上，将WebSocket的帧映射到SPDY的帧上。
* 融合关系，如微软在HTTP Speed+Mobility中所做的。
