### [JavaScript 引用类型](#top) <b id="top"></b> :maple_leaf:

----
:white_check_mark: `引用类型通常叫做类（class），也就是说，遇到引用值，所处理的就是对象`

- [x] :maple_leaf: [`Object 对象`](#object)
- [x] :maple_leaf: [`Boolean 对象`](#boolean)
- [x] :maple_leaf: [`Number 对象`](#number)
- [x] :maple_leaf: [`String 对象`](#string)
- [x] :maple_leaf: [`Array 对象`](#array)
- [x] :maple_leaf: [`Date 对象`](#date)
- [x] :maple_leaf: [`Function 对象`](#function)
- [x] :maple_leaf: [`Global 对象`](#global)
- [x] :maple_leaf: [`Math 对象`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math)

#####  :star2: [Object 对象](#top) <b id="object"></b>
`尽管JS支持对象,但是它并不支持接口和类的基本结构,引用类型又叫对象定义 描述属性和方法`
* `Object 是终极父类 Object 对象中的所有属性和方法都会出现在其他对象中`

`创建对象的方法`
```javascript
//1.0 构造函数
var person = new Object();
person.name = "kicker";
person.age = 15;
//2.0 对象字面法 更加常用
var apple = {
   color:"red"
}
//3.0
var phone = {};
phone.color = "red"
```
###### [Object 对象具有下列属性](#top)
* `constructor`:`对创建对象的函数的引用（指针）。对于 Object 对象，该指针指向原始的 Object() 函数。`
* `Prototype`:`对该对象的对象原型的引用。对于所有的对象，它默认返回 Object 对象的一个实例。`
###### [Object 对象还具有几个方法`](#top)
* `hasOwnProperty(property)`:`判断对象是否有某个特定的属性。必须用字符串指定该属性。（例如，o.hasOwnProperty("name")）`
* `IsPrototypeOf(object)`:`判断该对象是否为另一个对象的原型`
* `PropertyIsEnumerable`:`判断给定的属性是否可以用 for...in 语句进行枚举。`
* `ToString()`:`返回对象的原始字符串表示。对于 Object 对象，ECMA-262 没有定义这个值，所以不同的 ECMAScript 实现具有不同的值`
* `ValueOf()`:`返回最适合该对象的原始值。对于许多对象，该方法返回的值都与 ToString() 的返回值相同。`
`自己定义一个构造函数`
```javascript
function Person(Name,Age,Sex){
    this.name = Name;
    this.age = Age;
    this.sex = Sex;
    this.show = function(){
        console.log(`${this.name} ${this.sex} ${this.age}` )
    }
};

var p1 = new Person("kicker",17,true);
p1.show();
console.log
function Person(Name,Age,Sex){
    this.name = Name;
    this.age = Age;
    this.sex = Sex;
    this.show = function(){
        console.log(`${this.name} ${this.sex} ${this.age}` )
    }
};

var p1 = new Person("kicker",17,true);
p1.show();

console.log(`Name:${p1["name"]}`);
console.log(`Name:${p1["age"]}`);
console.log(`Name:${p1["sex"]}`);
```
* `访问属性的方式,不仅仅可以通过` `.` `的方式 还可以通过方括号` `[]` `变量的方式引用属性`

##### :maple_leaf: [Boolean 对象](#top)  <b id="boolean"></b>
* `Boolean 对象是 Boolean 原始类型的引用类型。要创建 Boolean 对象，只需要传递 Boolean 值作为参数：`
* `Boolean 对象将覆盖 Object 对象的 ValueOf() 方法，返回原始值，即 true 和 false。ToString() 方法也会被覆盖，返回字符串 "true" 或 "false"。`
* `遗憾的是，在 ECMAScript 中很少使用 Boolean 对象，即使使用，也不易理解。`
* `平时值类型的布尔类型的实际`
```javascript
var val = true;
console.log(val.toString());
```
`val 明明是值类型 为何还能够调用方法呢？ 类似于引用类型`
```javascript
// 实际做法 做了包装 在不调用方法的时候就是值类型 将要调用方法的时候将其转换为引用类型 
// 然后调用结束后 再转换会值类型  有一个包装的过程
var val = new Boolean(true);
console.log(val.toString());
```
#####  :star2: [Number 对象](#top) <b id="number"></b> 
`正如你可能想到的，Number 对象是 Number 原始类型的引用类型。要创建 Number 对象，采用下列代码：`
```javascript

var oNumberObject = new Number(68);

//要得到数字对象的 Number 原始值，只需要使用 valueOf() 方法

var iNumber = oNumberObject.valueOf();
```
* `toFixed() `:`方法返回的是具有指定位数小数的数字的字符串表示。`
* `toExponential() 方法`:`与格式化数字相关的另一个方法是 toExponential()，它返回的是用科学计数法表示的数字的字符串形式。`
* `toPrecision() 方法`:`toPrecision() 方法根据最有意义的形式来返回数字的预定形式或指数形式。它有一个参数，即用于表示数的数字总数（不包括指数）。例如，`
```javascript
var oNumberObject = new Number(68);
alert(oNumberObject.toFixed(2));  //输出 "68.00"
alert(oNumberObject.toExponential(1));  //输出 "6.8e+1"

alert(oNumberObject.toPrecision(1));  //输出 "7e+1"
alert(oNumberObject.toPrecision(2));  //输出 "68"
alert(oNumberObject.toPrecision(3));  //输出 "68.0"
```
#####  :star2: [String 对象](#top) <b id="string"></b> 
[`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) `官方文档解释方法属性`
`String 是一个基本包装类型,它是唯一的,一旦创建不能改变,每次改变实际上都是创建一个新的字符串`
* `String的属性`
  * `String.prototype`:`对该对象的对象原型的引用`
  * `String.length`:`字符串长度`
* `方法`
```javascript
String.fromCodePoint()
String.prototype.anchor()
String.prototype.big()
String.prototype.small()
String.prototype.fontsize()
String.prototype.fontcolor()
String.prototype.fixed()
/***************************************/
var myString = 'Table of Contents';

document.body.innerHTML = myString.anchor('contents_anchor');

var worldString = 'Hello, world';

console.log(worldString.small());     // <small>Hello, world</small>
console.log(worldString.big());       // <big>Hello, world</big>
console.log(worldString.fontsize(7)); // <fontsize=7>Hello, world</fontsize>

var worldString = 'Hello, world';

console.log(worldString.fontcolor('red') +  ' is red in this line');
// '<font color="red">Hello, world</font> is red in this line'

console.log(worldString.fontcolor('FF00') + ' is red in hexadecimal in this line');
// '<font color="FF00">Hello, world</font> is red in hexadecimal in this line'

var worldString = 'Hello, world';
console.log(worldString.fixed()); // "<tt>Hello, world</tt>"

/***************************************/
String.prototype.charAt()
String.prototype.charCodeAt()
String.prototype.codePointAt()
String.prototype.concat()
String.prototype.endsWith()
String.prototype.includes()
String.prototype.indexOf()
String.prototype.italics()
String.prototype.lastIndexOf()
String.prototype.link()
String.prototype.localeCompare()
String.prototype.match()
String.prototype.normalize()
//String.prototype.padEnd()
//String.prototype.padStart()

/*********************************************/
const str1 = 'Breaded Mushrooms';

console.log(str1.padEnd(25, '.'));
// expected output: "Breaded Mushrooms........"

const str2 = '200';

console.log(str2.padEnd(5));
// expected output: "200  "

/**********************************************/

String.prototype.quote()
String.prototype.repeat()
String.prototype.replace()
String.prototype.search()
String.prototype.slice()
String.prototype.split()
String.prototype.startsWith()
//String.prototype.strike()
//String.prototype.blink()
//String.prototype.bold()
/*********************************************/
var worldString = 'Hello, world'; 

console.log(worldString.blink()); // <blink>Hello, world</blink> 
console.log(worldString.bold()); // <b>Hello, world</b> 
console.log(worldString.italics()); // <i>Hello, world</i> 
console.log(worldString.strike()); // <strike>Hello, world</strike>
/*********************************************/
String.prototype.sub()
String.prototype.substr()
String.prototype.substring()
String.prototype.sup()
String.prototype.toLocaleLowerCase()
String.prototype.toLocaleUpperCase()
String.prototype.toLowerCase()
String.prototype.toSource() //非标准 请勿使用
String.prototype.toString()
String.prototype.toUpperCase()
String.prototype.trim()
String.prototype.trimEnd()
String.prototype.trimStart()
String.prototype.valueOf()
String.prototype[@@iterator]()
String.raw()
```
##### [Array 对象](#top) <b id="array"></b>  :maple_leaf:
`Array 对象,是一种不区分类型的数组，他可以存储任意类型的数组 在一个数组中 十分变态`

##### 创建数组 
* `使用构造函数`
```node
let ary = new Array(7);  //7位数组

let ary1 = new Array("a","b","c","d","e","f");// ["a","b","c","d","e","f"] 

let ary2 = new Array();//空数组
```
* `使用 操作符` `[]`
```node
let opo = [];

let pop1 = [1,2,3,4,"sd",{id:1,age:15},true];
```
##### 数组的属性
* `length`：`表示数组的长度 可以修改 一旦修改数组变长 也可以变短 变长后未赋值的值为 undefined`
##### 数组的检测
* `两种检测方式`
```node
if(pop1 instanceof Array){
    console.log('pop1 是否为数组:', true);
}

if(Array.isArray(pop1)){
    console.log('pop1 是否为数组:', true);
}
```
##### 数组转字符
```node
let pop2 = [1,2,3,4,"sd",true];
console.log('pop2:', pop2.toString()); // pop1: 1,2,3,4,sd,true
console.log('pop2:', pop2.join('-'));  // pop2: 1-2-3-4-sd-true
```
##### 栈与队列方法
* `push()`:`可以接受任意数量的参数,把他们逐个添加到数组末尾`
* `pop()`:`从数组末尾移出最后一项并且返回 减少length的值`
* `shift()`:`移出队列的第一项并且返回 length 减一`
* `unshift()`:`在数组前端添加任意多个值`


##### 排序方法
* `sort([?function(value,value1){return 0|1|-1;}])`:`排序方法 可以传入一个函数 排序,返回排序后的数组`
* `reverse()`:`数组反转排序 返回排序后的数组` 

##### 操作方法
* `concat()`:`数组合并 可以传入任意多个数组 或者 元素`
```node
var colors = ["grey","green","red"];

var array = [1,2,3,4,5,6,7,8,9];

let ary_new = colors.concat(array,"asd","123");

console.log('tag', ary_new); 
//tag [ 'grey', 'green', 'red', 1, 2, 3, 4, 5, 6, 7, 8, 9, 'asd', '123' ]

```
* `slice(start,end? = array.length)`:`切片操作`
* `splice(delete_start:int,delete_length:int,...new_add_value)`：`从什么地方删除多少个元素 然后将后面的元素添加到删除索引处 返回一个数组 表示删除的元素` 
```node
var array = [1,2,3,4,5,6,7,8,9];
let gg = array.splice(2,3,456,879);

console.log('gg:', gg);
console.log('array:', array);
/*
gg: [ 3, 4, 5 ]
array: [ 1, 2, 456, 879, 6, 7, 8, 9 ]
*/
```
* `indexOf(value)`:`要查找项的索引位置 顺序位置`
* `lastIndexOf(value)`:`要查找项的索引位置 倒叙位置 从后往前找`
##### 迭代方法
* `[返回 Boolean] every`:`对数组中的每一项运行给定函数,如果该函数对每一项都返回true 则返回true`
* `[返回 Array]   filter`:`对数组中的每一项运行给定函数，返回该函数会返回true的项组成的数组`
* `[返回 void]    forEach`:`对数组中的每一项运行给定函数,这个方法没有返回值`
* `[返回 Array]   map`:`对数组中的每一项运行给定函数 返回每次函数调用的结果组成的数组`
* `[返回 Boolean] some`:`对数组中的每一项运行给定函数,如果函数对任一项返回true 则返回`
* `传入的函数方法`:`function(currentValue, index,arr){} 类型 当前值 索引  数组`
##### 归并方法
* `reduce(function(prev,current,index,array))`:`都会迭代数组的所有项,然后构建一个最终的返回值 前一个值 当前值 索引 迭代的数组`
```node
var sum = values.reduce(function(prev,cur,index,array){
    console.log(prev);
    console.log(cur);
    console.log(index);
    console.log(array);
    return prev + cur;
})
//sum = 21
```
* `reduceRight`:`从后向前遍历 和reduce 方向相反`
```node
var sum = values.reduceRight(function(prev,cur,index,array){
    console.log(prev);
    console.log(cur);
    console.log(index);
    console.log(array);
    return prev + cur;
})
//sum = 21
```
##### [Date 对象](#top) <b id="date"></b>  :maple_leaf:
[`构造方法`](#top)
* `Date 对象实例表示单个时间点。我们使用下面的代码初始化 Date 对象`:`new Date()`
* `在内部，日期用 1970年1月1日（UTC）以来的毫秒数表示。这个日期很重要，因为就计算机而言，这就是一切开始的地方。`
* `重要：UNIX 时间戳的原因以秒（seconds）为单位。JavaScript 以毫秒（milliseconds）为单位记录时间。`
* `如果我们有 UNIX 时间戳，我们可以使用实例化 JavaScript Date 对象`
```node
const timestamp = 1530826365
new Date(timestamp * 1000)
```
* `如果我们传递 0 ，我们将得到一个 Date 对象，表示 1970年1月1日（UTC）的时间：`:`new Date(0)`
* `如果我们传递一个字符串而不是一个数字，那么Date对象使用 parse 方法来确定您传递的日期。例如：`
* `你也可以使用 Date.parse：Date.parse 将返回一个时间戳（以毫秒为单位）而不是 Date 对象。`
```node
new Date('2018-07-22')
new Date('2018-07') //July 1st 2018, 00:00:00
new Date('2018') //Jan 1st 2018, 00:00:00
new Date('07/22/2018')
new Date('2018/07/22')
new Date('2018/7/22')
new Date('July 22, 2018')
new Date('July 22, 2018 07:22:13')
new Date('2018-07-22 07:22:13')
new Date('2018-07-22T07:22:13')
new Date('25 March 2018')
new Date('25 Mar 2018')
new Date('25 March, 2018')
new Date('March 25, 2018')
new Date('March 25 2018')
new Date('March 2018') //Mar 1st 2018, 00:00:00
new Date('2018 March') //Mar 1st 2018, 00:00:00
new Date('2018 MARCH') //Mar 1st 2018, 00:00:00
new Date('2018 march') //Mar 1st 2018, 00:00:00


Date.parse('2018-07-22')
Date.parse('2018-07') //July 1st 2018, 00:00:00
Date.parse('2018') //Jan 1st 2018, 00:00:00
Date.parse('07/22/2018')
Date.parse('2018/07/22')
Date.parse('2018/7/22')
Date.parse('July 22, 2018')
Date.parse('July 22, 2018 07:22:13')
Date.parse('2018-07-22 07:22:13')
Date.parse('2018-07-22T07:22:13')
```
* `您还可以传递一组代表日期各部分的有序值：年，月（从0开始），日，小时，分钟，秒和毫秒：`
* `最小值应该是 3 个参数，但是大多数 JavaScript 引擎都能解析 2 个或 1 个参数：`
```node
new Date(2018, 6, 22, 7, 22, 13, 0)
new Date(2018, 6, 22)
```
##### 构造总结
* 不传参数，创建一个表示“现在”的Date对象
* 传递 number ，表示从格林威治标准时间1970年1月1日00:00开始的毫秒数
* 传递一个字符串，代表一个日期
* 传递一组参数，它们代表日期的不同部分

##### 时区
* `初始化日期时，您可以传递时区，因此日期不会被假定为 UTC ，然后转换为您当地的时区。`
* `您可以通过以 +HOURS 格式添加时区来指定时区，或者通过添加括在括号中的时区名称来指定时区：`
```node
new Date('July 22, 2018 07:22:13 +0700')
new Date('July 22, 2018 07:22:13 (CET)')
```
##### [日期转换和格式设置](#top)
```node
const date = new Date('July 22, 2018 07:22:13')
 
date.toString() // "Sun Jul 22 2018 07:22:13 GMT+0200 (Central European Summer Time)"
date.toTimeString() //"07:22:13 GMT+0200 (Central European Summer Time)"
date.toUTCString() //"Sun, 22 Jul 2018 05:22:13 GMT"
date.toDateString() //"Sun Jul 22 2018"
date.toISOString() //"2018-07-22T05:22:13.000Z" (ISO 8601 format)
date.toLocaleString() //"22/07/2018, 07:22:13"
date.toLocaleTimeString()    //"07:22:13"
date.getTime() //1532236933000
date.getTime() //1532236933000
```
##### [Date 对象的 getter 方法](#top)
```node
const date = new Date('July 22, 2018 07:22:13')
 
date.getDate() //22
date.getDay() //0 (0 means sunday, 1 means monday..)
date.getFullYear() //2018
date.getMonth() //6 (starts from 0)
date.getHours() //7
date.getMinutes() //22
date.getSeconds() //13
date.getMilliseconds() //0 (not specified)
date.getTime() //1532236933000
date.getTimezoneOffset() //-120 （将取决于您的位置和检查时间 - 这是夏季的CET）。 返回以分钟为单位表示的时区差异

date.getUTCDate() //22
date.getUTCDay() //0 (0 means sunday, 1 means monday..)
date.getUTCFullYear() //2018
date.getUTCMonth() //6 (starts from 0)
date.getUTCHours() //5 (not 7 like above)
date.getUTCMinutes() //22
date.getUTCSeconds() //13
date.getUTCMilliseconds() //0 (not specified)
```
##### [编辑日期](#top)
`Date对象提供了几种编辑日期值的方法：`
```node
const date = new Date('July 22, 2018 07:22:13')
 
date.setDate(newValue)
date.setDay(newValue)
date.setFullYear(newValue) //note: avoid setYear(), it's deprecated
date.setMonth(newValue)
date.setHours(newValue)
date.setMinutes(newValue)
date.setSeconds(newValue)
date.setMilliseconds(newValue)
date.setTime(newValue)
date.setTimezoneOffset(newValue)
```
* `也有一个相对应的 UTC set方法`
```node
const date = new Date('July 22, 2018 07:22:13')
 
date.setUTCDate(newalue)
date.setUTCDay(newValue)
date.setUTCFullYear(newValue)
date.setUTCMonth(newValue)
date.setUTCHours(newValue)
date.setUTCMinutes(newValue)
date.setUTCSeconds(newValue)
date.setUTCMilliseconds(newValue)
```
##### [`获取当前时间戳`](#top)

```node
Date.now()
new Date().getTime()
```

##### [`比较两个日期`](#top)
```node
const date1 = new Date('July 10, 2018 07:22:13')
const date2 = new Date('July 22, 2018 07:22:13')
const diff = date2.getTime() - date1.getTime() //difference in milliseconds

const date1 = new Date('July 10, 2018 07:22:13')
const date2 = new Date('July 10, 2018 07:22:13')
if (date2.getTime() === date1.getTime()) {
  //dates are equal
}
```
`请记住， getTime() 返回的毫秒数，因此您需要在比较中考虑时间因素。July 10, 2018 07:22:13 不等于 July 10, 2018 。在这种情况下，您可以使用 setHours(0, 0, 0, 0) 重置时间。`

##### [Function 对象](#top) <b id="function"></b>  :maple_leaf:
`函数本质是一个对象`

##### 声明函数--[`函数声明语法定义`](#top)
```node
 function sum(num1,num2){
    return num1 +num2;
 }
 // 另一种语法 函数表达式声明语法
 var sum = function(num1,num2){
    return num1 +num2;
 }
```
##### 声明函数--[`Function 构造函数`](#top)
> `前面声明参数 最后一个参数为方法体` `不推荐这样方法定义函数,因为这会导致解析两次代码 ` `1. 解析常规代码 2.解析字符串构造函数`

```node
var sum = new Function("num1","num2","return num1 + num2")
```

> `函数名仅仅是指向函数的指针,因此函数名与包含函数指针的其他变量没有什么不同,也就是说 一个函数可以有很多个函数名` <br/>
> `Javascript 函数没有重载 ` <br/>
> `Javascript 函数会率先读取函数声明并使其在执行任何代码之前可用【函数声明提升】，至于函数表达式必须等到解析器执行到它所在的代码行 才能真正被解析执行` <br/>
> `函数可以作为值传递给另一个函数`

##### 函数内部属性
> `arguments`:`类数组对象，包含着传入函数中的所有参数,保存函数参数,arguments还有一个名叫callee的属性 该属性是一个指针指向拥有arguments对象的函数
可以用来做阶乘`
> `caller 属性`：`显示当前函数在被那个函数调用`
> `length 属性`：`函数接受的函数个数`
> `prototype`:`父类指向`
> `this`:`对于ES5 普通函数 this执行函数运行时所在环境`
```node
function factorial(end){
    if(end <= 1){
        return 1;
    }eles{
        return end * arguments.callee(end - 1);
    }
}

//如果不用 callee 属性 当factorial 被赋予另一个函数的时候就会错误 factorial只是一个函数的引用  不是函数本身
function factorial(end){
    if(end <= 1){
        return 1;
    }eles{
        return end * factorial(end -1);
    }
}

var fac = factorial;

factorial = function(){
   return 0;
}

fac(5) //结果出错

```

##### apply / call 方法  手动指定this 
`两者的区别就在于，两者之间的参数。`
* `apply`:`参数为数组`
```node
var obj = {};
 
function foo(a, b, c) {
  console.log(b);
}
 
foo.apply(obj, [1, 2, 3])   打印结果： 2;
```
* `call`:`参数为一个一个传递`
```node
var obj = {};
 
function foo(a, b, c) {
  console.log(b);
}
 
foo.call(obj, 1, 2, 3)   //打印结果： 2;
```
##### [Global 对象](#top) <b id="global"></b>  :maple_leaf:
* `JavaScript 中有一个特殊的对象，称为全局对象（Global Object），它及其所有属性都可以在程序的任何地方访问，即全局变量。`
* `全局对象只是一个对象，而不是类。既没有构造函数，也无法用new实例化一个新的全局对象。`
* `实际上，ECMAScript 标准没有规定全局对象的类型，而在客户端 JavaScript 中，全局对象就是 Window 对象，表示允许 JavaScript 代码的 Web 浏览器窗口。浏览器把全局对象作为window对象的一部分实现了，因此，所有的全局属性和函数都是window对象的属性和方法。 `

> `中谈到，global对象可以说是ECMAScript中最特别的一个对象了，因为不管你从什么角度上看，这个对象都是不存在的。从某种意义上讲，它是一个终极的“兜底儿对象”，换句话说呢，就是不属于任何其他对象的属性和方法，最终都是它的属性和方法。我理解为，这个global对象呢，就是整个JS的“老祖宗”，找不到归属的那些“子子孙孙”都可以到它这里来认祖归宗。所有在全局作用域中定义的属性和函数，都是global对象的属性和方法，比如isNaN()、parseInt()以及parseFloat()等，实际都是它的方法；还有就是常见的一些特殊值，如：NaN、undefined等都是它的属性，以及一些构造函数Object、Array等也都是它的方法。总之，记住一点：global对象就是“老祖宗”，所有找不到归属的就都是它的。`

##### [拥有的方法](#top)
* `encodeURI`:`对整个URI 编码 编码后其他字符都原封不动 空格被替换为%20`
* `encodeURIComponent`:`使用对应的编码替换所有非字母数字字符 例如中文`
* `decodeURI`:`解码URI`
* `decodeURIComponent`:`解码`
* `eval方法 解析器`
