<a href="#top" id="top" >Node 中的全局变量,函数,对象 :maple_leaf:</a>
-----
`运用console命令将信息输入到控制台中`

##### [Node.js中的全局作用域和全局函数](#)
`虽然node 分模块的,存在模块作用域,在一个模块中定义的变量,函数和方法只能在该模块可以用,但可以通过exports对象的使用将其传递到模块底部,但是你会发现有些函数是每个模块都可以调用的,甚至不需要加载任何的的模块，在Node中任然存在一个全局作用域,既可以定义不需要通过任何模块加载就可以使用的函数 变量或类，
同时,也预先定义了一些全局方法和全局类,在Node中定义了一个Global 对象,代表Node的全局命名空间,任何全局变量,函数都是该对象的一个属性值`
```javascript
console.log(global);
//输出它,你会发现很多的变量和方法
```


##### [全局定时器](#)
`Node 中含定义了很多的全局函数`[`定时API官网文档`](https://nodejs.org/api/timers.html) `由于计时器函数是全局变量，因此无需调用require('timers')即可使用API。`
* `Class:Timeout`
    * `setTimeout(func,time,[args],[...])`
    * `timeout.ref()`:`返回：<Timeout>对引用timeout`
    * `timeout.refresh()`:`将计时器的开始时间设置为当前时间，并重新安排计时器以在之前指定的持续时间内调用其回调，并将其调整为当前时间。这对于在不分配新JavaScript对象的情况下刷新计时器非常有用。在已调用其回调的计时器上使用此选项将重新激活计时器。`
    * `timeout.unref()`:`调用时，活动Timeout对象不需要Node.js事件循环保持活动状态。如果没有其他活动使事件循环保持运行，则进程可以在Timeout调用对象的回调之前退出` `调用timeout.unref()创建一个内部计时器，它将唤醒Node.js事件循环。创建太多这些可能会对Node.js应用程序的性能产生负面影响。`
* `Class:Immediate`  
    * `immediate.hasRef()`
    * `immediate.unref()`:`Returns: <Immediate> a reference to immediate`
    * `immediate.ref()`:`Returns: <Immediate> a reference to immediate`
    * `immediate.setImmediate(callback[, ...args])`:`当进行多次调用时setImmediate()，callback函数按照创建顺序排队等待执行。每次事件循环迭代都会处理整个回调队列。如果立即计时器从执行的回调内部排队，则在下一个事件循环迭代之前不会触发该计时器。`
        * `callback <Function> 在Node.js事件循环本回合结束时调用的函数`
        * `...args <any>调用时传递的可选参数callback。`
        * `返回：<Immediate>用于clearImmediate()`
    * [`定时器nextTick()和setImmediate()区别`](https://www.jb51.net/article/57882.htm)    
    * ` 不要经常使用 unref ref 方法 可能会产生一些负面影响`
* `Class Interval`
    * `setInterval（callback，delay [，... args]）`
* `删除取消定时器`
    * `clearImmediate(immediate)`
    * `clearInterval(timeout)`
    * `clearTimeout(timeout)`
```javascript
let person = {
    name:"Kicker",
    age:17,
    sex:true
}

let timer = setTimeout(function () {
    console.log(person);
},2000,["a","b","c","d"]);

clearTimeout(timer);
```

`internal.js`
```javascript
let person = {
    name:"Kicker",
    age:17,
    sex:true
}

let timer = setTimeout(function () {
    console.log(person);
},2000,["a","b","c","d"]);


let interTimer =  setInterval(function () {
    console.log(arguments[0]);
},2000,"我是一个参数");



setTimeout(function () {
    clearInterval(interTimer);
},10000);

```


```javascript
setImmediate(function(){
    console.log("setImmediate延迟");
});
process.nextTick(function(){
    console.log("nextTick延迟")
});
console.log("正常执行");
```
`process.nextTick()中的回调函数执行的优先级要高于setImmediate()。这里的原因在于事件循环对观察者的检查是有先后顺序的，process.nextTick()属于
idle观察者，setImmediate()属于check观察者。在每一个轮循环检查中，idle观察者先于I/O观察者，I/O观察者先于check观察者。`

##### [与模块先关的全局函数及对象](#)
`在Node.js,可以使用require 函数来加载模块,代码如下` `加载一个自定义模块`<br/>

second.js
```javascript
let  person = {
    name :"kicker",
    age:18,
    sex:true
};

function addTwo(one,two){
    return one + two;
}

exports.user = person;
exports.add = addTwo;
```
app.ja
```javascript
let second = require('./modules/second');

console.log(second.user);
```
`其实每一个文件都是一个模块` `require.main 表示当前模块 主模块 也就是说执行模块 你可以 输出看一下` `console.log(require.main);`<br/>
模块加载的另一种写法
```javascript
module.exports = {
    user:{
        name :"kicker",
        age:18,
        sex:true
    },
    increse:4,
    add:function(one,two){
        return one + two + this.increse;
    }
};
```
##### [require.resolve](#)
`解析模块文件全部绝对路径:`

```javascript
let second = require('./modules/second');

console.log(require.resolve('./modules/second'));
//输出
D:\Users\Kick\WebstormProjects\node-wordspace\learing\modules\second.js
```
##### [require.cache 对象](#)
`它代表缓存了所有已被加载模块的缓冲区,在REPL 运行环境中 可是输出此对象 查看缓存内容`  `也可以通过delete 关键字删除缓存`
`cache可以是键值对的,通过访问模块 require.cache[require.resolve('./modules/second.js')];`
```javascript
delete require.cache[require.resolve('./modules/second.js')];
```




















