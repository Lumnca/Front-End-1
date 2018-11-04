### [:arrow_lower_left: ECS6 变量的解构赋值 :maple_leaf:](#top)
`ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。然而有点逆天 这个语法,简单的还是可以用一下`

- [x] :maple_leaf: [`数组的解构赋值`](#arraygetvalue) 
- [x] :maple_leaf: [`默认值`](#defaultvalue) 
- [x] :maple_leaf: [`对象的解构赋值`](#objectresolve)
- [x] :maple_leaf: [`字符串的解构赋值`](#stringresolve)
- [x] :maple_leaf: [`数值和布尔值的解构赋值`](#numberbooleanresolve)
- [x] :maple_leaf: [`函数参数的解构赋值`](#functionresolve)

##### [数组的解构赋值](#top) <b id="arraygetvalue"></b>
`基本的赋值结构是定义变量然后再逐个赋值例如：`
```node
int a = 10;
int b = 18;
int c = 8;
```
`ES6 允许写成下面这样。` **`最常见的用法`**
```node
 int [a,b,c] = [10,18,8];
```
`本质上，这种写法属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值` **`装逼的用法`**
```node
let [foo, [[bar], baz]] = [1, [[2], 3]];
foo // 1 bar // 2 baz // 3

let [head, ...tail] = [1, 2, 3, 4];
head // 1  tail // [2, 3, 4]

let [ , , third] = ["foo", "bar", "baz"];
third // "baz"

let [x, y, ...z] = ['a'];
x // "a"  y // undefined  z // []
```
* `如果解构不成功，变量的值就等于undefined。但是如果[] 解构不成功会变成 []  空数组`
* `有一种情况是不完全解构,不完全解构,那么会有部分值可以获得值但是解构还是可以成功`
###### [不完全解构](#top)
```node
let [x, y] = [1, 2, 3];
x // 1 y // 2

let [a, [b], d] = [1, [2, 3], 4];
a // 1 b // 2 d // 4
```
`如果等号的右边不是数组（或者严格地说，不是可遍历的结构，Iterator那么将会报错。`
```node
function* fibs() {
  let a = 0;
  let b = 1;
  while (true) {
    yield a;
    [a, b] = [b, a + b];
  }
}

let [first, second, third, fourth, fifth, sixth] = fibs();
```
##### [默认值](#top) <b id="defaultvalue"></b>
* `如果右边没有你需要的值,或者右边的值为 undefined `
* `ES6 内部使用严格相等运算符（===），判断一个位置是否有值。所以，只有当一个数组成员严格等于undefined，默认值才会生效。`
```node
let [foo = true] = [];
foo // true

let [x, y = 'b'] = ['a']; // x='a', y='b'
let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'
```
`如果默认值是一个表达式，那么这个表达式是惰性求值的，即只有在用到的时候，才会求值。`
```node
function f() {
  console.log('aaa');
}
let [x = f()] = [1];
```
##### [对象的解构赋值](#top) <b id="objectresolve"></b>
* `解构不仅可以用于数组，还可以用于对象。`
* `对象的解构与数组有一个重要的不同。数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值`
```node
let { bar, foo } = { foo: "aaa", bar: "bbb" };
foo // "aaa"
bar // "bbb"

let { baz } = { foo: "aaa", bar: "bbb" };
baz // undefined
```
**`如果吧一个对象的 name 属性赋值给一个变量 而这个变量又不是name名称该怎么办呢？ 例如这个变量 叫 Code`**
```
let {name:Code} = { name:"jxkivker",age:17,sex:true };
```
* `如果解构失败，变量的值等于undefined。` <br/>
**赋值关系如下 那么复杂,你还是不要用这个了 **
```javascript
let obj = {
  p: [
    'Hello',
    { y: 'World' }
  ]
};

let { p, p: [x, { y }] } = obj;
x // "Hello"
y // "World"
p // ["Hello", {y: "World"}]
```

##### [字符串的解构赋值](#top) <b id="stringresolve"></b>
* `类似数组的对象都有一个length属性，因此还可以对这个属性解构赋值。`
```javascript
const [a, b, c, d, e] = 'hello';
// a "h"
// b "e"
// c "l"
// d "l"
// e "o"
```
* `类似数组的对象都有一个length属性，因此还可以对这个属性解构赋值。`
```node
let {length : len} = 'hello';
len // 5
```
##### [数值和布尔值的解构赋值](#top) <b id="numberbooleanresolve"></b>
`数值和布尔值本质上还是对象 ,按照对象解构赋值就行`
- [x] :maple_leaf: [``](#)
```javascript
let {toString: s} = 123;
s === Number.prototype.toString // true

let {toString: s} = true;
s === Boolean.prototype.toString // true
```
##### [函数参数的解构赋值](#top) <b id="functionresolve"></b>
```node
function add([x, y]){
  return x + y;
}

add([1, 2]); // 3

[[1, 2], [3, 4]].map(([a, b]) => a + b);
// [ 3, 7 ]
```
