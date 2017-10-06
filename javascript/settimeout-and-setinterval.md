setTimeout =&gt; setInteval \(实际间隔 &gt;= timer\)

```js
function setInterval(callback, timer) {
    setTimeout(function() {
        callback();
        setTimeout(arguments.callee, timer);
    }, timer);
}
```

setInterva =&gt; setTimeout \(中间有未执行 则忽略\)

```js
function setTimeout(callback,  timer) {
    var timerId = setInterval(function() {
        callback();
        clearInterval(timerId);
    }, timer);
}
```



