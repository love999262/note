# 本篇主要记录一些ES6的学习心得与总结,参考了[Understanding ECMAScript 6](https://oshotokill.gitbooks.io/understandinges6-simplified-chinese/content/)以及[ECMAScript 6 入门](http://es6.ruanyifeng.com/)以及一些网上的零散博客,长期更新

- var&let&const
  ES6的时代,推荐所有的变量声明的方式全部改为默认const,按照需求将部分声明方式改为let,不推荐使用var,var的这种声明方式不管你在哪声明,都会在当前函数级作用域顶端做一个`变量声明提升`的操作,从而造成很多预期外的结果,let和const可以创建块级作用域,并且创建`暂存性死区（The Temporal Dead Zone）`,在当前代码块内任何声明之前就使用的方式都是不正确的.

- 解构(Destructuring for Easier Data Access)
  在ES5中,如果想要将对象或者是数组中的值提取出来并且赋值给本地变量需要写非常多的代码:

```js

let options = {
    repeat: true,
    save: false
};
// 从对象中提取数据
let repeat = options.repeat,
save = options.save;

//传统数组赋值做法
let nextValue = ['color', 'red'];
let name = nextValue[0];
let value = nextValue[1];

```

  单纯的看上面的例子可能还比较好,但是试想如果有大量的类似需求的话可能需要不断的进行类似的赋值操作并且极有可能为了访问一小块数据而遍历整个数据结构.

  ES6给对象和数组添加了`解构`:

```js
//obj
let node = {
        type: "Identifier",
        name: "foo"
    };

let { type, name } = node;

console.log(type);      // "Identifier"
console.log(name);      // "foo"

//arr
let [name, value] = ['color', 'red'];
// 如果不想将全部的值都解构可以之再爱数组字面量中给出对应的变量
let [,value] = ['color', 'red'];

```

  传统的ES5中,对象字面量和数组字面量是不能出现在赋值操作符左边的,在ES6中出现这种操作形式则代表解构,在此例中,node.type的值有本地变量type储存,node.name同理,type和name标识符具有本地声明变量和options对象属性的双重身份.

 在解构中使用var,let等来声明变量的时候必须要有由初始化操作,下面的代码会因为未进行初始化而报错.

```js

// 语法错误！
var { type, name };

// 语法错误！
let { type, name };

// 语法错误！
const { type, name };

```

  另外,对于之前已经被声明的变量来说同样也可以进行解构:

```js

let node = {
        type: "Identifier",
        name: "foo"
    },
    type = "Literal",
    name = 5;

// assign different values using destructuring
({ type, name } = node);

console.log(type);      // "Identifier"
console.log(name);      // "foo"

```

  在该例中,node对象中的type和name在声明处初始化,另外的同名变量也在之后被不同的值初始化,在往下用这两个值进行了解构,解构同样可作为参数传给函数:

```js

let node = {
        type: "Identifier",
        name: "foo"
    },
    type = "Literal",
    name = 5;

function outputInfo(value) {
    console.log(value === node);        // true
}

outputInfo({ type, name } = node);

console.log(type);      // "Identifier"
console.log(name);      // "foo"


```

  outputInfo() 函数在调用时被传入解构赋值表达式。表达式计算的结果为 node 是因为它就是右侧的值。type 和 name 的赋值正常进行同时 node 被传给了 outputInfo()。解构的左侧可以