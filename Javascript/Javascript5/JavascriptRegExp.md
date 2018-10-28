<a id="top"  href="#top">:arrow_lower_left: JavaScript5 正则表达式 vscode :maple_leaf:</a>
----
`Javascript 正则表达式的使用,正则表达式具体请 到此处学习` [`菜鸟正则表达式`](http://www.runoob.com/regexp/regexp-tutorial.html) 
[`RegExp官方文档`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)

- [x] <a href="#CreateObject">`创建RegExp 对象 注意模式`</a>
- [x] <a href="#BabelrcFile">`配置.Babelrc文件`</a>
- [x] <a href="#UseBabel">`使用babel`</a>


##### <a id="CreateObject" href="#CreateObject"> :whale2: 块级作用域绑定</a> <a href="#top">:arrow_up: </a>
* `RegExp 对象创建有三种模式 igm` <br/>  
   * `i`:`表示不区分大小写`
   * `g`:`加上以后不会再匹配到一个后就停止匹配,继续向后面匹配,默认匹配到第一个就停止匹配`
   * `m`:`表示多行模式`
* `Es6 里面添加新的模式`<br/>
   * `u`:`修饰符标识能够正确处理大于\uFFFF的Unicode字符。 ES6 引入了代理对 32位表示一个字符` [`理解`](http://www.softwhy.com/article-9165-1.html) 
   * `y`:`lastIndex初始值为0。规定正则表达式必须从lastIndex规定的位置开始进行匹配。`

`正则表达式创建RegExp`
```javascript
var expression = /at/gi
let val ="atsdsdsd atasd";

console.log(val.replace(expression,"**"));
//输出: **sdsdsd **asd
```
``
