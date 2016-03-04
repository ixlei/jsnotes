##useragent

&emsp;在浏览器中`navigator.userAgent`中保存着useAgent信息。
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
    
    var system = {
      win: false,
      mac: false,
      xll: false,
      iPhone: false,
      ipod: false,
      ipad: false,
      ios: false,
      android: false,
      winMobile: false
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
    	if(/Firefox\/(\S+)/.test(ua)) {
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

    var platform = navigator.platform;
    system.win = platform.indexOf('Win') == 0;
    system.mac = platform.indexOf('Mac') == 0;
    system.xll = platform == 'xll' || platform.indexOf('Linux');

    if(system.win) {
      if(/Win(?:dows)?\s([^do]{2})?\s?(\d+\.\d+)?/.test(ua)) {
      	if(RegExp.$1 === 'NT') {
      	  switch(RegExp.$2) {
      	  	case "5.0":
      	  	  system.win = "2000";
      	  	  break;
      	  	case "5.1":
      	  	  system.win = "xp";
      	  	  break;
      	  	case "6.0":
      	  	  system.win = "Vista";
      	  	  break;
      	  	case "6.1":
      	  	  system.win = "7";
      	  	  break;
      	  	case "6.2":
      	  	  system.win = "8";
      	  	  break;
      	  	case "6.3":
      	  	  system.win = "8.1";
      	  	  break;
      	  	case "10.0":
      	  	  system.win = "10";
      	  	  break;
      	  	default: 
      	  	  system.win = "NT";
      	  }
      	} else if(RegExp.$1 == '9x') {
      		system.win = "ME";
      	} else {
      		system.win = RegExp.$1;
      	}
      }
    }

    system.iphone = ua.indexOf('iPhone') > -1;
    system.ipod = ua.indexOf('iPod') > -1;
    system.ipad = ua.indexOf('iPad') > -1;
    
    if(system.mac && ua.indexOf('Mobile') > -1) {
      system.ios = /CPU\s(?:iPhone)?OS\s(\d+_\d+)/.test(ua) 
        ? parseFloat(RegExp.$1.replace('_', '.'))
        : 2;
    }

    if(/Android\s(\d+\.\d+)/.test(ua)) {
      system.android = parseFloat(RegExp.$1);
    }

    return {
      engine: engine,
      browser: browser,
      system: system
    };
    
}(); 

```