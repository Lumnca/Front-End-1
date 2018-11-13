 [Node 文件处理与读写](#top) <b id="top"></b>:maple_leaf:
 ----
`在客户端javascript脚本代码中，对于二进制数据并没有提供一个很好的支持。然后在nodejs中需要处理像TCP流或文件流时，必须要处理二进制数据。因此
在node.js中，定义了一个Buffer类，该类用来创建一个专门存放二进制数据的缓存区。` [`官方文档`](https://nodejs.org/dist/latest-v10.x/docs/api/fs.html)

- [x] [`文件读写模式`](#flag) :maple_leaf:
- [x] [`读取文件内容`](#read) :maple_leaf:
- [x] [`内容写入文件`](#write) :maple_leaf:
- [x] [`追加文件内容`](#append) :maple_leaf:
- [x] [`c语言读取方式`](#cread) :maple_leaf:

#### [零. 文件读写模式](#top) <b id="flag"></b>:maple_leaf:
`读写文件的option 选项里面的flag 属性的配置选项`

|模式 |说明 |
|:---:|:----|
|`r`  | `读取文件。如果文件不存在时抛出异常`|
|`r+` | `读取并写入。如果文件不存在时抛出异常`|
|`rs` | `以同步方式读取文件并通知操作系统忽略本地文件系统缓存。如果文件不存在时抛出异常`|
|`w`  | `写入文件。如果文件不存在时则创建该文件。如果文件已存在则清空文件内容`| 
|`w+` | `读取并写入文件。如果文件不存在时则创建该文件。如果文件已存在则清空文件内容`| 
|`wx` | `作用与”w”类似。但是以排他方式打开文件`| 
|`wx+`| `作用与”w+”类似。但是以排他方式打开文件`| 
|`a`  | `以追加方式写入文件。如果文件不存在时则创建该文件`| 
|`a+` | `读取并以追加方式写入文件。如果文件不存在时则创建该文件`|
|`ax` | `作用与”a”类似。但是以排他方式打开文件`|
|`ax+`| `作用与”a+”类似。但是以排他方式打开文件`|
 
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
#### [二. 内容写入文件](#top) <b id="write"></b>:maple_leaf: 
[`异步函数`](#top)
* `fs.writeFile(file, data[, options], callback)`:`异步方法`
   * `file <string> | <Buffer> | <URL> | <integer> filename or file descriptor`
   * `data <string> | <Buffer> | <TypedArray> | <DataView>`
   * `options <Object> | <string>`
     * `encoding <string> | <null> Default: 'utf8'`
     * `mode <integer> Default: 0o666`：`1.执行权限 2.写权限 4.读权限`
     * `flag <string> See support of file system flags. Default: 'w'.`
  * `callback <Function>`
     * `err <Error>`
```node
try{
    console.log("--写入文件--");
    fs.writeFile("./content/write.txt","这是文件的内容哦",{ flag:"w",encoding:"utf8" },function (err) {
        if(err){
            console.warn("--写入错误--");
        }else{
            console.log("--写入成功--");
        }
    });
}catch (e) {
    console.log(e);
}
```
`如果把flag 改为 a 那么就是追加文件`
[`同步函数`](#top)
* `fs.writeFileSync(file, data[, options])`
```node
try{
    fs.writeFileSync("./content/write.txt","同步写入文件内容这是",{
        encoding:"utf8",
        flag:"a"
    })
}catch (e) {
    console.log(e);
}
```
#### [三. 追加文件内容](#top) <b id="append"></b>:maple_leaf: 
`追加文件内容,`
`fs.appendFile(path, data[, options], callback)`
  * `callback <Function>`:`function(err)`
```node
try{
    fs.appendFile("./content/write.txt","追加 追加 追加",{
        encoding:"utf8",
    },function (err){
        if(err) console.log("错误信息");
    });
}catch (e) {
    console.log(e);
}
```
[`同步函数`](#top)
* `fs.appendFileSync(path, data[, options])`
```node
try{
    fs.appendFileSync("./content/write.txt","我..............................");
}catch (e) {
    console.log(e);
}
```
#### [四. c语言读取方式](#top) <b id="cread"></b>:maple_leaf: 
`node 也可以读取指定位置的文件内容,指定写入位置,但是不推荐使用` [官方文档](https://nodejs.org/dist/latest-v10.x/docs/api/)
* `fs.open(path, flags[, mode], callback)`
* `fs.openSync(path, flags[, mode])`
* `fs.read(fd, buffer, offset, length, position, callback)`
* `fs.write(fd, buffer[, offset[, length[, position]]], callback)`
* `fs.write(fd, string[, position[, encoding]], callback)`
* `fs.close(fd, callback)`
* `fs.closeSync(fd)`
