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

  和javascript不同的是，JSON对象没有声明变量，同时，没有末尾的分号
。值得注意的是，JSON中的每个属性都必须必须加双引号，没有事错误的。

