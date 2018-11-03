<a id="top"  href="#top">:arrow_lower_left: JavaScript5 正则表达式 vscode :maple_leaf:</a>
----
`Javascript 正则表达式的使用,正则表达式具体请 到此处学习` [`菜鸟正则表达式`](http://www.runoob.com/regexp/regexp-tutorial.html) 
[`RegExp官方文档`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)

- [x] <a href="#createregexp">`创建RegExp 对象 注意模式`</a>
- [x] <a href="#rugularprefix">`正则表达式修饰符`</a>
- [x] <a href="#UseBabel">`使用babel`</a>

##### :whale2:  [创建RegExp 对象 注意模式](#top) <b id="createregexp"></b>
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

##### :whale2:[字符串修饰符]()</a> <b id="rugularprefix"></b>
* `RegExp 对象创建有三种模式 igm` <br/>  
   * `i`:`表示不区分大小写`
   * `g`:`加上以后不会再匹配到一个后就停止匹配,继续向后面匹配,默认匹配到第一个就停止匹配`
   * `m`:`表示多行模式`
* `Es6 里面添加新的模式 u y`<br/>
   * `u`:`修饰符标识能够正确处理大于\uFFFF的Unicode字符。 ES6 引入了代理对 32位表示一个字符 例如在ES5中 .表示任意一个字符串 对于一个32位代理对字符他就无法匹配 就必须添加u这个修饰符` 
   * `y`:`lastIndex初始值为0。规定正则表达式必须从lastIndex规定的位置开始进行匹配。`[`理解`](http://www.softwhy.com/article-9165-1.html) 

`正则表达式创建RegExp`
```javascript
var expression = /at/gi
let val ="atsdsdsd atasd";

console.log(val.replace(expression,"**"));
//输出: **sdsdsd **asd
```

