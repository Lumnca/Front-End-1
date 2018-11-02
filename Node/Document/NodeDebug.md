[Node.js中使用调试器](#top) <b id="top"></b>:maple_leaf:
----
`Node.js 提供了一个在命令行界面中可以使用的调试器,可以利用该调试器来进行一些应用程序的简单调试` `使用` `node debug xxx.js` `启动调试`
- [x] [`使用VsCode 调试 Node.js`](#vscodedebug)
- [x] [`使用命令行调试 Node.js`](#usecodelinedebug)
  - [`c/cont`](#codecontinue)
  - [`n/next`](#codenext)
  - [`s/step`](#codestep)
  - [`o/out`](#codeout)
  - [`watch/unwatch`](#codewatch)
  - [`sb/setBreakpoint`](#setbreakpoint)
  - [`cb/clearBreakpoint`](#clearbreakpoint)

##### [使用VsCode 调试Node.js](#top) <b id="vscodedebug"></b>
`这个实在是很简单的,Vscode 提供了一个十分友好的Node调试功能,只要学会使用它,就可以满足Node调试的大部分需求,而且操作很简单,添加监视,断点`
`例如如下所示`
![Nodedebug](/Resources/NodeImage/vscodedebug.png)

##### [使用命令行调试 Node.js](#top) <b id="usecodelinedebug"></b>
`但是当你再linux 命令行编程的时候,或者特殊需要学会命令行调试也是很重要的。`
```node
//文件名:app.js
console.log("start to run");

function foo() {
    console.log('hello foo');
    return 100;
}
let bar  = "this is a pen";
console.log(bar);
let http = require("http");
let i = foo();
console.log(i);

```
* `打开命令行 输入 node debug app.js`
```javascript
PS E:\nodejs-workspace\study> node debug app.js
(node:756) [DEP0068] DeprecationWarning: `node debug` is deprecated. Please use `node inspect` instead.
< Debugger listening on ws://127.0.0.1:9229/8530d637-6ab2-44ae-86fa-c676c32abdfb
< For help, see: https://nodejs.org/en/docs/inspector
Break on start in app.js:1
> 1 (function (exports, require, module, __filename, __dirname) { console.log("start to run");
  2
  3 function foo() {
debug>
```
###### [c/ cont [continue]](#top) <b id="codecontinue"></b>
`输入` `c` 或者 `cont` `继续执行被暂停的脚本 它将会一直执行到断点处,也就是说没有断点的话,那么程序直接执行到最后面` 
###### [n/ next [next]](#top) <b id="codenext"></b>
`如果要执行到下一条语句的地方,而不是一下执行完输入 ` `n` `输入n 他就是一条一条执行的`
```node
PS E:\nodejs-workspace\study> node debug app.js
(node:11396) [DEP0068] DeprecationWarning: `node debug` is deprecated. Please use `node inspect` instead.
< Debugger listening on ws://127.0.0.1:9229/65f0b55a-dd53-4af1-b8fb-77a24c5acd74
< For help, see: https://nodejs.org/en/docs/inspector
Break on start in app.js:1
> 1 (function (exports, require, module, __filename, __dirname) { console.log("start to run");
  2
  3 function foo() {
debug> n
break in app.js:1
> 1 (function (exports, require, module, __filename, __dirname) { console.log("start to run");
  2
  3 function foo() {
debug> n
< start to run
break in app.js:7
  5     return 100;
  6 }
> 7 let bar  = "this is a pen";
  8 console.log(bar);
  9 let http = require("http");
debug> n
break in app.js:8
  6 }
  7 let bar  = "this is a pen";
> 8 console.log(bar);
  9 let http = require("http");
 10 let i = foo();
```
###### [s/step](#top) <b id="codestep"></b>  
`使用` `s` `或` `step` `命令可是进入函数内部 然后就可以在函数内部 单步调试了`
###### [o/out](#top) <b id="codeout"></b>  
`如果需要立即执行完函数内部的所有代码 跳出函数 可以使用这个` `o` `或` `out`
###### [watch/unwatch(#top)](#top) <b id="codewatch"></b>  
`如果你需要监视某个变量或者 变量表达式 你可以这样 在调试开始的时候 添加监视 也可以取消监视`
```node
watch('i')
watch('i==100')

unwatch('i==100') 一旦查看到结果也可以取消监视
```
```node
PS E:\nodejs-workspace\study> node debug app.js
(node:1540) [DEP0068] DeprecationWarning: `node debug` is deprecated. Please use `node inspect` instead.
< Debugger listening on ws://127.0.0.1:9229/08253620-b94f-43fa-8af9-a08b2f415404
< For help, see: https://nodejs.org/en/docs/inspector
Break on start in app.js:1
> 1 (function (exports, require, module, __filename, __dirname) { console.log("start to run");
  2
  3 function foo() {
debug> watch('i')
debug> watch('i==10')
debug> n
break in app.js:1
Watchers:
  0: i = undefined
  1: i==10 = false

> 1 (function (exports, require, module, __filename, __dirname) { console.log("start to run");
  2
  3 function foo() {
debug> n
< start to run
break in app.js:7
Watchers:
  0: i = undefined
  1: i==10 = false

  5     return 100;
  6 }
> 7 let bar  = "this is a pen";
  8 console.log(bar);
  9 let http = require("http");
  
  ....
  debug> n
< hello foo
break in app.js:11
Watchers:
  0: i = 100
  1: i==10 = false

  9 let http = require("http");
 10 let i = foo();
>11 console.log(i);
 12
 13
debug> unwatch('i==10')
debug> n
< 100
break in app.js:15
Watchers:
  0: i = 100

 13
 14
>15 });
  ....
```
##### [sb/setBreakpoint](#top) <b id="setbreakpoint"></b>
`设置断点` `sb(filename,line)` `在debug中使用`

##### [cb/clearBreakpoint](#top) <b id="clearbreakpoint"></b>
`取消断点` `cb(filename,line)`
`取消断点`
