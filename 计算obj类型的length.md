# 用JS算出OBJ类型的长度(非枚举)

```js

var objContent = function(obj) {
    var count = 0;
    if(typeof obj === 'object') {
        for(var i in obj) {
            count++;
        }
    } else {
        return 'object type parameter only!!!'
    }
    return count;
};
var testObj = {
    one: '1',
    two: function(){},
    three: 3,
    four: {_four:'four'},
    five: 'five',
    six:['six'],
    seven: null,
    eight: undefined,
    nine: NaN
};
console.log(objContent(testObj));

```
