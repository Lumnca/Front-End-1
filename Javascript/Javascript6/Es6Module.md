### [| -- ES6 Module加载语法 -- |](#top) <b id="top"></b>

----
`偶尔写一点笔记! 打发郁闷时光`

- [x] [`1.module 说明`](#target1)
- [x] [`2.export 命令: 导出模块信息`](#target2)


----
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

##### as 关键字
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
#### `default 命令`
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

##### const 模块导出常量
`那么这一个值要被多个模块共享`
```node
// constants.js 模块
export const A = 1;
export const B = 3;
export const C = 4;
```
