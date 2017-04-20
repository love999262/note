通常所说的封装是指将要做的功能的具体实现细节隐藏,仅提供一个接口给外部的实现方式,这种封装的好处是在出现问题时可以定位到被封装的函数/类/对象中去修改,而不需要再一大坨代码中改动,在修改的时候只要保证输出的正确性就不会影响全局的代码,维护起来也很方便.

先讲讲ES6中的一个最常用到的关键词:`let`:
let相对于原来的var关键词,类似的新关键词还有const,let是用来声明变量的,因为通过原来的var关键词声明出来的变量来说let关键字有以下特性:

- let声明的变量只可以在其声明的块或者子块中使用,这点与var类似,但是也有区别:

```
function varTest() {
  var x = 1;
  if (true) {
    var x = 2;  // 同样的变量!
    console.log(x);  // 2
  }
  console.log(x);  // 2
}

function letTest() {
  let x = 1;
  if (true) {
    let x = 2;  // 不同的变量
    console.log(x);  // 2
  }
  console.log(x);  // 1
}
```
可以看到用var声明的变量其子块和父块中都是公用的,换句话说在父级作用域中声明了的变量即便用var再在子块中重新声明一般,只要变量名相同他们就是一样的变量.而let声明的变量子块和父块中同名变量是彼此独立的.

- 模仿私有接口,在处理构造函数的时候可以通过let声明而不是闭包的方式

```
var SomeConstructor;

{
    let privateScope = {};

    SomeConstructor = function SomeConstructor () {
        this.someProperty = "foo";
        privateScope.hiddenProperty = "bar";
    }

    SomeConstructor.prototype.showPublic = function () {
        console.log(this.someProperty); // foo
    }

    SomeConstructor.prototype.showPrivate = function () {
        console.log(privateScope.hiddenProperty); // bar
    }

}

var myInstance = new SomeConstructor();

myInstance.showPublic();
myInstance.showPrivate();

console.log(privateScope.hiddenProperty); // error
```
上面的代码利用let创建块级作用域和作用域链的原理,将let出的privateScope的作用于控制在{}范围内,出了作用域便不会被取值到,从而人为的创建了私有作用域,当然,在ES5中我们可以通过闭包的方式来创建私有作用域:

```
    var o = (function() {
        var __name = 'sun'
        return {
            getName: function() {
                console.log(__name);
            }
        }
    })();
    o.getName();
    o.__name//undefined;
```
这种封装仅仅是数据层面的封装,利用闭包的特性将我们需要的保护的数据保护起来,但是封装不仅仅只指代数据的封装,还有一开始提到的封装.虽然话很少但是要如何封装还是需要一定的编码积累才能判断的很好的.
