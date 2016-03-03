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