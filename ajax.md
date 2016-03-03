##ajax

### XMLHttpRequest对象

```javascript

function createXHR() {
  return (function f() {
    if(typeof XMLHttpRequest !== 'undefined') {
     return new XMLHttpRequest();
   }
   
   if(typeof ActiveXObject !== 'undefined') {
     if(f.activeXObject !== 'string'){
     	var versions = ['MSXML2.XMLHttp.6.0', 'MSXML2.XMLHttp.3.0', 'MSXML2.XMLHttp'];
     	for(var i = 0, ii = versions.length; i < ii; i++) {
          try {
          	new ActiveXObject(versions[i]);
          	f.activeXObject = versions[i];
          	break;
          } catch(e) {

          }
     	}
     	return new ActiveXObject(f.activeXObject);
     }
   }

   throw new Error('no xhr');
  })();
}

```


###XHR的用法

`xhr.open(method, url, bool)`

* method表示请求方法,get,post。
* url表示请求地址。
* bool为true时发起异步请求，为false时同步请求。

`xhr.send(data)`表示请求主体发送数据，如果不发送，则必须指定为null。

###响应
* responseText作为响应的文本。
* responseXML 响应类型为"text/xml"或"application/xml",这个属性将保存响应数据的XML DOM文档。
* status 保存响应的状态码。
* statusText http状态说明。

###响应阶段
* 同步发送。

* 异步请求

0. : 未初始化。尚未调用open方法。
1. : 启动。调用open方法，但没有调用send。
2. : 发送数据。调用send,但没有接到响应数据。
3. : 接收。接收部分数据，但没有发送完。
4. : 完成。接收全部数据。客户端可以使用。

```javascript

function request(o) {
  var xhr = null;
  try {
    xhr = createXHR();
  } catch(e) {
    throw new Error('create XHR error');
  }
  
  xhr.onreadystatechange = function() {
    if(xhr.readyState === 4) {
      if((xhr.status >= 200 && xhr.status < 300) || xhr.status === 304) {
      	o.success(xhr.responseText);
      } else {
      	o.error(xhr.statusText);
      }
    } 
  } 

  xhr.open(o.method, o.ourl, o.async);
  xhr.send(o.data);
}

```
>xhr.onreadystatechange的callback没有使用this代替xhr,部分浏览错误.

`xhr.abort()`在接受响应之前停止请求。

### `xhr.setRequestHeader("myHeader", "myValue");`
>setRequestHeader不建议设置http的请求头,在调用时必须在open之后，send之前。

###XMLHttpRequest2

#####FormData序列化表单和创建和表单一样的数据

```javascript
var formdata = new FormData();
formdata.append("name", "yanglei");
```

```javascript
var form = document.forms.form;
var formdata = new FormData(form);
```

###跨域技术
* 图像ping
```javascript

var img = new Image();
img.onload = img.onerror = function() {
  console.log('Done');
};

img.url = url;

```

* JSONP

```javascript
function handleResponse(response) {
	//todo
}

var script = document.createElement('script');
script.src = url + '?callback=' + handleResponse;
document.body.appendChild(script);

```
