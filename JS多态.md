先从最基础一段代码的入手:

```
var makeSound = function(animal) {
	if(animal instanceof Duck) {
		console.log('guaguagua');
	} else if(animal instanceof Chicken) {
		console.log('gegege');
	} else {
		console.log('nothing');
	}
};
var Duck = function() {};
var Chicken = function(){};
makeSound(new Duck());
makeSound(new Chicken());
```
这段代码的makeSound根据传入的参数的不同会实现不同的方法,显然这并不能严格意义上称为好的代码,因为一旦添加了新的类型就必须在makeSound方法里添加对应的方法,这显然很蠢,维护起来也很困难.继续看下面的代码:

```
var Duck = function() {

};
Duck.prototype = {
	sound: function() {
		console.log('guaguagua');
	}
};
var Chicken = function() {

};
Chicken.prototype = {
	sound: function() {
		console.log('gegege');
	}
};
makeSound(new Duck());
makeSound(new Chicken());
```
这里makeSound方法不需要判断参数是什么,我默认你有我指定的方法,指定的方法是什么也不在makeSound里定义,而是交给各个参数本身,一般来说这种方式就较好的实现了耦合性.但是做到这一步还不太够,仔细想想ES6中的多态一般是怎么实现的,继续看一段ES6的代码.

```
class Animal {
	constructor() {
		this.shout();
	}
}
class Duck extends Animal {
	shout() {
		console.log('guaguagua');
	}
}
class Chicken extends Animal {
	shout() {
		console.log('gegegege');
	}
}
let duck = new Duck();
let chicken = new Chicken();
```
这里就和一些静态类型语言比如说JAVA很像了,利用extends关键字可以实现多态继承.

接下来要说一些高级并且在某些时候非常实用的ES5技巧(并且该技巧在现有项目中就有用到):

假设我有一个地图渲染函数,改函数负责控制渲染什么类型的地图,第一版需求是只需要渲染谷歌地图,那么一般来说我会这么写:
```
var gMap = {
	show: function() {
		console.log('google');
	}
}
var render = function() {
	gMap.show();
};
render();
```

好的,问题来了,产品经理说谷歌被墙了,我们换成百度地图吧,好,可能我会这么写:

```
var gMap = {
	show: function() {
		console.log('google');
	}
}
var bMap = {
	show: function() {
		console.log('baidu');
	}
};
var render = function(type) {
	switch(type) {
		case 'google':
			gMap.show();
		break;
		case 'baidu':
			bMap.show();
		break;
		default:;
	}
};
render('baidu');
```
这就犯了上面提到的维护性差的错误,如果后期类型越来越多那么每次更新都需要从switch语句中去更改,麻烦也容易出错:
其实我们完全可以将相同的部分抽象出来:

```
var render = function(map) {
	if(map.show && map.show instanceof Function) {
		map.show();
	}
};

var gMap = {
	show: function() {
		console.log('google');
	}
}
var bMap = {
	show: function() {
		console.log('baidu');
	}
};
render(gMap);
```
这样渲染器只做必要的类型检测,其余的方法交给各个类自己去解决的方式比较好.当然这个方法也有一些不足就是show这个方法名必须统一,但是相对来说还是可以克服的,解决的方法可能需要通过适配器模式来解决.
