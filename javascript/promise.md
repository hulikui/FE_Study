Promise

```js
var PENDING = 0;
var FULFILLED = 1;
var REJECTED = 2;

function Promise(callback) {
    this.status = PENDING;
    this.value = null;
    this.defferd = [];
    setTimeout(callback.bind(this, this.resolve.bind(this)), this.reject.bind(this), 0);
}

Promise.prototype = {
    constructor: Promise,
    resolve: function(res) {
        this.status = FULFILLED;
        this.value = res;
        this.done();
    },
    reject: function(error) {
        this.status = REJECTED;
        this.value = error;
    },
    handle: function(fn) {
        var value = this.value;
        var t = this.status;
        var p;
        if (t === PENDING) {
            this.defferd.push(fn);
        } else {
            if (t === FULFILLED && typeof fn.onfulfilled === 'function') {
                p = fn.onfulfilled(value);
            }
            if (t === REJECTED && typeof fn.onfulfilled === 'function') {
                p = fn.onrejected(value);
            }
        }
        var promise = fn.promise;
        if (promise) {
            if (p && p.contructor === Promise) {
                p.defferd = promise.defferd;
            } else {
                p = this;
                p.defferd = promise.defferd;
                this.done();
            }
        }
    },
    done: function() {
        var status = this.status;
        if (status === PENDING) return;
        for (var i=0; i < this.defferd.length; i++) {
            this.handle(this.defferd[i]);
        }
    },
    then: function(success, fail) {
        var o = {
            onfulfilled: success,
            onrejected: fail,
        };
        var status = this.status;
        o.promise = new this.constructor(function() {});
        if (status === PENDING) {
            this.defferd.push(o);
        } else {
            this.handle(o);
        }
        return o.promise;
    }
}
```



