get参数

```js
function getParams(url, key) {
    url = url || window.location.search;
    var res = {};
    if (url) {
        url = url.substr(url.indexOf('?') + 1);
        url.replace(/([^&]*)=([^&]*)/g, function(a, b, c){
            res[decodeURIComponent(b)] = decodeURIComponent(c);
        });
    }
    if (key) return res[key];
    return res;
}
```

JSONP

```js
（function (context) {
    var id = 0;
    var container = document.getElementByTagName('body')[0];
    function jsonp(options){
        var url = options.url;
        if (!options || !options.url) return;
        var script = document.cresateElement('script');
        var data = options.data || {};
        var callback = options.callback;
        var fnName = "JSONP" + id++;

        data["callback"] = fnName;
        var params = [];
        for (var key in data) {
            params.push(encodeURIComponent(key) + '=' + encodeURIComponent(data[key]));
        }
        url = url.indexOf('?') > -1 ? (url + '&') : (url + '?');
        url += params.join('&');
        script.src = url;
        context[fnName] = function(res) {
            callback && callback(res);
            container.removeChild(script);
            delete context[fnName];
        }
        script.type = "text/javascript";
        container.appendChild(script); 
    }
    context.jsonp = jsonp;

})(window)
```



