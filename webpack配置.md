## webpack的主要作用是模块的打包,压缩等功能算是辅助,如果过大的项目不建议用webpack本身的压缩功能,建议用谷歌closure,其提供的功能主要还是让你可以在浏览器中写JS像写NODE那样分类模块,最终将所有的模块打包成一个或者几个文件,便于代码的模块化,有点类似于Browserify,可以配合gulp使用实现一个基本的前端工程化流程.
## 首先安装nodejs安装好之后创建一个测试用的目录Webpacktest进入:

安装webpack(如果没有全局安装需要全局安装):

```
npm install webpack -g
npm install --save-dev webpack 
```

- 创建一个webpack.config.js的配置文件(最后有示例)

注意,相应的loader都需要通过npm安装

```
npm install --save-dev style-loader
```
关于压缩,打包后生成的一个或者多个文件在未压缩的情况下体积很大,这时候可以用第三方工具或者webpack自带的压缩工具进行压缩

new webpack.optimize.UglifyJsPlugin就是压缩方法

webpack模块之间互相导入的问题:
比较典型的就是从哪个网站随便下载而不是npm下来的jQuery和其他依赖jquery的模块之间总是会有各种$ is not defined 的问题,即使在index.js 中最先导入jquery依然会报错,这是因为????(我他妈也不知道因为什么,可能跟commonJs规范有关)

```
npm install imports-loader --save-dev
```

```入口的JS
{
    entry:{
    index:'./src/js/index.js'
    }
}

require('./jqGreen');
$('#box').css('color','green');
// $ is not defined
require('imports?$=jquery!./jqGreen');
```
上面代码，把变量$注入进模块jqGreen.js。同时，我们指定了变量$=jquery。等于是在jqGreen.js文件的最顶上，加上了var $=require('jquery')。这样，程序就不会报$ is not defined的错误了。
[segmentfault](https://segmentfault.com/a/1190000007515136)

## es2015的preset报错问题
```
npm install --save-dev babel-preset-es2015
```
## jQuery未找到问题

```
    plugins: [
        new webpack.ProvidePlugin({
            $: "jquery2",
            jquery: "jquery2",
            "window.jQuery": "jquery2",
            jQuery: "jquery2"
        })
    ]
```
## 字体文件错误问题

```
loaders: [{
            test: /\.(gif|jpg|png|woff|svg|eot|ttf)\??.*$/, 
            loader: 'url-loader?limit=50000&name=[path][name].[ext]'
        }
```

## WIN系统路径问题

```
和path有关暂时不想研究
```

#明明在全局环境中添加了jquery但是却任然报错问题:
- 可能该模块是按照commonjs标准写了并且引入了jQuery而npm的jquery模块名字和该模块内部定义的不太一样导致在运行该模块时并未找到jquery,需要手动去改.
比较完整的webpack应该是这样的:
```
var webpack = require('webpack');
module.exports = {
    entry: [
        './src/js/script.js'
    ],
    output: {
        path: './publish',
        filename: 'moe.min.js'
    },
    module: {
        loaders: [{
            test: /\.(gif|jpg|png|woff|svg|eot|ttf)\??.*$/, 
            loader: 'url-loader?limit=50000&name=[path][name].[ext]'
        }, {
            test: /\.less$/,
            loader: "style-loader!css-loader!less-loader"
        }, {
            test: /\.css$/,
            loader: "style-loader!css-loader"
        }, {
            test: /\.js$/,
            loader: 'babel-loader',
            exclude: /node_modules/,
            query: {
                presets: ['es2015']
            }
        }]
    },
    plugins: [
        new webpack.ProvidePlugin({
            $: "jquery2",
            jquery: "jquery2",
            "window.jQuery": "jquery2",
            jQuery: "jquery2"
        }),
        new webpack.optimize.UglifyJsPlugin({
            compress: {
                warnings: false
            }
        })
    ]
};

```
