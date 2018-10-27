<a id="top" href="#top">Node 小例子  :maple_leaf:</a> 
----
`运用node做一些简单的事情,来认识 体验node`
##### [`1.运用node 读取文件`](#)
* `首先加载文件模块 var fs = require('fs');  `
* `fs.readFile(path,function(error,data))`
  * `读取成功error 为null 返回数据  否则 data 为null 返回 error 错误对象`
```javascript
var fs = require('fs');
fs.readFile("./Resources/val2.json",function(error,data){
    if(!error){
        console.log("读取文件内容:");
        console.log("--------------------------")
        console.log(data.toString());
    }else{
        console.log(`错误路径: ${error.path} [文件不存在]`);
    }
    //默认文件中存储二进制 返回二进制转换为十六进制
}); 
console.log('run node');
```
* `读出来的数据是 二进制的 所以要用toString 方法转换为我们认识的文字`
* `error 是一个对象有许多的信息和属性`
##### [`2.运用node 写入文件`](#)
`运行 node 写入文件 `
```javascript
var name = "JiangXing";
var age = 18;
var data = `My name is ${name} and my age is ${age}`;

fs.writeFile('./Resources/my.txt',data,function(error){
    if(!error){
        console.log("文件写入成功");
    }
})
```
##### [`3.做一个简单的http 服务`](#)
```javascript
var http = require('http');
var fs=require('fs');
var server = http.createServer(); 

//浏览器处理请求事件绑定
server.on('request',function(){
    //记录日志文件
    let time = new Date();
    let ti = time.toLocaleString();
    fs.writeFile('./Resources/log.txt',`陌生用户登录 ${ti}`,function(error){
        if(error){
            console.log('错误:'+error.path);
        }
    });
});

server.listen(8088,function(){
    console.log('服务器开始启动！');
}); //端口号

```
* `它只处理请求,但是不返回信息`
* `Request` `请求对象`
   * `请求对象可以用来获取客户端的一些请求信息,例如请求路径`
* Response 响应对象
   * `响应对象可以用来给客户端发送响应信息`
```javascript
server.on('request',function(Request,Response){
    //记录日志文件
    let time = new Date();
    let ti = time.toLocaleString();
    fs.writeFile('./Resources/log.txt',`陌生用户登录 ${ti} 请求路径 ${Request.url}`,function(error){
        if(error){
            console.log('错误:'+error.path);
        }
    });
    /* 处理事务 */

});
```

##### [`4.返回响应`](#)
* `发出响应,但是必须调用end 方法 结束响应不然浏览器会一直等待`
```javascript
server.on('request',function(Request,Response){
    //记录日志文件
    let time = new Date();
    let ti = time.toLocaleString();
    fs.writeFile('./Resources/log.txt',`陌生用户登录 ${ti} 请求路径 ${Request.url}`,function(error){
        if(error){
            console.log('错误:'+error.path);
        }
    });

    console.log("请求路径:"+Request.url);

    /* 处理事务 */

    Response.write("Hello World");
    Response.end("");
});
```
*  响应内容只能是二进制数据或者字符串 对于数字 对象 数组 布尔值 都不行
##### [`5.请求路径`](#)
* `所有的请求路径都以/开始`
* `request.url 可以获得请求路径`
```javascript
let http = require('http');

let server = http.createServer();

server.on('request',function (request,response) {
    if(request.url!=='/favicon.ico'){
        response.end("end world!");
        let $url = request.url;
        console.log($url);
    }
});

server.listen(8080,function () {
    console.log(" 服务启动 ");
});
```
##### [`node中的js`]()
* `EcmaScript`
  * `没有Bom Dom`
* `核心模块`
* `第三方模块`
* `用户自定义模块`
* `模块支持js多文件编程`
##### 核心模块
`Node为js 提供了很多服务器级别的API,这些API绝大多数都被包装到了一个具名的核心模块中了,例如文件操作 fs核心模块
http服务构建的http模块 ，path路径操作模块,os操作系统信息 模块`
* `加载模块`
```javascript
var fs = require('fs');
var http = require('http');

let os = require('os');

console.log(os.cpus());//获取cpu的信息
```
##### [`模块 加载用户自定义模块`](#)
`执行其他文件的js代码的方法`
`first.js`
```javascript
console.log("first start");

require("./modules/second.js");

console.log("first end");
```
`second.js`
```javascript
console.log("second script");
```
`node first.js`
```
first start
second script
first end
```
##### [`在node 中没有全局作用域,只有模块作用域`](#)
* `./ 不能省略 js后缀名可以省略`
fisrt.js
```javascript
console.log("first start");

var  age = 20;

require("./modules/second.js");

function add(a,b){
    return a+b;
}

console.log("first end");

console.log(age);
```
`second.js`
```javascript
console.log("second script");

var  age = 30;

console.log(add(10+20));
```
`node first.js`
```javascript
console.log(add(10+20)); add is not defined 报错
age 变量输出还是为20 
```
`两个文件 是两个不一样的作用域,执行环境不同 { first.js }  {seconf.js} 相当于在两个不同的函数内部执行,相互都是局部变量`

##### [`模块加载与导出`](#)
* `exports 导出`
* `require('path') 导入`
`first.js`
```javascript
let second = require('./modules/second');
console.log(second.user.name);
console.log(second.add(15,36));
```
`second.js`
```javascript
let  person = {
    name :"kicker",
    age:18,
    sex:true
};

function addtwo(one,two){
    return one + two;
}

exports.user = person;

exports.add = addtwo;
```
`node first.js`
```
kicker
51
```
