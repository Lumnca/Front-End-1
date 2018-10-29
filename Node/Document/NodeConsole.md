<a href="#top" id="top" >Node 中的控制台 :maple_leaf:</a>
-----
`运用console命令将信息输入到控制台中`

- [x] :maple_leaf: `console.log()`
- [x] :maple_leaf: `console.dir()`
- [x] :maple_leaf: `console.error()`
- [x] :maple_leaf: `console.warn()`
- [x] :maple_leaf: `console.time()`
- [x] :maple_leaf: `console.timeEnd()`
- [x] :maple_leaf: `console.trace()`
- [x] :maple_leaf: `console.assert()`

----
* `1 代表重定向标准输出流,将myConsole里面是有console输出的信息 放到log.txt 里面去`
```node
node myConsole.js 1>log.txt

//逗号隔开 输出
console.log("hide","what",2);//hide what 2
```
#### 1.[console.error/console.warn](#)
`输出错误 警告信息,字体变色 红色,两者区别没有 可以相互代替`
```javascript
console.error("path is error");
```
#### 2.[console.dir](#)
`console.dir 方法阿用于查看一个对象中的内容并且将该对象的信息输出到控制台中`
```javascript
let person = {
    name:"Kicker",
    age:17,
    sex:true
}

console.dir(person);
```
#### 3.[console.time(lable)/console.timeEnd(lable)](#)
`当需要统计一段代码的执行时间的时候,可以使用这个两个方法,它会将结束时间与开始时间之间经过的毫秒数返回,但是他们需要一个`
```javascript
console.time("lable");
let person = {
    name:"Kicker",
    age:17,
    sex:true
}

console.dir(person);

console.timeEnd("lable");
/**
{ name: 'Kicker', age: 17, sex: true }
lable: 3.723ms
**/
```
#### 4.[console.trace(lable)](#)
`使用任何一个字符串,用于将当前位置处的堆栈信息打印出来,作为标准错误信息进行输出`
```javascript
console.time("lable");
let person = {
    name:"Kicker",
    age:17,
    sex:true
}
console.dir(person);
console.timeEnd("lable");
console.trace("lable");
//输出 堆栈信息
{ name: 'Kicker', age: 17, sex: true }
lable: 24.730ms
Trace: lable
    at Object.<anonymous> (D:\Users\Kick\WebstormProjects\node-wordspace\learing\myConsole.js:15:9)
    at Module._compile (internal/modules/cjs/loader.js:689:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:700:10)
    at Module.load (internal/modules/cjs/loader.js:599:32)
    at tryModuleLoad (internal/modules/cjs/loader.js:538:12)
    at Function.Module._load (internal/modules/cjs/loader.js:530:3)
    at Function.Module.runMain (internal/modules/cjs/loader.js:742:12)
    at startup (internal/bootstrap/node.js:279:19)
    at bootstrapNodeJSCore (internal/bootstrap/node.js:752:3)
```
#### 4.[console.assert(boolean 表达式,错误信息)](#)
`用于对一个表达式的执行结果进行评估,如果表达式的执行结果为false,则输出一个消息字符串并抛出一个AssertionError 异常`
```javascript
let person = {
    name:"Kicker",
    age:17,
    sex:true
}
console.assert(person.name == "Jake","this name is error");
console.dir(person);
/*
Assertion failed: this name is error
{ name: 'Kicker', age: 17, sex: true }
*/
```
