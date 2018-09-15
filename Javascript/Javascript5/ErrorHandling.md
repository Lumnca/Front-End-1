<a id="top">JavaScript5.错误处理 </a> :blue_heart:
----
`ECMA-262第三版引入try-catch语句,作为uJavaScript中处理异常的一种标准方式.基本的语法如下所示,这和Java中的try-catch是相似的`

* [x] <a href="#Sysstruct">语法基本结构</a>

* [x] <a href="#ErrorType">Error对象错误类型</a>

* [x] <a href="#ThrowError">抛出错误</a>

* [x] <a href="#DefineUserErrorBySelf">用户自定义错误</a>

* [x] <a href="#ErrorEvent">错误事件</a>

* [x] <a href="#ErrorTypeError">常见错误类型</a>

* [x] <a href="#DebugTechnologe">错误调试技术</a>

#### <a id="Sysstruct">基本结构</a> <a href="#top" >`置顶` :arrow_up:</a>  
```JavaScript
    try{
        window.someNotExisitFunction();
    }catch(error){
        console.log("Error Message："+error.message);
    }  
```
#### `error` 对象
* 所有浏览器都实现支持的：`message`属性 显示错误信息 跨浏览器编程最好只使用这个

* error是一个对象

* IE添加了一个和message属性完全相同的description属性

* Firefox 添加了 fileName，lineName和Stack(包含堆栈信息) 

* Safari 添加了line(表示行号),sourceId(表示内部错误代码)和sourceURL属性
#### finally 子句
```JavaScript
    try{
      window.someNotExisitFunction();
    }catch(error){
      console.log("错误信息:"+error.message);
    }finally{
      console.log("执行完毕");
    }
```
-----
#### <a id="ErrorType" >错误类型：</a><a href="#top" >`置顶` :arrow_up:</a>  
`ECMA-262 定义了7种错误类型`

-----
* `Error`:`是基类型,其他错误均集成自该类型,这个基类的目的是供开发人员抛出自定义错误`
* `EvalError`:`在使用Eval()函数而发生异常的时候抛出，如果没有吧Eval()当函数调用就会抛错`

  ```JavaScript
     new eval(); //抛出错误
     eval =foo ; //抛出错误
     
     // 有时候也抛出:Uncaught TypeError: eval is not a constructor 错误
     
  ```
* `RangeError`:`当数值超出相应范围时触发。例如数组越界`
* `ReferenceError`:`在一个变量未声明的时候使用就会抛出这个错误` `var obj=x; //x 为声明`
* `SystaxError`:`语法错误 会出现在eval函数之外`
* `TypeError`:`在变量中保存着意外的类型时,或者在访问不存在的方法时,都会导致这个错误。`
* `URIError`:`在使用encodeURI() ,decodeURL() 或者URI格式不正确的时候会抛出这个错误`

##### 利用instanceof 区分不同的错误类型
```JavaScript
    try{
        window.someNotExisitFunction();
        var a=new eval();
    }catch(error){
        if(error  instanceof TypeError ){
            //类型错误
            console.log("类型错误:"+error.message+"--[检查是否存在函数方法属性]");
        }else if(error instanceof ReferenceError){
            console.log("引用错误:"+error.message+"--[检查变量是否已经声明]]");
        }else if(error instanceof RangeError){
            console.log("越界错误:"+error.message+"--[检查是否访问越界或者数值无法表示]");
        }
    }  
```
#### <a id="ThrowError" >抛出错误：</a><a href="#top" >`置顶` :arrow_up:</a>  
`与tyr-catch语句相配的还有一个throw操作符,用于随时抛出自定义错误,抛出错误时,必须要给throw操作符一个值,这个值是什么类型,没有要求.下面代码
都是有效的`

``` JavaScript

 throw 123456
 throw "hello word"
 throw true;
 throw {name:"5"}
```
* 遇到throw操作符后 代码会立即停止执行,仅当异常被捕获代码才会继续执行。
* 通过使用某种内置错误类型，可以更加真实地模拟浏览器错误,每种错误类型的构造函数接受一个参数
```JavaScript

 throw new Error("Error sudden appearance");
 throw new TypeError("数据类型错误");
 throw new SysntaxError("语法错误");
 
```
#### <a id="DefineUserErrorBySelf" >用户自定义错误：</a><a href="#top" >`置顶` :arrow_up:</a>  
`用户可以利用继承自定义错误类型`

##### 这个采用原型链方式继承

