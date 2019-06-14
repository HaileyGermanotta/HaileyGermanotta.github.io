## JavaScript类型检测

- `typeof`
- `instanceof`
- constructor
- toString

### typeof

---

`typeof`可以返回 `"undefined"`,`"boolean"`,`"string"`,`"number"`,`"object"`,`"function"` 

##### "undefined" 没有声明过的变量会输出

```javascript
typeof(undefined) //"undefined"
typeof(apple) //"undefined"
```

##### "boolean"

```javascript
var isA = true;
typeof isA  //"boolean"		
```

##### "string" 

```javascript
var message = 'some strings';
console.log(typeof messsage); //"string"
console.log(typeof (message)); //"string"
typeof("85")   //"string"
```

##### "object"   数组、对象、null都返回object

```javascript
var people = {
  "name": "angel",
  "age":12
};
typeof(people) //"object"

var a = [];
typeof a //"object"

typeof(null) //"object"
```

```javascript
var car = null;
typeof car //"object"
```

##### "function"

```javascript
function check(){
  console.log("checked");
}
console.log(typeof check); //"function"	
```

##### "number" NaN的类型是number

```javascript
console.log(typeof 85); //"number"
typeof NaN  //"number"
typeof Infinity //"number"
```



### typeof 用处

---

如果要判断一个变量是否存在可以用`typeof`

```javascript
if(typeof a != "undefined"){
//code
}
```

对正则表达式应用typeof会返回"function"

### instanceof

---

- 用于判断一个对象是否是数组、判断一个对象是否是某个对象的实例
- 只可以判断是不是对象、函数，不可用于判断字符串和数字

```javascript
var a = {};  
alert(a instanceof Object);  //true  
var b = [];  
alert(b instanceof Array);  //true 
```



### constructor

---

```javascript
var a=[1,2,3];
console.log(a.constructor==Array);//true
console.log(a.constructor==RegExp);//false
console.log((1).constructor==Number);//true
var reg=/^$/;
console.log(reg.constructor==RegExp);//true
console.log(reg.constructor==Object);//false
```

- 由于类的原型可以重写，所以constructor检测出来的结果可能不准确
- constructor 不可以检测null 和 undefined



### toString()

---

检测某个值是不是数组

```javascript
var arr = [1,2,3];   
function isArrayFn(obj){  //封装一个函数  
  if (typeof Array.isArray === "function") {   
    return Array.isArray(obj); //浏览器支持则使用isArray()方法  
  }else{  //否则使用toString方法  
    return Object.prototype.toString.call(obj) === "[object Array]";   
  }   
}   
alert(isArrayFn(arr));// true 
```

由于在任何值上调用Object的原生的`toString（）`方法都会返回一个`[Object NativeConstructorName]`格式的字符串，由于原生数组的构造函数名与全局作用于无关，因此调用`toString()`方法就能保证返回一致的值。

```javascript
function isArray(value){
	return Object.prototype.toString.call(value) == "[Object Array]";
}
```

同样的思路

检测某个值是不是原生函数

```javascript
function isFunction(value){
	return Object.prototype.toString.call(value) == "[object Function]"; 
}
```

检测某个值是不是正则表达式

```javascript
function isFunction(value){
	return Object.prototype.toString.call(value) == "[object RegExp]"; 
}
```

```javascript
Object.prototype.toString.call('') ;   // [object String]
Object.prototype.toString.call(1) ;    // [object Number]
Object.prototype.toString.call(true) ; // [object Boolean]
Object.prototype.toString.call(Symbol()); //[object Symbol]
Object.prototype.toString.call(undefined) ; // [object Undefined]
Object.prototype.toString.call(null) ; // [object Null]
Object.prototype.toString.call(new Function()) ; // [object Function]
Object.prototype.toString.call(new Date()) ; // [object Date]
Object.prototype.toString.call([]) ; // [object Array]
Object.prototype.toString.call(new RegExp()) ; // [object RegExp]
Object.prototype.toString.call(new Error()) ; // [object Error]
Object.prototype.toString.call(document) ; // [object HTMLDocument]
Object.prototype.toString.call(window) ; //[object global] window是全局对象 global 的引用

```

但是`toString()`方法不能够检测非原生构造函数的构造函数名，开发人员定义任何构造函数都将返回`[object Object]`

