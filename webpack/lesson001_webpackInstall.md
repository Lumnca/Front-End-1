### [Webpack 安装使用](#top) :maple_leaf: <b id="top"></b>

----
:white_check_mark: `Webpack 的入门使用方式 在开始之前，请确保安装了 Node.js 的最新版本。使用 Node.js 最新的长期支持版本(LTS - Long Term Support)，是理想的起步`
- [x] :maple_leaf: [`命令行安装`](#install) 
- [x] :maple_leaf: [`起步咯`](#start) 

#### [(一.1).命令行安装](#top) <b id="install"></b> :maple_leaf:
`-g 是全局安装的意思`
```npm
 cnpm install webpack -g
 
 webpack -v //查看安装的版本
```

##### [(一.2)本地安装](#top)
`要安装最新版本或特定版本，请运行以下命令之一：`
```npm
npm install --save-dev webpack
npm install --save-dev webpack@<version>
```
`如果你使用 webpack 4+ 版本，你还需要安装 CLI。`
```npm
npm install --save-dev webpack-cli
```
`对于大多数项目，我们建议本地安装。这可以使我们在引入破坏式变更(breaking change)的依赖时，更容易分别升级项目。通常，webpack 通过运行一个或多个 npm scripts，会在本地 node_modules 目录中查找安装的 webpack：`
```node
"scripts": {
    "start": "webpack --config webpack.config.js"
}
```
> `当你在本地安装 webpack 后，你能够从 node_modules/.bin/webpack 访问它的 bin 版本。`
##### [(一.3).基本配置](#top) :maple_leaf:
`webpack --mode production` :`打包成一行  生产环境`<br/>
`webpack --mode development`：`打包就可以了,开发环境`

#### [(二. 1).起步咯-初次使用webpack](#top) <b id="start"></b> :maple_leaf:
(1).首先我们创建一个目录，初始化 npm，然后 在本地安装 webpack，接着安装 webpack-cli（此工具用于在命令行中运行 webpack）：
```linux
mkdir install && cd webpack-demo
npm init -y
npm install webpack webpack-cli --save-dev
```
(2).现在我们将创建以下目录结构、文件和内容：<br/>
![基本使用](/Resources/webpack/exmaple.png)

(3).Person.js
```node
function Person(name,age,sex){
    this.name = name;
    this.age = age;
    this.sex = sex;
}
Person.prototype.toString = function(){
    return `name:${this.name} age:${this.age} sex:${this.sex}`;
}
export default Person;
```
(4).address.js
```node
function address(states,street,code,province = "Sichuan",country = "China"){
    this.country = country;
    this.states = states;
    this.province = province;
    this.states = states;
    this.street = street
    this.code = code;
}

export default address;
```
(5).index.js
```node
import Person from "./compiler/address"
import address from "./compiler/person"

let person1 = new Person("jxKicker",18,true);
let person2 = new Person("RRlover",15,false);

let adr = new address("GA-YC","XinFen",8341);


console.log(person1);
console.log(person2);

console.log(adr);
```
(6).package.json
```json
{
  "name": "install",
  "version": "1.0.0",
  "description": "",
  "main": "main.js",
  "scripts": {
    "dev": "webpack --mode development",
    "build": "webpack --mode production"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "webpack": "^4.26.0",
    "webpack-cli": "^3.1.2"
  }
}

```
(7).index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    
</body>
<script src="main.js"></script>
</html>
```
(8).组织好文件后运行 npm run build 打包完成  dist文件夹里面生成一个 main.js
