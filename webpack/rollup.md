### [Rollup 打包器](#top) :grey_exclamation: <b id="top"></b>
Rollup 是一个 JavaScript 模块打包器，可以将小块代码编译成大块复杂的代码，例如 library 或应用程序。Rollup 对代码模块使用新的标准化格式:white_check_mark:

------

- [x] [`0.直接使用`](#target3)
- [x] [`1.快速入门指南(Quick start)`](#target1)
- [x] [`2.rollup介绍`](#target2)
- [x] [`3.使用配置文件`](#peizhi)
- [x] [`4.使用插件`](#plugins)
- [x] [`5.命令行的参数`](#line)
- [x] [`6.使用 Babel 插件`](#babel)


------
#####  :octocat: [0.直接使用](#top) <b id="target3"></b> 
`进入项目根目录后，运行命令`
```c#
 npm install --save-dev rollup
```

`在项目的根目录下新建一个新文件 rollup.config.js, 之后再在文件中添加如下代码`
```node
export default {
  input: './src/main.js',
  output: {
    file: './dist/js/main.min.js',
    format: 'iife'
  }
}
```
* `input： rollup先执行的入口文件。`
* `output：rollup 输出的文件。`
* `output.format: rollup支持的多种输出格式(有amd,cjs, es, iife 和 umd) `
* `sourceMap —— 如果有 sourcemap 的话，那么在调试代码时会提供很大的帮助`

`我们在package.json代码下 添加如下脚本`
```node
"scripts": {
  "build": "rollup -c"
}
```
`npm run build 即可完成打包；`
#####  :octocat: [1.快速入门指南](#top) <b id="target1"></b> 
Rollup 可以通过命令行接口(command line interface)配合可选配置文件(optional configuration file)来调用，或者可
以通过 JavaScript API来调用<br/>
**`全局安装`** :speech_balloon:
```node
npm install --global rollup 
```
**`本地安装`** :speech_balloon:
```node
npm install --save-dev rollup 
```
`命令假设应用程序入口起点的名称为 main.js 你想要所有 import 的依赖(all imports)都编译到一个名为 bundle.js 的单个文件中。`
```node
//对于浏览器
$ rollup main.js --file bundle.js --format iife
```
```node
//对于 Node.js:
$ rollup main.js --file bundle.js --format cjs
```
```node
//对于浏览器和 Node.js:
$ rollup main.js --file bundle.js --format umd --name "myBundle"

```

##### 打包一个文件 main.js ->  bundle.js :speech_balloon:
```node
rollup src/main.js -o bundle.js -f cjs
```

#####  :octocat: [2.rollup介绍](#top) <b id="target2"></b> 
* 除了使用 ES6 模块之外，Rollup 还静态分析代码中的 import，并将排除任何未实际使用的代码。这允许您架构于现有工具和模块之上，而不会增加额外的依赖或使项目的大小膨胀。
* 因为 Rollup 只引入最基本最精简代码，所以可以生成轻量、快速，以及低复杂度的 library 和应用程序。因为这种基于显式的 import 和 export 语句
的方式，它远比「在编译后的输出代码中，简单地运行自动 minifier 检测未使用的变量」更有效。

#####  :octocat: [3.使用配置文件](#top) <b id="peizhi"></b> 
命令行虽然好,但是如果添加更多的选项，这种命令行的方式就显得麻烦了。为此，我们可以创建配置文件来囊括所需的选项。配置文件由 JavaScript 写成，
比 CLI 更加灵活，在项目中创建一个名为 rollup.config.js 的文件，增加如下代码：

```c#
export default {
  input: 'src/main.js',
  output: {
    file: 'bundle.js',
    format: 'cjs'
  }
};
```
`我们用 --config 或 -c 来使用配置文件：` <br/>

##### 如果愿意的话，也可以指定与默认 rollup.config.js 文件不同的配置文件
```javascript
rollup --config rollup.config.dev.js
rollup --config rollup.config.prod.js
```


##### 配置文件选项
```node
// rollup.config.js
export default {
  // 核心选项
  input,     // 必须
  external,
  plugins,

  // 额外选项
  onwarn,

  // danger zone
  acorn,
  context,
  moduleContext,
  legacy

  output: {  // 必须 (如果要输出多个，可以是一个数组)
    // 核心选项
    file,    // 必须
    format,  // 必须
    name,
    globals,

    // 额外选项
    paths,
    banner,
    footer,
    intro,
    outro,
    sourcemap,
    sourcemapFile,
    interop,

    // 高危选项
    exports,
    amd,
    indent
    strict
  },
};
```

#####  :octocat: [4.使用插件](#top) <b id="plugins"></b>
目前为止，我们通过相对路径，将一个入口文件和一个模块创建成了一个简单的 bundle。随着构建更复杂的 bundle，通常需要更大的灵活性——引
入 npm 安装的模块、通过 Babel 编译代码、和 JSON 文件打交道等 我们可以用 插件(plugins) 在打包的关键过程中更改 Rollup 的行为

`安装一个插件`:`我们用的是 --save-dev 而不是 --save，因为代码实际执行时不依赖这个插件——只是在打包时使用`
```node
npm install --save-dev rollup-plugin-json
```
编辑 rollup.config.js 文件，加入 JSON 插件：

```node
// rollup.config.js
import json from 'rollup-plugin-json';

export default {
  input: 'src/main.js',
  output: {
    file: 'bundle.js',
    format: 'cjs'
  },
  plugins: [ json() ]
};
```
#####  :octocat: [5.命令行的参数](#top) <b id="line"></b>
```node
-i, --input                 要打包的文件（必须）
-o, --output.file           输出的文件 (如果没有这个参数，则直接输出到控制台)
-f, --output.format [es]    输出的文件类型 (amd, cjs, es, iife, umd)  
        amd – 异步模块定义，用于像RequireJS这样的模块加载器
        cjs – CommonJS，适用于 Node 和 Browserify/Webpack
        es – 将软件包保存为ES模块文件
        iife – 一个自动执行的功能，适合作为<script>标签。
             （如果要为应用程序创建一个捆绑包，您可能想要使用它，因为它会使文件大小变小。）
        umd – 通用模块定义，以amd，cjs 和 iife 为一体
-e, --external              将模块ID的逗号分隔列表排除
-g, --globals               以`module ID:Global` 键值对的形式，用逗号分隔开 
                              任何定义在这里模块ID定义添加到外部依赖
-n, --name                  生成UMD模块的名字
-m, --sourcemap             生成 sourcemap (`-m inline` for inline map)
--amd.id                    AMD模块的ID，默认是个匿名函数
--amd.define                使用Function来代替`define`
--no-strict                 在生成的包中省略`"use strict";`
--no-conflict               对于UMD模块来说，给全局变量生成一个无冲突的方法
--intro                     在打包好的文件的块的内部(wrapper内部)的最顶部插入一段内容
--outro                     在打包好的文件的块的内部(wrapper内部)的最底部插入一段内容
--banner                    在打包好的文件的块的外部(wrapper外部)的最顶部插入一段内容
--footer                    在打包好的文件的块的外部(wrapper外部)的最底部插入一段内容
--interop                   包含公共的模块（这个选项是默认添加的）
```

`打印帮助文档。`
```
-h/--help
```
`打印已安装的Rollup版本号。`
```
-v/--version
```
`监听源文件是否有改动，如果有改动，重新打包`
```
-w/--watch
```

##### 文件监听
```
npm install --save-dev rollup-watch
```
`然后在package.json 中设置 scripts属性即可：`
```node
"scripts": {
  "dev": "rollup -c -w",
  "build": "rollup -c"
}
```

#####  :octocat: [6.使用Babel插件](#top) <b id="babel"></b>
```
npm install --save-dev rollup-plugin-babel
```
修改配置文件
```node
// rollup.config.js
import resolve from 'rollup-plugin-node-resolve';
import babel from 'rollup-plugin-babel';

export default {
  input: 'src/main.js',
  output: {
    file: 'bundle.js',
    format: 'cjs'
  },
  plugins: [
    resolve(),
    babel({
      exclude: 'node_modules/**' // 只编译我们的源代码 不编译 node_modules文件夹里面的东西
    })
  ]
};
```
`在Babel实际编译代码之前，需要进行配置。 创建一个新文件.babelrc：`
```json
{
  "presets": [
    ["latest", {
      "es2015": {
        "modules": false
      }
    }]
  ],
  "plugins": ["external-helpers"]
}
```
--------------------
`作者:` `模板` 
`完成时间`:`2018年12月31日18:33:38`
`备注信息`: `禁止转载` 

