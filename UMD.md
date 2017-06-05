# UMD是指一种现在通用的JS组件的写法,用这种方式来写的JS组件既可以在浏览器中运行,也可以在NODE中运行,一般来说通过NPM的方式或者是通过<script>
标签引入的方式都可以加载,这也是现在一些出名的库用的较多的方法.

```
(function (window, factory) {
    if (typeof exports === 'object') {
    
        module.exports = factory();
    } else if (typeof define === 'function' && define.amd) {
    
        define(factory);
    } else {
    
        window.eventUtil = factory();
    }
})(this, function () {
    //module ...
});
```
