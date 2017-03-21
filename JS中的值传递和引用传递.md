先看一段代码:

```
var o = {
  a: '123',
  b: '456'
};
var _o = o;
_o.a = 'onetwothree';
console.log(o); 
console.log(_o);
console.log(o===_o); // true
```

问两次输出结果?
这里两次输出的结果都是一样的,而且对象也是恒等的,说明这两个对象指向同一处地址.

再看一段代码:
```
var num1 = 5;
var num2 = num1;
num2 += 10;
console.log(num1);// 5
console.log(num2);// 10
```
这里的num1 num2是基本数据类型中的string类型,在进行赋值操作的时候并不会仅仅加个指向,而会在内存中开辟一块新的区间存储新的值,num1和num2所储存的值完全是独立的,而当一个变量向另一个变量赋值引用类型的值得时候仅是添加了一个指针,实际上指针指向的都是同一个对象,对任何指向改地址的变量操作都会改变其他指针指向的变量.

- 参数
首先明确一点:ES中所有函数的参数都是按值传递的,光看这句话可能有点模糊,看下面的代码:

```
var count = 20;
function addTen(num) {
  num += 10;
  return num;
}
var result = addTen(count);
console.log(count); // 20
console.log(addTen(count));// 30
console.log(count);// 20
```

基本类型不必多说,下面我们来看引用类型:

```
var o = {
  a: '123'
}
function test(_o) {
  _o.a = '456';
  return _o;
}
console.log(o);
console.log(test(o));
console.log(o);
```
这里的o.a分别为'123','456','456',可以看到,作为参数传入后更改属性后原来的o的属性也跟着改变了,那么是否就可以据此说引用类型的参数是引用传递呢?当然是不能的.
继续看一段代码:

```
function test(_o) {
  __o = _o;
  __o.a = '456';
  __o = {};
  __o.a = '789';
}
var o = {a: '123'};
test(o);
console.log(o);
```
这里的o.a最终的结果是456,这说明即使在函数内部改变了参数的值,但是原始的引用依然未改变,事实上在函数内部重写obj的时候这个变量的引用就是一个局部对象的,这个局部对象会在函数执行完后被立即销毁.
