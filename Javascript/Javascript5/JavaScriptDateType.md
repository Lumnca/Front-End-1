<a id="top" href="#top">JavaScript 原生数据类型  :maple_leaf:</a> 
----
`1.undefined 派生自null  所以两个相等`
```javascript
var isEqual = (null == undefined)
console.log(isEqual)

```
`2.获得最大值最小值,有些值超越了这个界限 就变成了无限值 正无穷 负无穷 ` <br/>
`3.判断值是否是无穷 isFinite 无穷返回 false 有穷 返回 true `
```javascript
var max = Number.MAX_VALUE //获得最大值
var min = Number.MIN_VALUE //获得最小值

console.log(max) //1.7976931348623157e+308
console.log(min) //5e-324
console.log(isFinite(max)) //true
```
`4.Number 数值转换 将其他值转换为数值类型`:**`只有不为空的且非全数字的字符串 和 undefined 会转换成NaN`**
```javascript
var num1 = Number("6546sdf")
var num2 = Number("sdf")
var num3 = Number("")
var num4 = Number("00056")
var num5 = Number(true)
var num6 = Number(null)
var num7 = Number(undefined)
console.log(num1,num2,num3,num4,num5,num6,num7) 
         // NaN   NaN  0    56   1    0    NaN
```
`5.parseInt只认数字或者以数字开头 近能够进行进制转换`
```javascript
var num1 = parseInt("6546sdf")
var num2 = parseInt("sdf")
var num3 = parseInt("")
var num4 = parseInt("00056")
var num5 = parseInt(true)
var num6 = parseInt(null)
var num7 = parseInt(undefined)
var num8 = parseInt("523",8) // 转换8进制
var num9 = parseInt("AAA",16) //  16进制
console.log(num1,num2,num3,num4,num5,num6,num7,num8,num9) 
         // 6546  NaN  NaN  56   NaN  NaN NaN  339  2730
```
`6.parseFloat只认数字或者以数字开头 不能够进行进制转换`
```javascript
var num1 = parseFloat("4554.2jj")
var num2 = parseFloat("0085.2")
var num3 = parseFloat("15.2e5")
var num4 = parseFloat("asdsa")
var num5 = parseFloat(true)
var num6 = parseFloat(null)
var num7 = parseFloat(undefined)
var num8 = parseFloat("0523",8) // 转换8进制
var num9 = parseFloat("0xAAA",16) //  16进制
console.log(num1,num2,num3,num4,num5,num6,num7,num8,num9) 
         // 4554.2 85.2 1520000 NaN NaN NaN NaN 523 0
```
`7.Javascript 的字符串是一旦创建不可改变,一旦改变就必须先销毁原来的字符串,然后再用另一个包含新值的字符串填充变量`

`8.Object 是Js的终极父类`
```javascript
var o = new Object()
o.name = "kikcer"
o.constructor    
//constructor:保存着用于创建当前对象的函数,对于Object对象来说  就是Object()
console.log(o.hasOwnProperty("name")); //true
//hasOwnProperty(PropertyName) 判断属性在当前对象实例中而不是在实例的原型中
console.log(o.propertyIsEnumerable("name"));//true
//propertyIsEnumerable(name) 判断给定属性是否可以用for in  枚举
console.log(o.isPrototypeOf("name"));
//isPrototypeOf 检查传入的对象是否是当前对象的原型
for(var val in o){
    console.log(val)
}
//name
```
`9.toLocaleString 返回字符串表示 和toString 一样 只是会考虑地区 例如时间格式`
```javascript
console.log(o.toString())
console.log(o.toLocaleString()) 
console.log(o.valueOf()) //返回对象的字符串 数值或布尔表示 通常和toString 返回值一样
/*
[object Object]
[object Object]
{ name: 'kikcer' }
*/
```
`10.无穷乘以0 返回NaN  NaN乘以任何数字 等于NaN`
`11.严格模式下对于函数argument的影响`
```javascript
function minArgs(one,two){
  "use strict"
   console.log(one === arguments[0])
   console.log(two === arguments[1])

   one = "c"
   two = "e"
   console.log(one === arguments[0])
   console.log(two === arguments[1])
}
minArgs("gg","tt");
true
true
false
false
//去掉"use strict" 返回都是true 但是写js 最好使用严格模式
```
`12.js 函数没有重载`

##### [运算符 操作符号](#top)
`1. 逗号操作符`
```node
var i =1,num2 = 3 ,num4 = 5;
// 使用逗号操作符 一条语句运行多个操作
```
`2. === !== 全等和不全等运算符` <br/>
`== 和 != 在执行的时候回进行隐式转换 例如 7 == "7" 返回 true 但是 全等操作符 会比较类型 引用 7 === "7" 返回false`
<br/?
`3.for-in 运算符`
* `对于数组 返回索引,对于对象返回key`
```node
function Person(name,age){
    this.name = name;
    this.age = age;
}
Person.prototype.GetName = function () {
    return this.name.toLowerCase();
}

let p1 = new Person("JxKicker",19);

for (let val in p1) {
    console.log(val); //name age GetName
}

let array = ["list","jxkicker",true]

for(let value in array){
    console.log(value); // 0 1 2
}
```
-----
`其他的都很简答的`
