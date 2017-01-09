Browserify是一个node.js模块，主要用于改写现有的CommonJS模块，使得浏览器端也可以使用这些模块。
在终端输入：
```
$ npm install -g browserify
```
在全局环境中安装Browserify。

1.基本用法:
假设有一个commonjs文件：foo.js

```
//foo.js

// module.exports = function(x) {
//   console.log(x);
// };
var foo = (function(){
	function foo(x){
		console.log(x);
	}
	foo.prototype = {
		a:function(x){
			console.log(x);
		}
	}
	return foo;
})();
module.exports = foo;
```

另外有一个main.js文件用来加载foo.js文件

```
// main.js

var foo = require('./foo.js');
console.log(foo);
foo("foo fuc");
foo.prototype.a("foo.a");
```
使用Browserify，将main.js转化为浏览器可以加载的脚本compiled.js。

```
browserify main.js > compiled.js

# 或者

browserify main > compiled.js

# 或者

browserify main.js -o compiled.js
```

之所以转化后的文件叫做compiled.js，是因为该文件不仅包括了main.js，还包括了它所依赖的foo.js。两者打包在一起，保证浏览器加载时的依赖关系。

```
<script src="compiled.js"></script>
```
使用上面的命令，在浏览器中运行compiled.js，控制台会显示Hi。
