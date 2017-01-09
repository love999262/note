```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <script>
        var a = {
            a0 : "a0",
            a1 : "a1",
            a2 : "a2",
        }
        var b = {
            a0 : "b0",
            b0 : "b0",
            b1: "b1",
        }
        function merged(){
            for(var item in b){
                a[item]=b[item];
            }
        }
    </script>
</body>
</html>
```
代码如上

到了ES6中已经有了更加完善的解决方案，详细参考[Object.assign()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
