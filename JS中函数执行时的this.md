-  方法调用模式:
当一个函数被保存为对象的一个属性时,他就被称为一个方法,用.或者[]的形式调用方法的时候就会被当做一个方法调用:

```
var num = 'window456';
var test = {
  num: '123',
  a: function() {
    console.log(this.num);
  }
}   
test.a(); // '123'
```
方法调用模式在调用的时候this指向自己所属的对象.

- 函数调用模式当一个函数并非对象的属性的时候它就被当做函数来调用:
```

var num = 'window456';
var a = function() {
  console.log(this.num);
}
a();
```
函数调用模式的this指向全局对象,Douglas认为这是语言设计上的错误,所幸这一错误在ES6的()=>{}中得到了较好的修正.

```
// 预期外
var num = 'window456';
var test = {
  num: '123',
  a: function() {
    var a = function() {
      console.log(this.num);
    }
    a();
  }
}   

test.a(); // 'window456'
```
我们来看看ES6是怎么做的:


```
let num = 'window456';
let test = {
  num: '123',
  a: function() {
    let a = () => {
      console.log(this.num);
    }
    a();
  }
}   

test.a(); // 123
```

在ES5中也同样有简单通用的解决方案:

```
var num = 'window456';
var test = {
  num: '123',
  a: function() {
    var _this = this;
    var a = function() {
      console.log(_this.num);
    }
    a();
  }
}   

test.a(); // '123'

```
总结: 需要搞明白this只是一个指针一样的东西,他指向堆内存的内存地址.

- 构造器调用
通过new一个函数的方式调用

```
  var MyClass = function() {
      this.name = 'sun';
  }
  var obj = new MyClass();
  conosole.log(obj.name);//sun
  // 需要注意的是如果该函数显示的返回一个obj类型那么this将会指向返回的对象.
```

- call/apply
call,apply的功能都是相似的:都是将传入的第一个参数作为this的指向然后执行调用的方法,这么说可能有点绕,还是需要看具体的代码,唯一的区别就是第二个接受的参数不同,第如果是call则第二个以及以后的参数都作为方法的参数传入,如果是apply则把方法的参数以数组的形式传入.

```
var obj1 = {
  name: 'sun',
  getName: function() {
    return this.name
  }
}
var obj2 = {
  name: 'sun2'
}
console.log(obj1.getName());
console.log(obj1.getName.apply(obj2, []));
```
这两个关键字在JS中是少有的可以动态改变传入函数this的方法,该属性挂载在Function.prototype上,是JS函数式编程的重点.

- 有的时候我们借用call/apply并不关注this,而只是想借用某个对象的方法,这时候我们就可以用null代替某个具体的对象,当传入null的时候在非严格模式下this指向window而在严格模式下this===null,关于call/apply更详细的我会专门写一章.

```
Math.max.apply(null,[1,2,3,4,5]);
```

- this丢失的问题

考虑以下代码:

```
  var obj = {
    myName: 'sun',
    getName: function() {
      return this.myName
    }
  }
  console.log(obj.getName()); // sun
  var getName2 = obj.getName;
  console.log(getName2()); // undefined
```
第一次执行this指向obj,第二次指向window

- document.getElementById
考虑这样一个问题:为什么在封装document.getElementById的时候通常是
```
function(id) {
  return document.getElementById(id);
}
```
是因为this指向的问题:
```
    var getId = document.getElementById;
    // getId('test');
    var a = getId.apply(document, ['test']);
    console.log(a);
```
