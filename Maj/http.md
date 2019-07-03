##### get和post误区

（<https://mp.weixin.qq.com/s?__biz=MzI3NzIzMzg3Mw==&mid=100000054&idx=1&sn=71f6c214f3833d9ca20b9f7dcd9d33e4#rd> ）

1.长度

我们经常说get请求参数大小存在限制，而post请求的参数大小是无限制的，实际上，http协议从未规定过get/post请求的长度限制，对get参数的限制来源于浏览器和web服务器，不同的浏览器和web服务器限制的长度不一样

2.请求缓存

get请求类似于查找的过程，用户获取数据，可以不用每次都与数据库连接，所以可以使用缓存 post不同，post做的一般是修改和删除的工作，所以必须与数据库交互，所以不能使用缓存。因此post请求适合于请求缓存 

- GET在浏览器回退时是无害的，而POST会再次提交请求。
- GET产生的URL地址可以被Bookmark，而POST不可以。
- GET请求会被浏览器主动cache，而POST不会，除非手动设置。
- GET请求只能进行url编码，而POST支持多种编码方式。
- GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留。
- GET请求在URL中传送的参数是有长度限制的，而POST么有。
- 对参数的数据类型，GET只接受ASCII字符，而POST没有限制。
- GET比POST更不安全，因为参数直接暴露在URL上，所以不能用来传递敏感信息。
- GET参数通过URL传递，POST放在Request body中。

##### cookie如何防止xss攻击

xss(跨站脚本攻击)，是指攻击者在返回的html中嵌入js脚本

防止：httponly

##### websocket

websocket是一个持久化的协议,服务端就可以主动推送信息给客户端 

典型的websocket握手

```js
...
upgrade:websocket
connection:upgrade
...
```

同时，在传统的方式上，要不断的建立，关闭HTTP协议，由于HTTP是非状态性的，每次都要重新传输 identity info(鉴别信息），来告诉服务端你是谁。 虽然接线员很快速，但是每次都要听这么一堆，效率也会有所下降的， 但是Websocket只需要一次HTTP握手，所以说整个通讯过程是建立在一次连接/状态中，也就避免了HTTP的非状态性，服务端会一直知道你的信息，直到你关闭请求，这样就解决了接线员要反复解析HTTP协议，还要查看identity info的信息 

websocket如何检测心跳包



##### 如何理解http协议

##### http与https的区别

<https://juejin.im/post/5b44a485e51d4519945fb6b7#heading-40> 

#### 如何实现多页面共享登录？如何实现同项目多页面不同储存？

##### 解释一下三次握手和四次挥手

##### 如何理解http状态码 200、200（from cache）、304

##### 如何解决跨域

##### Last-Modified,Etag,Expire区别

**Last-Modified 与 ETag 是可以一起使用的，服务器会优先验证 ETag，一致的情况下，才会继续比对 Last-Modified，最后才决定是否返回 304。** 

<https://segmentfault.com/q/1010000004200644> 

https://www.cnblogs.com/waruzhi/p/3831089.html

last-modified 是httpheader中资源最后修改时间，如果带有last-modified，下一次发送http请求，将会带if-modified-since的httpheader，如果没有过期，将会收到304的响应，从缓存中获取。

etag是httpheader中代表资源的标签，在服务端生成。如果带有etag，下一次发送etag的请求，如果etag没有发生变化将收到304的响应，从缓存中获取

浏览器默认的缓存是放在内存内的，但我们知道，内存里的缓存会因为进程的结束或者说浏览器的关闭而被清除，而存在硬盘里的缓存才能够被长期保留下去。很多时候，我们在network面板中各请求的size项里，会看到两种不同的状态：`from memory cache` 和 `from disk cache`，前者指缓存来自内存，后者指缓存来自硬盘。而控制缓存存放位置的，不是别人，就是我们在服务器上设置的Etag字段。在浏览器接收到服务器响应后，会检测响应头部（Header），如果有Etag字段，那么浏览器就会将本次缓存写入硬盘中。

##### nginx部分知识

跨域（反向代理）

负载均衡（Upstream）

gzip

请求过滤（404  500 页面）

缓存与不缓存



**301,302**

301 **永久重定向** 

302 **临时重定向** 



##### cookie有那些属性

**name**:cookie的名称 

**value**:cookie的值 

**domain**:为可以访问此cookie的域名 

**path**:字段为可以访问此cookie的页面路径。 比如domain是abc.com,path是/test，那么只有/test路径下的页面可以读取此cookie 

**expires/max-age**:字段为此cookie超时时间。若设置其值为一个时间，那么当到达此时间后，此cookie失效。不设置的话默认值是Session，意思是cookie会和session一起失效。当浏览器关闭(不是浏览器标签页，而是整个浏览器) 后，此cookie失效 

**size**:此cookie大小 

**http**:cookie的httponly属性。若此属性为true，则只有在http请求头中会带有此cookie的信息，而不能通过document.cookie来访问此cookie 

**secure**:设置是否只能通过https来传递此条cookie 



**HTTP请求头含有那些属性**



Accept: 浏览器端可以接受的媒体类型( text/html ) ,Accept: */*  代表浏览器可以处理所有类型 

Accept-Encoding : 浏览器申明自己接收的编码方法，通常指定压缩方法，是否支持压缩，支持什么压缩方法（gzip，deflate），（注意：这不是只字符编码） 

Accept-Language : 浏览器申明自己接收的语言 

Content-type:

Content-Disposition:

Origin:发起一个针对跨域资源共享的请求（该请求要求服务器在响应中加入一个`Access-Control-Allow-Origin`的消息头，表示访问控制所允许的来源） 

Referer:告诉服务器我是从哪个页面链接过来的，服务器籍此可以获得一些信息用于处理。比如从我主页上链接到一个朋友那里，他的服务器就能够从HTTP Referer中统计出每天有多少用户点击我主页上的链接访问他的网站 

User-Agent:客户端使用的操作系统和浏览器的名称和版本 

cookie：

Host:初始URL的主机和端口















































