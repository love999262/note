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
