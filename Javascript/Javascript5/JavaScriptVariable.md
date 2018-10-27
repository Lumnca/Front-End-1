<a id="top" href="#top">JavaScript 变量 作用域 内存  :maple_leaf:</a> 
----
`JS 变量和其他语言的变量有很大区别,js变量是松散类型,他只是在特定时间用于保存特定值的一个名字而已，由于不存在定义某个变量必须保存何种数据类型值的规则
,变量的值和数据可以在脚本的生命周期内改变,尽管开起来很强大,但是容易出问题,而且复杂`

#### :blue_heart: <a href="#top">`变量`</a>
* `ECS 包含两种不同的数据类型：`
  * `基本类型值`:`简单的数据段 ` `Undefind` `Null` `Boolean` `Number` `String` `这五种类型都是按值访问`
  * `引用类型值`:`可以由多个值构成的对象 保存在内存中 按引用访问,实际操作是引用`
  
##### 	:purple_heart: [`动态属性`](#)
`JS 对象的属性是动态的,可以动态的为一个对象添加删除属性 未定义属性返回undefined 但是不会报错`
```javascript
var apple = new Object();
apple.color = "red";
apple.place = "XiaoMing"
apple.isExisit = true;

console.log(apple.place); //XiaoMing
console.log(apple.owner); //undefined
```
##### :green_heart: [`变量复制的问题`](#)
 * `基本类型值`:`按值 复制 复制值 在一个新的数据段里面`
 * `引用类型值`:`复制引用`
 * `Js 函数参数都是按照值传递,传递的值类型会被赋值给一个函数内部的局部变量`
 ```javascript
 function setName(obj){
    obj.Name = "Nike";
    obj = new Object(); //申请了一个新的内存
    obj.Name = "maike";
}

var o = new Object();
setName(o);
console.log(o.Name); //Nike
```
#### :blue_heart: <a href="#top">`检测类型`</a>
`对于一般的检测我们可以使用 typeof 检测类型  对于null 也是object 类型 所有的引用类型都是 object的实例 ` 
```javascript
var o = "Nicholas";
var b = true;
var u = 22;
var n ;
var q =null;
var w = new Object();

console.log(typeof o);//string
console.log(typeof b);//boolean
console.log(typeof u);//number
console.log(typeof n);//undefined
console.log(typeof q);//object
console.log(typeof w);//object
```
* `使用typeof 检测函数的时候,该操作符会返回function  在Safari 5 和 Chrome 7 和之前的版本中使用typeof 检测正则表达式的时候,由于规范的原因这个操作符也会返回 function 在IE he Firefox中 正则返回Object `
* `ECMA-262 规定  任何在内部实现[[Call]] 方法的对象都应该在应用typeof 操作符时返回function  `
```javascript
console.log(typeof setName);//object function
```

`对于复杂的判断想具体指导是什么类型的时候 可以使用 instanceof ` `variable instanceof constructor`
 
```javascript
var person = new Object();
var colors = ["Red","Yellow","Purple"];
var pattern = /$\a/;

console.log(person instanceof Object);  //true
console.log(colors instanceof Array);   //true
console.log(pattern instanceof RegExp); //true
```
#### :blue_heart: <a href="#top">`执行环境和作用域`</a>
`执行环境简称 环境,是JavaScript中最为重要的一个概念,执行环境定义了变量或函数有权访问的其他数据,决定了他们各自的行为,每个执行环境都有一个与之关联
的` **`变量对象[Variable  object]`** `环境中定义的所有变量和函数都保存在这个对象中.虽然我们编写的代码无法访问这个对象,单解析器在处理数据时会在后台使用它。`
* `全局环境是最外围的一个执行环境,在web浏览器中,全局环境被认为是window对象,因为此所有全局编和函数都是作为window对象的属性和方法创建` 
* **`注意: 某个执行环境中的所有代码执行完之后,这个环境就会被销毁,保存在其中的所有变量和函数定义也会被销毁 [全局变量会在应用程序退出后 关闭网页/浏览器 之后被销毁]`**
* `每个函数都有自己的作用域,当执行流进入一个函数的时,函数的环境就会被推入一个环境栈中,执行完成后 环境栈再弹出环境,吧控制权返回给之前的函数环境 ECS 程序中的执行流正式有这个方便的机制控制着`

##### 作用域链
`当代码在一个环境中执行时，都会创建一个作用域链。 作用域链的用途是保证对执行环境有权访问的所有变量和函数的有序访问`
* `整个作用域链是由不同执行位置上的变量对象按照规则所构建一个链表。作用域链的最前端，始终是当前正在执行的代码所在环境的变量对象。`
* `如果这个环境是函数，则将其活动对象（activation object)作为变量对象。活动对象在最开始时只包含一个变量，就是函数内部的arguments对象[全局环境不存在]`
* `标识符解析 是从内部 向外部 查找解析,所有最好使用局部变量,减少搜索时间`

```javascript
function buildName(){
    var qs = "?Name=jx";
    with(location){
        var url = href + qs;
    }
    return url; //file:///E:/ecs5-workspace/ecs5-Bom/index.html?Name=jx
}

console.log(buildName());
```
##### 作用域
* `js没有块级作用域`
* `但是有函数局部环境 有局部变量 使用var 声明变量 避免直接使用变量 不声明变量`
```javascript
{
    if(true){
        var color = "blue";
    }
    console.log(color);//blue
}
```
##### 垃圾回收机制
* `标记清楚`:`常用,几乎所有浏览器都有,差异只在垃圾收集的时间间隔不一样`
* `引用计数`:`有循环引用的问题`
* `何时启动垃圾回收呢!它是周期性运行的`
* `通常分配给web浏览器的可用内存数量比纷飞给卓明应用程序的少,这是出于安全考虑,防止运行js 耗尽全部系统资源,导致系统崩溃,所以
为了优化内存占用,一旦数据不再有用,那么最好通过将其值设置为null 来释放引用,这叫做接触引用`









