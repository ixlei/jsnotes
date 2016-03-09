##千位分隔符实现

&emsp;千位分隔符实现很常见，例如`-1,233,552,214,233.214`;

```javascript

function getType(num) {
  return Object.prototype.toString.call(num);
}

function thoundBitSeparator(num) {
  let type = getType(num);
  if(type !== '[object Number]') {
    throw new TypeError(`${type} is not number`);
  }
  let regExp = /^([+-])?(\d+)(?=\d{3})(\.\d+)?/,
      strNum = num + '',
      $1, $s;
  while(regExp.test(strNum)) {
    $1 = RegExp.$1;
    $2 = RegExp.$2;
    strNum = $1 + $2 + ',' + strNum.replace($1 + $2, '');
  }

  return strNum;
}

```
```javascript
thoundBitSeparator(-12514752232.21)   //-12,514,752,232.21
thoundBitSeparator(10)                //10

```