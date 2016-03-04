##storage

###离线检测

* `navigator.onLine`

&emsp; navigator.onLine为true时，在线状态，反之为离线。

* 'online 和 offline'事件。当在线状态改变时就会触发这两个事件。在window上触发。

```javascript
window.addEventListener('online', function(e) {
	//todo
}, false);

window.addEventListener('offline', function(e) {
	 //todo
}, false);

```

###应用缓存


###数据存储

####Cookie分为持久Cookie和临时会话Cookie。

####Cookie的构成。

* 名称：一个唯一确定cookie的名字，不区分大小写，在实践中最好区分，主要是某些服务器会在乎，同时名称必须经过URL编码,即通过decodeURIComponent来解码和encodeURIComponent来编码。
* 值：存储cookie的值得字符串。值必须经过URL编码。
* 域：特定域的cookie才会发送。
* 路径： 指定域中的路径，向服务器发送cookie。
* 失效时间：GMT格式的时间。持久化的cookie即使浏览器关闭也会保存。
* 安全标志: 此字段没有值，制定后只有使用SSL连接的时候才会发送到服务器
每一段信息通过分号分隔。

```javascript
name=value
name=value;expires=expires_time
name=value;expires=expires_time;path=domain_path;domain=domain_name;secure
```

####javascript中的cookie。

`document.cookie`可读写。

```javascript

var cookieUtil = {
  getCookie: function(name, _cookie) {
     name = encodeURIComponent(name);
     var cookieValue = null,
         cookie = _cookie,
         itemArr = null,
         itemOb = {},
         key = '',
         value = '';

     if(!cookie) {
       return cookieValue;
     }

     itemArr = cookie.split(';');
     itemArr.forEach(function(data) {
     	item = data.split('=');
     	key = typeof item[0] === 'string' ? item[0].trim() : item[0];
     	value = typeof item[1] === 'string' ? item[1].trim() : item[1];
        itemOb[key] = value;
     });

     return decodeURIComponent(itemOb[name]) || cookieValue;
  },

  setCookie: function(name, value, expires, path, domain, secure) {
    var cookie = encodeURIComponent(name) + '=' + encodeURIComponent(value),
        item = [];
    item.push(cookie);
    if(expires instanceof Date) {
      item.push('expires=' + expires.toGMTString());
    }

    if(path) {
      item.push('path=' + path);
    }

    if(domain) {
      item.push('domain=' + domain);
    }

    if(secure) {
       item.push('secure');
    }

    document.cookie = item.join('; ');
    console.log(item.join('; '));
  }
};




