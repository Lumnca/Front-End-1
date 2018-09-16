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
  - <a href="#ChangeIndex">`function: replaceWith / replaceAll`</a>
- [x] :maple_leaf: <a href="#deleteFlexManaer">`删除元素`</a>
  - <a href="#detachIndex">`function: detach`</a>
  - <a href="#emptyIndex">`function: empty`</a>
  - <a href="#removeIndex">`function: remove`</a>
  - <a href="#unwrapIndex">`function: unwrap`</a>
- [x] :maple_leaf: <a href="#deleteFlexManaer">`包裹元素`</a>
  - <a href="#wrapIndex">`function: wrap`</a>
  - <a href="#wrapAllIndex">`function: wrapAll`</a>
  - <a href="#wrapInnerIndex">`function: wrapInner`</a>


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
####  <a id="ChangeIndex" href="#ChangeIndex">function: replaceWith / replaceAll</a>  :star2: <a href="#top"> :arrow_up: </a>
* `replaceWith(普通字符串/jQuery对象)`：`用提供的内容替换集合中所有匹配的元素并且返回被替换元素的集合`
* `replaceWith(function(index,html))`:`函数可以接受到两个参数：第一个是当前元素的序号、第二个是当前元素内的html return 的数据就是替换成的内容（可以为html元素，也可以是jQuery对象）`
* `replaceAll(target)`:`用集合的匹配元素替换每个目标元素。`
  * `target`:`一个选择器字符串，jQuery对象，DOM元素，或者元素数组，包含哪个元素被替换。`

#####  <a id="deleteFlexManaer" href="#deleteFlexManaer">删除元素</a>  :star2: <a href="#top"> :arrow_up: </a>

#####  <a id="detachIndex" href="#detachIndex">detach</a>  :star2: <a href="#top"> :arrow_up: </a>
`detach( )`:`从DOM中去掉所有匹配的元素`
```javascript
  $("#list>ul").detach();
```
#####  <a id="emptyIndex" href="#emptyIndex">empty</a>  :star2: <a href="#top"> :arrow_up: </a>
`从DOM中移除集合中匹配元素的所有子节点。`
`empty()`:`这个方法不接受任何参数。`
```javascript
  $("button").click(function () {
    $("p").empty();
  });
```
#####  <a id="removeIndex" href="#removeIndex">remove</a>  :star2: <a href="#top"> :arrow_up: </a>
`remove() 将匹配元素集合从DOM中删除。（注：同时移除元素上的事件及 jQuery 数据。）`
```javascript
$("button").click(function () {
  $("p").remove();
});
```
#####  <a id="unwrapIndex" href="#unwrapIndex">unwrap</a>  :star2: <a href="#top"> :arrow_up: </a>
` 将匹配元素集合的父级元素删除，保留自身（和兄弟元素，如果存在）在原来的位置。`
```javascript
  $(document).ready(function(event) {
      $("#list>ul").unwrap();
  });
```
#####  <a id="wrapIndex" href="#wrapIndex">wrap</a>  :star2: <a href="#top"> :arrow_up: </a>
`wrap( wrappingElement )`:`在每个匹配的元素外层包上一个html元素。` <br/>
`wrap( function(index) )`:`回调函数，返回用于包裹匹配元素的 HTML 内容或 jQuery 对象。index 参数表示匹配元素在集合中的集合。该函数内的 this 指向集合中的当前元素。`
```javscript
  $("#list>ul").unwrap();
  $('ul').wrap('<div id="list" ></div>');
```
#####  <a id="wrapAllIndex" href="#wrapAllIndex">wrapAll</a>  :star2: <a href="#top"> :arrow_up: </a>
* `wrapAll( wrappingElement )`:`在所有匹配元素外面包一层HTML结构。`
* `wrappingElement 类型: String, Selector, Element, jQuery 用来包在外面的HTML片段，选择表达式，jQuery对象或者DOM元素。`
```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <script src="../js/jquery-3.3.1.min.js"></script>
        <title>Document</title>
        <style>
            #list{
                background-color: rebeccapurple;
            }
        </style>
    </head>

    <body>
        <img src="../resource/timg.jpg" width="150px" id="sdsd">
        <input type="text" value="你们好啊" placeholder="请输入账号" class="class1" />
        <input type="password" value="" placeholder="请输入密码" class="class2" />
        <div class="list" id="list" >
            <ul>
                <li>王者辅助1</li>
                <li>王者辅助2</li>
                <li>王者辅助3</li>
                <li>王者辅助4</li>
                <li>王者辅助5</li>
                <li>王者辅助6</li>
                <li>王者辅助7</li>
                <li>王者辅助8</li>
                <li>王者辅助9</li>
                <li>王者辅助10</li>
            </ul>
        </div>
    </body>
    <script>
        $(document).ready(function(event) {
            $("#list>ul").unwrap();
            $('ul,#sdsd').wrapAll('<div id="list" ></div>');
        });
    </script>

</html>
```
#####  <a id="wrapInnerIndex" href="#wrapInnerIndex">wrapInner</a>  :star2: <a href="#top"> :arrow_up: </a>
`wrapInner( wrappingElement )`:`在匹配元素里的内容外包一层结构。` <br/>
`wrapInner( function(index) )`:`一个返回HTML结构的函数，用来包在匹配元素内容的外面。接收集合中元素的索引位置作为参数。在函数中 ，this指向集合中当前的元素。/div>`






