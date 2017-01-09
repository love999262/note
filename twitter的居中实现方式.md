```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
    *{
        margin: 0;
        padding: 0;
    }
    .gallery{
        position: fixed;
        overflow: hidden;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        z-index: 3000;
        text-align: center;
    }
    .alert-panel{
        position: relative;
        display: inline-block;
        vertical-align: middle;
        min-width: 500px;
        min-height: 346px;
        background-color: #fff;
        background: url(images/alert-bg.png);
    }
    .gallery:before{
        content: "";
        height: 100%;
        display: inline-block;
        vertical-align: middle;
    }
    </style>
</head>
<body>
    <div class="gallery">
        <div class="alert-panel"></div>
    </div>
</body>
</html>
```
先抠下来，以后有空研究
-----------------------
研究完了，据知乎上某大神说其实就是伪元素把行撑开了所以使得line-height被改变了，故而使得vertail-align有用。
