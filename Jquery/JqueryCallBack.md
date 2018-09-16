<a id="top" href="#top">Jquery callbacks 对象  :maple_leaf:</a> 
----
`jQuery 1.7 版本中新增的 jQuery.Callbacks() 函数返回一个全能的对象，此对象对管理回调列表提供了强大的方式。它能够增加、删除、触发、禁用回调函数。
类似于C#的委托一般的样子`

- [x] :maple_leaf: <a href="#callbacksAddIndex">`callbacks.add(callbacks)`</a>
- [x] :maple_leaf: <a href="#callbacksdisableIndex">`callbacks.disable()`</a>
- [x] :maple_leaf: <a href="#callbacksdisabledIndex">`callbacks.disabled()`</a>
- [x] :maple_leaf: <a href="#callbacksemptyIndex">`callbacks.empty()`</a>
- [x] :maple_leaf: <a href="#callbacksfireIndex">`callbacks.fire()`</a>
- [x] :maple_leaf: <a href="#callbacksfirewithIndex">`callbacks.fireWith([context ] [, args ])`</a>
- [x] :maple_leaf: <a href="#callbacksfireddIndex">`callbacks.fired()`</a>
- [x] :maple_leaf: <a href="#callbacksemptyIndex">`callbacks.has()`</a>
- [x] :maple_leaf: <a href="#callbackslockIndex">`callbacks.lock()`</a>
- [x] :maple_leaf: <a href="#callbackslockedIndex">`callbacks.locked()`</a>
- [x] :maple_leaf: <a href="#callbacksremoveIndex">`callbacks.remove()`</a>
- [x] :maple_leaf: <a href="#callbackscallBackIndex">`jQuery.Callbacks()`</a>

####  <a id="callbacksAddIndex" href="#callbacksAddIndex">callbacks.add(callbacks)</a>  :star2: <a href="#top"> :arrow_up: </a>
`回调列表中添加一个回调或回调的集合。` **`callbacks.add( callbacks )`**
* `callbacks 类型: Function, Array 一个函数，或者一个函数数组，用来添加到回调列表。`
```javascript
  //两个函数对象
  var fisrtFunction =function(value){
      console.log("CallBack1 :"+value);
  }    
  var secondFunction = function(val){
      console.log("CallBack2 :"+val);
  }
  //创建一个 回调函数对象
  var callbacks = $.Callbacks(); 
  callbacks.add( fisrtFunction );
  callbacks.add( secondFunction );
  callbacks.fire("Call Function");
```

####  <a id="callbacksdisableIndex" href="#"callbacksdisableIndex" >callbacks.disable() </a>  :star2: <a href="#top"> :arrow_up: </a>
`禁用回调列表中的回调,这个方法不接受任何参数,此方法返回绑定它的那个回调对象(this).`
```javascript
  var fisrtFunction =function(value){
      console.log("CallBack1 :"+value);
  }    
  var secondFunction = function(val){
      console.log("CallBack2 :"+val);
  }
  var callbacks = $.Callbacks(); //创建一个 回调函数对象
  callbacks.add( fisrtFunction );
  callbacks.add( secondFunction );
  callbacks.disable();//禁止回调
  callbacks.fire("Call Function"); //函数将不会支持
```
####  <a id="callbacksdisabledIndex" href="#callbacksdisabledIndex">callbacks.disabled()</a>  :star2: <a href="#top"> :arrow_up: </a>
` 确定回调列表是否已被禁用。,这个方法不接受任何参数`
```javascript
  var fisrtFunction =function(value){
      console.log("CallBack1 :"+value);
  }    
  var secondFunction = function(val){
      console.log("CallBack2 :"+val);
  }
  var callbacks = $.Callbacks(); //创建一个 回调函数对象
  callbacks.add( fisrtFunction );
  callbacks.add( secondFunction );
  callbacks.disable();//禁止回调
  if(callbacks.disabled()){
      console.log("回调函数已经被禁止了");
  }
  callbacks.fire("Call Function"); //函数将不会支持
```
####  <a id="callbacksemptyIndex" href="#callbacksemptyIndex">callbacks.empty()</a>  :star2: <a href="#top"> :arrow_up: </a>
`从列表中删除所有的回调.这个方法不接受任何参数`
```javascript
  var fisrtFunction =function(value){
      console.log("CallBack1 :"+value);
  }    
  var secondFunction = function(val){
      console.log("CallBack2 :"+val);
  }
  var callbacks = $.Callbacks(); //创建一个 回调函数对象
  callbacks.add( fisrtFunction );
  callbacks.add( secondFunction );
  callbacks.empty(); //清空函数列表
  callbacks.fire("Call Function"); //已经没有函数执行了
```
####  <a id="callbacksfireIndex" href="#callbacksfireIndex">callbacks.fire()</a>  :star2: <a href="#top"> :arrow_up: </a>
`传入指定的参数调用所有的回调`
* `callbacks.fire( arguments )`
  * `arguments`:`类型: Anything 这个参数或参数列表传回给回调列表。`
```javascript
  var fisrtFunction =function(value){
      console.log("CallBack1 :"+value);
  }    
  var secondFunction = function(val){
      console.log("CallBack2 :"+val);
  }
  var callbacks = $.Callbacks(); //创建一个 回调函数对象
  callbacks.add( fisrtFunction );
  callbacks.add( secondFunction );
  callbacks.fire("Call Function"); //执行函数 传入参数
```
####  <a id="callbacksfirewithIndex" href="#callbacksfirewithIndex">callbacks.fireWith()</a>  :star2: <a href="#top"> :arrow_up: </a>
`访问给定的上下文和参数列表中的所有回调。`
* `callbacks.fireWith([context ] [, args ] )`
  * `context Type` : `该列表中的回调被触发的上下文引用`  `args Type` : `一个参数或参数列表传回给回调列表。`
