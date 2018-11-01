### [Node 事件处理机制和时间环机制 :maple_leaf: ](#top)<span id="top"></span>
`课客户端JavaScript 脚本代码一样，Node.js中,许多对象也将会触发事件.例如，针对代表了web服务器的http.Server对象来说,可能也会触发 接收到客户端请求
,产生链接错误,等各种事件,针对每个不同的事件,都需要进行不同的事件处理`
- [x] [`EventEmitter`](#eventemitter)
- [x] [`事件环机制`](#eventloop)

#### [eventEmitter](#) :white_check_mark: <span id="eventemitter"></span>	
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
#### [事件环机制 :white_check_mark:](#) <span id="eventloop"></span>	
`在Node.js中,与JavaScript或其他语言一样,采用事件环机制`<br/>
```
在Node.js中，与JavaScript或其他语言中一样，采用事件环机制。我们知道，在JavaScript中，大
部分代码均用于进行诸如“onclick”、“onmouseover”之类的用户交互事件的处理。在服务器端，虽然
不会存在由用户对于界面上的操作而产生的事件，但是将存在一个服务器应用程序中所可能触发的各种
事件。例如，当一个用户向服务器端发出一个客户端请求时，将会触发HTTP服务器的一个在Node.js中
被定义为request的事件。

在Node.js中，采用非阻塞型I/O机制，这意味着所有要求应用程序所进行的处理，如HTTP请求、数据库
查询、文件的输入/输出等，都不会在处理结束之前阻碍其他处理的进行，也就是说，这些处理都是独立
进行的，当处理结束时，会触发一个回调事件，也就是说，在Node.js中，我们所要编写的是各种I/O事
件的回调函数中的处理。

许多开发者可能已经非常熟悉JavaScript中的事件驱动式编程，因为它就像我们在日常生活中所做的处理：
假设你正在切菜，而炉子里的水正好在这个时刻烧开了。你必须先暂停切菜，关闭炉子，然后返回继续切菜
，而不能一边切菜，一边关闭炉子，尽管如果你关炉子的速度非常快，这两者看起来没什么区别。在JavaS
cript中的事件驱动编程也是如此，在一个时刻只能执行一个回调函数，因为在JavaScript中只能使用单线程。

单线程的概念是非常重要的，因为在Node.js中使用的是V8 JavaScript脚本语言，所以也只能使用单线
程，并不存在并行处理的概念。但是，在Node.js中使用的是非阻塞型I/O，所以Node.js对于每个回调
函数的执行速度将会是非常快的，因为它并不需要等待任何I/O处理的结束。

对于事件环机制的另一个恰当的比喻是将它比作一个邮递员，而每个事件就好比是邮递员需要送达的一封邮件。
他手上有大量需要依序送达的邮件，而他需要按照指定路线来送达这些邮件，而回调函数就好比这些路线，由
于邮递员只有一双腿，所以他每次只能按照指定路线来送达一封邮件，也就是说，他每次只能处理一个回调函
数。在他按照某条指定路线送达某封邮件的途中，可能会有人给他新的邮件，这就是代码中要求他处理的新
的事件。这种情况下，邮递员将会转而处理新的事件（包括触发事件、初始化该事件的回调函数等），在该事
件处理完毕之后，转而送达原本要送达的邮件，也就是说，在回调函数的执行过程中，他将转而处理新的事
件，在该事件处理完毕之后，转而继续处理原回调函数。这种环状处理机制，在Node.js中称为事件环机制。

让我们用实际应用程序中的例子来看一下该邮递员的行为。假设我们有一个HTTP服务器，它需要接收客户端
请求，根据请求参数从数据库中获取一些数据，然后将这些数据返回给用户。在这种场景下我们有几个事件
需要处理。首先，用户在页面上向服务器端发出一个客户端请求，这将触发HTTP服务器对象的一个request
事件，在事件回调函数（假定函数被命名为callbackA）中处理该请求，根据请求参数来决定需要从数据库
中获取哪些数据，然后向数据库中发出获取数据的请求，并且将另一个函数（假定函数被命名为callbackB）
指定为当数据库获取到数据时触发的response事件的事件回调函数。当向数据库发出获取数据的请求后，就
可以继续执行callbackA回调函数中的后续代码。当数据库中数据获取完毕后，将触发数据库对象的respon
se事件，调用callbackB回调函数将数据返回给用户。

在这个处理中，由于Node.js中采用的是非阻塞I/O机制，因此不需要等待数据库中的数据获取完毕才能继续
执行callbackA回调函数中的后续代码，而是为数据库对象绑定一个新的事件并初始化该事件的事件回调函数。
```
