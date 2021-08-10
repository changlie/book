# Introduction

Hypertext Transfer Protocol (HTTP) is an application-layer protocol for transmitting hypermedia documents, such as HTML. It was designed for communication between web browsers and web servers, but it can also be used for other purposes. HTTP follows a classical client-server model, with a client opening a connection to make a request, then waiting until it receives a response. HTTP is a stateless protocol, meaning that the server does not keep any data (state) between two requests.

![logo](img/http.jpeg)


### 参考
[MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/HTTP)


# Summary
http 由头部, body组成。  
头部信息比较重要信息有请求方法，响应状态码，Content-Type, Content-length，
Cookie, Set-Cookie。

### 请求方法
**请求方法**是用来指示这个将要干嘛的，是否是安全,是否幂等,请求结果能否被缓存。  
比如，GET说明这个方法从语义上看，获取资源的；DELETE是用来删除数据的。

这里**安全**指的是否会改变服务器的状态，就是说会不会修改数据，比如GET, HEAD, OPTIONS。    
但是有些方法从语义是安全，可实现上它是可以修改数据的，比如用GET做删除，更新操作，我以前经常干这种事情。

**幂等**是指方法没有副作用，请求执行一次或多次，服务器的最终状态是一致的，比如GET，DELETE。  
GET请求取数据，无论你取多少次，最终服务器的数据还是这么点，不多不少。    
DELETE请求删数据，无论你删多少次，最终服务器的都少那么几个你删除的数据，不会多删少删。  
> （the GET, HEAD, PUT, and DELETE methods are idempotent, but not the POST method. All safe methods are also idempotent.）

### 响应状态码
Response Status Code 由3们数字组成。  
3开头表示重定向:  
301,308 永久重定向  
302,307 临时重定向  

4开头一般表示前端出错，比如： 
400 - Bad Request （错误请求） 服务器不理解请求的语法   
401 表示无权访问  
403 Forbidden 代表客户端错误，指的是服务器端有能力处理该请求，但是拒绝授权访问。这个状态类似于 401，但进入该状态后不能再继续进行验证。该访问是长期禁止的，并且与应用逻辑密切相关（例如不正确的密码）。    
404 很有可能是url写错了  
405 Method Not Allowed 很有可能是请求方法用错了，服务器要求这个请求要用POST，但前端用了GET导致出错

5开头表示程序出错，一般是因为程序缺陷引起的:  
500 Internal Server Error（服务器内部错误）  
502 Bad Gateway（错误网关）  
504 Gateway Timeout （网关超时）

### Content-Type, Content-length
这两者一般成对出现，因为它们分别描述的是body的数据类型及数据大小  
此外与body有关的头部`Content-Encoding`表示的是body数据所使用的压缩算法名

### Cookie, Set-Cookie
http是无状态的，一些网站需要用户登录才能使用，故服务器可使用Set-Cookie响应头给浏览器发送Session Id， 浏览器会将Set-Cookie响应头的信息保存本地作为当前网站的Cookie信息，
之后每次访问这个网站的时候，带上这些Cookie信息，这样浏览器与服务器就建立了Session关联


