<a id="top" href="#top">:blue_heart: JavaScript 引用类型  :maple_leaf:</a> 
----
:white_check_mark: `引用类型通常叫做类（class），也就是说，遇到引用值，所处理的就是对象`

- [x] :maple_leaf: <a href="#ObjectObject" id="ObjectObject" >`Object 对象`</a>
- [x] :maple_leaf: <a href="#BooleanObject" id="BooleanObject" >`Boolean 对象`</a>
- [x] :maple_leaf: <a href="#NumberObject" id="NumberObject" >`Number 对象`</a>
- [x] :maple_leaf: <a href="#StringObject" id="StringObject" >`String 对象`</a>
- [x] :maple_leaf: <a href="#ArrayObject" id="ArrayObject" >`Array 对象`</a>
- [x] :maple_leaf: <a href="#DateObject" id="DateObject" >`Date 对象`</a>
- [x] :maple_leaf: <a href="#RegExpObject" id="RegExpObject" >`RegExp 对象`</a>
- [x] :maple_leaf: <a href="#FunctionObject" id="FunctionObject" >`Function 对象`</a>
 
####  :star2: <a id="EventStream" href="#EventStream">Object 对象 </a><a href="#top">:whale2:</a>
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
##### [`Object 对象具有下列属性`](#)
* `constructor`:`对创建对象的函数的引用（指针）。对于 Object 对象，该指针指向原始的 Object() 函数。`
* `Prototype`:`对该对象的对象原型的引用。对于所有的对象，它默认返回 Object 对象的一个实例。`
##### [`Object 对象还具有几个方法`](#)
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
- [x] :maple_leaf: <a href="#BooleanObject" id="BooleanObject" >Boolean 对象</a>
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
//实际做法 做了包装 在不调用方法的时候就是值类型 将要调用方法的时候将其转换为引用类型  然后调用结束后 再转换会值类型  有一个包装的过程
var val = new Boolean(true);
console.log(val.toString());
```
####  :star2: <a id="NumberObject" href="#NumberObject">Number 对象 </a><a href="#top">:whale2:</a>
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
####  :star2: <a id="NumberObject" href="#NumberObject">Number 对象 </a><a href="#top">:whale2:</a>
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
