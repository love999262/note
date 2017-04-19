先看看 jQuery里一个类似的东西吧: `$.Deferred()`
[$.deffered](http://api.jquery.com/?s=%24.Deferred)
下面开一下传统$.ajax处理回调函数的做法:
```
$.ajax({
  url: "test.html",
  success: function(){
    alert("哈哈，成功了！");
  },
  error:function(){
    alert("出错啦！");
  }
});
```
很熟悉的success error的两个回调函数,那么我们变一下
```
$.ajax("test.html")
.done(function(){ alert("哈哈，成功了！"); })
.fail(function(){ alert("出错啦！"); });
```

> By default, all requests are sent asynchronously (i.e. this is set to true by default). If you need synchronous requests, set this option to false. Cross-domain requests and dataType: "jsonp" requests do not support synchronous operation. Note that synchronous requests may temporarily lock the browser, disabling any actions while the request is active. As of jQuery 1.8, the use of async: false with jqXHR ($.Deferred) is deprecated; you must use the success/error/complete callback options instead of the corresponding methods of the jqXHR object such as jqXHR.done().
