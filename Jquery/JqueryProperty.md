<a id="top" href="#top">Jquery 属性操作  :maple_leaf:</a> 
----
`Jquery 属性操作,类操作`

- [x] :maple_leaf: <a href="#top">`HTML 属性操作方法`</a>
   - [x] <a href="#JqueryIndex">`function：attr`</a>
   - [x] <a href="#removeAttrIndex">`function：removeAttr`</a>
   - [x] <a href="#propIndex">`function：prop`</a>
   - [x] <a href="#removePropIndex">`function：removeProp`</a>
   - [x] <a href="#addClassIndex">`function：addClass`</a>
   - [x] <a href="#hasClassIndex">`function：hasClass`</a>
   - [x] <a href="#removeClassIndex">`function：removeClass`</a>
   - [x] <a href="#toggleClassIndex">`function：toggleClass`</a>
   - [x] <a href="#htmlIndex">`function：html`</a>
   - [x] <a href="#textIndex">`function：text`</a>
   - [x] <a href="#valIndex">`function：val`</a>
- [x] :maple_leaf: <a href="#cssIndex">`Css 操作方法`</a>
- [x] :maple_leaf: <a href="#top">`属性快捷获取`</a>
   - [x] <a href="#heightIndex">`function：height`</a>
   - [x] <a href="#widthIndex">`function：width`</a>
   - [x] <a href="#offsetIndex">`function：offset`</a>
   - [x] <a href="#scrollLeftIndex">`function：scrollLeft`</a>
   - [x] <a href="#scrollTopIndex">`function：scrollTop`</a>
   - [x] <a href="#innerHeightIndex">`function：innerHeight`</a>
   - [x] <a href="#innerWidthIndex">`function：innerWidth`</a>
   - [x] <a href="#outerHeightIndex">`function：outerHeight`</a>
   - [x] <a href="#outerWidthIndex">`function：outerWidth`</a>

###  <a id="JqueryIndex" href="#JqueryIndex">attr </a>  :star2: <a href="#top"> :arrow_up: </a>
* `attr("PropertyName")`: 获取某个属性的值 没有属性值返回 undefined
* `attr("PropertyName","value")`: 设置某个属性的值
* `attr({"PropertyName"："value","PropertyName":"value"})`: 设置多个属性的值以Object 属性的形式
* `attr("PropertyName",function(index,PropertyValue))`: 
  * ①`属性的值` 
  * ②`函数(index, attr)`:`这个函数返回用来设置的值，this指向当前的元素接收表示元素在匹配集合中的索引位置的参数和表示元素上原来的 该属性 值的参数
    return的数据就是这个属性的值`                               
```javascript
  $(document).ready(function (event) {
      $.each($("img"), function(index, val){
         let imgs=$(val);
         console.log(`${index}  src : ${imgs.attr("src")} width： ${imgs.width()}px`);
         imgs.attr("src","../resource/sdsdasd.jpg");

         imgs.attr({
             "width":"200px",
             "alt":"小绿龙"
         });
      });
      
      $("input").attr("type",function(index,attrValue){
          console.log(`${index}: ${attrValue}`);
      })

  });
```
####  <a id="removeAttrIndex" href="#removeAttrIndex">removeAttr</a>  :star2: <a href="#top"> :arrow_up: </a>
`为匹配的元素集合中的每个元素中移除指定的属性`
* `removeAttr("PropertyName")` :删除指定的属性
* `removeAttr("PropertyName PropertyName PropertyName")`:一次性删除多个属性
```javascript
 $("img:eq(1)").removeAttr("src");
 $("img:eq(1)").removeAttr("src alt");
```
####  <a id="propIndex" href="#propIndex">prop</a>  :star2: <a href="#top"> :arrow_up: </a>
`prop也是用来获取和设置属性的值，但和attr也有一些使用场合的区别`
* `prop("PropertyName")`:返回属性的值,返回true/false 对于那些属性
* `prop("PropertyName",false/true)`:设置属性 选中或者没有选中
```javascript
  $("input").prop("disabled",true);
  $.each($("input"),function (index,val) {
      console.log(index +":"+ $(val).prop("disabled"));
  })
```
* `使用注意：`
  * `1.添加属性名称该属性就会生效应该使用prop`
  * `2.prop()方法适用于Boolean值的属性 其他则使用attr`
  * `3.建议以下属性使用prop方法 checked、readonly、selected、disabled、autofocus等`