```JavaScript
    function MyNumberError(message){
        this.name="MyNumberError";
        this.message=message;
    }
    MyNumberError.prototype=new Error();

    try{
        throw new MyNumberError("数值错误");
    }catch(error){
        if(error  instanceof MyNumberError){
            //类型错误
            console.log("数值错误:"+error.message+"--[检查是否存在参数错误]");
        }
    }     
    /*注意：IE只有在抛出Error对象的时候才会显示自定义错误.对于其他类型,它都五一例外地显示“exception thrown a
      nd not caught”（抛出异常,且未被捕获）*/
```
##### 抛出异常的时机
```JavaScript
  function process(values){
     values.sort();
     
     for(var i=0;i<values.length;i++){
        if(values[i]>100) return values[i];
     }
     return -1;
  }

```
* 如果一开始values传入的不是数组,而是String或者Number....那么就会报错
* 但是不同的浏览器报错还不一样
```xml
    <IE ErrorMessage="属性或方法不存在" />

    <Firefox ErrorMessage="values.sort()不是函数" />

    <Safari ErrorMessage="值underfine (表达式values.sort()的结果)不是对象">

    <Chrome ErrorMessage="对象名没有方法sort">

    <Opera ErrorMessage="类型不匹配(通常在需要对象的地方使用了非对象值)">
    
```
  
`结果：对于一个大型的复杂的Web程序,很难以发现错误,排查错误来源,这个时候如果自定义抛出异常的时机或者信息,那么就方便得多了`

```JavaScript
  function process(values){
     if(!values instanceof Array){
        throw new Error("process() :Arugment must be an Array");
     }
     values.sort();
     
     for(var i=0;i<values.length;i++){
        if(values[i]>100) return values[i];
     }
     return -1;
  }

```
#### <a id="ErrorEvent" >错误事件：</a><a href="#top" >`置顶` :arrow_up:</a>  
:maple_leaf:`任何没有通过try-catch-finally处理的错误都会触发window对象的error事件。这个事件是web浏览器最早支持的事件之一,IE,FireFox Chrome为了保持向后兼容并没有对着干事件做任何的修改,（Opera和Safari不支持error事件),在任何Web浏览器中onerror 时间处理程序都不会创建event对象,但是它可以接受三个错误:` `错误信息`,`错误所在的URL,行号` `多数情况下，只有错误信息有用` `因为URL只是给出了文档的位置,而行号所指的代码行即可能出自外部代码` 
 
* `处理onerror 事件`:`必须要是Dom0级技术,它没有遵循Dom2级事件的标准格式` 
* `注意`：`理想情况最好不要使用,作为最后一道防线,最好使用try-catch 捕获处理`
```JavaScript
    
    window.onerror = function(message,url,line){
        alert(message);
    }
   
```

* :x: `如果加一个return false 可以阻止浏览器报告错误的默认行为` `测试了一下:好像浏览器换代了好多代了这个已经不起作用了 JavaScript5 以后被废弃了`
 

```JavaScript
    
    window.onerror = function(message,url,line){
        alert(message);
        return false;
    }
   
```
#### <a id="ErrorTypeError" >常见错误类型：</a><a href="#top" >`置顶` :arrow_up:</a>  
`处理错误的核心在于首先知道代码里面会发生什么错误,一般来说有三种错误`

##### 常见三类错误

* :white_check_mark: `类型转换错误`

  * `利用 === 或者 !== == != instanceof typeof去检测类型` 

* :white_check_mark: `数据类型错误`

  * `在函数传递参数使用的时候,最后对参数类型进行检测`
  
  * `使用数组要用 value instanceof Array 判断是否是数组`
  
  * `使用字符串要判断 typeof value == "string" `
  
  * `常常一些默认的隐式转换会导致错误,例如boolean 很多类型都可以转换为boolean 所以要事先判断`

* :white_check_mark: `通信错误`

  *  `常常发生在Ajax技术中 常见错误是在讲数据发送给服务器之前没有使用encodeURIComponent对数据进行编码`
  
----
##### 错误分类

 * 致命错误: `程序无法使用,明显影响用户操作,导致连带错误`
 * 非致命错误: `影响部分功能,不影响用户主要任务,可以恢复,重复操作可以消除错误`

#### <a id="DebugTechnologe" >错误调试技术：</a><a href="#top" >`置顶` :arrow_up:</a> 

##### 将错误信息输出到控制台上面
`一般我们通过console对象将错误信息输出到控制台`

* `console.error(msg)` ： 将错误信息记录输出到控制台 :输出后字体为`红色` 字体背景 `红色`

* `console.info(msg)`: 将信息性消息记录到控制台 :输出后字体为`黑色` 字体背景 `白色`

* `console.log(msg)`: 将一般性消息记录到控制台 :输出后字体为`黑色` 字体背景 `白色`

* `console.warn(msg)`: 将信息性消息记录到控制台 :输出后字体为`黑色` 字体背景 `黄色`    












