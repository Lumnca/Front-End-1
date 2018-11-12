 [Node 文件处理与读写](#top) <b id="top"></b>:maple_leaf:
 ----
`在客户端javascript脚本代码中，对于二进制数据并没有提供一个很好的支持。然后在nodejs中需要处理像TCP流或文件流时，必须要处理二进制数据。因此
在node.js中，定义了一个Buffer类，该类用来创建一个专门存放二进制数据的缓存区。` [`官方文档`](https://nodejs.org/dist/latest-v10.x/docs/api/fs.html)

- [x] [`读取文件内容`](#read) :maple_leaf:

#### [一. 读取文件内容](#top) <b id="read"></b>:maple_leaf: 
`读取文件内容有两种方法,同步读取,异步读取`
* `同步读取的意思就是,在执行这段代码的时候,下面的代码无法执行`
* `异步读取,采用回调函数,读取文件的时候,下面的代码任然可以执行`
#### [一.1 读取函数](#top)
[`异步函数`](#top)
* `fs.readFile(path[, options], callback)`:`路径 配置选项 回调函数`
  * `path <string> | <Buffer> | <URL> | <integer> filename or file descriptor`
  * `options <Object> | <string>`
     * `encoding <string> | <null> Default: null` :`编码方式`
     * `flag <string> See support of file system flags. Default: 'r'.` `读取方式 有 r r+ w w+ wx rs.....类似于c++ c`
  * `callback <Function>(err,data)`
    * `err <Error>`:`错误对象`
    * `data <string> | <Buffer>`
<br/>

`err 对象内容:`

```node
{ 
 [Error: ENOENT: no such file or directory, open 'E:\nodejs-workspace\study\content\reads.txt'] //错误原因
  errno: -4058, //编号
  code: 'ENOENT', //代码
  syscall: 'open', 
  path: 'E:\\nodejs-workspace\\study\\content\\reads.txt' //错误路径
}
```

`读取代码`
```node
let fs = require('fs');

fs.readFile("./content/read.txt",{ flag:"r", encoding:"utf-8"},function (err,data) {
    if(err){
        console.warn(err);
    }else{
        console.log("1---------------------------------内容如下-----------------------------------1");
        console.log(data);
        console.log("1---------------------------------读取完成-----------------------------------1");
    }
});
//异步方法  下面的代码先执行完 
console.log("--------------------------------正在读取文件----------------------------------");
console.log("...");
console.log("...");
```
[`同步函数`](#top)
* `fs.readFileSync(path[, options])`
   * `path <string> | <Buffer> | <URL> | <integer> filename or file descriptor`
   * `options <Object> | <string>`   
      * `encoding <string> | <null> Default: null`
      * `flag <string> See support of file system flags. Default: 'r'.`
   * `Returns: <string> | <Buffer>`
```node
try{
    console.log("--------------------------------------------------------------------同步方法开始读取")
    console.time("sync");
    let data =  fs.readFileSync("./cosntent/read.txt",{ flag:"r", encoding:"utf-8"});

    console.log(data);
    console.log("--------------------------------------------------------------------同步方法读取完毕");
    console.timeEnd('sync');
}catch (e) {
    console.log(e);
}
```
`同步方法为了安全 应该放在 try catch 文件中 可以检测到错误异常,因为同步方法没有回调函数 直接返回读取结果`













