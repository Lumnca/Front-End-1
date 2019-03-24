#### [webpack-dev-server 使用](#top) :speech_balloon:

----
`webpack-dev-server 为你提供了一个简单的 web 服务器，并且能够实时重新加载(live reloading)。小型的Node.js Express服务器,它使用
webpack-dev-middleware来服务于webpack的包,除此自外，它还有一个通过Sock.js来连接到服务器的微型运行时.`

- [x] [`参考资料`](https://segmentfault.com/a/1190000012536871)

`安装`
```node
npm install --save-dev webpack-dev-server
```
`可以通过指定 content-base 来修改这个默认行为`

##### 1.简单的配置信息
`webpack-dev-server 默认会以当前目录为基本目录,除非你制定它.`
```node
devServer:{
    contentBase: './dist',
    port: 9000, //端口改为9000
    open:true // 自动打开浏览器，适合懒人,
    compress:true, //压缩
    index:'front.html', // 与HtmlWebpackPlugin中配置filename一样
    inline:true, //默认为true, 意思是，在打包时会注入一段代码到最后的js文件中，用来监视页面的
     //改动而自动刷新页面,当为false时，网页自动刷新的模式是iframe，也就是将模板页放在一个frame中
}
```

`通过命令使用`:`webpack-dev-server --content-base build/`

##### 2.自动刷新
`webpack-dev-server支持两种模式来自动刷新页面`
* `iframe模式 (页面放在iframe中,当发生改变时重载)`
* `inline模式 (将webpack-dev-sever的客户端入口添加到包(bundle)中)`

##### 3.启动命令
`package.json 中添加一条命令`:`"start": "webpack-dev-server --open"`
```javascript
{
  "name": "es6-demo",
  "version": "1.0.0",
  "description": "vue demo ready",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "product": "webpack --mode=production",
    "dev": "webpack --mode=development",
    "rollup": "rollup -c",
    "build": "webpack",
    "watch": "webpack --watch",
    "start": "webpack-dev-server --open"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "babel": "^6.23.0",
    "babel-core": "^6.26.3",
    "babel-loader": "^7.1.5",
    "babel-preset-env": "^1.7.0",
    "rollup": "^1.7.0",
    "webpack": "^4.29.6",
    "webpack-cli": "^3.3.0",
    "webpack-dev-server": "^3.2.1"
  }
}

```
