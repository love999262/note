# 首先得设置canvas标签，然后获取到该画布的DOM节点之后调用getContext("2d")方法传入2d上下文，将获取到的2D上下文对象赋值给一个变量存档以便后面调用。

```js
    <canvas id="canvas"></canvas>
    <script>
    var $ = function(name) {
        return document.querySelector(name);
    }
    var canvas = $("#canvas")
    var context = canvas.getContext("2d");
```

- 第一步，先设置该画布的宽高属性。

```js
    var width = 1000;
    var height = 800;
    canvas.width = width;
    canvas.height = height;

```

- 设置完成火就可以通过操作context来进行canvas绘画了

```js
    var arr = [
        "爱萝莉真是太好了",
        "Miku赛高！！！",
        "⑨月⑨日打卡签到",
        "第一！！！",
        "好无聊，我看了300遍就关了(｡•ˇ‸ˇ•｡)",
        "前方福利",
        "三周目",
        "我是世界第几帅？",
        "这是我老婆",
        "老婆你怎么在这里"
    ];
    context.font="30px Times New Roman";
    for(var i = 0 ; i < arr.length ; i++){
    context.font = "24px";
        context.fillText(arr[i],100*i,100*i);
    }
```

```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
    #canvas {
        background-color: #dadada;
    }
    </style>
</head>

<body>
    <img src="images/bg389.jpg" alt="" id="img">
    <canvas id="canvas"></canvas>
</body>
<script>
var $ = function(name) {
    return document.getElementById(name)
}
var canvas = $("canvas");
var img = $("img");
var w = 1000;
var h = 1000;
canvas.width = w;
canvas.height = h;
var ctx = canvas.getContext("2d");
document.addEventListener("click", function(e) {
    ctx.drawImage(img,222,222,800,600,0,0,500,500)
}, false)
</script>

</html>
```