####  <a id="removePropIndex" href="#removePropIndex">removeProp</a>  :star2: <a href="#top"> :arrow_up: </a>
`使用很少,一般我们都是直接将属性设置为false 就可以了 而不是把他干掉`
* `removeProp("PropertyName")` :删除指定的属性
* `removeProp("PropertyName PropertyName PropertyName")`:一次性删除多个属性
####  <a id="addClassIndex" href="#addClassIndex">addClass</a>  :star2: <a href="#top"> :arrow_up: </a>
`为每个匹配的元素添加指定的样式类名`
* `class名称（字符串）`:`每个匹配元素添加的一个或多个用空格隔开的样式名`
* `function(index, currentClass)`:`有多少个匹配元素，这个函数就会执行多少次！函数可以接受到两个参数：第一个是当前元素的序号、第二个是当
前元素拥有class  函数内部this代表当前的html元素对象 return 的数据就是类名`
```javascript
 $("input:eq(0)").addClass("input_form");

 $("input").addClass(function (index,currentClassValue) {
     console.log(`${index}: ${currentClassValue}`);
     return "class10"; //添加的类名称
 });
```
####  <a id="hasClassIndex" href="#hasClassIndex">hasClass</a>  :star2: <a href="#top"> :arrow_up: </a>
`确定任何一个匹配元素是否含有给定的（样式）类，返回true或false`
* `hasClass("ClassName")` :返回true或false
```javascript
 let bool = $("input:eq(0)").hasClass("class2");
 console.log(bool);
```
####  <a id="removeClassIndex" href="#removeClassIndex">removeClass</a>  :star2: <a href="#top"> :arrow_up: </a>
`移除集合中每个匹配元素上一个，多个或全部样式`
* `removeClass("ClassName")` :`从元素上面移出指定类`
* `removeClass(function(index, className))`:`第一个是当前元素的序号、第二个是当前元素拥有class  函数内部this代表当前的html元素对象 返回一个或多个(用空格隔开)将要被移除的样式名`

```javascript
 $("input:eq(0)").removeClass("class1");
```

####  <a id="toggleClassIndex" href="#toggleClassIndex">toggleClass</a>  :star2: <a href="#top"> :arrow_up: </a>
` 切换！如果存在（不存在）类就删除（添加）这个类`
* `toggleClass()`:`不传参数 对已有的class进行切换！`
* `toggleClass(StringOfClass)`:`传入类型: String 在匹配的元素集合中的每个元素上用来切换的一个或多个（用空格隔开）样式类名`
* `toggleClass(Function( Integer index, String className ) )`:`index 为序号 className 当前元素拥有的class返回应该显示的样式`
```javascript
 $("input:eq(0)").toggleClass("class1");
```
####  <a id="htmlIndex" href="#htmlIndex"> html </a>  :star2: <a href="#top"> :arrow_up: </a>
`获取集合中第一个匹配元素的HTML内容 或 设置每一个匹配元素的html内容。`
* `html() => String [返回类型]`:`获取选择的第一个元素在html元素在内容` 
* `html(string) => JqueryObject [返回Jquery类型]`:`设置选择的第一个元素在html元素在内容 返回元素的Jquery 对象` 
```javascript
 $(document).ready(function(){
     console.info($("#form1").html());
     $("#form1").html("<h2> 你们在内容已经被替换了！ 哈哈哈哈</h2>")
 });
```
####  <a id="textIndex" href="#textIndex"> text </a>  :star2: <a href="#top"> :arrow_up: </a>
`得到匹配元素集合中每个元素的文本内容结合，包括他们的后代，或设置匹配元素集合中每个元素的文本内容为指定的文本内容。`

* `text() => String [返回类型]`:`获取选择的第一个元素的所有文本内容包含子代标签的内容` 
* `text(string) => JqueryObject [返回Jquery类型]`:`设置选择的第一个元素在html为输入的文本 返回元素的Jquery 对象` 
```javascript
    $(document).ready(function(){
        let txt= $(".demo-container:eq(0)").text();
        $(".demo-container:eq(0)").text("我是你家大王哟");
        console.info(txt);
    });
```
####  <a id="valIndex" href="#valIndex"> val</a>  :star2: <a href="#top"> :arrow_up: </a>
`获得匹配元素的当前值！ 用于具有value html属性值的元素上面`

