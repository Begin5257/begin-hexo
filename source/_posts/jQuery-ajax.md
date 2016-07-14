title: jQuery-ajax
date: 2016-04-06 20:00:36
categories: 归纳整理 #文章文类
tags: [ajax] #文章标签，多于一项时用这种格式
---

想了解一下jQuery是如何封装Ajax的，在网上找到了下面的代码(一种类似jQuery的实现方式)。
读了源码，加了注释。

ajax.js
```
(function(exports, document, undefined){
    "use strict";
    function Ajax(){
        if(!(this instanceof Ajax)) return;
        return this;
    }
    Ajax.prototype = {
        init: function(opts){
            opts = opts || {};
            this.opts = opts;
            this.opts.type = opts.type || 'get'; //若没有设定type类型则默认GET
            this.opts.url = opts.url || '';
            this.opts.data = opts.data || '';
            this.opts.dataType = opts.dataType || 'text';
            this.opts.async = opts.async || true;
            this.opts.success = opts.success || null;
            this.opts.error = opts.error || null;
            this.xhr = this.createXMLHttpRequest.call(this);
            this.initEvent.call(this);
            return this;
        },
        ajax: function(opts){
            this.init.apply(this, arguments); //扩充作用域
            this.open.call(this);
            this.send.call(this);
        },
        createXMLHttpRequest: function(){
            var xhr;
            try{
                xhr = new XMLHttpRequest();
            }catch(e){
                console.log(e);//捕获错误
            }
            return xhr;
        },
        initEvent: function(){
            var _this = this;
            this.xhr.onreadystatechange = function(){
                if(_this.xhr.readyState == 4 && _this.xhr.status == 200){
                    if(_this.xhr.status == 200){
                        if(_this.opts.dataType === 'text' || _this.opts.dataType === 'TEXT'){
                            _this.opts.success && _this.opts.success(_this.xhr.responseText, 'success', _this.xhr);
                            //若dataType为text，则返回内容为Text
                        }else if(_this.opts.dataType === 'xml' || _this.opts.dataType === 'XML'){
                            _this.opts.success && _this.opts.success(_this.xhr.responseXML, 'success', _this.xhr);
                            //若dataType为text，则返回内容为XML
                        }else if(_this.opts.dataType === 'json' || _this.opts.dataType === 'JSON'){
                            //若dataType为json，则返回内容为JSON
                            _this.opts.success && _this.opts.success(JSON.parse(_this.xhr.responseText), 'success', _this.xhr);
                        }
                    }else if(_this.xhr.status != 200){
                        //若status不为200，则报错
                        _this.opts.error && _this.opts.error(_this.xhr, 'error');
                    }
                }
            }
        },
        open: function(){
            if(this.opts.type === 'GET' || this.opts.type === 'get'){
                var str = (typeof this.opts.data === 'string') && this.opts.data || this.objectToString.call(this, this.opts.data),
                    url = (str === '') && this.opts.url || (this.opts.url.split('?')[0] + '?' + str);
                    //GET方法下，若不传参则url不变；若传参，则其参数会被data替代
                this.xhr.open(this.opts.type, url, this.opts.async);
            }else if(this.opts.type === 'POST' || this.opts.type === 'post'){
                    //POST方法下，url则为问号分隔符前面的部分；
                this.xhr.open(this.opts.type, this.opts.url.split('?')[0], this.opts.async);
            }
            return this;
        },
        send: function(){
            if(this.opts.type === 'GET' || this.opts.type === 'get'){
                this.xhr.send();
            }else if(this.opts.type === 'POST' || this.opts.type === 'post'){
                //若POST参数为string，则传参；若不是，则将通过objectToString函数将object转化为string；
                var str = (typeof this.opts.data === 'string') && this.opts.data || this.objectToString.call(this, this.opts.data);
                this.xhr.setRequestHeader('content-type', 'application/x-www-form-urlencoded');
                this.xhr.send(str);
            }
        },
        objectToString: function(data){
            if(typeof data !== 'object') return data;
            var str = '';
            for(var prop in data){
                //遍历data，将其中的元素用&分开且练成字符串
                str += '&' + prop + '=' + data[prop];
            }
            return str.slice(1);
        }
    }
    exports.Ajax = Ajax; //将Ajax方法导出；
})(window, document);
```

通过json-server搭建后台数据；
(这个环境用于测试超级方便～)

使用方法如下：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>ajax</title>
</head>
<body>
    <script src="ajax.js"></script>
    <script>
        new Ajax().ajax({
            type: 'get',
            url: 'http://localhost:3000/db?c=123',      
            // data: 'c=456',           
            // data: {c: 456},
            dataType: 'json',
            async: false,
            success: function(data, status, xhr){
                console.log(data);
            },
            error: function(xhr, status){
                console.log(xhr);
            }
        });
        new Ajax().ajax({
            type: 'post',
            url: 'http://localhost:3000/db?c=123',      
            data: 'c=456',              
            // data: {c: 456},
            dataType: 'text',
            success: function(data, status, xhr){
                console.log(data);
            },
            error: function(xhr, status){
                console.log(xhr);
            }
        });
    </script>
</body>
</html>
```

原生Ajax
```
var xhr = new createXHR()；
xhr.onreadystatechange = function (){
    if(xhr.readyState == 4){
        if((xhr.status >= 200 && xhr.status < 300) || xhr.status ==304 ){
            console.log(xhr.responseText);
        }else{
            console.log("error"+xhr.status);
        }
    }
};
//get请求
xhr.open('get','url',true);
xhr.setRequestHeader("header","hello");
xhr.send(null);

//post请求
xhr.open('post','url',true);
xhr.setRequstHeader("Content-Type","application/x-www-form-urlencoded");
var form = document.getElementById('form');
//用serialize将表单序列化，创建字符串
xhr.send(serialize(form));

//FormData
var form = document.getElementById('form');
xhr.send(new FormData(form));

//此外还有load,progress等进度事件 
```