```javascript
    var fisrtFunction =function(value){
        console.log("CallBack1 :"+value);
    }    
    var secondFunction = function(val){
        console.log("CallBack2 :"+val);
    }
    var callbacks = $.Callbacks(); //创建一个 回调函数对象
    callbacks.add( fisrtFunction );
    callbacks.add( secondFunction );
    callbacks.fireWith( window, ["foo"]);
```
####  <a id="callbacksfireddIndex" href="#callbacksfireddIndex">callbacks.fired()</a>  :star2: <a href="#top"> :arrow_up: </a>
`确定回调是否至少已经调用一次,这个方法不接受任何参数`
```javascript
  var fisrtFunction =function(value){
      console.log("CallBack1 :"+value);
  }    
  var secondFunction = function(val){
      console.log("CallBack2 :"+val);
  }
  var callbacks = $.Callbacks(); //创建一个 回调函数对象
  callbacks.add( fisrtFunction );
  callbacks.add( secondFunction );

  console.log(callbacks.fired()); //返回false

  callbacks.fireWith( window, ["foo"]);

  console.log(callbacks.fired()); //返回true
```
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
`确定列表中是否提供一个回调,callback 类型: Function() 用来查找的回调函数。`
```javascript
  function third(){
      console.log("CallBack1 :"+value);
      return true;
  }
  var fisrtFunction =function(value){
      console.log("CallBack1 :"+value);
  }    
  var secondFunction = function(val){
      console.log("CallBack2 :"+val);
  }
  var callbacks = $.Callbacks(); //创建一个 回调函数对象
  callbacks.add( fisrtFunction );
  callbacks.add( secondFunction );

  console.log("是否具有 fisrtFunction : " + callbacks.has(fisrtFunction));
  console.log("是否具有 third :"+callbacks.has(third));

  callbacks.fireWith( window, ["foo"]);
```
####  <a id="callbackslockIndex" href="#callbackslockIndex">callbacks.lock()</a>  :star2: <a href="#top"> :arrow_up: </a>
`锁定回调列表的当前状态。,没有参数 此方法返回绑定它的那个回调对象 ,一旦锁定,不可调用`
```javascript
  var fisrtFunction =function(value){
      console.log("CallBack1 :"+value);
  }    
  var secondFunction = function(val){
      console.log("CallBack2 :"+val);
  }
  var callbacks = $.Callbacks(); //创建一个 回调函数对象
  callbacks.add( fisrtFunction );
  callbacks.lock(); //锁定
  callbacks.add( secondFunction );
  callbacks.fire();
```
####  <a id="callbackslockedIndex" href="#callbackslockedIndex">callbacks.locked()</a>  :star2: <a href="#top"> :arrow_up: </a>
`返回布尔值,确定是否被锁定了`
####  <a id="callbacksremoveIndex" href="#callbacksremoveIndex">callbacks.remove(callbacks)</a>  :star2: <a href="#top"> :arrow_up: </a>
`callbacks.remove( callbacks )`:`从回调列表中删除的一个函数，或者函数数组。`
```javascript
  var fisrtFunction =function(value){
      console.log("CallBack1 :"+value);
  }    
  var secondFunction = function(val){
      console.log("CallBack2 :"+val);
  }
  var callbacks = $.Callbacks("MyCallback"); //创建一个 回调函数对象
  callbacks.add( fisrtFunction );
  callbacks.add( secondFunction );

  callbacks.remove(secondFunction); //secondFunction 函数已经被移出

  callbacks.fire("Call Fucntion");
```
####  <a id="callbackscallBackIndex" href="#callbackscallBackIndex">jQuery.Callbacks()</a>  :star2: <a href="#top"> :arrow_up: </a>
`一个多用途的回调列表对象，提供了强大的的方式来管理回调函数列表。` <br/>
`jQuery.Callbacks( flags )`:`flags 类型: String 一个用空格标记分隔的标志可选列表,用来改变回调列表中的行为。`
* `once: 确保这个回调列表只执行（.fire()）一次(像一个递延 Deferred)`
```javascript
  function fn1( value ) {
      console.log( value );
  }

  function fn2( value ) {
      fn1("fn2 says: " + value);
      return false;
  }
  var callbacks = $.Callbacks( "once" );
  callbacks.add( fn1 ); 
  callbacks.fire( "foo" ); //调用了
  callbacks.add( fn2 );
  callbacks.fire( "bar" ); //只能被调用一次  无法调用
  callbacks.remove( fn2 );
  callbacks.fire( "foobar" ); // 已经被调用一次 无法调用
```
* `memory: 保持以前的值，将添加到这个列表的后面的最新的值立即执行调用任何回调(像一个递延Deferred).`
```javascript
$(document).ready(function(event) {
    function fn1( value ) {
        console.log( value );
    }

    function fn2( value ) {
        fn1("fn2 says: " + value);
        return false;
    }
    var callbacks = $.Callbacks( "memory" );
    callbacks.add( fn1 );
    callbacks.fire( "foo" );
    callbacks.add( fn2 );
    callbacks.fire( "bar" );
    callbacks.remove( fn2 );
    callbacks.fire( "foobar" );

    /*
    output:
    foo
    fn2 says:foo
    bar
    fn2 says:bar
    foobar
    */
```
* `unique: 确保一次只能添加一个回调(所以在列表中没有重复的回调)`
* `stopOnFalse: 当一个回调返回false 时中断调用`
`$.Callbacks( 'unique stopOnFalse' ) 也可以使用多个标志`






