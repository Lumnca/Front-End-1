<a id="top" href="#top">Jquery 选择符 :maple_leaf:</a> 
----
`Jquery 选择法兼容了Css选择器 也扩展了一些选择器...`

- [x] :maple_leaf: <a href="#CssSelector">`Css 选择器`</a>
  - <a href="#InnnerCoreSelector">`Core Selector`</a>
  - <a href="#PropertySelector">`Property Selector`</a>
  - <a href="#RelationshipSelector">`Relationship  Selector`</a>
  - <a href="#PseudoSelector">`Pseudo Selector`</a>
  - <a href="#JointSelectorAndInverseSelector">`Joint selector and inverse selector`</a>
- [x] :maple_leaf: <a href="#ListJquery">`jQuery 选择器`</a>
- [x] :maple_leaf: <a href="#UnderstandResult">`理解选择结果`</a>
  - <a href="#eachFunction">`function:each(function)`</a>
  - <a href="#getFunction">`function:get(index)`</a>
  - <a href="#lengthFunction">`Property: length`</a>
  - <a href="#sizeFunction">`function:size()`</a>
  - <a href="#toArrayFunction">`function:toArray()`</a>
  - <a href="#sizeFunction">`function:size()`</a>
  - <a href="#sizeFunction">`function:size()`</a>
  - <a href="#sizeFunction">`function:size()`</a>
  - <a href="#addFunction">`function:add()`</a>
- [x] :maple_leaf: <a href="#GetNeedUnderstandResult">`对结果集进行筛选`</a>
  - <a href="#TongYongFucntion">`通用方法`</a>
  - <a href="#GetChilds">`获取元素子集`</a>
  - <a href="#GaaaaeadatChilds">`过滤元素`</a>
  - <a href="#GeasdasdasdChilds">`基于后代元素过滤结果集`</a>
  - <a href="#checkChilds">`检测结果集`</a>
  - <a href="#asdjkhajsdtChilds">`根据现有结果集得到另一个结果集`</a>
  - <a href="#EndBacjChilds">`修改、回退结果集`</a>
  

####  <a id="CssSelector" href="#CssSelector">Css 选择器</a>  :star2: <a href="#top"> :arrow_up: </a>
`Query支持的选择器相当强大，我们在CSS里面使用的选择器，在jQuery里面都可以使用`
#####  <a id="InnnerCoreSelector" href="#InnnerCoreSelector">核心选择器</a>  :star2: <a href="#top"> :arrow_up: </a>
* `核心选择器（应用最广泛的选择器）`
  * `*`:`选择所有元素`
  * `TagName`:`选择特定类型的元素`
  * `.类名`:`选择具有特定class的元素`
  * `TagName.类名`:`选择具有特定class的某类元素`
  * ` #id名`:`选择具有特定id属性值的元素`         		
           	
#####  <a id="PropertySelector" href="#PropertySelector">Css 属性选择器</a>  :star2: <a href="#top"> :arrow_up: </a>       	
* `属性选择器（根据元素的属性来选择元素）`
  * `[attr]`	`选取定义了attr属性的元素，即使这个属性没有值`
  * `[attr="val"]`	`选取attr属性值等于字符串val的元素`
  * `[attr^="val"]`	 `选取attr属性值以字符串val开头的元素`
  * `[attr$="val"]`	`选取attr属性值以字符串val结尾的元素`
  * `[attr*="val"]`	`选取attr属性值包含字符串val的元素`
  * `[attr~="val"]`	`选取attr属性其中一个值是字符串val的元素`
  * `[attr|="val"]`	`选取attr属性值等于字符串val，或属性值为连字符分隔的值列表且第一个值是字符串val的元素`
  * `[selector1][selector2][selectorN]`	`复合属性选择器，需要同时满足多个条件时使用`      	

#####  <a id="RelationshipSelector" href="#RelationshipSelector">Css 关系选择器 </a>  :star2: <a href="#top"> :arrow_up: </a>
* `关系选择器`
  * `<selector1>  <selector2>`	`在给定的祖先元素下匹配所有的后代元素`
  * `<selector1> > <selector2>`	`在给定的父元素下匹配所有的子元素`
  * `<selector1> + <selector2>`	`匹配所有紧接在 <selector1> 元素后的 <selector2>`
  * `<selector1> ~ <selector2>`	`匹配 所有在<selector1> 元素之后的所有同辈 <selector2> 元素`
