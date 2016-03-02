## JSON

>JSON(javascript 对象表示法)是一种重要的数据格式，相对于xml,它更受开发者喜欢。


###语法
* 简单值： JSON可以表示字符串，数值，布尔值，null。但是不能表示undefined。
* 对象：对象是一种比较复杂的数据结构，表示一组无序的键值对。
每个键值对中的值可以是简单值，也可以是对象。
* 数组：数组也是一种复杂的数据结构，数组的值可以是简单值，对象，数组。

###简单值

```javascript
'javascript'  //string
true          //boolean
5             //number
null          //null
```

### 对象

javascript中的对象

```javascript
var person = {
	name: "yanglei",
	age: 21,
	school: {
       name: "DUT",
       address: "dalian"
  }
};
```
JSON中的对象表示上述对象

```javascript
{
  "name": "yanglei",
  "age": 21,
  "school": {
     "name": "DUT",
     "address": "dalian"
  }
}
```
&emsp;javascript不同的是，JSON对象没有声明变量，同时，没有末尾的分号。值得注意的是，JSON中的每个
属性都必须必须加双引号，没有事错误的。

###数组

js中的数组

```javascript
var values = [25, null, "javascript", {type: "array"}, [666, 25]];
```
JSON表示上述数组

```javascript
  [25, null, "javascript", {"type": "array"}, [666, 25]]
```

##序列化和解析

###系列化
&emsp;`JSON.stringify`可以把js对象序列化为JSON字符串

```javascript
JSON.stringify(plainobject, filter, space);
```
* 序列化 plain Object

```javascript
var person = {
	name: "yanglei",
	age: 21,
	school: {
       name: "DUT",
       address: "dalian"
  }
};

var jsonText = JSON.stringify(person);

// {"name":"yanglei","age":21,"school":{"name":"DUT","address":"dalian"}}

typeof jsonText    //string

```
> `JSON.stringify` serialize circular structure object will throw TypeError;

* 非数组对象的属性不能保证以特定的顺序出现在序列化后的字符串中。
* 布尔值、数字、字符串的包装对象在序列化过程中会自动转换成对应的原始值。
*不能序列化circular structure。
* 不可枚举的属性会被忽略。
* undefined、任意的函数以及 symbol 值，在序列化过程中会被忽略（出现在非数组对象的属性值中时）或者被转换成 null（出现在数组中时）。
* 所有以 symbol 为属性键的属性都会被完全忽略掉，即便 replacer 参数中强制指定包含了它们。


```javscript
JSON.stringify(window)  //web环境下

//throw error `Uncaught TypeError: Converting circular structure to JSON`
```
>`JSON.stringify` 会忽略属性为`non-enumerable`；

```javascript
var err = new Error('error message');
var jsonText = JSON.stringify(err);
console.log(jsonText);   //{}
```
读取对象属性的特性

```javascript
var ownPropertyNames = Object.getOwnPropertyNames(err),
    descriptor = null;

ownPropertyNames.forEach(function(key, index, arr) {
	descriptor = Object.getOwnPropertyDescriptor(err, item);
	console.log(key + ' enumerable',  descriptor.enumerable);
});
res:
 //stack enumerable false
 //message enumerable false
```
解决方案:

```javascript

function stringifyError(err, filter, space) {
    var plainObject = {};
	Object.getOwnPropertyNames(err).forEach(function(key, index, arr) {
       plainObject[key] = err[key];
	});
	return JSON.stringify(plainObject, filter, space);
}
```
test:
```javascript
var jsonErrText = stringifyError(err);
console.log(jsonErrText);
```
>`undefined function` stringify

```javascript
JSON.stringify({key: undefined, f: function() {}});  //{}
//ignore value is undefined and function

JSON.stringify([undefined, function(){}, 14, true]);  //[null,null,14,true]

```

### 过滤

####参数为数组
```javascript

var person = {
	name: "yanglei",
	age: 21,
	school: {
       name: "DUT",
       address: "dalian"
  }
};

var filterRes = JSON.stringify(person, ["name", "age"]);
console.log(filterRes);   // {"name":"yanglei","age":21}  
```

####参数为函数
&emsp;此时会传入两个参数，key和value,初始化时，key为空，value要JSON的对象，然后每个键值对也会一级一级的传入这个函数。

* 如果value是number、boolean类型会调用toString()去转化value。
* 如果value是string,直接加入。
* 如果value是function, undefined,则忽视。
* 如果value是object,则递归以上规则。


```javascript

var person = {
	name: "yanglei",
	age: 21,
	school: {
       name: "DUT",
       address: "dalian"
  }
};

var filterRes = JSON.stringify(person, function(key, value) {
	switch(key) {
      case "school": return undefined;
      default: return value;
   }
});

console.log(filterRes);

//{"name":"yanglei","age":21}
```
###字符串缩进
&emsp; 用于字符串缩进和空白符，可以是数字，也可以是字符串，如果是数字，大于10的会被转化为10，字符串最长为10。

```javascript

var person = {
	name: "yanglei",
	age: 21,
	school: {
       name: "DUT",
       address: "dalian"
  }
};

var jsonText = JSON.stringify(person, null, 4);
console.log(jsonText);

/*
{
    "name": "yanglei",
    "age": 21,
    "school": {
        "name": "DUT",
        "address": "dalian"
    }
}
*/
```
###toJSON方法

返回JSON方法的数据格式

```javascript
var person = {
	name: "yanglei",
	age: 21,
	school: {
       name: "DUT",
       address: "dalian"
  },
  toJSON: function() {
    return 'toJSON';
  }
};

var jsonText = JSON.stringify(person);

console.log(jsonText);  // "toJSON"
```

&emap;序列化顺序
* 如果存在toJSON,则调用toJSON。否则返回对象。
* 如果存在第二个参数，则调用该方法。否则返回对象本身。
* 如果存在第三个参数，则格式化json。


###解析json

`JSON.parse`可以接受另一个参数，还原函数。此函数接受两个参数，一个键和一个值。如果函数返回undefined,则会删除改键。

```javascript

var person = {
	name: "yanglei",
	age: 21,
	school: {
       name: "DUT",
       address: "dalian"
  }
};

var jsonText = JSON.stringify(person);

var personCopy = JSON.parse(jsonText);

console.log(personCopy);

```
>parse circle struct 会抛出错误.

```javascript

JSON.parse(window);

//Uncaught SyntaxError: Unexpected token

```



