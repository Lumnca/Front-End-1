### [ECMASCript6  数值的扩展](#top) :maple_leaf: <b id="top"></b>
`ES6 对于数值也提供了扩展`
- [x] :maple_leaf: [`二进制和八进制表示法`](#doubleeight) 
- [x] :maple_leaf: [`Number 扩展方法`](#number) 
- [x] :maple_leaf: [`Math 对象的扩展`](#math) 
- [x] :maple_leaf: [`新增运算符`](#yunsuan) 
  
##### :maple_leaf:  [二进制和八进制表示法](#top) <b id="doubleeight"></b>
`ES6 提供了二进制和八进制数值的新的写法，分别用前缀0b（或0B）和0o（或0O）表示。` `是` **`零`** `不是` `欧`
* `二进制`:`Binary`
* `八进制`:`Octal`
* `十六进制`:`Hexadecimal`
```node
0b111110111 === 503 // true
0o767 === 503 // true

Number('0b111')  // 7
Number('0o10')  // 8
```
##### :maple_leaf:  [Number 扩展方法](#top) <b id="number"></b> 
`ES6 在Number对象上，新提供了Number.isFinite()和Number.isNaN()两个方法。`
`ES6 将全局方法parseInt()和parseFloat()，移植到Number对象上面，行为完全保持不变。`
`ES6 在Number对象上面，新增一个极小的常量Number.EPSILON。根据规格`
* `Number.isFinite()用来检查一个数值是否为有限的（finite），即不是Infinity。`
* `Number.isNaN()用来检查一个值是否为NaN。`
* `Number.parseInt() `
* `Number.parseFloat() `
```node
Number.parseInt === parseInt // true
Number.parseFloat === parseFloat // true
```
* :white_check_mark:`Number.isInteger()`：`新增方法 判断一个数是否是整数` 
* :white_check_mark:`Number.EPSILON`：`它表示 1 与大于 1 的最小浮点数之间的差。`
* :white_check_mark:`Number.isSafeInteger()`:`安全整数 JavaScript 能够准确表示的整数范围在-2^53到2^53之间（不含两个端点），超过这个范围，无法精确表示这个值。`
```node
Number.EPSILON === Math.pow(2, -52)
// true
Number.EPSILON
// 2.220446049250313e-16
Number.EPSILON.toFixed(20)
// "0.00000000000000022204"
```
##### :maple_leaf: [Math 对象的扩展](#top) <b id="math"></b>
`Math.trunc() 方法用于去除一个数的小数部分，返回整数部分。`
```node
Math.trunc(4.9) // 4
Math.trunc(-4.1) // -4
```
`Math.sign() 方法用来判断一个数到底是正数、负数、还是零。对于非数值，会先将其转换为数值。`
* `它会返回五种值。`
   * `参数为正数，返回+1;`
   * `参数为负数，返回-1;`
   * `参数为 0，返回0;`
   * `参数为-0，返回-0;`
   * `其他值，返回NaN。`
```node
Math.sign(-5) // -1
Math.sign(5) // +1
Math.sign(0) // +0
Math.sign(-0) // -0
Math.sign(NaN) // NaN
```
`Math.cbrt() 方法用于计算一个数的立方根。`
```node
Math.cbrt(-1) // -1
Math.cbrt(0)  // 0
Math.cbrt(1)  // 1
Math.cbrt(2)  // 1.2599210498948734

Math.cbrt = Math.cbrt || function(x) {
  var y = Math.pow(Math.abs(x), 1/3);
  return x < 0 ? -y : y;
};
```
##### :maple_leaf: [新增运算符](#top) <b id="yunsuan"></b>
`ES2016 新增了一个指数运算符（**）。`
```node
2 ** 2 // 4
2 ** 3 // 8

let b = 4;
b **= 3;
// 等同于 b = b * b * b;
```
