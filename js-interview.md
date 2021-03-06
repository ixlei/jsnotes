## js篇
* 手写Promise实现 （搜狐－校招1面）
* 手写字符串转int（搜狐－校招1面）
```javascript
function hash(a) {
  const d = /\d/;
  if(d.test(a)) {
      return a;
  }
  const regexp = [/[a|A]/, /[b|B]/, /[c|C]/, /[d|D]/, /[e|E]/, /[f|F]/];
  const res = [10, 11, 12, 13, 14, 15];
  for(let i = 0; i < 5; i++) {
     if(regexp[i].test(a)) {
         return res[i];
     }
  }
  return 0;
}

function atoi(str) {
    str = str.trim();
    const regexp = /^([+-])?(0x([0-9a-fA-F]+)*|(\d+))/;
    let temp = regexp.exec(str);
    if(temp === null) {
       return 0;
    }
    let res = 0, 
        minVal = Number.MIN_VALUE, 
        maxVal = Number.MAX_VALUE,
        isPositveNum = temp[1] !== '-',
        isTenDigit = temp[4] !== undefined;
    let digit = isTenDigit ? temp[4] : temp[3];
    let ordinal = isTenDigit ? 1 : 1 << ((digit.length - 1) << 2);
    for(let i = 0, ii = digit.length; i < ii; i++) {
        res *= 10;
        if(isTenDigit) {
           res += digit.charAt(i) * ordinal;
         } else {
           res += hash(digit.charAt(i)) * ordinal;
           ordinal = ordinal >> 4;
         }
         if((!isPositveNum && -res <= minVal) 
         || (isPositveNum && res >= maxVal)) {
             return !isPositveNum ? minVal : maxVal;
         }
     }
    return !isPositveNum ? -res : res;
}
```

