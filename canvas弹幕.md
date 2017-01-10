```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>canvas弹幕</title>
    <style>
    * {
        color: #fff;
    }
    
    #canvas {
        background-color: #dadada;
    }
    </style>
</head>

<body>
    <canvas id="canvas"></canvas>
    <script>
    var $ = function(name) {
        return document.querySelector(name);
    }
    var canvas = $("#canvas")
    var context = canvas.getContext("2d");
    var width = 1000;
    var height = 800;
    canvas.width = width;
    canvas.height = height;
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
    context.font = "30px Times New Roman";
    var left = $("#canvas").offsetWidth;
    var top = $("#canvas").offsetHeight;
    /*    var closure = function(store) {
            return function() {
                function a() {

                }

                setInterval(function() {
                    context.clearRect(0, 0, canvas.width, canvas.height);
                    context.save();

                    function leftOff() {
                        left -= 10;
                        return left;
                    }
                    context.fillText(arr[store], leftOff(), Math.random() * 1000);
                    context.restore();
                }, 1000);
            }
        }
        for (var i = 0; i < arr.length; i++) {
            context.font = "24px";
            closure(i)();
        }*/
    function leftOff() {
        left -= 10;
        return left;
    }
    var arrT = [];
    for (var j = 0; j < arr.length; j++) {
        var a = Math.random() * 1000;
        arrT.push(a);
    }
    var timer = setInterval(function() {
        context.clearRect(0, 0, canvas.width, canvas.height);

        for (var i = 0; i < arr.length; i++) {
            var aaa = Math.random() * 1000;
            context.fillText(arr[i], leftOff(), arrT[i]);
        }
    }, 200);
    </script>
</body>

</html>

```
