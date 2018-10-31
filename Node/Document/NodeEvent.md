### [Node 事件处理机制和时间环机制 :maple_leaf: ](#top)<span id="top"></span>
`课客户端JavaScript 脚本代码一样，Node.js中,许多对象也将会触发事件.例如，针对代表了web服务器的http.Server对象来说,可能也会触发 接收到客户端请求
,产生链接错误,等各种事件,针对每个不同的事件,都需要进行不同的事件处理`
- [x] [EventEmitter](#eventemitter)
- [x] [`事件环机制`](#Eventloop)

## [eventEmitter](#) :white_check_mark: <span id="eventemitter"></span>	
`在Node 中用户实现各种事件处理的event模板中,定义了一个EventEmitter类,所有可能触发事件的对象都是一个继承了EventEmitter类的子实例对象,在Node.js中
为EventEmitter 类定义了许多方法,所有与对象的事件处理函数的绑定和接触相关的处理均依靠这些方法的调用来执行

* `emitter.addListener(eventName, listener)`:`对指定事件绑定事件处理函数`
* `emitter.emit(eventName[, ...args])`:`手工触发指定事件`
* `emitter.eventNames()`:`返回一个数组，该列表列出了发射器已注册侦听器的事件。数组中的值将是字符串或符号。`<br/><br/>
  ```javascript
  const EventEmitter = require('events');
  const myEE = new EventEmitter();
  myEE.on('foo', () => {});
  myEE.on('bar', () => {});

  const sym = Symbol('symbol');
  myEE.on(sym, () => {});

  console.log(myEE.eventNames());
  // Prints: [ 'foo', 'bar', Symbol(symbol) ]
  //列出已经监听的事件 返回 Array
  ```
* `emitter.getMaxListeners()`:`返回最大可以绑定多少个事件侦听器`
* `emitter.listenerCount(eventName)`:`获取指定事件的事件处理函数的数量`
* `emitter.listeners(eventName)`：`获取指定事件的所有事件处理函数` <br/><br/>
  ```node
  const EventEmitter = require('events');
  const myEE = new EventEmitter();
  myEE.on('foo', () => { console.log(1); });
  myEE.on('bar', () => { console.log(2); });
  myEE.on('bar', () => { console.log(3); });

  const sym = Symbol('symbol');
  myEE.on(sym, () => {});

  let func_count = myEE.listenerCount('bar');
  console.log(func_count);//输出函数绑定个数

  let funds = myEE.listeners('bar');
  for (let index in funds){
     funds[index]();//执行函数
  }
  ```
* `emitter.off(eventName, listener)`:`别名为emitter.removeListener()。*`
* `emitter.on(eventName, listener)`:`addListener 一样 别名而已`
* **`emitter.once(eventName, listener)`**:`对指定事件指定只执行一次事件处理函数`
* `emitter.prependListener(eventName, listener)`:``
emitter.prependOnceListener(eventName, listener)
* `emitter.removeAllListeners([eventName])：`删除所有侦听器或指定的侦听器eventName。`
* `emitter.removeListener(eventName, listener)`：`一定指定事件的事件处理函数`
* `emitter.setMaxListeners(n)`:`设置绑定事件处理函数的最大数量，n为整数值`
emitter.rawListeners(eventName)
```
##### EventEmitter 本身的事件
* `newListener`:`绑定事件的处理函数的时候,都会触发这个事件`
* `removeListener`:`取消事件处理函数的时候触发`
```node
emitter.on('removeListener',function(event,function){
  //事件处理函数代码
  * event: 被取消的事件
  * function: 被取消的事件处理函数
});
```
#### [事件环机制 :white_check_mark:](#) <span id="Eventloop"></span>	
`在Node.js中,与JavaScript或其他语言一样,采用事件环机制`<br/>
