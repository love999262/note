```
function Parent(name){
    this.name = name || "Adam"
}
Father.prototype = {
    say: function(){
        console.log(this.name);
    }
}
function Child(name){

}
inherit(Child,Parent);
```
这段代码中的inherit功能是让子元素Child继承父元素Parent的方法，需要自己实现，下面讲讲几种inherit的实现方法

- 默认模式
```
function inherit(C,P){
    C.prototype = new p();
}
```
这是最常用的，用new p()构造一个对象并将该对象赋值给C的原型，这样C就从P的示例中获取了他的功能。
此时C.prototype拥有了和P实力完全一样的obj，这时候：
```
var kid = new Child();
kid.say();//"Adam"
```
缺点：可能会继承不必要的属性，并且不能通过传参来更改属性值，只能不断的更改父元素，非常麻烦。

------
```
var A = {name:'sun'}
var B = function(){}
B.prototype = A;
var a = new A();
console.log(a.name);//sun
```
- 首先,JS引擎尝试遍历对象a中所有的属性,尝试找到name但是失败了.

- 第一次失败之后查找name属性的这个请求被委托给对象a的构造器的原型,它被a.__proto__记录并且指向B.prototype,而B.prototype指向A

- 在A中找到了值并且成功返回.

```
    var A = function() {}
    A.prototype = {
        name: 'father'
    }
    var B = function() {}
    B.prototype = function() {}
    B.prototype = new A();
    var b = new B();
    console.log(b.name);
```
这段代码提供了类似'类'继承的过程,这段代码的执行过程中又发生了什么呢:

- 首先,尝试遍历对象b中的所有属性,没有找到name这个属性.

- 查找name属性的请求被委托给对象b的构造器原型,被b.__proto__ 记录并指向B.prototype,而B.prototype被设置为一个通过new A()创建出来的对象.

- 在该对象中任然没有找到name属性于是请求被继续委托给这个对象构造器的原型A.prototype.

- 在A.prototype中找到了name属性并且返回它的值

和把B.prototype直接指向一个对象字面量相比,通过B.prototype = new A()形成的原型链比之前多了一层,但是其实并没有本质区别,都是将对象构造器的原型指向另一个对象,`继承总是发生在对象和对象之间`

原型链会一直向上追溯到Object.prototype如果Object.prototype中也没有要找的属性就会返回undefined
