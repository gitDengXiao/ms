项目中用过webpack吗？详细描述一下。

##### webpack:

devServer : HtmlWebpackPlugin插件 webpack会自动将打包好的JS注入到这个index.html模板里面。

module : css-loader使你能够使用类似@import 和 url(...)的方法实现 require()的功能；style-loader将所有的计算后的样式加入页面中； 二者组合在一起使你能够把样式表嵌入webpack打包后的JS文件中。postcss-loader生成写CSS的时候浏览器前缀

module ： webpack最终会将各个模块打包成一个文件，因此我们样式中的url路径是相对入口html页面的，而不是相对于原始css文件所在的路径的。这就会导致图片引入失败。这个问题是用file-loader解决的，file-loader可以解析项目中的url引入（不仅限于css），根据我们的配置，将图片拷贝到相应的路径，再根据我们的配置，修改打包后文件引用路径，使之指向正确的文件。另外，如果图片较多，会发很多http请求，会降低页面性能。这个问题可以通过url-loader解决

按路由加载。react-router4.0以上提供了react-loadable

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

#### 公共块提取(build)

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
