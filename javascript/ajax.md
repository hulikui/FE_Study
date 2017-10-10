AJAX

```js
window.$ = {};
$.ajax = function(options) {
    if(!options || typeof options != 'object') {
        return false;
    }

// 请求类型
var type = options.type || 'get';
// 请求地址
var url = options.url || location.pathname;
// 默认异步
var async = (options.async === false) ? false ：true;
// 格式
var contentType = options.contentType || "text/html";

// 数据拼接
var data = options.data || {};
var dataStr = '';
for (var key in data) {
    dataStr += key + '=' + data[key] + '&';
}

var xhr = '';
if (window.XMLHttpRequest) {
    xhr = new XMLHttpRequest();
} else if (window.ActiveXObject) {
    xhr = new ActiveXObject("Microsoft.XMLHTTP");
}

xhr.open(type, type === 'get' ? url + '?' + dataStr : url, async);

if (type === 'post') {
    xhr.setRequestHeader('content-Type', 'application/x-www-form-urlencoded');
}

xhr.send(type === 'get'? null : dataStr);
xhr.onreadystatechange = function() {
    if (xhr.readyState === 4 && xhr.status === 200) {
        var data = '';
        var contentType = xhr.getResponseHeader('content-Type');
        if (contentType.indexOf('xml') > -1) {
            data = xhr.responseXML;
        } else if (contentType.indexOf('json') > -1) {
            data = JSON.parse(xhr.responseText);
        } else {
            data = responseText;
        }
        options.success && options.success(data);
    } else if (xhr.readyState === 4) {
        options.error && options.error('request error.');
    }
}
}
```



