### GET与POST请求区别
- 缓存：一般浏览器会对get请求进行缓存，而post不会
- 长度：浏览器对get请求的长度有限制，而post不会
- 安全性：相比之下，post请求比get请求更为安全，get请求会被浏览器记录
- 数据类型：post请求的参数类型比get请求更多
- 使用场景：get请求一般用于对服务无影响的场景，例如获取资源、获取数据等；post请求一般用于对服务有影响的场景，例如表单提交等

### 常见的请求头、响应头
- 请求头（Request Header）
    - Accept-Language
    - Accept-Encoding
    - Connection
    - Host
    - Referer
    - Cookie
- 响应头（Response Header）
    - Date
    - server
    - Connection
    - Cache-Control
    - content-type
        - application/www-form-urlencoded
        - multipart/form-data
        - application/json
        - text/xml

### OPTIONS使用场景
- 用来询问服务端支持的所有请求方法
- 用来询问访问权限，在跨域场景下对于复杂请求通过发起options请求可以判断是否对当前请求资源有访问权限

### http1.0与http1.1的区别
- 连接：http1.0默认不支持持久化连接，因此每次的请求都需要重新建立tcp连接；http1.1默认支持持久化连接，可实现多http请求共用同一个tcp连接。
- 资源请求：http1.0请求资源默认全部返回；而http1.1支持断点传送，可设置请求资源的访问范围
- 缓存策略：http1.0只支持If-modified-since、Expires缓存策略；http1.1在此基础上多了Etag等多种新的缓存策略
- 请求方式：相对http1.0，http1.1新增了多种请求方式，如OPTIONS、PUT、HEAD等

### http1.1 与 http2.0 区别
- http2.0实现了多路复用，解决了“头部阻塞”问题
- http2.0采用二进制编码协议；而http1.1采用ASCII码
- http2.0支持头信息压缩
- http2.0支持服务端推送

### http 与 https 区别
- https需要CA认证（花钱），http不需要
- https通过SSL加密传输，http通过明问传输
- https端口号为443，http为80
- https是ssl与http构建的加密协议传输形式、需要身份认证等传输更安全

### 浏览器输入地址到回车 发生了什么？
- URL解析：浏览器对URL解析，获取URL的传输协议以及判断URL地址的合法性
- 本地缓存判定：浏览器根据url地址判断是否存在本地缓存且在有效期内，如果有直接使用，如果没有则向服务器发起资源请求
- DNS解析：根据URL地址解析对应的DNS地址，如本地有DNS缓存则用本地缓存，若没有则向最近的dns服务发起请求
- 获取MAC地址：根据IP地址获取对应的MAC地址
- 建立TCP连接：浏览器发起请求，携带请求报文以及随机序号 请求服务端；服务端接受报文后，返回确认连接报文、随机序号给客户端；客户端接受报文后向服务端发起确认报文，两端建立TCP连接
- https握手：若请求为https请求，则需要额外一次TSL握手。客户端携带版本号、随机数以及加密算法请求服务端；服务端确认加密算法，并发送随机数和加密证书给客户端；客户端检测加密证书有效性，且根据证书公钥对随机数进行加密请求服务端；服务端根据私钥进行解密；此后双端根据生成的三个随机数生成密钥进行后续传输内容的加解密
- 返回数据：客户端接受到服务端返回的资源信息，开始解析进行页面渲染
- 页面渲染：浏览器根据html文件构建DOM，加载资源文件构建CSSOM，最终合成render tree，进行页面的布局、绘制
- 断开TCP连接：客户端认为服务端传输结束时会发起一个释放连接的请求，服务端接收到之后会发送一个确认断开的报文，并进入close_wait状态，此期间服务端仍可以向客户端传送数据，完毕后向客户端发送释放请求报文，客户端接受请求后会发送确认释放的报文

### 什么是keep-alive
keep-alive即长连接，http1.0默认不开启keep-alive，每次访问、应答，客户端/服务端都需要重新建立连接；通过设置Connection:keep-alive则开启长连接模式，请求结束后连接不会断开而是等待下一个请求，http1.1默认开启长连接。
- 优点：
    - 减少重建连接带来的网络延迟
    - 降低请求阻塞
- 缺点：
    - 长时间连接，会导致系统占用不被释放，可通过设置Connection:close手动关闭

### 一个完整的URL包含哪些部分
- 协议
- 域名
- 端口号
- 路径
- 查询参数
- 锚

### 常见的状态码
- 2xx 请求成功
    - 200 请求成功
    - 202 请求成功，但无响应实体
    - 206 范围请求
- 3xx 请求重定向
    - 301 永久重定向
    - 302 临时重定向
    - 304 协商缓存，命中
- 4xx 客户端错误
    - 400 请求报文语法异常
    - 401 身份认证
    - 403 无访问权限
    - 404 未找到请求资源
    - 405 请求方法错误
    - 415 服务端无法解析请求附带的数据格式
- 5xx 服务端错误
    - 500 服务端异常
    - 502 网关异常
    - 503 服务器无法访问
    - 504 网关超时

### 常见请求头
- Accept：浏览器支持的MIME类型，对应服务端的Content-Type
- Accept-Encoding：浏览器支持的压缩类型
- Content-Type：客户端发送内容的类型
- Cache-Control：缓存控制
- If-Modified-Since：缓存控制，对应Last-Modified
- If-None-Match：缓存控制，对应Etag
- Expires：缓存控制
- Max-age：最大过期时间
- Host：请求服务器的URL
- Origin：最初的请求
- Referer：页面的来源URL
- Cookie：cookie信息
- Connection：客户端与服务端连接时对长连接的处理
- User-Agent：客户端的一些信息


### 什么是简单请求、复杂请求
- 简单请求
    - 请求方法为get、post、head
    - 没有自定义头
    - Content-Type设置为 text/plain、multipart/form-data、application/x-www-form-urlencoded
- 复杂请求
    - 其他所有

### 解决跨域的方式有哪些
- CORS
- JSONP
- 反向代理

### 什么是XSS攻击
XSS是一种跨站脚本植入技术，即通过对网站植入恶意脚本，从而获取用户信息、流量劫持、DOM结构篡改、模拟请求攻击服务器等

### 什么是CSRF攻击
跨站请求伪造攻击