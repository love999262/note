```
@keyframes cssKey{
  0%{
    top:0;
  }100%{
    top:100%;
  }
}
```
看上面的代码，这是CSSanimation动画形如(    /* animation: ulLoop 5s linear 0s infinite alternate; */)中定义关键帧的基本形式，一般来说keyframes都是写死数值不需要更改了的，但是就是有那么几个需求需要根据情况动态的更改关键帧，那么该怎么改呢？用 document.styleSheets属性。
```
  document.styleSheets[1].insertRule("@-webkit-keyframes ulLoop {0% {-webkit-transform:translateY(-100%);transform:translateY(-100%);}100% {-webkit-transform:translateY("+$(".l4-ul").height()+"px);transform:translateY("+$(".l4-ul").height()+"px);}}", 0);
```
上面这段代码表示在第二个样式表的第一项中添加"@-webkit-keyframes ulLoop {0% {-webkit-transform:translateY(-100%);transform:translateY(-100%);}100% {-webkit-transform:translateY("+$(".l4-ul").height()+"px);transform:translateY("+$(".l4-ul").height()+"px);}}"这么一段代码，还有addRule()，removeRule(),等方法可以调用。
