```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>

<body>
    <script src="js/jquery-2.2.0.min.js"></script>
    <script>
        var wait = function(){
            var dtd = $.Deferred();
            try{
                nonefuc();
                dtd.resolve();
            }catch(e){
                alert("bbb");
                dtd.reject();
            }
            return dtd.promise();
        }
        $.when(wait())
        .done(
            function(){
                    alert("success")
                }
            )
        .fail(
            function(){
                    alert("fail")
                }
            );
    </script>
</body>

</html>

```
最近遇到一个比较大的麻烦，我要写一个HTML5的活动页同时兼容IOS和安卓，当然，浏览器的兼容肯定是可以的，关键是IOS和安卓的各自的接口函数有大问题，IOS是异步加载的，就是说打开了浏览器之后不一定能找到IOS的方法，而安卓又是同步的，就是说即便是用回调的方式回调IOS也没有办法兼容安卓，假设安卓和IOS的接口实现行为都是一样的，但是因为这坑爹的机制导致页面在两者上展示不一样，而且非但不一样，在IOS上那是完全不能用啊，唯一的笨方法是加定时器延迟接口函数的执行时间，但是定时器也有坑爹的地方，因为我需要接口函数的值，但是定时器并不能达到return的效果，这样只有将接口返回的值加到全局命名空间里面去了，但是这样问题就更大了：有很多地方一进页面就需要命名空间的值，但是这时候他的值是空，但是这些函数并不会等待而是直接取空，这样会发生很多的错误，这个看似简单的问题真的是很头疼，有人推荐我用jquery的deferred,我看了下，这个并不能解决我的问题，因为我的需求是要在客户端里展示一种状态，客户端外展示另一种状态，这个deferred走到接口函数那里依然是空我还是要和客户端回调。就是说不走客户端不行，IOS回调是必须的，或者就加定时器然后所有方法全部延迟，这真的是一个大坑。
