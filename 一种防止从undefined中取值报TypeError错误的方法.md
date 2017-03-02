```
var obj = {
  a: '123'
}
obj.b._son
```
这样会报Uncaught TypeError: Cannot read property '_son' of undefined错可以利用&&短路的特性
```
obj.b && obj.b._son
```

返回undefined,虽然是undefined但是不会报错了,也不用写难看的try catch语句,挺好的.
