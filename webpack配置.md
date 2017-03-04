# 首先安装nodejs安装好之后创建一个测试用的目录Webpacktest进入:

安装webpack(如果没有全局安装需要全局安装):

```
npm install webpack -g
npm install --save-dev webpack 
```

- 创建一个webpack.config.js的配置文件:
```
var webpack = require('webpack');
module.exports = {
    entry: [
    // 入口文件,可以使数组或者是字符串,会在加载的时候找到对应的模块加载
        'webpack/hot/only-dev-server',
        './js/app.js'
    ],
    output: {
    输出目录和输出最终的文件名,打包成一个模块的最终成品.
        path: './build',
        filename: 'bundle.js'
    },
    module: {
    模块加载器
        loaders: [
        { test: /\.js?$/, loaders: ['react-hot', 'babel'], exclude:     /node_modules/ },
        { test: /\.js$/, exclude: /node_modules/, loader: 'babel-loader'},
        { test: /\.css$/, loader: "style!css" },
        {test: /\.less/,loader: 'style-loader!css-loader!less-loader'}
        ]
    },
    resolve:{
        extensions:['','.js','.json']
    },
    plugins: [
        new webpack.NoErrorsPlugin()
    ]
};
```
```
var webpack = require('webpack');
var path = require('path');
module.exports = {
    entry: [
        // 入口文件
        './src/js/script.js'
    ],
    output: {
        // 输出目录和输出最终的文件名,打包成一个模块的最终成品.
        path: './publish',
        filename: 'moe.min.js'
    },
    module: {
        loaders: [{
            test: /\.css$/,
            loader: "style-loader!css-loader"
        }, {
            test: /\.(png|jpg|gif|ttf|eot|svg|woff)$/,
            loader: 'url-loader?limit=819200'
        }, {
            test: /\.less$/,
            loader: "style-loader!css-loader!less-loader"
        },  {
            test: /\.css$/, 
            loader: "style-loader!css-loader"
        }, {
            test: /\.js$/,
            loader: 'babel-loader'
        }]
    }
};

```
注意,相应的loader都需要通过npm安装

```
npm install --save-dev style-loader
```
关于压缩,打包后生成的一个或者多个文件在未压缩的情况下体积很大,这时候可以用第三方工具或者webpack自带的压缩工具进行压缩:
```
var webpack = require('webpack');
var path = require('path');
module.exports = {
    entry: [
        './src/js/kaguya.js'
    ],
    output: {
        // 输出目录和输出最终的文件名,打包成一个模块的最终成品.
        path: './',
        filename: 'kaguya.min.js'
    },
    module: {
        loaders: [{
            test: /\.less$/,
            loader: "style-loader!css-loader!less-loader"
        }, {
            test: /\.js$/,
            loader: 'babel-loader'
        }, {
            test: /\.(png|jpg)$/,
            loader: 'url-loader?limit=40000'
        }]
    },
    plugins: [
        new webpack.optimize.UglifyJsPlugin({
            compress: {
                warnings: false
            }
        })
    ]
};

```
new webpack.optimize.UglifyJsPlugin就是压缩方法
