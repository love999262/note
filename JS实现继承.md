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

- 
