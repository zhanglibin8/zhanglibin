# ��String����չ����

## ��ȡ�������ַ����Ϣ

```
;(function () {
    function queryURLParameter() {
        var obj = {},
            reg = /([^?&=#]+)=([^?&=#]+)/g;
        this.replace(reg, function () {
            obj[arguments[1]] = arguments[2];
        });
        //->��ȡhashֵ
        reg = /#([^?&=#]+)/;
        if (reg.test(this)) {
            obj['HASH'] = reg.exec(this)[1];
        }
        return obj;
    }
    String.prototype.queryURLParameter = queryURLParameter;
    })();
```

## ��ʽ��ʱ���ַ���
```
   ;(function () {
   function formatTime(template) {
        template = template || '{0}��{1}��{2}�� {3}ʱ{4]��{5]��';
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