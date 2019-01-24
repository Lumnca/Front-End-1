### [JavaScript Dom1 文档对象模型](#top) :grey_exclamation: <b id="top"></b>
`文档对象模型（Document Object Model，简称DOM），是W3C组织推荐的处理可扩展标志语言的标准编程接口。在网页上，组织页面（或文档）的
对象被组织在一个树形结构中，用来表示文档中对象的标准模型就称为DOM。` :speech_balloon:

------

- [x] [`1.节点层次`](#target1)
- [x] [`2.Node 类型`](#target2)
- [x] [`3.节点关系`](#target3)
- [x] [`4.节点操作`](#target4)

------

#####  :octocat: [1.节点层次](#top) <b id="target1"></b> 
`概括`:`节点是层次关系的 一层嵌套一层 组成了 Dom的结构 本质上 你可以把他看成一棵树 `
```html
<!DOCTYPE html>
<html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>首页</title>
  </head>
  <body>
     <div>Hello World!</div>
  </body>
</html>
```
`Document 是文档对象 最高的根节点 Dom 结构就是数据结构中 树`
```c#
Document
    |
    |_ _ Element Html
          |
          |
          |_ _ Element head
          |     |
          |     |_ _ meta 
          |     |     |
          |     |     |_ _ Attribute "charset UTF-8"
          |     |
          |     |_ _ title 
          |          |
          |          |_ _ Text 首页
          |
          |
          |— — Element body
               |
               |_ _ div
                    |
                    |_ _ Text Hello World!
```

#####  :octocat: [2.Node 类型](#top) <b id="target2"></b> 
`Dom1 级定义了一个Node 接口,该接口将由Dom 中所有的节点类型实现 每一个节点都有一个 nodeType 表名节点的类型,任何节点类型必然是这十二个节点之一`

<table>
<tbody><tr>
<th colspan="1">值</th>
<th colspan="1">节点类型</th>
<th>描述</th>
<th>子节点</th>
</tr>
<tr>
<td style="width:5%;">1</td>
<td style="width:25%;">Element</td>
<td style="width:35%;">代表元素</td>
<td>Element, Text, Comment, ProcessingInstruction, CDATASection, EntityReference</td>
</tr>
<tr>
<td>2</td>
<td>Attr</td>
<td>代表属性</td>
<td>Text, EntityReference</td>
</tr>

<tr>
<td>3</td>
<td>Text</td>
<td>代表元素或属性中的文本内容。</td>
<td>None</td>
</tr>

<tr>
<td>4</td>
<td>CDATASection</td>
<td>代表文档中的 CDATA 部分（不会由解析器解析的文本）。</td>
<td>None</td>
</tr>

<tr>
<td>5</td>
<td>EntityReference</td>
<td>代表实体引用。</td>
<td>Element, ProcessingInstruction, Comment, Text, CDATASection, EntityReference</td>
</tr>

<tr>
<td>6</td>
<td>Entity</td>
<td>代表实体。</td>
<td>Element, ProcessingInstruction, Comment, Text, CDATASection, EntityReference</td>
</tr>

<tr>
<td>7</td>
<td>ProcessingInstruction</td>
<td>代表处理指令。</td>
<td>None</td>
</tr>

<tr>
<td>8</td>
<td>Comment</td>
<td>代表注释。</td>
<td>None</td>
</tr>
<tr>
<td>9</td>
<td>Document</td>
<td>代表整个文档（DOM 树的根节点）。</td>
<td>Element, ProcessingInstruction, Comment, DocumentType</td>
</tr>
<tr>
<td>10</td>
<td>DocumentType</td>
<td>向为文档定义的实体提供接口</td>
<td>None</td>
</tr>
<tr>
<td>11</td>
<td>DocumentFragment</td>
<td>代表轻量级的 Document 对象，能够容纳文档的某个部分</td>
<td>Element, ProcessingInstruction, Comment, Text, CDATASection, EntityReference</td>
</tr>
<tr>
<td>12</td>
<td>Notation</td>
<td>代表 DTD 中声明的符号。</td>
<td>None</td>
</tr>
</tbody></table>


* `nodeName`:`Node.nodeName 表名节点名称 例如 body div p`
* `nodeType`:`返回数字 节点类型的值 它属于 Node 类型枚举之一  `
* `nodeValue`:`这个属性的值始终都是 null`

```node
<body id="main">

</body>
var node = document.getElementById("main");
console.log(node.nodeName); // BODY
console.log(node.nodeType); // 1

let isElem = (node.nodeType == Node.ELEMENT_NODE) ? "是Element 类型 节点":"不是Element 类型节点";
console.log(isElem); //是Element 类型 节点

console.log(node.nodeValue); //null
```

#####  :octocat: [3.节点关系](#top) <b id="target3"></b> 
`节点具有如下几种关系 关系都是指针  也成为关系指针 他们是只读的`
* `父子节点`:`元素内部的空格换行也被当做了子节点 非常`
   * `childNodes`:`获得一个节点的所有子节点的 返回  NodeList 类型 它可以使用索引访问  但是他不是数组,但是我们可以将他们转换为数组 返回的
   NodeList 对象是访问时 对于Dom 结构的一次快照 也就是说 他不是动态的  每次获取它  他都会对Dom 结构进行一次[拍摄] 获取 Dom结构快照`
      * `NodeList对象的属性 length`:`节点个数`
      * `forEach`:`遍历方法`
      * `item`:`索引器`
      * `keys`:`每一个Node 的键 也就是 nodeName`
   * `parentNode`:`每一个节点都具有的指向父节点的指针属性`
   * `firstChild`:`第一个节点`
   * `lastChild`:`最后一个节点`
   
* `兄弟节点`
   * `previousSibling`:`当前节点的前一个节点 如果html 节点之前具有字符/空格 那么 值会 返回 #text 没有返回 null`
   * `nextSibling`:`当前节点的后一个节点 如果html 节点之后具有字符/空格 那么 值会 返回 #text 没有返回 null`
* `节点判断`
   * `hasChildNodes`:`判断当前节点是否具有子节点`
   * `ownerDocument`:`该属性指向表示整个文档的文档节点,每一个节点都具有`
`跨浏览器将nodeList 转换为数组`
```node
function ConvertNodeListToArray(_nodeList){
    var array = null;
    try {
        array = Array.prototype.slice.call(_nodeList,0);
    } catch (error) {
        array = new Array();
        for(var i = 0,len = _nodeList.length; i < len; i++ ){
            array.push(_nodeList.item(i));
        }
    }
    return array;
}
```

```node
var body = document.getElementsByTagName("body")[0]; //获得body
console.log(body);
console.log(body.childNodes);

console.log(body.firstChild); //第一个节点
console.log(body.lastChild); //最后一个节点
```

##### 解决换行 空格问题
`很多的时候返回的 子节点中或者 兄弟节点会是 #text 类型也不是我们需要的 Element 类型 这非常的糟糕 新版JS 提供了 只返回Element 类型的属性指针`
* `firstElementChild`:`第一个 Element 类型的元素`
* `lastElementChild`:`最后一个 Element 类型的元素`
* `ParentNode.childElementCount`:`返回 Elment 类型元素的个数`

* `previousElementSibling`:`前一个 Element类型的 兄弟节点`
* `nextElementSibling`:`后一个 Element类型的 兄弟节点`

#####  :octocat: [4.节点操作](#top) <b id="target4"></b> 
`操作一般分为四种 增删改查`
* `父子节点的操作`
   * `Container.appendChild(node)`:`增加子节点 在 childNodes列表的末尾添加一个节点 添加成功后返回一个新增的节点`
   * `Container.insertBefore(node,nodeplace)`:`nodeplace 是第一个插入位置的参考值,新加入的元素会被插入到  Container 
   元素中的 nodeplace节点之前`
   
   * `Container.replaceChild(newNode,replaceNode):`新节点 替换 Container 节点中的 replace子节点`
   * `Container.removeChild(needMoveNode)`:`删除匹配到的子节点`
   * `Node.cloneNode`:`拷贝一个完全相同的副本`
   * `normalise`:`处理文档树的文本节点,删除空文本节点,合并相邻的文本节点`



--------------------
`作者:` `模板` 
`完成时间`:`2018年12月31日18:33:38`
`备注信息`: `禁止转载` 
