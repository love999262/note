在原生xhr对象中有一个progress方法，一般用这种方法做取下载进度条：

```
var xhr = new XMLHttpRequest();
xhr.addEventListener("progress",function(event){
  if(event.lengthComputable){
    var percentComplete = (event.loaded/event.total) * 100;
    console.log(percentComplete + "%");
  }else {
    console.log(event.target);
  }
},false);
```

一般来说是没有问题的，需要关注三个属性：
- e.lengthComputable：代表是否知道内容长度。是则返回true,需要后段返回content-length才能知道。
- e.loaded：代表目前传输的字节数。
- e.total：代表总字节数。

-------
在jquery中用$.ajax的方式获取的xhr对象并没有progress事件需要我们自己添加：
```
$.ajax({
    xhr: function() {
        var xhr = new window.XMLHttpRequest();
        xhr.upload.addEventListener("progress", function(evt) {
            if (evt.lengthComputable) {
                var percentComplete = evt.loaded / evt.total;
                //Do something with upload progress here
            }
       }, false);

       xhr.addEventListener("progress", function(evt) {
           if (evt.lengthComputable) {
               var percentComplete = evt.loaded / evt.total;
               //Do something with download progress
           }
       }, false);

       return xhr;
    },
    type: 'POST',
    url: "/",
    data: {},
    success: function(data){
        //Do something on success
    }
});
```
以上情况只适用于符合同源策略的地址，如果是跨域的话jquery能请求到但是不能识别xhr对象。

-----
