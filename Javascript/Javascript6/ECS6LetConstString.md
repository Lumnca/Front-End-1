### <a id="top"  href="#top">:arrow_lower_left: JavaScript6 块级作用域.字符串.正则:maple_leaf:</a>
`JS6新语法提供了let实现块级作用域,字符串也新增了许多功能,增加了箭头函数,默认参数,不定参数`

- [x] <a href="#letconst">`块级作用域绑定`</a>
- [x] <a href="#stringexpend">`字符串扩展`</a>
- [x] <a href="#regularexpend">`模板字符串`</a>


##### 1. :whale2:  `块级作用域绑定` <a id="letconst" href="#letconst">let,const</a>    <a href="#top">----:arrow_up::arrow_up: </a>
* `块级作用域 是用let 声明变量,可以把变量变成块级`
* let `可以使得变量避免变量提升,不允许重复声明,使得变量成为块级变量,隔绝在块级作用域之间,而不会混淆`
* `未声明访问会报错,而不是underfine输出`
* `其他特性和C,C++，C# Java等等一样`
```javascript
  //使用实例
  (function UseVar(){
      if(true){
          var let=10; 
          console.log(val);
      }else{
      }
      console.log(val); //这里无法访问val 会报错
  })();
```
* const `和let一样,不同的的就是一旦声明必须初始化,一旦初始化不允许改变.`
* `值类型不允许改变值,引用类型不允许改变引用`
##### 1.2 块级作用域多循环的影响
* `为了打出0~10 js5要做那么多事情 还需要使用立即调用函数表达式`
```javascript

var func= [];
for(var i=0;i<=10;i++){
    func.push(function(){
        console.log(i);
    });
}

func.forEach(function(func_){
    func_();
});

// 10 10 11 11 11 11 11 11 11 11 11 11 11

var funcs= [];

for(var i=0;i<=10;i++){
    funcs.push(
    
    (function(value){
       return function(){
           console.log(value);
       };
    })(i)
    
    );
}

funcs.forEach(function(funcs_){
    funcs_();
});
// 打印出 0~10
```
* JS6 Let对循环函数的影响 
```javascript
  var func= []; //把i声明为let 就行
  for(let i=0;i<=10;i++){
      func.push(function(){
          console.log(i);
      });
  }

  func.forEach(function(func_){
      func_();
  });
```
##### 1.3 全局作用域绑定
* `全局作用域不会被绑定到window的全局属性中,所以不会产生覆盖window的属性的情况,`

##### 2.	:whale2:  `字符串和正则表达式` <a id="stringexpend" href="#stringexpend">`代理对`,normalize,,=></a>    <a href="#top"> ----:arrow_up::arrow_up: </a>

`JS5的字符串是基于16位的UTF-16编码进行构建的,每十六位表示一个编程单元,代表一个字符,许多字符串方法和属性都是基于此编程单元的的,但是过去16足够了但是
Unicode引入扩展字符集,编码规则不得不进行变更,所有不再限制在16位,扩展到了32位,一个字符对应一个码位例如 55362 表示 吉这个字符.UTF-16中,前面`2<sup>16</sup>`码位 均以16位的编码单位表示,这个范围被称为基于多文中平面(BMP)`<br/>
`超过这个范围的码位则要归属于某个辅助平面,其中码位仅用16位就无法表示了,为此UTF-16引入` **`代理对`** `其规定用两个16位编码单位表示一个码位,也就是说,字符串里的字符有两种,一种是16位编码单位的BMP字符,一种是两个编码单位的32位字符串,为此产生了很多的问题`
* `1.采用了代理对的一个字符串长度为2,例如` `let val="𠮷"; console.log(val.length);` `结果长度为2`

* `2.不利于对字符串进行排序和比较,要使用normalize() 方法进行等效关系标准化.`

##### 针对代理对编码提供了码点方法
* `codePointAt() 方法,  能够正确处理 4(32位) 个字节储存的字符，返回一个字符的码点。` `charCodeAt() 方法只能返回16位的码点,无法兼容到代理对`
* `ES5 提供String.fromCharCode方法，用于从码点返回对应字符，但是这个方法不能识别 32 位的 UTF-16 字符（Unicode 编号大于0xFFFF）。ES6 提供了String.fromCodePoint方法，可以识别大于0xFFFF的字符，弥补了String.fromCharCode方法的不足。在作用上，正好与codePointAt方法相反。`