#####  <a id="PseudoSelector" href="#PseudoSelector">伪元素和伪类选择器</a>  :star2: <a href="#top"> :arrow_up: </a>
* `伪元素和伪类选择器`
  * `:checked`:`用于表单，匹配所有被选中元素(复选框、单选框等，不包括select中的option)`
  * `:disabled`:`用于表单，匹配所有不可用元素`
  * `:enabled`:`用于表单，匹配所有可用元素`
  * `:focus`:`主要用于表单，选取得到焦点的元素`
  * `:required`:`用于表单，选取具有required属性的元素`
  * `:optional`:`用于表单，选取缺少required属性的元素`
  * `:empty`:`匹配所有既不包含子元素也不包含文本的空元素`
  * `:first-child`:`选取第一个子元素`
  * `:last-child`:`选取最后一个子元素`
  * `:nth-child(n)`:`选取元素的第n个子元素(从1开始计数)n可为even或odd`
  * `:nth-last-child(n)`:`选取元素的倒数第n个子元素`
  * `:nth-of-type(n)`:`选择同属于一个父元素之下，并且标签名相同的元素中的第n个(注：从1开始计数)`
  * `:nth-last-of-type(n)`:`选择同属于一个父元素之下，并且标签名相同的元素中的倒数第n个`
  * `:only-child`:`如果某个元素是父元素中唯一的子元素，那将会被匹配`
  * `:only-of-type`:`选择所有没有兄弟元素，且具有相同的元素名称的元素`
  * `:root`:`选取文档的根元素，在html文档中即是<html>元素`
####  <a id="JointSelectorAndInverseSelector" href="#JointSelectorAndInverseSelector">联合选择器和反选择器</a>  :star2: <a href="#top"> :arrow_up: </a>
* `通过对选择器的合理安排，我们几乎能达成任何目标。我们还可以利用选择器组合实现联合选择和反选择`
  * `<selector>,<selector>,<selector>..`:`选取匹配第一个选择器的元素和匹配第二个选择器的元素`
  * `:not(selector)`:`选取不匹配指定选择器的元素`
####  <a id="ListJquery" href="#ListJquery">jQuery扩充的选择器</a>  :star2: <a href="#top"> :arrow_up: </a>
`上面是css中本身就提供的选择器，为了满足更复杂的需求，jQuery还额外的支持一些选择器，这些选择器不但给我们带来方便，还能实现更细的控制。选择器可以单独使用，也可以配合其他选择器使用！`
* `扩展选择器列表`           
  * `:animated`:`匹配所有正在执行动画效果的元素`
  * `:contains(text)`:`如果元素内或者后代元素内包含指定的文本即被选中`
  * `:eq(n)`:`选择第n个元素（从0开始计数）`
  * `:first`:`选择第一个匹配的元素`
  * `:last`:`选择最后一个匹配的元素`
  * `:lt(n)`:`选择序号小于n的所有元素（从0开始计数）`
  * `:gt(n)`:`选择序号大于n的所有元素（从0开始计数）`
  * `:odd`:`选择所有奇数元素(从0开始计数)`
  * `:even`:`选择所有的偶数元素（从0开始计数）`
  * `:has(选择器)`:`匹配包含`
  * `:text`:`用于表单，匹配所有的单行文本框`
  * `:button`:`匹配所有按钮（input标签type为button以及<button>标签）`
  * `:checkbox`:`用于表单，选择所有的复选框（匹配所有复选框）`
  * `:file`:`用于表单，选择所有的文件上传输入框`
  * `:input`:`用于表单，选择所有的input元素（匹配所有 input, textarea, select 和 button 元素）`
  * `:password`:`用于表单，选择所有的密码输入框`
  * `:radio`:`用于表单，选择所有的单选框`
  * `:submit`:`用于表单，选择所有的表单提交按钮`
  * `:image`:`用于表单，匹配所有图像域`
  * `:reset`:`用于表单，选择所有的表单重置按钮`
  * `:selected`:`用于表单，匹配所有选中的option元素`
  * `:header`:`匹配如 h1,h2,h3之类的标题元素`
  * `:hidden`:`选择所有的被隐藏文件`
  * `:visible`:`选择所有的可见元素`
  * `:parent`:`匹配含有子元素或者文本的元素`
        
