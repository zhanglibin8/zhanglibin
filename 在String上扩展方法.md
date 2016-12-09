# 在String上扩展方法

## 获取浏览器地址栏信息

```
;(function () {
    function queryURLParameter() {
        var obj = {},
            reg = /([^?&=#]+)=([^?&=#]+)/g;
        this.replace(reg, function () {
            obj[arguments[1]] = arguments[2];
        });
        //->获取hash值
        reg = /#([^?&=#]+)/;
        if (reg.test(this)) {
            obj['HASH'] = reg.exec(this)[1];
        }
        return obj;
    }
    String.prototype.queryURLParameter = queryURLParameter;
    })();
```

## 格式化时间字符串
```
   ;(function () {
   function formatTime(template) {
        template = template || '{0}年{1}月{2}日 {3}时{4]分{5]秒';
        var ary = this.match(/\d+/g);
        template = template.replace(/\{(\d+)\}/g, function () {
            var index = arguments[1],
                result = ary[index];
            result = result || '00';
            result.length < 2 ? result = '0' + result : null;
            return ary[arguments[1]];
        });
        return template;
    }
    String.prototype.formatTime = formatTime;
})();
```