* `val() => String [返回类型]`:`获取具有value 属性的值` 
* `val(string) => JqueryObject [返回Jquery类型]`:`具有value 属性值` 
```javascript
 $(document).ready(function(){
     console.log(`${$("#form1>input:eq(0)").val()}`);
     $("#form1>input:eq(0)").val("123456789ABC");
 });
```
##### 对于select 标签
```html
  <select id="single">
      <option>Single</option>
      <option>Single2</option>
  </select>

  <select id="multiple" multiple="multiple">
      <option selected="selected">Multiple</option>
      <option>Multiple2</option>
      <option selected="selected">Multiple3</option>
  </select><br/>

  $(document).ready(function(){
      $("#single").val("Single2"); //单选的:第二个被选中
      $("#multiple").val(["Multiple2","Multiple"]); //多选的 第一二个被选中
  });
```
####  <a id="cssIndex" href="#cssIndex">css</a>  :star2: <a href="#top"> :arrow_up: </a>
`获取css 属性值,如果用户没有设置,那么会返回css 默认值`
* `css( propertyName)=> String `:`返回某一个css 属性值`
* `css( propertyNames) => Array`:`返回多个属性的值,成数组格式返回，字符串数组`
* `css( propertyName, value) `:`设置属性的值`
* `css( properties ) 键值对`:`设置多个对象`
* `css( propertyName, function(index, value) )`:`你们懂得 都是套路 就不解释了 `
```javascript
 $(document).ready(function(){
     var fot =  $("#form1").css("font-size");
     var clr =  $("#form1").css("color");
     console.info("font-size:"+fot);
     console.info("color:"+clr);
     $("#single").css({
         "width":"200px",
         "height":"30px"
     });
 });
```
####  <a id="heightIndex" href="#heightIndex">height</a>  :star2: <a href="#top"> :arrow_up: </a>
`获取匹配元素集合中的第一个元素的当前计算高度值 或 设置每一个匹配元素的高度值。`
* `height() => number`:`获得第一个元素的当前高度`
* `height( value[number] )`:`设置每一个匹配元素的高度值。`
* `height( function(index, height){})`:`this指向元素集合中的当前元素 索引/当前高度值`
```javascript
 $("#getp").click(function () {
   showHeight("paragraph", $("p").height());
 });
```
####  <a id="widthIndex" href="#widthIndex">width</a>  :star2: <a href="#top"> :arrow_up: </a>
`获取匹配元素集合中的第一个元素的当前计算宽度值 或 设置每一个匹配元素的宽度值。`
* `width() => number`:`获得第一个元素的当前宽度`
* `width( value[number] )`:`设置每一个匹配元素的宽度值。`
* `width( function(index, height){})`:`this指向元素集合中的当前元素 索引/当前宽度值`
```javascript
 $("#getp").click(function () {
   showHeight("paragraph", $("p").width());
 });
```
####  <a id="offsetIndex" href="#offsetIndex">offset</a>  :star2: <a href="#top"> :arrow_up: </a>
`在匹配的元素集合中，获取的第一个元素的当前坐标，或设置每一个元素的坐标，坐标相对于文档`
* `offset()`：`获得元素的位置 JqueryCoordinate 具有两个属性 top left 反应元素的位置相当于网页的左上方` 
* `offset( {top:number,left:number} )`:`设置位置`
* `offset( function(index, coords) )`:`你们都懂的 cords表示当前元素的坐标`
```javascript
 $(document).ready(function (event) {
     var coordinate =$(".class1").offset();
     console.log("left :"+ coordinate.left);
     console.log("top :"+ coordinate.top);

     var coor = { top: 150, left: 150 };//改变坐标
     $(".class1").offset(coor);
 });
```
####  <a id="scrollLeftIndex" href="#scrollLeftIndex">scrollLeft</a> :star2: <a href="#top"> :arrow_up: </a>
`获取匹配的元素集合中第一个元素的当前垂直滚动条的位置或设置每个匹配元素的垂直滚动条位置。`
* `scrollLeft()`:`获取值`
* `scrollLeft( value )`:`设置值`
####  <a id="scrollTopIndex" href="#scrollTopIndex">scrollTop</a> :star2: <a href="#top"> :arrow_up: </a>
`获取匹配的元素集合中第一个元素的当前垂直滚动条的位置或设置每个匹配元素的水平滚动条位置。`
* `scrollTop()`:`获取值`
* `scrollTop( value )`:`设置值`
####  <a id="innerWidthIndex" href="#innerWidthIndex">innerWidth</a> :star2: <a href="#top"> :arrow_up: </a>
`为匹配的元素集合中获取第一个元素的当前计算宽度值,包括padding，但是不包括border。`
####  <a id="innerHeightIndex" href="#innerHeightIndex">innerHeight</a> :star2: <a href="#top"> :arrow_up: </a>
`为匹配的元素集合中获取第一个元素的当前计算高度值,包括padding，但是不包括border。`
####  <a id="outerWidthIndex" href="#outerWidthIndex">outerWidth</a> :star2: <a href="#top"> :arrow_up: </a>
`获取元素集合中第一个元素的当前计算高度值,包括padding，border和选择性的margin。返回一个整数（不包含“px”）表示的值  ，或如果在一个空集合上调用该方法，则会返回 null。`
####  <a id="outerHeightIndex" href="#outerHeightIndex">outerHeight</a> :star2: <a href="#top"> :arrow_up: </a>
`获取元素集合中第一个元素的当前计算宽度值,包括padding，border和选择性的margin。（注：返回一个整数（不包含“px”）表示的值，或如果在一个空集合上调用该方法，则会返回 null。）`

