<a id="top" href="#top">Jquery Dom 操作  :maple_leaf:</a> 
----
`用Dom的添加删除移动元素,包裹元素.....操作DOM文档结构`

- [x] :maple_leaf: <a href="#InsertDomIndex">`创建新元素`</a>
  - <a href="#StringIndex">`function: String`</a>
  - <a href="#cloneIndex">`function: clone`</a>
- [x] :maple_leaf: <a href="#InsertDomIndex">`插入元素`</a>
  - <a href="#appendIndex">`function: append/appendTo `</a>
  - <a href="#prependIndex">`function: prepend/prependTo`</a>
  - <a href="#afterIndex">`function: after/insertAfter`</a>
  - <a href="#beforeIndex">`function: before/insertBefore`</a>
- [x] :maple_leaf: <a href="#ReplaceElementIndex">`替换元素`</a>
- [x] :maple_leaf: <a href="#">``</a>
- [x] :maple_leaf: <a href="#">``</a>

####  <a id="InsertDomIndex" href="#InsertDomIndex">创建JqueryDom对象</a>  :star2: <a href="#top"> :arrow_up: </a>
`创建元素有两种方法,一种是通过字符串的方式创建 第二种是通过clone 深拷贝一个对象`
#####  <a id="StringIndex" href="StringIndex">通过字符串创建新元素</a>  :star2: <a href="#top"> :arrow_up: </a>
`字符串的方式`：**`使用$函数创建新元素`**
```javascript
 let li_new =$("<li>王者辅助11</li>");
 $("#list>ul").append(li_new);
```
* `创建的新元素不会自动的把新元素插入到页面中，我们还需要明确的指定其插入到页面中的位置`
* `使用$函数创建元素，是返回的是jQuery对象`

#####  <a id="cloneIndex" href="cloneIndex">克隆已有的元素 clone</a>  :star2: <a href="#top"> :arrow_up: </a>
`使用clone方法以已有的元素(或者新创建的元素)为模子生成新元素,clone方法会复制jQuery对象内包含后代元素在内的所有元素`
* `clone( [withDataAndEvents ] [, deepWithDataAndEvents ] )`:`这两个参数都可以不填写 默认为false / false`

* `第一个参数`：`一个布尔值（true 或者 false）指示目标元素的事件处理函数以及关联数据是否会被复制`
* `第二个参数（默认情况下与第一个参数一致）`：`一个布尔值，指示是否对克隆的元素的所有子元素的事件处理程序以及关联数据进行复制`
```javascript
 $('.hello').clone().appendTo('.goodbye'); 
```
#####  <a id="InsertDomIndex" href="#InsertDomIndex"> 插入元素</a>  :star2: <a href="#top"> :arrow_up: </a>
`你可以选择 向某个元素插入DomElement 也可以将某一个元素插入到另一个元素`
#####  <a id="appendIndex" href="appendIndex">function: append / appendTo </a>  :star2: <a href="#top"> :arrow_up: </a>
`在每个匹配元素里面的末尾处插入参数内容。`
* `$('body').append('html字符串');` :`可以添加一个或者多个元素 会自动将html字符串转换为Jquery对象`
* `$('body').append($('#name'));`:`传入Jquery对象`
* `appendTo(目标Jquery对象)`:`将匹配的元素插入到目标元素的最后面（译者注：内部插入）。`
```javascript
  /* 我们需要将 <li>王者辅助11</li> 插入到ul中 */
  let li_new =$("<li>王者辅助11</li>");
  $("#list>ul").append(li_new); // li_new.appendTo("#list>ul");
```
#####  <a id="prependIndex" href="prependIndex">function: prepend / prependTo </a>  :star2: <a href="#top"> :arrow_up: </a>
`将参数内容插入到每个匹配元素内部的 最前面。`
* `$('body').prepend('html字符串');` :`可以添加一个或者多个元素 会自动将html字符串转换为Jquery对象`
* `$('body').prepend($('#name'));`:`传入Jquery对象`
* `prependTo(目标Jquery对象)`:`将匹配的元素插入到目标元素的最前面（译者注：内部插入）。`
```javascript
  /* 我们需要将 <li>王者辅助0</li> 插入到ul中 */
  let li_new =$("<li>王者辅助0</li>");
  $("#list>ul").prepend(li_new); // li_new.prependTo("#list>ul");
```
####  <a id="afterIndex" href="#afterIndex">function: after/insertAfter</a>  :star2: <a href="#top"> :arrow_up: </a>
`在匹配元素集合中的每个元素的 后面 插入参数所指定的内容，作为其兄弟节点`
* `after( content [, content ] )`
  * `content 类型`:` String, Element, jQuery`
    * `一个元素，HTML字符串，或者jQuery对象，用来插在每个匹配元素的后面。`
* `after( function(index) )`
  * `function(index) 类型: Function()`
    * `一个返回HTML字符串，DOM 元素， 或者 jQuery 对象的函数，插在每个匹配元素的后面。接收元素在集合中的索引位置作为参数。在函数中this指向元素集合中的当前元素。`
* `insertAfter( target )`
  `一个选择器，元素，HTML字符串或者jQuery对象，匹配的元素将会被插入在由参数指定的目标后面。`
```javascript
  //将<p>Test</p> 插入到.inner 中
 $('.inner').after('<p>Test</p>');
 $('<p>Test</p>').insertAfter(`.inner`);
```
####  <a id="beforeIndex" href="#beforeIndex">function: before/insertBefore</a>  :star2: <a href="#top"> :arrow_up: </a>
`在匹配元素集合中的每个元素的 前面 插入参数所指定的内容，作为其兄弟节点`
* `before( content [, content ] )`
  * `content 类型`:` String, Element, jQuery`
    * `一个元素，HTML字符串，或者jQuery对象，用来插在每个匹配元素的前面。`
* `before( function(index) )`
  * `function(index) 类型: Function()`
    * `一个返回HTML字符串，DOM 元素， 或者 jQuery 对象的函数，插在每个匹配元素的前面。接收元素在集合中的索引位置作为参数。在函数中this指向元素集合中的当前元素。`
* `beforeAfter( target )`
  `一个选择器，元素，HTML字符串或者jQuery对象，匹配的元素将会被插入在由参数指定的目标前面。`
```javascript
  //将<p>Test</p> 插入到.inner 中
 $('.inner').before('<p>Test</p>');
 $('<p>Test</p>').beforeAfter(`.inner`);
```
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>