####  <a id="UnderstandResult" href="#UnderstandResult">理解选择结果</a>  :star2: <a href="#top"> :arrow_up: </a>
`使用$函数选择元素返回的是一个对象，我们可以称这个对象为jQuery对象（就是一种叫法）,我们在jQuery执行一些操作的时候很多情况  `
#####  <a id="eachFunction" href="#eachFunction">each(Function)</a>  :star2: <a href="#top"> :arrow_up: </a>
`在每个元素上运行给定的function 遍历jQuery对象中的所有元素，传个一个函数 jQuery对象中有多少个元素，传入的函数就会自动的调用多少次！
 调用这个函数时，会传入当前这个元素在 jQuery对象中的序号！我们使用一个参数即可获取！在函数内部this代表当前的html元素对象！
返回 'false' 将停止循环 (就像在普通的循环中使用 'break')。返回 'true' 跳至下一个循环(就像在普通的循环中使用'continue')`
##### <a id="getFunction" href="#getFunction">get(index)</a>  :star2: <a href="#top"> :arrow_up: </a>
`返回给定索引值(index)对应的HTMLElement对象`
##### <a id="lengthFunction" href="#lengthFunction">length</a>  :star2: <a href="#top"> :arrow_up: </a>
` 返回jQuery对象中包含元素的个数`
##### <a id="sizeFunction" href="#sizeFunction">function:size()</a>  :star2: <a href="#top"> :arrow_up: </a>
`返回jQuery对象中包含元素的个数`
##### <a id="toArrayFunction" href="#toArrayFunction">function:toArray()</a>  :star2: <a href="#top"> :arrow_up: </a>
`返回一个jQuery对象中包含的元素构成的HTMLElement对象数组`
##### <a id="addFunction" href="#addFunction">add 方法</a>  :star2: <a href="#top"> :arrow_up: </a>
* `注意点：add方法不会改变原来的jQuery对象，而是返回新的jQuery对象, 向jQuery对象中添加更多的元素主要就是使用jQuery对象中的add方法！`
  * `add(选择器)、add(选择器,上下文)`:`把匹配选择器的所有元素添加到调用add方法的jQuery对象中`
  * `add(HTMLElement)、add(HTMLElement[])`:`把一个或一组HTMLElement添加到jQuery对象`
  * `add(jQuery对象)`:`把参数jQuery对象中的元素添加到当前jQuery对象`

#####  <a id="TongYongFucntion" href="#TongYongFucntion">通用方法</a>  :star2: <a href="#top"> :arrow_up: </a>
`注意点：这些操作不会改变原来的jQuery对象，而是返回新的jQuery对象`
* `从结果集中获取某个元素`
  * `first()`:`得到第一个元素`
  * `last()`：`得到最后一个元素`
  * `eq(index)`：`得到第index个元素 当index为正值时，从第一个元素开始计数，为负数时则从jQuery中的最后一个元素开始计数`             
             
#####  <a id="GetChilds" href="#GetChilds">获取元素子集</a>  :star2: <a href="#top"> :arrow_up: </a>
`获取元素子集`
* `slice()`:`方法用来获取特定一组子元素`
* `slice(从第几个开始,结束的位置)`:`如果不提供第二个参数则从第一个参数一直获取到元素集合的末尾`
#####  <a id="GaaaaeadatChilds" href="#GaaaaeadatChilds">过滤元素</a>  :star2: <a href="#top"> :arrow_up: </a>
* `使用filter方法可以将所有 不满足 某个指定条件的元素剔除     `
  * `filter(selector)`:`得到匹配选择器的元素`
  * `filter(HTMLElement)`:`得到参数对应的元素`
  * `filter(jQuery)`:`得到原始集合与参数jQuery对象所含元素集合的交集`
  * `filter(function(index))`:`每一个元素调用一次参数函数，若某个元素调用参数函数的返回值为false，就剔除该元素它接受一个参数index，这是元素在jQuery集合的索引。在函数内， this指的是当前的DOM元素。原来的jQuery对象里面含有多少个元素，传入的函数就会被执行多少次！如果函数返回的是true，那么对于的元素就留下来 如果函数返回的false，或者不返回 那么对于的元素就剔除！`
    * `原来的jQuery对象里面含有多少个元素，传入的函数就会被执行多少次！`
    * `如果函数返回的是true，那么对于的元素就留下来`
    * `如果函数返回的false，或者不返回 那么对于的元素就剔除！`  