```javascript
    let g="𠮷";
    console.log("[𠮷] 长度为:"+g.length);    
    console.log(g.charCodeAt(0));
    console.log(g.codePointAt(0));//Unicode 代理对
    console.log(String.fromCodePoint(134071)); 
    console.log(String.fromCharCode(134071)); 
    //输出
    /*
      [𠮷] 长度为:2
      55362
      134071
      𠮷
      ஷ    
    */
```

```javascript
   //判断是否是代理对
   function is32Bit(code){
       return code.codePointAt(0)>0XFFFF;
   }
```

-----
**`注意`**:`fromCodePoint方法定义在String对象上，而codePointAt方法定义在字符串的实例对象上。`
##### 标准化 normalize
`许多欧洲语言有语调符号和重音符号。为了表示它们，Unicode 提供了两种方法。一种是直接提供带重音符号的字符，比如Ǒ（\u01D1）。另一种是提供合成符号（combining character），即原字符与重音符号的合成，两个字符合成一个字符，比如O（\u004F）和ˇ（\u030C）合成Ǒ（\u004F\u030C）。这两种表示方法，在视觉和语义上都等价，但是 JavaScript 不能识别。JavaScript 将合成字符视为两个字符，导致两种表示方法不相等。`

-----
* `ES6 提供字符串实例的normalize()方法，用来将字符的不同表示方法统一为同样的形式，这称为 Unicode 正规化。`

* `normalize方法可以接受一个参数来指定normalize的方式，参数的四个可选值如下。`
   * `NFC，默认参数，表示“标准等价合成”（Normalization Form Canonical Composition），返回多个简单字符的合成字符。所谓“标准等价”指的是视觉和语义上的等价。`
  * `NFD，表示“标准等价分解”（Normalization Form Canonical Decomposition），即在标准等价的前提下，返回合成字符分解的多个简单字符。`
  * `NFKC，表示“兼容等价合成”（Normalization Form Compatibility Composition），返回合成字符。所谓“兼容等价”指的是语义上存在等价，但视觉上不等价，比如“囍”和“喜喜”。（这只是用来举例，normalize方法不能识别中文。）`
  * `NFKD，表示“兼容等价分解”（Normalization Form Compatibility Decomposition），即在兼容等价的前提下，返回合成字符分解的多个简单字符。`
* `normalize方法目前不能识别三个或三个以上字符的合成，默认 NFD 形式`
```C#
    '\u01D1'==='\u004F\u030C' //false

    '\u01D1'.length // 1
    '\u004F\u030C'.length // 2

     console.log('\u01D1'.normalize() === '\u004F\u030C'.normalize());
    // true
    '\u004F\u030C'.normalize('NFC').length // 1
    '\u004F\u030C'.normalize('NFD').length // 2
    // 上面代码表示，NFC参数返回字符的合成形式，NFD参数返回字符的分解形式。
```
```javascript
    let values=["𠮷","天","下","王","者","J","i","1","5","q"];
    //默认排序
    console.log(values.sort());

    //标准化后 第一种排序加标准化
    let normalized=values.map(function(text){
        return text.normalize();
    })
    console.log(normalized.sort(function(one,two){
               if(one <two){
                   return 1;
               }else if(one == two){
                   return 0;
               }else{
                   return -1;
               }
        })
    );
    // 第二种排序加标准化
    console.log(values.sort(function(first,second){
        let firstNormalized=first.normalize();
        let secondNormalized=second.normalize();
        if(firstNormalized <secondNormalized){
            return 1;
        }else if(firstNormalized == secondNormalized){
            return 0;
        }else{
            return -1;
        }
    }));
```
##### 字符串遍历器
`for...of循环遍历，除了遍历字符串，这个遍历器最大的优点是可以识别大于0xFFFF的码点，传统的for循环无法识别这样的码点。`
```C#
  for (let codePoint of 'foo') {
    console.log(codePoint)
  }
  // "f"
  // "o"
  // "o"
```
##### 字符串对象新增加的实例方法
* **`str.includes(string [,indexStart])`** ：`返回布尔值，表示是否找到了参数字符串。`
* **`str.startsWith(string [,indexStart])`** ：`返回布尔值，表示参数字符串是否在原字符串的头部。`
* **`str.endsWith(string [,indexStart])`** ：`返回布尔值，表示参数字符串是否在原字符串的尾部。`
* **`str.repeat(number)`** :`方法返回一个新字符串，表示将原字符串重复n次。`
* **`str.padStart(time,string)`** : `用于头部补全`
* **`str.padEnd(time,string)`** : `用于尾部补全`
* **`str.matchAll(pattern)`**:`方法返回一个正则表达式在当前字符串的所有匹配`
```javascript
  let s = 'Hello world!';

  s.startsWith('Hello') // true
  s.endsWith('!') // true
  s.includes('o') // true
```
* 这三个方法都支持第二个参数，表示开始搜索的位置。
```javascript
  let s = 'Hello world!';

  s.startsWith('world', 6) // true
  s.endsWith('Hello', 5) // true
  s.includes('Hello', 6) // false
```
* repeat
```javascript
  'x'.repeat(3) // "xxx"
  'hello'.repeat(2) // "hellohello"
  'na'.repeat(0) // ""
```
* padStart
```javascript
  'x'.padStart(5, 'ab') // 'ababx'
  'x'.padStart(4, 'ab') // 'abax'

  'x'.padEnd(5, 'ab') // 'xabab'
  'x'.padEnd(4, 'ab') // 'xaba'
```

