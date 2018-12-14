### [JavaScript6 Promise 异步编程](#top) :grey_question: <b id="top"></b>

----
:star: [`Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。它由社区最早提出和实现，ES6 将其写进了语言标准，统一了
用法，原生提供了Promise对象`](#top)

---
- [x] [Promise 介绍](#intro)
- [x] [Promise 基操](#use)


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
`让我们来写一个Promise 吧 Promise 操作声明完立即执行`
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
* `执行 new Promise 里面的代码`
* `执行器 一看到 then 方法 执行下面的代码 吧 Promise里面执行代码 丢给其他线程执行 `
* `执行Promise 下面的代码`
* `转到..异步线程 执行异步代码 执行完成后..`
* `如果成功 执行 resolve`
* `如果失败 执行 reject`

##### 将Promise 作为返回值













































