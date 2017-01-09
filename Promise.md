```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <script>
    var global = {
        mes:""
    }
        function a(mesage){
            return new Promise(function(resolve,reject){
                setTimeout(function(){
                    global.mes = mesage;
                    resolve(global.mes);
                },1000);
                reject("失败！");
            });
        }
        a("测试数据").then(function(response){
            alert(response);
        })
    </script>
</body>
</html>
```


```
getDanmakuList(uri) {
        // AJAX获取弹幕列表
        let danmakuLoad = (uri) => {
            return new Promise(function(resolve, reject) {
                let url = uri || "/bPlayer/src/js/danmakuList.json";
                let xhr = new XMLHttpRequest();
                xhr.open("get", url, true);
                xhr.onreadystatechange = function() {
                    if (xhr.readyState == 4) {
                        if (xhr.status >= 200 && xhr.status < 300 || xhr.status == 304) {
                            resolve(JSON.parse(xhr.responseText).danmakuList);
                        } else {
                            reject("response failed --");
                        }
                    }
                };
                xhr.send(null);
            });
        }
        danmakuLoad().then((response) => {
            this.danmakuList = response;
            this.launchDanmaku();
        });
    }
```
