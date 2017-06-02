# 在某些程序中我们经常会看见一些非native的事件被某些方法监听,那么这是怎么做到的呢?

- 这里以jQuery为例,jQuery中有一个trigger的方法,调用该方法无需用户主动去触发时间,会自动的触发指定的事件,比如说`click`事件,原本是需要用户点击之后才会触发的,这里我们可以$(dom).trigger('click')来直接触发指定dom元素上的click事件,这种特性为自定义时间提供了可能.下面给个DEMO

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>test</title>
	<style type="text/css">
		.test{
			width: 100px;
			height: 100px;
			background-color: #000;
		}
	</style>
</head>
<body>
	<div class="test"></div>
	<script type="text/javascript" src="js/jquery.min.js"></script>
	<script type="text/javascript">
		$('.test').on('click', function() {
			alert('click');
			$('.test').trigger('_click');
		});

		$('.test').on('_click', function(){
			alert('_click');
		});
	</script>
</body>
</html>
```

- 该DEMO指定了一个DOM元素,为该元素监听了一个native事件`click`,在触发click事件的同时会用trigger去调用该DOM元素上的一个叫做`_click`的事件,但是我们知道`_click`这个事件浏览器本身是没有的,我们可以用on来监听自定义事件,一旦trigger触发了自定义事件就会被on监听到从而去执行对应的function.
