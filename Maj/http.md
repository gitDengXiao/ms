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





##### nginx部分知识

跨域（反向代理）

负载均衡（Upstream）

gzip

请求过滤（404  500 页面）

缓存与不缓存