##### 3.1	:whale2:  [`模板字符串`](#top) <b id="regularexpend"></b>
`传统的 JavaScript 语言，输出模板通常是这样写的（下面使用了 jQuery 的方法）。`
```node
$('#result').append(
  'There are <b>' + basket.count + '</b> ' +
  'items in your basket, ' +
  '<em>' + basket.onSale +
  '</em> are on sale!'
);
```
`上面这种写法相当繁琐不方便，ES6 引入了模板字符串解决这个问题。`
```node
$('#result').append(`
  There are <b>${basket.count}</b> items
   in your basket, <em>${basket.onSale}</em>
  are on sale!
`);
```
`模板字符串（template string）是增强版的字符串，用反引号（``）标识。它可以当作普通字符串使用，也可以用来定义` `多行字符串` `，或者在字符串中嵌入变量。`
```node
/ 普通字符串
`In JavaScript '\n' is a line-feed.`

// 多行字符串
`In JavaScript this is
 not legal.`

console.log(`string text line 1
string text line 2`);

// 字符串中嵌入变量
let name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`
```
###### [模板实例](http://es6.ruanyifeng.com/#docs/string#%E5%AE%9E%E4%BE%8B%EF%BC%9A%E6%A8%A1%E6%9D%BF%E7%BC%96%E8%AF%91)

###### 标签模板
`模板字符串的功能，不仅仅是上面这些。它可以紧跟在一个函数名后面，该函数将被调用来处理这个模板字符串。
这被称为“标签模板”功能（tagged template）。`
```node
alert`123`
// 等同于
alert(123)

let a = 5;
let b = 10;

tag`Hello ${ a + b } world ${ a * b }`;
// 等同于
tag(['Hello ', ' world ', ''], 15, 50);
```
* `函数tag依次会接收到多个参数。`
```node
function tag(stringArr, ...values){
  // ...
}
```
```node
let a = 5;
let b = 10;

function tag(s, v1, v2) {
  console.log(s[0]);
  console.log(s[1]);
  console.log(s[2]);
  console.log(v1);
  console.log(v2);

  return "OK";
}

tag`Hello ${ a + b } world ${ a * b}`; //=tag(['Hello ', ' world ', ''], 15, 50)
// "Hello "
// " world "
// ""
// 15
// 50
// "OK"
```
**`末班实例`**
```node
let total = 30;
let msg = passthru`The total is ${total} (${total*1.05} with tax)`;

function passthru(literals) {
  let result = '';
  let i = 0;

  while (i < literals.length) {
    result += literals[i++];
    if (i < arguments.length) {
      result += arguments[i];
    }
  }

  return result;
}
```
##### [String.raw()](#top)
`ES6 还为原生的 String 对象，提供了一个raw方法。往往用来充当模板字符串的处理函数，返回一个斜杠都被转义（即斜杠前面再加一个斜杠）的字符串，对应于替换变量后的模板字符串。`
```node
String.raw`Hi\n${2+3}!`;
// 返回 "Hi\\n5!"

String.raw`Hi\u000A!`;
// 返回 "Hi\\u000A!"

String.raw`Hi\\n`
// 返回 "Hi\\\\n"
```
`作为函数，String.raw的代码实现基本如下。`

```node
String.raw({ raw: 'test' }, 0, 1, 2);
// 't0e1s2t'

// 等同于
String.raw({ raw: ['t','e','s','t'] }, 0, 1, 2);

String.raw = function (strings, ...values) {
  let output = '';
  let index;
  for (index = 0; index < values.length; index++) {
    output += strings.raw[index] + values[index];
  }

  output += strings.raw[index]
  return output;
}
```









