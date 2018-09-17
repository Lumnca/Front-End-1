<a id="top" href="#top">Jquery 有用的方法  :maple_leaf:</a> 
----
`Jquery 工具类`
- [x] :maple_leaf: <a href="#extendIndex">`$.extend( target [, object1 ] [, objectN ] )`</a>
- [x] :maple_leaf: <a href="#mergeIndex">`$.merge( first, second )`</a>
- [x] :maple_leaf: <a href="#eachIndex">`$.each( collection, callback(indexInArray, valueOfElement))`</a>
- [x] :maple_leaf: <a href="#trimIndex">`$.trim()`</a>
- [x] :maple_leaf: <a href="#trimIndex">`$.grep( array, function(elementOfArray, indexInArray) [, invert ] )`</a>
- [x] :maple_leaf: <a href="#mapIndex">`$.map( array, callback(elementOfArray, indexInArray))`</a>
- [x] :maple_leaf: <a href="#trimIndex">`$.unique( array )`</a>
- [x] :maple_leaf: <a href="#parseJSONIndex">`$.parseJSON()`</a>
- [x] :maple_leaf: <a href="#noConflictIndex">`$.noConflict()`</a>


####  <a id="extendIndex" href="#extendIndex">$.extend( target [, object1 ] [, objectN ] )</a>  :star2: <a href="#top"> :arrow_up: </a>
`jQuery.extend( target [, object1 ] [, objectN ] )`
```javascript
var object = $.extend({}, object1, object2);
```
####  <a id="mergeIndex" href="#mergeIndex">jQuery.merge()</a>  :star2: <a href="#top"> :arrow_up: </a>
`合并两个数组内容到第一个数组。$.merge()函数是破坏性的。它会修改第一个数组的内容，并将第二个数组的内容添加到第一个数组中。`
```javascript
let list = new Array(1,2,3,4,5,6,7);
let listTwo = new Array(10,12,14,16,18,20);
let result = $.merge(list,listTwo);
alert(result);
alert(list);
```
####  <a id="eachIndex" href="#eachIndex">$.each( collection, callback(indexInArray, valueOfElement))</a>  :star2: <a href="#top"> :arrow_up: </a>
`$.each()函数和 $(selector).each()是不一样的，那个是专门用来遍历一个jQuery对象。$.each()函数可用于迭代任何集合`
```javascript
$.each([52, 97], function(index, value) {
  alert(index + ': ' + value);
});
```
####  <a id="trimIndex" href="#trimIndex">$.trim()</a>  :star2: <a href="#top"> :arrow_up: </a>
`去掉字符串起始和结尾的空格。`
```javascript
$.trim("    hello, how are you?    ");
```
####  <a id="grepIndex" href="#grepIndex">$.grep( array, function(elementOfArray, indexInArray) [, invert ] )</a>  :star2: <a href="#top"> :arrow_up: </a>
`查找满足过滤函数的数组元素。原始数组不受影响。`
* `array 类型: Array 用于查询元素的数组。`
* `function(elementOfArray, indexInArray) 类型: Function() 该函数来处理每项元素的比对。第一个参数是正在被检查的数组的元素，第二个参数是该元素的索引值。该函数应返回一个布尔值。this将是全局的window对象。`
* `invert 类型: Boolean 如果“invert”为false，或没有提供，函数返回一个“callback”中返回true的所有元素组成的数组，。如果“invert”为true，函数返回一个“callback”中返回false的所有元素组成的数组。`
```javascript
let vals =[0,1,2];
let lsmore0 = $.grep( vals, function(value,index){
    return value > 0;
},false); //筛选出满足条件的

let lsless0 = $.grep( vals, function(value,index){
    return value > 0;
},true);

console.log(lsmore0);
console.log(lsless0);
console.log(vals);
```
####  <a id="mapIndex" href="#mapIndex">map( array, callback(elementOfArray, indexInArray))</a>  :star2: <a href="#top"> :arrow_up: </a>
`将一个数组中的所有元素转换到另一个数组中。`
* `array 类型: Array 待转换数组。`
* `callback(elementOfArray, indexInArray) 类型: Function() 处理每一个元素的函数。第一个参数是数组元素，第二个参数是该元素的索引值。该函数可以返4回任何值。在函数内部，this将是全局的window对象。`
```javascript
let vals = $.map( [0,1,2], function(n){
    return n > 0 ? n + 1 : null; //组成一个新的数组 返回的值
});
console.log(vals);
```
####  <a id="uniqueIndex" href="#uniqueIndex">$.unique( array )</a>  :star2: <a href="#top"> :arrow_up: </a>
`删除数组中重复元素。只处理删除DOM元素数组，而不能处理字符串或者数字数组。`
* `array 类型: Array DOM元素的数组。`
```javascript
let vals = $.unique([12,12,13,15,12,60,1,-1,1,56,60]);
console.log(vals);
```
####  <a id="parseJSONIndex" href="#parseJSONIndex">$.parseJSON()</a>  :star2: <a href="#top"> :arrow_up: </a>
`接受一个标准格式的 JSON 字符串，并返回解析后的 JavaScript 对象。`
```javscript
var obj = jQuery.parseJSON('{"name":"John"}');
alert( obj.name === "John" );
```
####  <a id="noConflictIndex" href="#noConflictIndex">$.noConflict()</a>  :star2: <a href="#top"> :arrow_up: </a>
`放弃jQuery控制$ 变量。 使用另外一个别名`
```javascript
 var jq=jQuery.noConflict();
 let val = jq.trim("asdasdasd     ");
 console.log(val);
```








