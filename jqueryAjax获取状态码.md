这个东西其实很简单了,但是因为一直都取的回调函数的一个参数没有想到jQuery把状态吗封装在回调的参数里了,以为是哪个属性所以还是有必要记录一下的.
```
$.ajax({
    url: 'https://github.com/love999262/Diary/new/master'
    type: 'post',
    data: self._data,
    xhrFields: {
        withCredentials: true
    },
    dataType: 'json',
    success: function(res, textStatus, xhr) {
        console.log(res);
        console.log(textStatus);
        console.log(xhr);
    },
    error: function(xhr, textStatus) {
        console.log(xhr);
        console.log(textStatus);
    }
});
```
xhr 参数就是状态码了不过需要注意的是如果失败了是不会有状态码的
