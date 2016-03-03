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

