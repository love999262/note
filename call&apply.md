关于call/apply是JS中的一个实用的方法,某些人认为只有用好它才能真正成为一个JavaScript程序员,下面总结下这两个函数:

- 改变this指向,关于这点我在前面的章节已经说过了,不过没有提到具体的场景: 考虑一个div节点的click事件的例子

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style type="text/css">
        #div1 {
            width: 100px;
            height: 100px;
            background-color: #000; 
        }
    </style>
</head>
<body>
    <div id="div1"></div>
    <script type="text/javascript">
        var a = document.getElementById('div1');
        a.onclick = function() {
            console.log(this.id); // div1
            var func = function() {
                console.log(this.id); // undefined
            };
            func();
        }
    </script>
</body>
</html>
```
该节点所绑定的this事件中有一个内部的function,当执行这个function的时候就遵循前面我所说的this指向规则指向到了window,这显然不是我所想要的结果,我当然可以用self=this的方式来做,但是我今天想说的是call/apply,所以考虑用apply的方式来解决这个问题:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style type="text/css">
        #div1 {
            width: 100px;
            height: 100px;
            background-color: #000; 
        }
    </style>
</head>
<body>
    <div id="div1"></div>
    <script type="text/javascript">
        var a = document.getElementById('div1');
        a.onclick = function() {
            console.log(this.id); // div1
            var func = function() {
                console.log(this.id); // undefined
            };
            func.call(this);
        }
    </script>
</body>
</html>
```

- Function.prototype.bind

目前来说绝大部分浏览器都具有Function.prototype.bind,改方法用来指定函数内部this的指向,即便是没有我们也可以写一个pollyfill:

```
  Function.prototype.bind = function(ctx) {
    var self = this;
    return function() {
      return self.apply(ctx, arguments);
    }
  }
  var obj = {
    name: 'sun'
  };
  var func = function() {
    console.log(this.name);
  }.bind(obj);
  func(); //sun
```
通过Function.prototype.bind来包装func函数,并且传入一个ctx来当做参数,这个作为参数的ctx对象就是我们想修正的this对象.

- 借用其他对象的方法

JS底层提供了很多好用又常用的原生方法,可是这些方法往往绑定在某些具体的数据类型上,比如说Math.max,举一个非常常用的例子:

函数的参数列表是一个类似JS数组的arguments对象,他并非真正的数组,并不具有数组的一些方法,但是我们可以用call/apply的方式让它成为真正的数组.

```
  Array.prototype.slice.apply(arguments);
```
