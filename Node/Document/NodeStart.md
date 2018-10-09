<a id="top" href="#top">Node 起步  :maple_leaf:</a> 
----
`让我们把环境搭建起来,运行起来一个node,其他的Node的历史,还有各种原因请查看Node的书籍,这里是记录干货,笔记`
- [x] :maple_leaf: <a href="#InstallNode">`Node 环境`</a>
- [x] :maple_leaf: <a href="#NodeServer">`Node Web Server`</a>

####  <a id="InstallNode" href="#InstallNode">Node 环境</a>  :star2: <a href="#top"> :arrow_up: </a>
`请自行安装node 环境直到在命令行中 有如下反应 版本不限制... 这代表node环境已经有了`
```shell
node -v
v10.11.0
npm -v
6.4.1
```
`新建一个index.js文件里面输入一些js代码`
```javascript
 var age = 18;
 console.log("你好啊");
 console.log("age:"+age);
```
`命令行中运行,请到文件的目录下面(Shift+右键  就会有在此打开命令行) 运行 node index.js 就会看到结果 `<br/>'

####  <a id="InstallNode" href="#NodeServer">Node Web Server</a>  :star2: <a href="#top"> :arrow_up: </a>
`让我们跑起来一个简单的web请求页面`<Br/>
`替换index.js代码为如下：`
```javascript
var http = require('http');
http.createServer(function(request,response){
    //创建一个web服务器
    //处理服务器请求 并返回响应
    response.writeHead(200,{"Content-Type":"text/html; charset=utf-8" })
    if(request.url!=='/favicon.ico'){
        //清楚二次访问 没有这个判断 那么回请求两次 第二次去请求 favicon.ico
        response.write(" hello world.......");
        console.log("using...");
        response.end(".....end world"); //结束响应
        // end response 
    }
}).listen(8080);
// listem 8080

console.log("hello the world run on server open http://localhost:8080");
```
`再次运行这个文件 node index.js 打开浏览器,访问 http://localhost:8080/` `然后你就会发现新的大陆.一个新的创建web服务的方式`
