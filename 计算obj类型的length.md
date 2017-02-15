```
var objContent = function(obj) {
    var count = 0;
    if(typeof obj === 'object') {
        for(var i in obj) {
            count++;
        }
    } else {
        return 'object parameter only!!!'
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
