## Deep copy in JS

深度拷贝是指拷贝出一个新的实例，与被拷贝的实例互不影响。

深度拷贝一般有**两种**办法，一种是通过**递归**来实现，一种是通过**`JSON.parse`和`JSON.stringify`**来实现。

##### 递归：

```javascript
function cloneDeep(obj){
  if( typeof obj !== 'object' || Object.keys(obj).length === 0 ){
    //如果进来的不是一个对象，则返回本身
    //如果进来的obj是一个对象，但是里面没有属性，就返回对象本身
      return obj
  }
  let resultData = {}
  return recursion(obj, resultData)
}

function recursion(obj, data={}){
  for(key in obj){
      if( typeof obj[key] == 'object' && Object.keys(obj[key]).length>0 )){
          data[key] = recursion(obj[key])//采用递归的方法将对象中的对象也拷贝过来
      }else{
          data[key] = obj[key]
      }
  }
  return data
}
let obj = {name:'程序猿',age:{child:20}}
let obj2 = cloneDeep(obj)
obj.name = '单身狗'
obj2.age.child = 24
console.log(obj) // {name:'程序猿',age:{child:20}}
```

##### 递归：

```javascript
// 递归实现一个深拷贝
function deepClone(source){
   if(!source || typeof source !== 'object'){
     throw new Error('error arguments', 'shallowClone');
   }
   var targetObj = source.constructor === Array ? [] : {};
   for(var keys in source){
      if(source.hasOwnProperty(keys)){
         if(source[keys] && typeof source[keys] === 'object'){
           targetObj[keys] = source[keys].constructor === Array ? [] : {};
           targetObj[keys] = deepClone(source[keys]);
         }else{
           targetObj[keys] = source[keys];
         }
      } 
   }
   return targetObj;
}
```

##### JSON方式：

弊端就是：在序列化JavaScript对象时，所有函数和原型成员会被有意忽略就（即方法复制不过去

```javascript
// 利用JSON序列化实现一个深拷贝
function deepClone(source){
  return JSON.parse(JSON.stringify(source));
}
```

JSON中的`stringify`可以把js对象序列化为一个json字符串，`parse`可以把json字符串反序列化为一个json对象。



## 浅拷贝 

对一个数组或者对象的浅拷贝

```javascript
function shallowClone(source) {
  if (!source || typeof source !== 'object') {  
    //判断进来的参数是不是一个对象，因为无论数组还是对象，本质都是对象
    throw new Error('error arguments');//如果不是的话，就抛出错误
  }
  var targetObj = source.constructor === Array ? [] : {};
  //根据进来的参数的类型决定，拷贝生成的是一个对象还是数组，这里用到了constructor来判断对象的类型
  for (var keys in source) {//遍历对象或者数组中的每一个属性
    if (source.hasOwnProperty(keys)) { //判断进来的对象数组是否具有这么一个属性
      targetObj[keys] = source[keys]; //如果有的话，将这个属性值赋给新建的数组/对象
    }
  }
  return targetObj;//返回一个数组/对象
}
```





参考链接：

[JavaScript中的浅拷贝和深拷贝](https://segmentfault.com/a/1190000008637489)

[JavaScript复制（合并）对象](https://segmentfault.com/a/1190000011492291)

