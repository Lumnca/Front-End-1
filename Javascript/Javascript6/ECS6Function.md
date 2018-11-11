[ECMASCript6  函数扩展](#top) :maple_leaf: <b id="top"></b>
----
`ES增强了函数,提供了默认参数,多参数,箭头函数[lambda 表达式] name属性 双冒号运算符`
 * [x] :maple_leaf: [`函数默认值`](#default)
 * [x] :maple_leaf: [`函数多参数`](#args)
 * [x] :maple_leaf: [`严格模式`](#strict)
 * [x] :maple_leaf: [`name 属性`](#name)
 * [x] :maple_leaf: [`箭头函数`](#arrow)
 * [x] :maple_leaf: [`双冒号运算符`](#aa)
 
 ##### [函数默认值](#top) <b id="default"></b>
  `如果不传递参数或者传递的参数为undefined 那么就会适应默认值,默认值可以是值 可以是对象 可以是表达式`
  `通常情况下，定义了默认值的参数，应该是函数的尾参数 非默认值放在前面 默认值放在后面`
  ```node
  function add(one = 0,two = 0){
    return one + two;
}

console.log(add(12));

/* es5.1 实现 */

function add() {
    var one = arguments.length > 0 && arguments[0] !== undefined ? arguments[0] : 0;
    var two = arguments.length > 1 && arguments[1] !== undefined ? arguments[1] : 0;

    return one + two;
}

console.log(add(12));
```
`利用解构加上表达式`
```node
let number = 15 ;
/* 利用解构  加上表达式 */
function change({name,age,sex} = {name:"jxkicker",age:17,sex:true},count = number + 1,isChange = true  ){
    if(isChange == true){
        return {
            UserName : name,
            UserAge:age,
            UserSex:sex, 
            UserCount:count
        }
    }else{
        return {};
    }
}
const val =  change();
console.log(val.UserName);

function update(obj = {set:"Dan Wa lin Get",count:15,isUpdate:true}){
    console.log(obj);
}
```
`表达式 参数的重名问题`
```node
var x = 1;

function f(x, y = x) {
  console.log(y);
}

f(3) // 3

var g = 1;

function f(t, y = g) {
  console.log(y);
}

f(3) // 1

```
##### [函数的 length 属性](#top)
`指定了默认值以后，函数的length属性，将返回没有指定默认值的参数个数。也就是说，指定了默认值后，length属性将失真。`
```node
(function (a) {}).length // 1
(function (a = 5) {}).length // 0
(function (a, b, c = 5) {}).length // 2
(function(...args) {}).length // 0
```
 ##### [函数多参数](#top) <b id="args"></b>
`ES6 引入 rest 参数（形式为...变量名），用于获取函数的多余参数，这样就不需要使用arguments对象了。rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中。`
```node
function push(array, ...items) {
    items.forEach(function(item) {
        array.push(item);
        console.log(item);
    });
}

var a = [5,6,7];
push(a, 1, 2, 3);
```
##### [严格模式](#top) <b id="strict"></b>
`从 ES5 开始，函数内部可以设定为严格模式。` `ES2016 做了一点修改，规定只要函数参数使用了默认值、解构赋值、或者扩展运算符，那么函数内部就不能显式设定为严格模式，否则会报错。`
```node
function doSomething(value = 70) {
    'use strict';
    return value;
}
```
##### [name 属性](#top) <b id="name"></b>
`函数的name属性，返回该函数的函数名。`
```node
function foo() {}
foo.name // "foo"
```
##### [箭头函数](#top) <b id="arrow"></b>
`ES6 允许使用“箭头”（=>）定义函数。 就是 lambda表达式`
 
```node
/* 无参数 箭头函数*/
var f = v => v;

var insert = name => console.log(name);

var select = val => val.age + 12;

var f = function f(v) {
    return v;
};

var sum = (num1, num2) => { return num1 + num2; }

[1,2,3].map(x => x * x);

/*es5*/
var insert = function insert(name) {
    return console.log(name);
};

var select = function select(val) {
    return val.age + 12;
};

var sum = function sum(num1, num2) {
    return num1 + num2;
};

```
* `箭头函数有几个使用注意点。`
  * `函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。this对象的指向是可变的，但是在箭头函数中，它是固定的。`
  * `不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。`
  * `不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。`
  * `不可以使用yield命令，因此箭头函数不能用作 Generator 函数。`
```node
function foo() {
  setTimeout(() => {
    console.log('id:', this.id);
  }, 100);
}

var id = 21;

foo.call({ id: 42 });
// id: 42
/*
上面代码中，setTimeout的参数是一个箭头函数，这个箭头函数的定义生效是在foo函数生成时，而它的真正执行要等到 100 毫秒后。
如果是普通函数，执行时this应该指向全局对象window，这时应该输出21。但是，箭头函数导致this总是指向函数定义生效时所在的对象
（本例是{id: 42}），所以输出的是42。

箭头函数可以让setTimeout里面的this，绑定定义时所在的作用域，而不是指向运行时所在的作用域
*/

function Timer() {
  this.s1 = 0;
  this.s2 = 0;
  // 箭头函数
  setInterval(() => this.s1++, 1000); //箭头函数 作用域固定 this.s2等于 timer.s1
  // 普通函数
  setInterval(function () {
    this.s2++;  //普通函数 执行的时候是window 环境 所有 this.s2等于 window.s2
  }, 1000);
}

var timer = new Timer();

setTimeout(() => console.log('s1: ', timer.s1), 3100);
setTimeout(() => console.log('s2: ', timer.s2), 3100);
// s1: 3
// s2: 0
```
* `箭头函数可以让this指向固定化，这种特性很有利于封装回调函数。`
```node
var handler = {
  id: '123456',

  init: function() {
    document.addEventListener('click',
      event => this.doSomething(event.type), false);
  },

  doSomething: function(type) {
    console.log('Handling ' + type  + ' for ' + this.id);
  }
};
```
`this指向的固定化，并不是因为箭头函数内部有绑定this的机制，实际原因是箭头函数根本没有自己的this，导致内部的this就是外层代
码块的this。正是因为它没有this，所以也就不能用作构造函数。`

```node
function foo() {
    setTimeout(() => {
    console.log('id:', this.id);
    }, 100);
};

/*
function foo() {
    var _this = this;

    setTimeout(function () {
        console.log('id:', _this.id);
    }, 100);
};
*/
```
##### [小例子](#top)
`请问下面的代码之中有几个this？`
```node
function foo() {
  return () => {
    return () => {
      return () => {
        console.log('id:', this.id);
      };
    };
  };
}

var f = foo.call({id: 1});

var t1 = f.call({id: 2})()(); // id: 1
var t2 = f().call({id: 3})(); // id: 1
var t3 = f()().call({id: 4}); // id: 1
```
`上面代码之中，只有一个this，就是函数foo的this 箭头函数没有自己的this`
##### [箭头函数的问题](#top)
* `由于箭头函数使得this从“动态”变成“静态”，下面两个场合不应该使用箭头函数。`
```node
const cat = {
  lives: 9,
  jumps: () => {
    this.lives--;
  }
}
/*
上面代码中，cat.jumps()方法是一个箭头函数，这是错误的。调用cat.jumps()时，如果是普通函数，该方法内部的this指向cat；
如果写成上面那样的箭头函数，使得this指向全局对象，因此不会得到预期结果。
*/
```
*  `第二个场合是需要动态this的时候，也不应使用箭头函数。`
##### [双冒号运算符](#top)  <b id="aa"></b>
* `箭头函数可以绑定this对象，大大减少了显式绑定this对象的写法（call、apply、bind）。但是，箭头函数并不适用于所有场合，所以现在有一个提案，提出了“函数绑定”（function bind）运算符，用来取代call、apply、bind调用。`
* `函数绑定运算符是并排的两个冒号（::），双冒号左边是一个对象，右边是一个函数。该运算符会自动将左边的对象，作为上下文环境（即this对象），绑定到右边的函数上面。`
```node
foo::bar;
// 等同于
bar.bind(foo);

foo::bar(...arguments);
// 等同于
bar.apply(foo, arguments);

const hasOwnProperty = Object.prototype.hasOwnProperty;
function hasOwn(obj, key) {
  return obj::hasOwnProperty(key);
}
```
