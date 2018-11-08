### [Buffer 类处理二进制数据](#top) <b id="top"></b>:maple_leaf:
`在客户端javascript脚本代码中，对于二进制数据并没有提供一个很好的支持。然后在nodejs中需要处理像TCP流或文件流时，必须要处理二进制数据。因此
在node.js中，定义了一个Buffer类，该类用来创建一个专门存放二进制数据的缓存区。  `

- [x] [Encode 类](#encode) :maple_leaf:
- [x] [Buffer 类](#buffer) :maple_leaf:


#### [1. 编码](#top) <b id="buffer"></b>:maple_leaf: 
* `ascii`:	 `ASCLL字符串`
* `utf8`:	`UTF-8字符串`
* `utf16le`	:`UTF-16LE字符串`
* `ucs2`:`UCS2字符串`
* `base64`:` 经过BASE64编码后的字符串`
* `binary`:`二进制数据(不推荐使用)`
* `hex`:` 使用16进制数值表示的字符串`
#### [2. Buffer 类](#top) <b id="buffer"></b>:maple_leaf:
`Buffer 是一个全局类,不需要加载任何模板`

##### Buffer 构造函数
`Buffer 构造函数有数个,但是在v7.0.0 版本之后 Buffer的构造函数就开始被废弃,现在开始使用类方法 Buffer.from()不同参数的方法来构造Buffer对象`
* `废弃的构造函数`
  * `new Buffer(arrayBuffer[, byteOffset[, length]])`
  * `new Buffer(buffer)`
  * `new Buffer(size)`
  * `new Buffer(string[, encoding])`
```node
/* 1.0 */
const buf = new Buffer([0x62, 0x75, 0x66, 0x66, 0x65, 0x72]);

/* 2.0 */
const arr = new Uint16Array(2);
arr[0] = 5000;
arr[1] = 4000;
const buf = new Buffer(arr.buffer);
/* 3.0 */
const buf1 = new Buffer('this is a tést');
const buf2 = new Buffer('7468697320697320612074c3a97374', 'hex');

console.log(buf1.toString());
// Prints: this is a tést
console.log(buf2.toString());
// Prints: this is a tést
console.log(buf1.toString('ascii'));
// Prints: this is a tC)st
```
* `新的的构造方法`
  * `Buffer.from(arrayBuffer[, byteOffset[, length]]) `
  * `Buffer.from(buffer)`
  * `new Buffer(string[, encoding])`
```node
const buf = Buffer.from([0x62, 0x75, 0x66, 0x66, 0x65, 0x72]);

const arr = new Uint16Array(2);
arr[0] = 5000;
arr[1] = 4000;
const buf = Buffer.from(arr.buffer);
```
