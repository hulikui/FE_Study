bind

```js
Function.prototype.bind = function(callback, context) {
    var args = Array.prototype.slice.call(arguments, 1);
    var that = this;
    return function() {
        var arg = [].concat(args).concat(Array.prototype.slice.call(arguments, 0));
        return callback.apply(that, arg);
    }
}
```

deepCopy

```js
function deepCopy(source, target){
    var target = target || {};
    for (var key in source) {
        if (typeof source[key] === 'object') {
            target[key] = source[key].contructor === Array ? [] : {};
            deepCopy(source[key], target[key]);
        } else {
            target[key] = source[key];
        }
    }
    return target;
}
```