* 利用insertBefore实现insertAfter（美团－实习1面）
```javascript
function insertAfter(ele, newEle) {
  let parentNode = ele && ele.parentNode;
  if(!parentNode) {
    return;
  }
  parentNode.insertBefore(newEle, ele.nextSibling);
}
```
* 实现deepEqual (美团－实习2面)
```javascript
function deepEqual(a, b) {
    if (a === b) {
      return true;
    }
    
    //if a = NaN, a !== a is true
    if(a !== a && b !== b) {
      return true;
    }

    if (a === null || b === null) {
      return false;
    }

    if (isFunction(a)) {
      if (isFunction(b)) {
        return a.toString() === b.toString();
      }
      return false;
    }

    if (isObject(a) && isObject(b)) {
      if (Array.isArray(a)) {
        if (Array.isArray(b)) {
          const lena = a.length;
          if (lena === b.length) {
            for (let i = 0; i < lena; i++) {
              if (!deepEqual(a[i], b[i])) {
                return false;
              }
            }
            return true;
          }
          return false;
        }
        return false;
      }

      if (isDate(a)) {
        if (isDate(b)) {
          return a.getTime() === b.getTime();
        }
        return false;
      }

      if (isRegExp(a)) {
        if (isRegExp(b)) {
          return a.toString() === b.toString() && a.lastIndex === b.lastIndex;
        }
        return false;
      }

      if (isDeepObject(a)) {
        if (isDeepObject(b)) {
          for (const key in a) {
            if (!deepEqual(a[key], b[key])) {
              return false;
            }
          }

          for (const key in b) {
            if (!deepEqual(a[key], b[key])) {
              return false;
            }
          }
          return true;
        }
        return false;
      }
    }
    return false;
  }
```
* 实现ajax （腾讯－校招1面）
```javascript
function ajax(o) {
  let xhr;
  if(typeof XMLHttpRequest != 'undefined') {
    xhr = new XMLHttpRequest();
  } else {
    xhr = new ActiveXObject("Microsoft.XMLHTTP");
  }
  xhr.open(o.url, o.method || 'get', false);
  xhr.onreadystatechange = fucntion(res) {
    if(xhr.readystate == 4) {
      if(xhr.status == 200 || xhr.status == 304) {
        o && o.success && o.success(res)
      } else {
        o && o.error && o.error(res)
      }
    }
  }
  xhr.send(o.data || '');
}
```
* 实现请求参数获取（百度－校招2面）
```javascript
function getParam() {
  let query = location.search.substring(1);
  query = encodeURIComponent(query);
  let regexp = /([^&=]+)(=([^=&]+))*/g;
  let temp, res = {};
  while(temp = regexp.exec(query)) {
    res[temp[1]] = temp[3];
  }
  return res;
}
```
* 无限滑屏滚动实现（百度－校招2面）
* 使用react遇到的问题？（美团－实习2面&百度－校招2面）
* 手写实现ajax跨域（百度－校招1面）
*  == 和 === 的区别（百度－校招1面）
*  apply、call、bind以及this的考察。（百度－校招2面）
*  去除抖动（百度－校招2面）
```javascript
let debounce = {
  timeout: null,
  nodebounce(cb) {
    if(timeout) {
      clearTimeout(timeout);
    } 
    timeout = setTimeout(cb, 350);
  }
}
```
*  优雅的防止ajax的缓存（百度－校招1面）
*  js实现面向对象（百度－校招1面）
*  前端异步通信方式（美团－实习1面）
*  讲一讲fetch （今日头条－校招1面）
*  ajax的api？状态？（今日头条－校招1面）
*  setTimeout 和 ng中timeout的区别（阿里－实习1面）
*  讲一讲你实现的组件或者你看过的组件？（阿里－实习1面）
*  讲一讲redux（阿里－实习1面）
*  angualr中的directive的实现原理（阿里－实习1面）
*  如何保障nodejs 服务的稳定？（阿里－实习2面）
*  你使用的模版引擎有哪些？（阿里－实习1面）
*  你是怎样调试nodejs代码的？（阿里－实习1面）
*  讲一讲事件代理（阿里－实习1面）
*  你有读过jquery源码吗？（阿里－实习1面）
*  复杂表单事件绑定（阿里－实习2面）
*  redux中store的api（阿里－实习2面）
*  react中state和props的区别和用法？（阿里－实习2面&今日头条－校招3面）
*  实现元素拖动动画（腾讯－校招2面）
*  事件模型，冒泡及其作用（腾讯－内推2面）
*  angular的双向绑定实现方式？如果是你来实现，你打算怎么做？（腾讯－内推2面）
*  react中的单向数据流？react 的生命周期？virtualdom 算法（蘑菇街－校招2面）
*  react组件中模态窗是怎么实现的？（小米－校招1面）
*  angular中相同层级的control怎么样实现通信（小米－校招2面）
*  变量提升级let、const、var（小米－校招2面）
*  string的api有哪些？（小米－校招2面）
*  react服务端同构（小米－校招2面）
*  讲一讲redux的container（小米－校招2面）
*  redux中异步action是怎么实现的？（小米－校招2面）
*  你写过哪些express的中间件？（小米－校招2面）
* react-router的实现原理（搜狐－校招1面）
* virtualdom算法（搜狐－校招1面）
* 前端继承实现（腾讯－内推1面）
```javascript
function inherits(parent, child) {
  child.prototype = Object.create(parent.prototype);
  child.prototype.constructor = child;
}
function Parent(){

}
function Child() {
  Parent.call(this);
}
```
* 作用域链和原型链？（腾讯－内推1面）
* 前端跨域实现（今日头条－校招1面）
* ajax的跨域浏览器实现？页面中跨域和直接在浏览器中输入网址一样吗？https页面跨域访问http协议是否可行，反之？服务端跨域实现？cookies跨域访问？（今日头条－校招3面）
* js由哪些部份构成？window有哪些api（搜狐－校招1面）
* react、angular的异同？ （腾讯－校招1面）
* js实现动画的方式，和css的不同，优缺点。setTimeout、setInterval、requestAnimation的不同（腾讯－内推2面）
* 如何nodejs的多进程管理（腾讯－校招1面）
* ajax的跨域实现（腾讯－校招1面）
* js的垃圾回收机制及优化（去哪儿校招）
* 在捕获阶段stoppropagation，冒泡阶段能收到吗？（去哪儿）
* 讲一讲es6中generator、promise、symbol中的iterator 及set、map（美团－实习1面）
* 什么是函数式编程？（美团－实习2面）
* react组件的优化（今日头条－校招3面）
* js能够表示的最大位数（今日头条－校招3面）
* 在加法、乘法、位运算中那个最快？为什么？（今日头条－校招3面）
* 如果没有框架？你打算怎么办？（腾讯－校招2面）
* 怎么实现一个框架？（腾讯－内推3面）
* webpack怎么实现依赖分析的（搜狐－校招1面）
* 下面输出哪些数字
```javascript
if([]){ 
  console.log(1)
}
if({}) {
  console.log(2)
}
if([] === false) {
  console.log(3)
}
if({} === true) {
  console.log(4)
}
```