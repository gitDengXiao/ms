#### 1.什么是nuxt

Nuxt 是一个基于 Vue 生态的更高层的框架，为开发**服务端渲染**的 Vue 应用提供了极其便利的开发体验 。

#### 2.SSR 可以解决什么问题

1.解决单页面应用的 **SEO** 的问题，对于一般网站影响不大，但是对于论坛类，内容类网站来说是致命的，搜索引擎无法抓取页面相关内容，也就是用户搜不到此网站的相关信息 。

2.更快的**内容到达时间**(time-to-content)，特别是对于缓慢的网络情况或运行缓慢的设备 。传统的SPA应用是将bundle.js从服务器获取，然后在客户端解析并挂载到dom。而SSR直接将HTML字符串传递给浏览器。大大加快了首屏加载时间 

#### 3.安装搭建

yarn create nuxt-app <项目名> 

可以选择：

​	集成的服务器端框架 

​	UI框架 

​	...

```js
|-- assets                           // 用于组织未编译的静态资源入LESS、SASS 或 JavaScript
|-- components                       // 用于自己编写的Vue组件，比如滚动组件，日历组件，分页组件
|-- layouts                          // 布局目录，用于组织应用的布局组件，不可更改。
|-- middleware                       // 用于存放中间件
|-- pages                            // 用于存放写的页面，我们主要的工作区域
|-- plugins                          // 用于存放JavaScript插件的地方
|-- static                           // 用于存放静态资源文件，比如图片
|-- store                            // 用于组织应用的Vuex 状态管理。
|-- server                           // node文件
|-- .editorconfig                    // 开发工具格式配置
|-- .eslintrc.js                     // ESLint的配置文件，用于检查代码格式
|-- .gitignore                       // 配置git不上传的文件
|-- nuxt.config.json                 // 用于组织Nuxt.js应用的个性化配置，已覆盖默认配置
|-- package.json                     // npm包管理配置文件
```



```js
//koa server下面的index.js
const Koa = require('koa')
const consola = require('consola')
const { Nuxt, Builder } = require('nuxt')

const app = new Koa()

// Import and Set Nuxt.js options
let config = require('../nuxt.config.js')
config.dev = !(app.env === 'production')

async function start() {
  // Instantiate nuxt.js
  const nuxt = new Nuxt(config)

  const {
    host = process.env.HOST || '127.0.0.1',
    port = process.env.PORT || 3000
  } = nuxt.options.server

  // Build in development
  if (config.dev) {
    const builder = new Builder(nuxt)
    await builder.build()
  } else {
    await nuxt.ready()
  }

  app.use(ctx => {
    ctx.status = 200
    ctx.respond = false // Bypass Koa's built-in response handling
    ctx.req.ctx = ctx // This might be useful later on, e.g. in nuxtServerInit or with nuxt-stash
    nuxt.render(ctx.req, ctx.res)
  })

  app.listen(port, host)
  consola.ready({
    message: `Server listening on http://${host}:${port}`,
    badge: true
  })
}

start()

```

#### 4.layout页面

```html
//默认
<template>
  <nuxt/>
</template>
```

```vue
//自定义 layouts/blog.vue
<template>
  <div>
    <div>我的博客导航栏在这里</div>
    <nuxt/>
  </div>
</template>

<template>
<!-- Your template -->
</template>
<script>
    export default {
      layout: 'blog'
    }
</script>

//layouts文件夹下建立一个error.vue文件，它相当于一个显示应用错误的组件
```

#### 5.**nuxt.config.js**  文件配置

**配置 head** 

title meta link ...

**loading**

该配置项用于个性化定制 Nuxt.js 使用的加载组件 

**引入css**

**router** 

该配置项可用于覆盖 Nuxt.js 默认的 `vue-router` 配置 

**modules** 

该配置项允许您将Nuxt模块添加到项目中 

**build**

Nuxt.js 允许你在自动生成的 `vendor.bundle.js` 文件中添加一些模块，以减少应用 bundle 的体积。如果你的应用依赖第三方模块 



**跨域**：npm i @nuxtjs/axios @nuxtjs/proxy -D

```js
  modules : [
    '@nuxtjs/axios',
    '@nuxtjs/proxy'
  ],
  axios: {
    proxy: true
  },
  proxy : [
    [
      '/api',
      {
        target : 'http://localhost:3033', 
        pathRewrite : {'^/api' : '/'}
      }
    ]
  ]
```

##### 加入插件比如**element**

在文件**plugins**新建 name.js

```js
import Vue from 'vue'
import ElementUI from 'element-ui'
Vue.use(ElementUI)
```

在文件nuxt.config.js添加代码 

```js
  vender:[
    'element-ui'    //防止多次打包
  ],

  plugins: [
    { src: '~plugins/name.js', ssr: true }   //如果是  ssr:false  只是在客户端用
  ]


```

#### 6.异步数据

Nuxt.js 扩展了 Vue.js，增加了一个叫 `asyncData` 的方法，使得我们可以在**设置组件的数据之前能异步获取或处理数据**。 

**注意：**由于`asyncData`方法是在组件 初始化 前被调用的，所以在方法内是没有办法通过 `this` 来引用组件的实例对象。 

```js
export default {
  async asyncData ({ params }) {
    let { data } = await axios.get(`https://my-api/posts/${params.id}`)
    return { title: data.title }
  }
}
```

在服务器端调用`asyncData`时，您可以访问用户请求的`req`和`res`对象 

```js
export default {
  async asyncData ({ req, res }) {
    // 使用 req 和 res
    if (process.server) {  // 检查是否在服务器端
     return { host: req.headers.host }
    }
    return {}
  }
}
```

#### 7.中间件

中间件允许您定义一个自定义函数运行在一个页面或一组页面渲染之前。 

```js
export default function ({ store, redirect }) {
  
  if (!user) {
    return redirect('/login')
  }
}
//页面
export default {
    middleware: 'auth'
  }

```



#### 8.server端api编写

nuxt的server端使用的是express，故server端api直接编写express router即可。server端目录组织如图： 

![img](https://user-gold-cdn.xitu.io/2017/8/9/1320b802915a7122191bd101f4a27820?imageView2/0/w/1280/h/960/format/webp/ignore-error/1) 

server/index.js 文件是express的启动文件，plugins和middleware文件是axios的配置，api文件夹内即api接口。

server/index.js文件里面对api引用如下：

![img](https://user-gold-cdn.xitu.io/2017/8/9/3c91bc54c791678f56d11bfb182a2806?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

我们先看看axios的配置，通过对process.env的匹配来区分线上与测试环境，同时在middleware文件中对接口进行鉴权。

![img](https://user-gold-cdn.xitu.io/2017/8/9/042eaaaeea63368ac4c176cea851d19a?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

![img](https://user-gold-cdn.xitu.io/2017/8/9/cdacbb318bc983120c2e97d6691c9cb5?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

之后在api/index.js文件中对各接口进行引用和聚合

![img](https://user-gold-cdn.xitu.io/2017/8/9/3672d06d4dd4cdd1bc3b435f929fa7f5?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

在所有接口文件中，以announcement.js举例：

![img](https://user-gold-cdn.xitu.io/2017/8/9/209f429d29bb0a703cf835526049df00?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)









  















 

 

 