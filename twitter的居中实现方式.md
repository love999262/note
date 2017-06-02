# 以下内容仅作为一种类似于hack的手段,并且增加了一些无用的节点,对于CSS3来说有更加简便的方法来做到下面的效果,即便不支持CSS3也可以用一些其他的方式来完成,所以以下内容也变得不合时宜了.

```html
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
