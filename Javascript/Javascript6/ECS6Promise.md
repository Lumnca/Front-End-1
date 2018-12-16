### [JavaScript6 Promise 异步编程](#top) :grey_question: <b id="top"></b>

----
:star: [`Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。它由社区最早提出和实现，ES6 将其写进了语言标准，统一了
用法，原生提供了Promise对象`](#top)

---
- [x] [Promise 介绍](#intro)
- [x] [Promise 基操](#use)
- [x] [Promise.prototype.then()](#then)
- [x] [Promise.prototype.catch()](#catch)
- [x] [Promise.prototype.finally()](#finally)
- [x] [Promise.all()](#all)
- [x] [Promise.race()](#race)
- [x] [Promise.resolve()](#resolve)

----
#### [Promise 介绍](#top) :grey_exclamation: <b id="intro"></b>
`所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操
作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。`
* :fire: `对象的状态不受外界影响。Promise对象代表一个异步操作，有三种状态：pending（进行中）、fulfilled(已成功)【resolved统一只指fulfilled状态】
和rejected（已失败)`
  * > `只有异步操作结果可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是Promise这个名字的由来，它的英语意思就是“承诺”，
        表示其他手段无法改变`
* :fire: `一旦状态改变，就不会再变，任何时候都可以得到这个结果 且只可能 发送 从 pending => fulfilled  或者  pending =>和rejected 转变一旦发生状态固定 
无法改变 `
  * > `这也叫做 resolved（已定型）你再对Promise对象添加回调函数，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错
过了它，再去监听，是得不到结果的。`
* :fire: `避免了层层嵌套的回调函数。此外，Promise对象提供统一的接口，使得控制异步操作更加容易。`

---
`有了Promise对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。此外，Promise对象提供统一的接口，使得控制异步操作更加容易。`

#### [Promise 基本操作](#top) :grey_exclamation: <b id="use"></b>
`让我们来写一个Promise 吧` **`Promise 操作声明完立即执行`**
* `Promise构造函数接受一个函数作为参数，该函数的两个参数分别是` **`resolve`** `和` **`reject`** `。它们是两个函数，由 JavaScript 引擎提供，不用自己部署。`
   * resolve:`将Promise对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved）`
   * reject: `将Promise对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected）`
   
* `then方法可以接受两个回调函数作为参数。第一个回调函数是Promise对象的状态变为resolved时调用，第二个回调函数是Promise对象的
状态变为rejected时调用 第二个函数是可选的，不一定要提供。这两个函数都接受Promise对象传出的值作为参数。可以用catch 代替 他可以用来捕获异常并且自动完成reject
的状态转换功能 [下面有介绍]`
```node
function Operation(){
    /*异步操作 */
    return true;
}
/**
 * resolve: 执行成功的时候的回调函数
 * reject：执行失败的时候回调函数
 */
let p1 = new Promise((resolve,reject)=>{
     let isSuccess = Operation();
     //Operation 函数的代码也可以直接写在 里面
     if(isSuccess){
         resolve("成功执行回调函数");   
     }else{
         reject("Error Info: carry out failed");
     }
}).then((res)=>{
    console.log(res);
},(rej)=>{
    console.log(rej);
});

console.log("Finish");

// then 当传入两个参数的时候 第一个参数 指定 resolve函数 第二参数 指定 reject函数

/* 执行结果：                             */
// Finish
// 成功执行回调函数
```
##### 执行流程
* `Promise 新建后立即执行`
* `hen方法指定的回调函数，将在当前脚本所有同步任务执行完才会执行，所以resolved最后输出 `
* `一般来说，调用resolve或reject以后，Promise 的使命就完成了，后继操作应该放到then方法里面，而不应该直接写在resolve或reject的后面`
```node
let promise = new Promise(function(resolve, reject) {
  console.log('Promise');
  resolve();
});

promise.then(function() {
  console.log('resolved.');
});

console.log('Hi!');

// Promise
// Hi!
// resolved
```
##### 将Promise 作为返回值
```javascript
/*
    setTimeout的三个参数:

    1.code/function 	必需。要调用一个代码串，也可以是一个函数。
    2.milliseconds 	可选。执行或调用 code/function 需要等待的时间，以毫秒计。默认为 0。
    3.param1, param2, ... 	可选。 传给执行函数的其他参数（IE9 及其更早版本不支持该参数）。
*/
function timeout(ms) {
    return new Promise((resolve, reject) => {
        setTimeout(resolve, ms, 'done');
    });
};
  
timeout(1000).then((value) => {
     console.log(`1000ms later is ${value}`);
});
```

##### 加载图片的小例子
```node
function loadImageAsync(url) {
  return new Promise(function(resolve, reject) {
    const image = new Image();

    image.onload = function() {
      resolve(image);
    };

    image.onerror = function() {
      reject(new Error('Could not load image at ' + url));
    };

    image.src = url;
  });
}
```

##### 封装一个ajax
```node
const getJSON = function(url) {
  const promise = new Promise(function(resolve, reject){
    const handler = function() {
      if (this.readyState !== 4) {
        return;
      }
      if (this.status === 200) {
        resolve(this.response);
      } else {
        reject(new Error(this.statusText));
      }
    };
    const client = new XMLHttpRequest();
    client.open("GET", url);
    client.onreadystatechange = handler;
    client.responseType = "json";
    client.setRequestHeader("Accept", "application/json");
    client.send();

  });

  return promise;
};

getJSON("/posts.json").then(function(json) {
  console.log('Contents: ' + json);
}, function(error) {
  console.error('出错了', error);
});
```
#### [Promise.prototype.then()](#top) :grey_exclamation: <b id="then"></b>
`Promise 实例具有then方法，也就是说，then方法是定义在原型对象Promise.prototype上的 then方法的第一个参数是resolved状态的回调函数，第二个参数（可选）是rejected状态的回调函数。`
* `then方法返回的是一个新的Promise实例（注意，不是原来那个Promise实例）。因此可以采用链式写法，即then方法后面再调用另一个then方法。回调函数的回调`
```node
getJSON("/posts.json")
.then(function(json) {
  return json.post;
}).then(function(post) {
  // ...
});
```
#### [Promise.prototype.then()](#top) :grey_exclamation: <b id="catch"></b>
`Promise.prototype.catch方法是.then(null, rejection)的别名，用于指定发生错误时的回调函数。`
```node
getJSON('/posts.json').then(function(posts) {
  // ...
}).catch(function(error) {
  // 处理 getJSON 和 前一个回调函数运行时发生的错误
  console.log('发生错误！', error);
});
```
`如果异步操作抛出错误，状态就会变为rejected，就会调用catch方法指定的回调函数，处理这个错误。另外，then方法指定的回调函数，如果
运行中抛出错误，也会被catch方法捕获 ，promise抛出一个错误，也会被catch方法指定的回调函数捕获。`
```node
const promise = new Promise(function(resolve, reject) {
  try {
    throw new Error('test');
  } catch(e) {
    reject(e);
  }
});
promise.catch(function(error) {
  console.log(error);
});
```
**`Promise 错误吃掉`**
```node
const someAsyncThing = function() {
  return new Promise(function(resolve, reject) {
    // 下面一行会报错，因为x没有声明
    resolve(x + 2);
  });
};

someAsyncThing().then(function() {
  console.log('everything is great');
});

setTimeout(() => { console.log(123) }, 2000);
// Uncaught (in promise) ReferenceError: x is not defined
// 123

上面代码中，someAsyncThing函数产生的 Promise 对象，内部有语法错误。浏览器运行到这一行，会打印
出错误提示ReferenceError: x is not defined，但是不会退出进程、终止脚本执行，2 秒之后还是会输
出123。这就是说，Promise 内部的错误不会影响到 Promise 外部的代码，通俗的说法就是“Promise 会
吃掉错误”。

```
#### [Promise.prototype.finally()](#top) :grey_exclamation: <b id="finally"></b>
* `finally方法用于指定不管 Promise 对象最后状态如何，都会执行的操作。该方法是 ` **ES2018** ` 引入标准的。`
* `finally方法的回调函数不接受任何参数 这意味着没有办法知道，前面的 Promise 状态到底是fulfilled还是rejected ，所以他不依赖于 Promise 的执行结果`
* `finally本质上是then方法的特例。`
```node
promise
.then(result => {···})
.catch(error => {···})
.finally(() => {···});

//例子
server.listen(port)
  .then(function () {
    // ...
  })
  .finally(server.stop);
```
**本质上**
```
promise
.finally(() => {
  // 语句
});

// 等同于
promise
.then(
  result => {
    // 语句
    return result;
  },
  error => {
    // 语句
    throw error;
  }
);
```
#### [Promise.all()](#top) :grey_exclamation: <b id="all"></b>
`Promise.all方法用于将多个 Promise 实例，包装成一个新的 Promise 实例。 方法接受一个数组作为参数 如果参数不是 Promise类型将会转换为
Promise类型`
* `（Promise.all方法的参数可以不是数组，但必须具有 Iterator 接口，且返回的每个成员都是 Promise 实例。）`
* `如果作为参数的 Promise 实例，自己定义了catch方法，那么它一旦被rejected，并不会触发Promise.all()的catch方法。`
```node
const p = Promise.all([p1, p2, p3]);
//p的状态由p1、p2、p3决定，分成两种情况。
（1）只有p1、p2、p3的状态都变成fulfilled，p的状态才会变成fulfilled，此时p1、p2、p3的
返回值组成一个数组，传递给p的回调函数。

（2）只要p1、p2、p3之中有一个被rejected，p的状态就变成rejected，此时第一个被reject的
实例的返回值，会传递给p的回调函数。
```

```node
// 生成一个Promise对象的数组
const promises = [2, 3, 5, 7, 11, 13].map(function (id) {
  return getJSON('/post/' + id + ".json");
});

Promise.all(promises).then(function (posts) {
  // ...
}).catch(function(reason){
  // ...
});
```
##### 要成功就全成功
```node
let p1 = new Promise((resolve,reject)=>{
    resolve("p1 执行成功");
});

let p2 = new Promise((resolve,reject)=>{
    resolve("p2 执行成功");
});

let p3 = new Promise((resolve,reject)=>{
    resolve("p3 执行成功");
});

let p = Promise.all([p1,p2,p3]).then( result=>{
    console.log(result);
    //[ 'p1 执行成功', 'p2 执行成功', 'p3 执行成功' ]
}).catch(error =>{
    console.log(error);
})
```
##### 一个失败全失败
```node
 p1 = new Promise((resolve,reject)=>{
    let x = 1;
    let x = 1;
    resolve("p1 执行成功");
});

let p2 = new Promise((resolve,reject)=>{
    resolve("p2 执行成功");
});

let p3 = new Promise((resolve,reject)=>{
    resolve("p3 执行成功");
});

let p = Promise.all([p1,p2,p3]).then( result=>{
    console.log(result);
}).catch(error =>{
    console.log("error:");
    console.log(error);
    /*
    error:
    index.html:28 SyntaxError: Identifier 'x' has already been declared
        at new Promise (<anonymous>)
        at index.html:9

    */
});
```
#### [Promise.race()](#top) :grey_exclamation: <b id="race"></b>
`Promise.race方法同样是将多个 Promise 实例，包装成一个新的 Promise 实例`
* `跑多个任务 只要一个完成就行 `
```
const p = Promise.race([p1, p2, p3]);

上面代码中，只要p1、p2、p3之中有一个实例率先改变状态，p的状态就
跟着改变。那个率先改变的 Promise 实例的返回值，就传递给p的回调函数。
```
#### [Promise.resolve()](#top) :grey_exclamation: <b id="resolve"></b>
`有时需要将现有对象转为 Promise 对象，Promise.resolve方法就起到这个作用。`
* `参数是一个 Promise 实例`:`原封不动返回`
* `参数是一个thenable对象 thenable对象指的是具有then方法的对象，Promise.resolve方法会将这个对象转为 Promise 对象，然后就立即执行thenable对象的then方法。`
* `参数不是具有then方法的对象，或根本就不是对象 如果参数是一个原始值，或者是一个不具有then方法的对象，则Promise.resolve方法返回一个新的 Promise 对象，状态为resolved。`

* `不带有任何参数`:`Promise.resolve方法允许调用时不带参数，直接返回一个resolved状态的 Promise 对象。`

##### Promise.reject()
`Promise.reject(reason)方法也会返回一个新的 Promise 实例，该实例的状态为rejected。`

##### Promise.try() 
`database.users.get()可能还会抛出同步错误（比如数据库连接错误，具体要看实现方法），这时你就不得不用try...catch去捕获。`
```node
try {
  database.users.get({id: userId})
  .then(...)
  .catch(...)
} catch (e) {
  // ...
}
```
`上面这样的写法就很笨拙了，这时就可以统一用promise.catch()捕获所有同步和异步的错误。`
```node
Promise.try(database.users.get({id: userId}))
  .then(...)
  .catch(...)
```














