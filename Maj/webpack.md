项目中用过webpack吗？详细描述一下。

```js
//  webpack4.0
//  基本

//  html-webpack-plugin webpack打包出来的js文件我们需要引入到html中
//  clean-webpack-plugin 清空文件夹
//  autoprefixer  css添加浏览器前缀
//  mini-css-extract-plugin  css样式从js文件中提取到单独的css文件中。这里需要说的细一点,上面我们所用到的mini-css-extract-plugin会将所有的css样式合并为一个css文件。如果你想拆分为一一对应的多个css文件,我们需要使用到extract-text-webpack-plugin，而目前mini-css-extract-plugin还不支持此功能。我们需要安装@next版本的extract-text-webpack-plugin
//  url-loader ile-loader   搭配使用，功能与 file-loader 类似，如果文件小于限制的大小。则会返回 base64 编码，否则使用 file-loader 将文件移动到输出的目录中
//  babel-loader  js代码兼容更多的环境

// 优化 
// 打包速度 
// mode development production两个参数 production模式下会进行tree shaking(去除无用代码)和uglifyjs(代码压缩混淆)
// HappyPack 多进程Loader转换
// webpack-parallel-uglify-plugin  优化代码的压缩时间
// DllPlugin DllReferencePlugin 抽离三方模块 对于开发项目中不经常会变更的静态依赖文件。类似于我们的elementUi、vue全家桶等等。因为很少会变更，所以我们不希望这些依赖要被集成到每一次的构建逻辑中去。 这样做的好处是每次更改我本地代码的文件的时候，webpack只需要打包我项目本身的文件代码，而不会再去编译第三方库。以后只要我们不升级第三方包的时候，那么webpack就不会对这些库去打包，这样可以快速的提高打包的速度。
// cache-loader 缓存 我们每次执行构建都会把所有的文件都重复编译一遍，这样的重复工作是否可以被缓存下来呢，答案是可以的，目前大部分 loader 都提供了cache 配置项。比如在 babel-loader 中，可以通过设置cacheDirectory 来开启缓存，babel-loader?cacheDirectory=true 就会将每次的编译结果写进硬盘文件（默认是在项目根目录下的node_modules/.cache/babel-loader目录内，当然你也可以自定义）
// 体积
// externals  按照官方文档的解释，如果我们想引用一个库，但是又不想让webpack打包，并且又不影响我们在程序中以CMD、AMD或者window/global全局等方式进行使用，那就可以通过配置Externals。这个功能主要是用在创建一个库的时候用的，但是也可以在我们项目开发中充分使用Externals的方式，我们将这些不需要打包的静态资源从构建逻辑中剔除出去，而使用 CDN
// tree-shaking  清除代码中无用

```

**babel编译原理、AST**

- babylon 将 ES6/ES7 代码解析成 AST

- babel-traverse 对 AST 进行遍历转译，得到新的 AST

- 新 AST 通过 babel-generator 转换成 ES5

  抽象语法树 (Abstract Syntax Tree)，是将代码逐字母解析成 树状对象对象 的形式 



提取公共代码：

```js
entry: {
    app:[
        path.join(__dirname, '../src/index.js')
    ],
    vendor: ['react', 'react-router-dom', 'redux', 'react-dom', 'react-redux']
},
output: {
    path: path.join(__dirname, '../dist'),
    filename: '[name].[hash].js',
    chunkFilename: '[name].[chunkhash].js'
},

```

提取css：

```css
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

{
    test: /\.css$/,
    use: [{loader: MiniCssExtractPlugin.loader}, {
        loader:'css-loader',
        options: {
            modules: true,
            localIdentName: '[local]--[hash:base64:5]'
        }
    }, 'postcss-loader']
 }
 
 new MiniCssExtractPlugin({ // 压缩css
    filename: "[name].[contenthash].css",
    chunkFilename: "[id].[contenthash].css"
})

```

hash、chunkhash和contenthash：

hash是跟整个项目的构建相关，只要项目里有文件更改，整个项目构建的hash值都会更改，并且全部文件都共用相同的hash值

chunkhash和hash不一样，它根据不同的入口文件(Entry)进行依赖文件解析、构建对应的chunk，生成对应的哈希值。

contenthash是针对文件内容级别的，只有你自己模块的内容变了，那么hash值才改变，所以我们可以通过contenthash解决上诉问题

#### 文件压缩(build)

以前webpack使用uglifyjs-webpack-plugin来压缩文件，使我们打包出来的文件体积更小。

现在只需要配置mode即可自动使用开发环境的一些配置，包括JS压缩等等

```js
mode:'production'
```

公共块提取(build)

这表示将选择哪些块进行优化。当提供一个字符串，有效值为all，async和initial。提供all可以特别强大，因为这意味着即使在异步和非异步块之间也可以共享块。

```css
optimization: {
    splitChunks: {
      chunks: 'all'
    }
}
```

#### css压缩(build)

```css
const OptimizeCssAssetsPlugin = require('optimize-css-assets-webpack-plugin');

plugins: [
    ...
    new OptimizeCssAssetsPlugin()
],

```

## 打包清空(build)

const CleanWebpackPlugin = require('clean-webpack-plugin');

new CleanWebpackPlugin(), // 每次打包前清空

Manifest
你的应用程序中，形如 index.html 文件、一些 bundle 和各种资源加载到浏览器中，会发生什么？你精心安排的 /src 目录的文件结构现在已经不存在，所以 webpack 如何管理所有模块之间的交互呢？这就是 manifest 数据用途的由来……
当编译器compiler开始执行、解析和映射应用程序时，他会保留所有模块的详细要点。这个数据集合称为manifest，当完成打包并发送到浏览器时，会在运行时通过 Manifest 来解析和加载模块。无论你选择哪种模块语法，那些 import 或 require 语句现在都已经转换为 __webpack_require__ 方法



### webpack4

webpack——模块打包工具

package.json 调整 package.json 文件，以便确保我们安装包是private(私有的)，并且移除 main入口。这可以防止意外发布你的代码 

webpack4速度更快，大型项目节约90%构建时间，内置更多api



##### loader

url-loader,图片打包成base64，减少请求个数，如果太大会增加js大小同时造成页面加载白屏，同时限制图片大小，与file-loader类似

##### postcss-loader，autoprefixer

自动增加css前缀

importloaders,数量默认是0 

``` js
{ loader: 'css-loader', options: { modules: true, importLoaders: 1 } }   
//modules  样式不冲突
```

##### plugin  

plugin可以在webpack运行到某个时刻的时候帮你做一些事情

htmlwebpackplugin 打包结束后自动生成html并把打包的js自动引入html

##### sourcemap

我们在打包中，将开发环境中源代码经过压缩，去空格，babel编译转化，最终可以得到适用于生产环境的项目代码，这样处理后的项目代码和源代码之间差异性很大，会造成无法debug的问题 ,sourcemap就是为了解决上述代码定位的问题，简单理解，就是构建了处理前的代码和处理后的代码之间的桥梁。主要是方便开发人员的错误定位。 

##### webpackdevserver()

##### modules replacement    (hmr功能)

##### tree shaking （只支持es module 也就是 import）  

##### webpack-merge

##### code-splitting

##### 懒加载

##### library



##### 