* `not方法与filter方法正好相反`
  * `not(选择器)`:`删除匹配选择器的元素`
  * `not(HTMLElement[])、not(HTMLElement)`:`删除指定的元素或者元素集合`
  * `not(jQuery)`:`删除原始集合与参数jQuery对象所含元素集合的交集`
  * `not(function(index))`:`每个元素调用一次参数函数`
#####  <a id="GeasdasdasdChilds" href="#GeasdasdasdChilds">基于后代元素过滤结果集</a>  :star2: <a href="#top"> :arrow_up: </a>
`我们可以使用has方法指定一个选择器、一个或多个HTMLElement对象为参数，从而得到拥有指定后代的元素保留包含特定后代的元素，去掉那些不含有指定后代的元素`
<br/>
* `has(selector/object)方法`:`如果jQuery对象中的元素里面含有匹配的后代元素，那么对应的元素就留下来！一个选择器
一个或多个HTMLElement对象为参数`
            
#####  <a id="checkChilds" href="#checkChilds">检测结果集</a>  :star2: <a href="#top"> :arrow_up: </a>
* `使用is方法确定jQuery对象中的某个或某些元素是否满足测试条件`
  * `is(选择器)`:`如果结果含有匹配选择器的元素则返回true`
  * `is(HTMLElement[])、is(HTMLElement)`:`如果结果集中包含指定的HTMLElement或者至少含有指定HTMLElement[]中的一个元素`
  * `is(jQuery)`:`如果结果集中至少包含一个参数对象中的元素，返回true`
  * `is(function(index))`:`如果有一任意次参数函数返回true，则返回true 函数用来作为测试元素的集合。它接受一个参数index，这是元素在jQuery集合的索引。在函数内， this指的是当前的DOM元素。`
            
#####  <a id="asdjkhajsdtChilds" href="#asdjkhajsdtChilds">根据现有结果集得到另一个结果集</a>  :star2: <a href="#top"> :arrow_up: </a>
* `children()`
   * 不传参数：得到结果集内所有元素的子元素
   * 传入选择器：得到结果集内 元素的匹配传入选择器的子元素	
* `find()`
   * 传入选择器：得到匹配选择器的后代元素
   * 传入jQuery、HTMLElement、HTMLElement[]
* `next()`
  * `取得一个包含匹配的元素集合中每一个元素紧邻的下一个同辈元素的元素集合`
  * `可以传入选择器进行筛选`
* `nextAll()`
  * `查找当前元素之后所有的同辈元素`
  * `可以传入选择器进行筛选`
* `nextUntil()`
  * `查找当前元素之后所有的同辈元素，直到（但不包括）遇到匹配的那个元素才停止。`
  * `第一个传入参数：DOMElement,jQuery对象，选择器`
* `第二个传入参数（可选）：选择器(对结果进行筛选)`
  * `prev()`
  * `取得一个包含匹配的元素集合中每一个元素紧邻的前一个同辈元素的元素集合`
* `可以传入选择器进行筛选`
  * `prevAll()`
  * `查找当前元素之前所有的同辈元素`
* `可以传入选择器进行筛选`
  * `prevUntil()`
  * `查找当前元素之前所有的同辈元素，直到（但不包括）遇到匹配的那个元素才停止`
* `第一个传入参数：DOMElement,jQuery对象，选择器`
  * `第二个传入参数（可选）：选择器(对结果进行筛选)`
  * `siblings()`
* `取得一个包含匹配的元素集合中每一个元素的所有同辈元素的元素集合`
  * `可以传入选择器进行筛选`
#####  <a id="EndBacjChilds" href="#EndBacjChilds">修改、回退结果集</a>  :star2: <a href="#top"> :arrow_up: </a>
* `end()方法`
  * `使用end方法得到上一个结果集`
* `addBack()方法`
  * `使用addBack()可以得到原结果集与当前结果的合集，也可传入选择器来过滤原结果集    `
