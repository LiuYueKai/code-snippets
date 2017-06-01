## 实现功能

核心function `dlo`接受一个function，结果返回一个新的function，包装后的function在100ms内多次调用仅会调用一次。

#### 适用场景

grid控件每次执行操作之后需要执行afterCreate逻辑来进行一定计算，在短时间内频繁执行操作时为提高性能仅最后执行一次。

## 具体代码

### 核心代码

```
// 核心代码
delayOnce = dlo = function(fun,delayTime) {
    var d = Math.random().toString(36).substr(2);
    delayTime = delayTime? delayTime: 100;
    return function() {
        var arg = arguments;
        if (window[d])
            clearTimeout(window[d]);
        window[d] = setTimeout(function() {
            fun.apply(this, arg)
            window[d] = null;
        }, delayTime);
    }
}

// 验证代码
var fun = function(name) {
    console.log(name);
}

var newFun = dlo(fun);

for (var i = 0; i < 100; i++) {
    newFun(i);
}

for (var i = 0; i < 100; i++) {
    fun(i + 's');
}
```
