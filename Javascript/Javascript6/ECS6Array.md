### [ECMASCript6  数组的扩展](#top) :maple_leaf: <b id="top"></b> 

----
`ES6 给数组扩展了新的方法和运算服务`

* [x] :maple_leaf: [`扩展运算符`](#dian)
    * `复制数组` `合并数组`  `Iterator 接口` `展开字符串`
* [x] :maple_leaf: [`Array.from`](#from)
* [x] :maple_leaf: [`Array.of`](#of)
* [x] :maple_leaf: [`Array.copyWithin`](#copyWithin)
* [x] :maple_leaf: [`find() 和 findIndex()`](#find)
* [x] :maple_leaf: [`数组实例的 fill()`](#fill)
* [x] :maple_leaf: [`数组实例的 entries(),keys() 和 values() `](#kve)
* [x] :maple_leaf: [`数组实例的 includes()`](#includes)
* [x] :maple_leaf: [`数组实例的 flat()，flatMap()`](#flat)
* [x] :maple_leaf: [`数组的空位`](#null)

##### :maple_leaf: [扩展运算符](#top) <b id="dian"></b>

`点` `...` `展开运算符`
```node
console.log(...[1, 2, 3])
// 1 2 3

console.log(1, ...[2, 3, 4], 5)
// 1 2 3 4 5
[...document.querySelectorAll('div')]
// [<div>, <div>, <div>]

[...[], 1]
// [1]  注意:如果是空数组 那么解析出来是没有 不是 null/undefined
```
`运用`:`将一个数组，变为参数序列。`
```node
function add(x, y) {
  return x + y;
}

const numbers = [4, 38];
add(...numbers) // 42
```
`由于扩展运算符可以展开数组，所以有时候不再需要apply方法，将数组转为函数的参数了。`
```node
// ES5 的写法
Math.max.apply(null, [14, 3, 77])

// ES6 的写法
Math.max(...[14, 3, 77])

// 等同于
Math.max(14, 3, 77);
```
##### 复制数组 
* `ES5 只能用变通方法来复制数组。 深拷贝 不是浅拷贝`
```node
const a1 = [1, 2];
const a2 = a1.concat();

a2[0] = 2;
a1 // [1, 2]
```
* `ES6 可以使用扩展运算符 复制数组`
```node
const a1 = [1, 2];
// 写法一
const a2 = [...a1];
// 写法二     有点奇怪的写法 解构
const [...a2] = a1;

//解构 数组
let [head, ...tail] = [1, 2, 3, 4];
head // 1
tail // [2, 3, 4]

```
##### 合并数组 
`展开运算符合并数组`
```node
const arr1 = ['a', 'b'];
const arr2 = ['c'];
const arr3 = ['d', 'e'];

// ES5 的合并数组
arr1.concat(arr2, arr3);
// [ 'a', 'b', 'c', 'd', 'e' ]

// ES6 的合并数组
[...arr1, ...arr2, ...arr3]
// [ 'a', 'b', 'c', 'd', 'e' ]
```
##### 展开字符串
```node
[...'hello']
// [ "h", "e", "l", "l", "o" ]
```
##### Iterator 接口 
* `任何 Iterator 接口的对象（参阅 Iterator 一章），都可以用扩展运算符转为真正的数组。` 
* `扩展运算符内部调用的是数据结构的 Iterator 接口，因此只要具有 Iterator 接口的对象，都可以使用扩展运算符，比如 Map 结构。`
```node
let map = new Map([
  [1, 'one'],
  [2, 'two'],
  [3, 'three'],
]);

let arr = [...map.keys()]; // [1, 2, 3]
```
* `Generator 函数运行后，返回一个遍历器对象，因此也可以使用扩展运算符。`
```node
const go = function*(){
  yield 1;
  yield 2;
  yield 3;
};

[...go()] // [1, 2, 3]
```
##### :maple_leaf: [Array.from](#top) <b id="from"></b>
`Array.from方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）
的对象（包括 ES6 新增的数据结构 Set 和 Map）。`
* `Array.from将它转为真正的数组`
```node
let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
};

// ES5的写法
var arr1 = [].slice.call(arrayLike); // ['a', 'b', 'c']

// ES6的写法
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']

Array.from('hello')
// ['h', 'e', 'l', 'l', 'o']

let namesSet = new Set(['a', 'b'])
Array.from(namesSet) // ['a', 'b']
```
* [`如果参数是一个真正的数组，Array.from会返回一个一模一样的新数组。`](#top)
```node
Array.from([1, 2, 3])
// [1, 2, 3]
```
* [`Array.from还可以接受第二个参数，作用类似于数组的map方法，用来对每个元素进行处理，将处理后的值放入返回的数组。`](#top)
```node
Array.from(arrayLike, x => x * x);
// 等同于
Array.from(arrayLike).map(x => x * x);

Array.from([1, 2, 3], (x) => x * x)
// [1, 4, 9]

Array.from([1, , 2, , 3], (n) => n || 0)
// [1, 0, 2, 0, 3]
```
* `内容`
```node
Array.from({ length: 2 }, () => 'jack')
// ['jack', 'jack']
```
##### :maple_leaf: [Array.of](#top) <b id="of"></b>
`Array.of方法用于将一组值，转换为数组。`
```node
Array.of(3, 11, 8) // [3,11,8]
Array.of(3) // [3]
Array.of(3).length // 1
```
##### :maple_leaf: [实例方法:copyWithin](#top) <b id="copyWithin"></b>
`Array.prototype.copyWithin(target, start = 0, end = this.length)`
* `target（必需）：从该位置开始替换数据。如果为负值，表示倒数。`
* `start（可选）：从该位置开始读取数据，默认为 0。如果为负值，表示倒数。`
* `end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数。`
```node
// 将3号位复制到0号位
[1, 2, 3, 4, 5].copyWithin(0, 3, 4)
// [4, 2, 3, 4, 5]
```
##### :maple_leaf: [find() 和 findIndex()](#top) <b id="find"></b>
`数组实例的find方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出
第一个返回值为true的成员，然后返回该成员。如果没有符合条件的成员，则返回undefined。`

```node
[1, 4, -5, 10].find((n) => n < 0)
// -5

[NaN].findIndex(y => Object.is(NaN, y))
// 0
```
##### :maple_leaf: [数组实例的 fill()](#top) <b id="fill"></b>
`数组填充方法`
```node
['a', 'b', 'c'].fill(7)
// [7, 7, 7]

new Array(3).fill(7)
// [7, 7, 7]
```
* [`fill方法还可以接受第二个和第三个参数，用于指定填充的起始位置和结束位置。`](#top)
```node
['a', 'b', 'c'].fill(7, 1, 2)
// ['a', 7, 'c']

let arr = new Array(3).fill({name: "Mike"});
arr[0].name = "Ben";
```
##### :maple_leaf: [数组实例的 entries(),keys() 和 values()](#top) <b id="kve"></b>
* `ES6 提供三个新的方法——entries()，keys()和values()——用于遍历数组`
```node
for (let index of ['a', 'b'].keys()) {
  console.log(index);
}
// 0
// 1

for (let elem of ['a', 'b'].values()) {
  console.log(elem);
}
// 'a'
// 'b'

for (let [index, elem] of ['a', 'b'].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"
```
##### :maple_leaf: [数组实例的 includes()](#top) <b id="includes"></b>
`Array.prototype.includes方法返回一个布尔值，表示某个数组是否包含给定的值，与字符串的includes方法类似。ES2016 引入了该方法。`
```node
[1, 2, 3].includes(2)      // true
[1, 2, 3].includes(4)      // false
[1, 2, NaN].includes(NaN)  // true

[NaN].indexOf(NaN)
// -1
//includes使用的是不一样的判断算法，就没有这个问题。
[NaN].includes(NaN)
// true
```
##### :maple_leaf: [数组实例的 flat()，flatMap()](#top) <b id="flat"></b>
* `数组的成员有时还是数组，Array.prototype.flat()用于将嵌套的数组“拉平”，变成一维的数组。该方法返回一个新数组，对原数据没有影响。`
```node
[1, 2, [3, 4]].flat()
// [1, 2, 3, 4]
```
* `flat()默认只会“拉平”一层，如果想要“拉平”多层的嵌套数组，可以将flat()方法的参数写成一个整数，表示想要拉平的层数，默认为1。`
```node
[1, 2, [3, [4, 5]]].flat()
// [1, 2, 3, [4, 5]]

[1, 2, [3, [4, 5]]].flat(2)
// [1, 2, 3, 4, 5]
```
* `flatMap()方法对原数组的每个成员执行一个函数（相当于执行Array.prototype.map()），然后对返回值组成的数组执行flat
()方法。该方法返回一个新数组，不改变原数组。`
```node
// 相当于 [[2, 4], [3, 6], [4, 8]].flat()
[2, 3, 4].flatMap((x) => [x, x * 2])
// [2, 4, 3, 6, 4, 8]
```
##### :maple_leaf: [数组的空位](#top) <b id="null"></b>
`Array(3) // [, , ,]`   `Array(3)返回一个具有 3 个空位的数组。注意，空位不是undefined，一个位置的值等于undefined，依然是有值的。
空位是没有任何值`
```node
0 in [undefined, undefined, undefined] // true
0 in [, , ,] // false
```
* `ES5 对空位的处理，已经很不一致了，大多数情况下会忽略空位。`
* `Array.from方法会将数组的空位，转为undefined`
* `copyWithin()会连空位一起拷贝。`
* `fill()会将空位视为正常的数组位置。`:`new Array(3).fill('a') // ["a","a","a"]`
```node
[...['a',,'b']]
// [ "a", undefined, "b" ]
```
* `entries()、keys()、values()、find()和findIndex()会将空位处理成undefined。`
