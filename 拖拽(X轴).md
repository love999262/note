```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
    #slider {
        width: 100px;
        height: 100px;
        position: absolute;
        background-color: #000;
    }
    
    #slider2 {
        width: 100px;
        height: 100px;
        position: absolute;
        top: 500px;
        left: 500px;
        background-color: red;
    }
    </style>
</head>

<body>
    <div id="slider"></div>
    <div id="slider2"></div>
    <script>
    var _$ = function(idName) {
        return document.querySelector(idName);
    }

    function draggable(node) {
        var isDragging = undefined;
        document.addEventListener("mousedown", function(e) {
            if (e.target.id == node.id) {
                isDragging = 1;
                console.log(e);
                console.log(e.clientX + "x");
                console.log(e.clientY + "y");
                console.log(isDragging);
            }
        }, false)
        document.addEventListener("mousemove", function(e) {
            if (isDragging == 1) {
                console.log(e);
                console.log(e.clientX + "x");
                console.log(e.clientY + "y");
                console.log(isDragging);
                node.style.left = (e.clientX - (node.offsetWidth / 2)) + "px";
            }
        }, false)
        document.addEventListener("mouseup", function(e) {
            isDragging = undefined;
            console.log(e);
        }, false)
    }
    draggable(_$("#slider"));
    draggable(_$("#slider2"));
    </script>
</body>

</html>
```
