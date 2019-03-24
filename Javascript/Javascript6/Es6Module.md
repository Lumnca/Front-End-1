### [ES6 Module加载语法 :speech_balloon: ](#top) <b id="top"></b>

----
`偶尔写一点笔记! 打发郁闷时光`:grey_exclamation:

- [x] [`0.环境配置`](#target0) :arrow_lower_left:
- [x] [`1.module 说明`](#target1) :arrow_lower_left:
- [x] [`2.export 命令: 导出模块信息`](#target2) :arrow_lower_left:
- [x] [`3.import 命令: 导入模块信息`](#target3) :arrow_lower_left:


----
##### [0.环境配置](#top) <b id="target0"></b>

```json
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

`rollup.config.js`
```node
export default {
    input: './src/index.js',
    output: {
        file: './src/rollupjs/index.bundle.js',
        format: 'iife'
    }
}
```

`webpack.config.js`
```javascript
const path = require('path');
const webpack = require('webpack');

module.exports = {
    devtool: 'source-map', //正常打包请换为: eval
    entry: {
        index: './src/index.js'
    },
    devServer:{
        contentBase: './dist'
    },
    mode: 'development', //mode: 'production',
    output: {
        filename: '[name].bundle.js',
        path: path.resolve(__dirname, 'dist/script')
    },
    module: {
        rules: [{
            test: /\.js$/,
            exclude: /(node_modules)/,
            use: {
                loader: 'babel-loader',
                options: {
                    presets: ['env']
                }
            }
        }]
    },
    plugins: [
        new webpack.BannerPlugin({ //这是webpack内置的插件，所以不用require导入，但是对于第三方插件要先导入
            banner: 'sicnu version 1.2.0.0 \nserver 2019~2021 LTS\nauthors jxkicker,lmc'
        })
    ]    
};
```

##### [1.module 说明](#top) <b id="target1"></b>
`ES6 的模块自动采用严格模式，不管你有没有在模块头部加上"use strict";`
`严格模式主要有以下限制。`

* `1.变量必须声明后再使用`
* `2.函数的参数不能有同名属性，否则报错`
* `3.不能使用with语句`
* `4.不能对只读属性赋值，否则报错`
* `5.不能使用前缀 0 表示八进制数，否则报错`
* `6.不能删除不可删除的属性，否则报错`
* `7.不能删除变量delete prop，会报错，只能删除属性delete global[prop]`
* `8.eval不会在它的外层作用域引入变量`
* `9.eval和arguments不能被重新赋值`
* `10.arguments不会自动反映函数参数的变化`
* `11.不能使用arguments.callee`
* `12.不能使用arguments.caller
* `13.禁止this指向全局对象`
* `14.不能使用fn.caller和fn.arguments获取函数调用的堆栈`
* `15.增加了保留字（比如protected、static和interface）`

`其中，尤其需要注意this的限制。ES6 模块之中，顶层的this指向undefined，即不应该在顶层代码使用this。`

##### [2.export 命令: 导出模块信息](#top) <b id="target2"></b>
`一个模块就是一个独立的文件。该文件内部的所有变量，外部无法获取。如果你希望外部能够读取模块内部的某个变量，就必须使用export关键字输出该变量。
下面是一个 JS 文件，里面使用export命令输出变量。`

`1.边声明边导出 ` `但是 export 1; 是不被允许的`
```javascript
export var firstName = 'Michael';
export var lastName = 'Jackson';
export var year = 1958;

export function multiply(x, y) {
  return x * y;
};
```
`2.也可以是这样写 先声明后导出 但是必须写在大括号中`
```node
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;

function multiply(x, y) {
  return x * y;
};
export {firstName, lastName, year,multiply};
```

##### :one: as 关键字
`如果你不想暴露模块中引用的内部名称 你可以使用 as 重命名`

```node
function v1() { ... }
function v2() { ... }

export {
  v1 as streamV1,
  v2 as streamV2,
  v2 as streamLatestVersion
};
```
##### :two: default 命令
`有的时候我们仅仅使用一个js 文件导出一个对象或者一个函数,那么名称对于这个模块其实不那么重要`

`func.js`
```node
export default function () {
  console.log('foo');
}
```
`obj.js`
```node
export default {
    input: './src/index.js',
    output: {
        file: './src/rollupjs/index.bundle.js',
        format: 'iife'
    }
}
```

`再引入的地方你可以适宜任何名称接受这个导出的对象或者函数`
```node
import func_foo from './func.js'
import obj_ from './obj.js'
```

##### :three: const 模块导出常量
`那么这一个值要被多个模块共享`
```node
// constants.js 模块
export const A = 1;
export const B = 3;
export const C = 4;
```

##### [3.import 命令: 导入模块信息](#top) <b id="target3"></b>
`使用export命令定义了模块的对外接口以后，其他 JS 文件就可以通过import命令加载这个模块。`

```node
import {firstName, lastName, year} from './profile.js';

function setName(element) {
  element.textContent = firstName + ' ' + lastName;
}
```
`如果值导出一个对象或者方法`
```node
import add from "./devTool.js"
import SystemInfo  from "./models/system"
```

##### :one: 如果导出是默认 default
`可以使用任何名称接受`
```node
//user.js
export default {
    name:"wangzhe",
    age:18
}
```

```node
import user from "./models/user"
```
`如果导入的模块既有 default 也有其他接口 那么得到导出的default的方法是` `import { default as foo } from 'modules';`

##### :two: 整体加载模块
`除了指定加载某个输出值，还可以使用整体加载，即用星号（*）指定一个对象，所有输出值都加载在这个对象上面。`
```node
import * as circle from './circle';
```
`模块整体加载所在的那个对象（上例是circle），应该是可以静态分析的，所以不允许运行时改变。你懂的函数不能赋值一个变量`

```node
import * as circle from './circle';

// 下面两行都是不允许的
circle.foo = 'hello';  //foo 是一个函数
circle.area = function () {}; //area 也是一个函数
```


















