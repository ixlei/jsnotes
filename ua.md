##useragent

&emsp;在浏览器中`navigator.userAgent`中保存着useragent信息。
* [ie userAgent](http://www.useragentstring.com/pages/Internet%20Explorer/)
* [edge userAgent](https://msdn.microsoft.com/en-us/library/hh869301(v=vs.85).aspx)
* [Chrome userAgent](http://www.useragentstring.com/pages/Chrome/)
* [FireFox userAgent](http://www.useragentstring.com/pages/Firefox/)
* [Safari userAgent](http://www.useragentstring.com/pages/Safari/)
* [Konqueror userAgent](http://www.useragentstring.com/pages/Konqueror/)

```javascript

var client = function() {
	var ua = navigator.userAgent;
	var engine = {
      ie: 0,
      gecko: 0,
      webkit: 0,
      opera: 0,
      khtml: 0,
      ver: null
    };
    
    var browser = {
      ie: 0,
      firefox: 0,
      chrome: 0,
      safari: 0,
      opera: 0,
      konq: 0,
      ver: null
    };

    switch(true) {
      case Boolean(window.opera):
        engine.ver = browser.ver = window.opera.version();
        engine.opera = browser.opera = parseFloat(engine.ver);
        break;
      case /AppleWebKit\/(\S+)/.test(ua):
        engine.ver = RegExp.$1;
        engine.webkit = parseFloat(engine.ver);
        if(/Chrome\/(\S+)/.test(ua)) {
          browser.ver = RegExp.$1;
          browser.chrome = parseFloat(browser.ver);
        } else if(/Version\/(\S+)/.test(ua)) {
          browser.ver = RegExp.$1;
          browser.safari = parseFloat(browser.ver);
        } else {
        	var safariVersion = 1;
        	if(engine.webkit < 100) {
        		safariVersion = 1
        	} else if(engine.webkit < 312) {
        		safariVerssion = 1.2;
        	} else if(engine.webkit < 412) {
        		safariVersion = 1.3;
        	} else {
        		safariVersion = 2;
        	}

        	browser.safari = browser.ver = safariVersion;
        }
        break;
      case /rv:([^\)]+)\) Gecko\/(\d{8})/.test(ua):
        engine.ver = RegExp.$1;
    	engine.gecko = parseFloat(engine.ver);
    	if(/FireFox\/(\S+)/.test(ua)) {
    		browser.ver = RegExp.$1;
    		browser.firefox = parseFloat(browser.ver);
    	}
    	break;
      case /MSIE ([^;])/.test(ua):
         engine.ver = browser.ver = RegExp.$1;
    	 engine.ie = browser.ie = parseFloat(engine.ver);
    	 break;
      case /KHTML\/(\S+)/.test(ua): 
        engine.ver = browser.ver = RegExp.$1;
        engine.khtml = browser.konq = parseFloat(engine.ver);
    	break;
      case /Edge/.test(ua):
        engine.ver = browser.ie = 12;
        browser.ver = browser.edge = 1;
    	break;
      case /Trident\/7\.0; rv\:11\.0/.test(ua):
        engine.ver = browser.ver = engine.ie = browser.ie =  11;
        break;
    }

    return {
      engine: engine,
      browser: browser
    };
    
}(); 

```