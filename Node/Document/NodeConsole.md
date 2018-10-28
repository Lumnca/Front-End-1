<a href="#top" id="top" >Node 中的控制台 :maple_leaf:</a>
-----
`运用console命令将信息输入到控制台中`

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
