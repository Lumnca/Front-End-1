<a id="top" href="#top">Node 注意问题  :maple_leaf:</a> 
----
- [x] :maple_leaf: <a href="#NodeServer">`Node 编码问题`</a>
- [x] :maple_leaf: <a href="#returnHtml">`返回一个html页面`</a>

#####  <a id="NodeServer" href="#NodeServer">Node 编码问题</a>  :star2: <a href="#top"> :arrow_up: </a>
`服务器默认编码是utf-8编码,但是浏览器不知道你是utf-8 浏览器在不知道的情况下会按照当前操作系统的编码解析,然而很多
的中文操作系统支持的gbk 所以可能会产生乱码问题`
* `设置http 请求编码格式`
   * `response.setHeader("Content-Type","text/plain;charset=utf-8"); `
```javascript
let http = require('http');

let server = http.createServer();

server.on('request',function (request,response) {
    if(request.url!=='/favicon.ico'){
        //设置http响应头部
        response.setHeader("Content-Type","text/plain;charset=utf-8");
        response.end("你好啊！小伙子！看的清楚不");
        //浣犲ソ鍟婏紒灏忎紮瀛愶紒鐪嬬殑娓呮涓� 不加就是乱码
    }
});

server.listen(8080,function () {
    console.log("Server Running");
});
```
* `response.end(data); 支持两种数据类型,二进制 字符串`
* `图片不需要支持编码`

#####  <a id="returnHtml" href="#returnHtml">返回一个html页面</a>  :star2: <a href="#top"> :arrow_up: </a>
`返回一个html 文件还有依赖 css png`

```shell
Content/
fonts/
history/
modules/
Resources/  
Scripts/  
views/
myServer.js  
```

```javascript
let http = require('http');
let fs = require('fs');
let server = http.createServer();

server.on('request',function (request,response) {
    if(request.url!=='/favicon.ico'){
        //设置http响应头部
        let $url = request.url;
        let path = "."+ $url;
        console.log(path);
        fs.readFile(path,function (error,data) {
            if(!error){
                if($url.startsWith('/Content')){
                    response.setHeader("Content-Type","text/css;charset=utf-8");
                    response.end(data);
                }
                else if($url.startsWith('/Resources')){
                    response.end(data);
                }
                else if($url.startsWith('/views')){
                    response.setHeader("Content-Type","text/html;charset=utf-8");
                    response.end(data);
                }else{
                    response.end("无效请求 404");
                }
            } else{
                response.end("错误路径:"+error.path);
            }
        });
    }
});

server.listen(8080,function () {
    console.log("Server Running");
});
```
