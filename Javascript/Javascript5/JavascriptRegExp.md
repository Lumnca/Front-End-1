<a id="top"  href="#top">:arrow_lower_left: JavaScript5 正则表达式 vscode :maple_leaf:</a>
----
`Javascript 正则表达式的使用,正则表达式具体请 到此处学习` [`菜鸟正则表达式`](http://www.runoob.com/regexp/regexp-tutorial.html) 
[`RegExp官方文档`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)

- [x] <a href="#createregexp">`创建RegExp 对象`</a>
- [x] <a href="#rugularprefix">`正则表达式修饰符`</a>
- [x] <a href="#newfucntion">`新增的属性/ 方法`</a>

##### :whale2:  [创建RegExp 对象](#top) <b id="createregexp"></b>
`在 ES5 中，RegExp构造函数的参数有两种情况。`
* 第一种情况是，参数是字符串，这时第二个参数表示正则表达式的修饰符（flag）。
```javascript
  var regex = new RegExp('xyz', 'i');
  // 等价于
  var regex = /xyz/i;
```
* 第二种情况是，参数是一个正则表示式，这时会返回一个原有正则表达式的拷贝。
```javascript
  var regex = new RegExp(/xyz/i); //修饰符跟在后面此时不允许使用第二个参数
  // 等价于
  var regex = /xyz/i;
```
ES6 改变了这种行为。如果RegExp构造函数第一个参数是一个正则对象，那么可以使用第二个参数指定修饰符。而且，返回的正则表达式会忽略原有的正则表达式的修饰符，只使用新指定的修饰符。
```javascript
let reg=new RegExp(/abc/ig, 'i');
console.log(reg.flags);// 返回正则对象的修饰符
// "i" 
// 原有正则对象的修饰符是ig，它会被第二个参数i覆盖。
```
`正则表达式创建RegExp`

```javascript
var expression = /at/gi
let val ="atsdsdsd atasd";

console.log(val.replace(expression,"**"));
//输出: **sdsdsd **asd
```

##### :whale2:[字符串修饰符](#top)</a> <b id="rugularprefix"></b>
* `RegExp 对象创建有三种模式 igm` <br/>  
   * `i`:`表示不区分大小写`
   * `g`:`加上以后不会再匹配到一个后就停止匹配,继续向后面匹配,默认匹配到第一个就停止匹配`
   * `m`:`表示多行模式`
* `Es6 里面添加新的模式 u y`<br/>
   * `u`:`修饰符标识能够正确处理大于\uFFFF的Unicode字符。 ES6 引入了代理对 32位表示一个字符 例如在ES5中 .表示任意一个字符串 对于一个32位代理对字符他就无法匹配 就必须添加u这个修饰符` [`理解`](http://www.softwhy.com/article-9165-1.html) 
   ```node
    let val1 =  /a{2}/.test('aa');  /* true*/

    let val2 = /a{2}/u.test('aa'); /* true */

    let val3 = /𠮷{2}/.test('𠮷𠮷'); /* false*/

    let val4 = /𠮷{2}/u.test('𠮷𠮷'); /* true*/

    console.log(val1,val2,val3,val4);
   ```
   * `y`:`lastIndex初始值为0。规定正则表达式必须从lastIndex规定的位置开始进行匹配。` [y](http://es6.ruanyifeng.com/#docs/regex#y-%E4%BF%AE%E9%A5%B0%E7%AC%A6)
  *  `s`:`s 修饰符：dotAll 模式 . 匹配符匹配任意单字符,但是不能匹配 \n 如果想让他匹配 \n 那么只需要加上s 修饰符` 
  ```javascript
    /foo.bar/.test('foo\nbar')
    // false
    /foo[^]bar/.test('foo\nbar')
    // true
    /foo.bar/s.test('foo\nbar') // true
    const re = /foo.bar/s;
    // 另一种写法
    // const re = new RegExp('foo.bar', 's');

    re.test('foo\nbar') // true
    re.dotAll // true
    re.flags // 's'
  ```

##### :whale2:[新增的属性](#top)</a> <b id="newfucntion"></b>
* `RegExp.prototype.flags`：`ES6 为正则表达式新增了flags属性，会返回正则表达式的修饰符 字符串`
* `RegExp.prototype.unicodes`:`正则实例对象新增unicode属性，表示是否设置了u修饰符。 Boolean`
* `RegExp.prototype.sticky`:`与y修饰符相匹配，ES6 的正则实例对象多了sticky属性，表示是否设置了y修饰符。Boolean`
* `dotAll `:`是否加上了 s 修饰符 允许匹配\n . `
##### 方法
`String.prototype.matchAll`:`String.prototype.matchAll方法，可以一次性取出所有匹配。不过，它返回的是一个遍历器（Iterator），而不是数组。`
```node
const string = 'test1test2test3';

// g 修饰符加不加都可以
const regex = /t(e)(st(\d?))/g;

for (const match of string.matchAll(regex)) {
  console.log(match);
}
```
`如果不用matchALL方法`
```node
var regex = /t(e)(st(\d?))/g;
var string = 'test1test2test3';

var matches = [];
var match;
while (match = regex.exec(string)) {
  matches.push(match);
}
```

* `字符串对象共有 4 个方法，可以使用正则表达式：match()、replace()、search()和split()。`
* `ES6 将这 4 个方法，在语言内部全部调用RegExp的实例方法，从而做到所有与正则相关的方法，全都定义在RegExp对象上。`
