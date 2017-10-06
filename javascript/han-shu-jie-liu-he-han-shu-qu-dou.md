函数节流 **throttle \(每隔一段时间才执行\)**

```js
var throttle = function(fn, delay){

    var last = 0;
    return function() {
        var cur = + new Date();
        if (cur - last > delay) {
            fn.apply(this, arguments);
            last = cur;
        }
    }
}
```

函数去抖 **debounce \(一段时间内只运行一次\)**

```js
var debounce = function(fn, delay){
    var last = 0;
    return function() {
        var ctx = this;
        var args = arguments;
        clearTimeout(last);
        last = setTimeout(function(){
            fn.apply(ctx, args);
        }, delay);
    }
}
```

once 

```js
var once = function(callback, context){
    var fn = callback;
    return function() {
        var args = arguments; 
        if (fn) {
            res = fn.apply(context || this, args);
            fn = null;
            return res;
        }   
    }
}
```



