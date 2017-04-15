```
var A = (function() {
    var instance;
    var A = function(o) {
        if (instance) {
            return instance;
        }
        this.init();
        return instance=this;
    };
    A.prototype = {
        a: '123',
        init: function(o) {

        }
    }
    return A;
})();
```
上面这种方式可以实现一个基本的单例,无论执行多少次new的操作符总会返回同一个单例,但是扩展性不强,如果有这种从单例变为多实例的需求的话就要大修改,可以采用下面的代理单例的方式去做,每次从代理中new,原函数并不需要修改.

```
var A = (function() {
    var A = function(o) {
        this.init();
    };
    A.prototype = {
        a: '123',
        init: function(o) {

        }
    }
    return A;
})();
var proxySingle = (function() {
    var instance;
    return function(o) {
        if(!instance) {
            instance = new A(o);
        }
        return instance;
    }
})();
```
下面的proxySingle用了一个立即执行的匿名函数+闭包的方式来保存创建的对象,这样每次从代理中new一个新的函数就可以了.
