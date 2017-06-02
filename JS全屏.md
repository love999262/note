# js全屏

```js
window.onresize = function() {
    if (window.outerHeigth == screen.heigth && window.outerWidth == screen.width) {
        alert("不是全屏");
    } else {
        alert("是全屏");
    }
}

function launchFullscreen(element) {
    if (element.requestFullscreen) {
        element.requestFullscreen();
    } else if (element.mozRequestFullScreen) {
        element.mozRequestFullScreen();
    } else if (element.webkitRequestFullscreen) {
        element.webkitRequestFullscreen();
    } else if (element.msRequestFullscreen) {
        element.msRequestFullscreen();
    }
}

function exitFullscreen() {
    if (document.exitFullscreen) {
        document.exitFullscreen();
    } else if (document.mozCancelFullScreen) {
        document.mozCancelFullScreen();
    } else if (document.webkitExitFullscreen) {
        document.webkitExitFullscreen();
    }
}
exitFullscreen();

```

```js
全屏属性和事件
不幸的是，全屏属性和事件的相关方法也需要添加浏览器前缀，但我相信很快就不需要这样做了。

document.fullScreenElement: 全屏显示的网页元素。
document.fullScreenEnabled: 判断当前是否处于全屏状态。
fullscreenchange事件会在启动全屏或退出全屏时触发：

var fullscreenElement = document.fullscreenElement || document.mozFullScreenElement || document.webkitFullscreenElement;
var fullscreenEnabled = document.fullscreenEnabled || document.mozFullScreenEnabled || document.webkitFullscreenEnabled;
你仍然可以使用上面判断浏览器种类的方法给这个事件加上前缀。

全屏样式CSS
各种浏览器都提供了一个非常有用的全屏模式时的css样式规则：

:-webkit-full-screen {
  /* properties */
}

:-moz-full-screen {
  /* properties */
}

:-ms-fullscreen {
  /* properties */
}

:full-screen { /*pre-spec */
  /* properties */
}

:fullscreen { /* spec */
  /* properties */
}

/* deeper elements */
:-webkit-full-screen video {
  width: 100%;
  height: 100%;
}

/* styling the backdrop*/
::backdrop {
  /* properties */
}
::-ms-backdrop {
  /* properties */
}


fullscreen API 接口
属性1：fullscreenElement 该属性返回当前处于全屏模式的DOM元素。

属性2：fullscreenEnabled 该属性返回当前 document 是否进入了可以请求全屏模式的状态。

方法1：requestFullscreen() 请求进入全屏模式。

方法2：exitFullscreen() 退出全屏模式。

事件1：fullscreenchange 进入/退出全屏模式切换时会触发。

事件2：fullscreenerror 进入/退出全屏模式失败时会触发。

由于fullscreen API 存在浏览器兼容性问题，所以我们在使用的时候需要进行跨浏览器处理，参考代码：

跨浏览器返回正处于全屏的元素

function fullscreenElement(){

var fullscreenEle = document.fullscreenElement ||

document.mozFullScreenElement ||

document.webkitFullscreenElement;

//注意：要在用户授权全屏后才能获取全屏的元素，否则 fullscreenEle为null

console.log("全屏元素："+fullscreenEle);

return fullscreenEle;

}

跨浏览器返回当前 document 是否进入了可以请求全屏模式的状态

function fullscreenEnable(){

var isFullscreen = document.fullscreenEnabled ||

window.fullScreen ||

document.webkitIsFullScreen ||

document.msFullscreenEnabled;

//注意：要在用户授权全屏后才能准确获取当前的状态

if(isFullscreen){

console.log('全屏模式');

}else{

console.log('非全屏模式');

}

}

跨浏览器发动全屏

function lanchFullscreen(element){

if(element.requestFullscreen){

element.requestFullscreen();

}

else if(element.mozRequestFullScreen){

element.mozRequestFullScreen();

}

else if(element.msRequestFullscreen){

element.msRequestFullscreen();

}

else if(element.webkitRequestFullscreen){

element.webkitRequestFullScreen();

}

}

跨浏览器退出全屏

function exitFullscreen(){

if(document.exitFullscreen){

document.exitFullscreen();

}

else if(document.mozCancelFullScreen){

document.mozCancelFullScreen();

}

else if(document.msExitFullscreen){

document.msExiFullscreen();

}

else if(document.webkitCancelFullScreen){

document.webkitCancelFullScreen();

}

}

各浏览器fullscreenchange 事件处理

document.addEventListener('fullscreenchange', function(){ /*code*/ });

document.addEventListener('webkitfullscreenchange', function(){ /*code*/});

document.addEventListener('mozfullscreenchange', function(){ /*code*/});

document.addEventListener('MSFullscreenChange', function(){ /*code*/});

 

各浏览器fullscreenerror 事件处理

document.addEventListener('fullscreenerror', function(){ /*code*/ });

document.addEventListener('webkitfullscreenerror', function(){ /*code*/});

document.addEventListener('mozfullscreenerror', function(){ /*code*/);

document.addEventListener('MSFullscreenError', function(){ /*code*/ });

 

跨浏览器全屏模式下样式代码

:-webkit-full-screen { }

:-moz-full-screen { }

:-ms-fullscreen { }

:fullscreen { }
// Webkit-base: element.onwebkitfullscreenchange  
  
// Firefox: element.onmozfullscreenchange  
  
   
  
// W3C Method:  
  
element.addEventListener(‘fullscreenchange’, function(e) {  
  
if (document.fullScreen) {                     // document.webkitIsFullScreen  
  
/* make it look good for fullscreen */  
  
} else {  
  
/* return to the normal state in page */  
  
}  
  
}, true);  
```