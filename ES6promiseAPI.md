先看看 jQuery里一个类似的东西吧: [$.deffered](http://api.jquery.com/?s=%24.Deferred)
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
.done(function(){console.log('success')})
.fail(function(){console.log('error')});
```

> By default, all requests are sent asynchronously (i.e. this is set to true by default). If you need synchronous requests, set this option to false. Cross-domain requests and dataType: "jsonp" requests do not support synchronous operation. Note that synchronous requests may temporarily lock the browser, disabling any actions while the request is active. As of jQuery 1.8, the use of async: false with jqXHR ($.Deferred) is deprecated; you must use the success/error/complete callback options instead of the corresponding methods of the jqXHR object such as jqXHR.done().

这种链式调用的方法只有在1.5以后的版本的jQuery中才可以使用,在这之前返回的是JQXHR对象,而之后返回的则是deferred对象,目前来看用惯了前者的人可能感觉还是前者比较顺手,或者两者用起来差不多,那么我们继续往下看:

```
$.ajax("test.html")
.done(function(){callback1()})
.fail(function(){console.log('error')} )
.done(function(){callback2()});
```
这里加入了两个callback,按照顺序依次执行,这个例子传统回调好像也是可以做到的,虽然稍微麻烦一点.

再看:
```
$.when($.ajax("test1.html"), $.ajax("test2.html"))
.done(function(){console.log('success all')})
.fail(function(){console.log('error')});
```
$.when? what the fuck?先不急,先说下这段代码的意思,这里是指如果$.when中的两个$.ajax成功
了就走done方法否则就走fail方法

好,继续看[$.when](http://api.jquery.com/jQuery.when/)方法:

```
var wait = function(){
  var tasks = function(){
    alert("执行完毕！");
  };
  setTimeout(tasks,5000);
};
```
如果想要为wait函数指定一个回调函数改怎么做呢?

```
var wait = function(callback){
  var tasks = function(){
    alert("执行完毕！");
  };
  setTimeout(tasks,5000);
  callback();
};
```
???我们当然不会犯上面这种新手级错误,但是你所想的就一定正确吗?

```
　　$.when(wait())
　　.done(function(){console.log('success')})
　　.fail(function(){console.log('error')});
```

上面这段函数会不报错的执行,但是并不会得到我们的预期结果,因为wait()方法返回的并不是 $.deferred对象, 我们可以进行改写:

```
　　var dtd = $.Deferred(); // 新建一个deferred对象
　　var wait = function(dtd){
　　　　var tasks = function(){
　　　　　　alert("执行完毕！");
　　　　　　dtd.resolve(); // 改变deferred对象的执行状态
　　　　};
　　　　setTimeout(tasks, 5000);
　　　　return dtd;
　　};
```
这段函数执行最终返回$.deferred对象,并且在原本预期的末尾触发resolve()事件改变他的状态从而使得他能够进入下一步
```
　　$.when(wait())
　　.done(function(){console.log('success')})
　　.fail(function(){console.log('error')});
```
此时就可以得到我们预期的结果了,原理和trigger自定义事件差不多.

上面提到了一个叫做deferred.resolve()的方法,其实还有一个叫做deferred.reject(),这里我有理由相信ES6的promise是借鉴了该方法或者是相互借鉴,因为promise里面的两种状态连名字都和这一模一样,其实代表的含义也是大同小异了,在$.ajax操作中,deferred对象会根据返回的结果自动将deferred的状态做出相应的更改,但是在自定义的比如说wait()函数中就需要自己来做这个操作了,那么resolve()的意思就是说将状态从pending改为已完成,反之reject就是讲状态从pending改为已失败,从而可以将状态控制到下一步对应的接受状态中

```
　　var dtd = $.Deferred(); // 新建一个Deferred对象
　　var wait = function(dtd){
　　　　var tasks = function(){
　　　　　　alert("执行完毕！");
　　　　　　dtd.reject(); // 改变Deferred对象的执行状态
　　　　};
　　　　setTimeout(tasks,5000);
　　　　return dtd;
　　};
　　$.when(wait(dtd))
　　.done(function(){ alert("哈哈，成功了！"); })
　　.fail(function(){ alert("出错啦！"); });
```

考虑到一个问题: 如果dtd对象是一个全局对象,那么在其他地方执行改变状态的函数是否会先于预期处先执行从而影响结果?另外如果有两处改变状态的函数一处为成功一处为失败,是否会都执行?

在ES6promise中状态一旦发生改变就不会再变,
```
var promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```

```
promise.then(function(value) {
  // success
}, function(error) {
  // failure
});
```

```
function timeout(ms) {
  return new Promise((resolve, reject) => {
    setTimeout(resolve, ms, 'done');
  });
}

timeout(100).then((value) => {
  console.log(value);
});
```


在jQuery中同样有相同的方式

```
　　var wait = function(dtd){
　　　　var dtd = $.Deferred(); //在函数内部，新建一个Deferred对象
　　　　var tasks = function(){
　　　　　　alert("执行完毕！");
　　　　　　dtd.resolve(); // 改变Deferred对象的执行状态
　　　　};

　　　　setTimeout(tasks,5000);
　　　　return dtd.promise(); // 返回promise对象
　　};
　　$.when(wait())
　　.done(function(){ alert("哈哈，成功了！"); })
　　.fail(function(){ alert("出错啦！"); });
```

可以直接用$.Deffered包裹`函数名`的方式防止状态被外部改变
```
　　$.Deferred(wait)
　　.done(function(){ alert("哈哈，成功了！"); })
　　.fail(function(){ alert("出错啦！"); });
```

deferred.then():
和ES6promise类似的then,用一个then包裹两个作为参数的函数,第一个参数为.done的方法,第二个参数为.fail的方法

```
　$.when($.ajax( "/main.php" ))
　　.then(successFunc, failureFunc );
```

最后还可以加一个.always方法,用法和名字一样
```
　　$.ajax( "test.html" )
　　.always( function() { console.log('always') );
```
