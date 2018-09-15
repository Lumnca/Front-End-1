<a id="top" href="#top">JavaScript 原生Form :maple_leaf:</a> 
----
`一个网站的关键在于表单，他决定用户的输入,向服务器提交的数据,Js对于它有许多的方法和属性对象,以便我们开发更优秀的前端界面`
- [x] :maple_leaf: <a href="#FormBasicKnow">`表单的基本知识`</a>
  - <a href="#GetFromElement">`获取表单：HTMLFormElement `</a> 
  - <a href="#FormSubmit">`提交表单：Submit `</a> 
  - <a href="#resetform">`重置表单：Reset `</a> 
  - <a href="#formfiled">`表单字段 element`</a> 
  - <a href="#formfiledProperty">`表单字段公共属性`</a> 
  - <a href="#formfiledFunction">`表单字段公共方法`</a> 
  - <a href="#formfiledEventFunction">`表单字段公共事件`</a> 
- [x] :maple_leaf: <a href="#TextScript">`文本框脚本`</a>
  - <a href="#getvaluetext">`获取表单文本的值`</a> 
  - <a href="#Shoosetext">`选择文本select`</a> 
  - <a href="#keypressevent">`过滤输入`</a>
- [x] :maple_leaf: <a href="#copypaste">`粘贴板事件`</a>
- [x] :maple_leaf: <a href="#">``</a>

####  <a id="FormBasicKnow" href="#FormBasicKnow">表单的基本知识</a>  :star2: <a href="#top"> :arrow_up:  :arrow_up:</a>
<a href="#">`表单对应：HTMLFormElement  --->继承自 HTMLElement`</a> <br/>

* `在HTML中，表单由form标签，在javascript中，表单对应HTMLFormElement类型，HTMLFormElement类型继承HTMLElement类型，所
有它和其他的Element元素有相同的默认属性，同时它也有自己的属性和方法：`
  * `acceptCharset`：`服务器能够处理的字符集；等价于 HTML 中的 accept-charset 特性。`
  * `action`：`接受请求的 URL；等价于 HTML 中的 action 特性 。`
  * `elements`：`表单中所有控件的集合（HTMLCollection）。`
  * `enctype`：`请求的编码类型；等价于 HTML 中的 enctype 特性。`
  * `length`：`表单中控件的数量。`
  * `method`：`要发送的 HTTP 请求类型，通常是"get"或"post"；等价于 HTML 的 method 特性。`
  * `name`：`表单的名称；等价于 HTML 的 name 特性。`
  * `reset()`：`将所有表单域重置为默认值。`
  * `submit()`：`提交表单。`
  * `target`：`用于发送请求和接收响应的窗口名称；等价于 HTML 的 target 特性`
##### <a href="#GetFromElement" id="GetFromElement">`获取表单：HTMLFormElement `</a> <br/>
`每一个表单都应该有一个唯一的id和name 且id和name应该相同`
* `我们可以通过id或者name获取`：`var formElement=document.getElementById("form1");` 
* `通过document.forms来取得页面中的所有表单元素`:`var forms=document.forms;`
* `通过forms属性通过数组字典获取form`：`var firstForm=document.forms[0];` `var form2=document.forms['form2'];`
```javascript
window.onload=function(){
  var formElement=document.getElementById("form1");
  console.log("表单提交方式："+formElement.method);
  console.log("表单请求的编码类型："+formElement.enctype);
  console.log("表单中控件数目："+formElement.length);
  console.log("表单提交服务器: "+formElement.action);
  console.log("表单名称："+formElement.name);
  console.log("Form 表单个数: ["+formElement.elements.length +"]");
  console.log("Form Target: "+formElement.target);

  var forms=document.forms;
  console.log("HTML表单数目: "+forms.length);
}
```
##### <a href="#FormSubmit" id="FormSubmit">`提交表单：submit submit事件 `</a> 
`每一个表单里面的input或者,type为submit的button,或者图像按钮 都可以下直接提交表单`
```html
 <input type="submit" value="提交" class="btn btn-warning btn-sm"  />
 <button type="submit" class="btn btn-danger btn-sm">提交</button>
 <input type="image" src="../Resources/Image/Icon/button.png" width="25px" />
```
`当浏览器在将请求发送给服务器之前会触发submit事件,这样就有机会验证表单数据,这样我们就有机会验证表单数据,并据此决定是否允许表单提交,如果想住个提交
，那么阻止这个事件的默认行为就可以取消表单提交`
```javascript
formElement.addEventListener("submit",function(event){
 alert("输出错误,无法提交");
 this.submit();
 event.preventDefault();//取消浏览器默认事件
},false);
```
##### <a href="#resetform" id="resetform">`重置表单：reset() reset事件 `</a> 
`用户单击重置,表单会被重置。使用type 特性值的<input> 或<button> 都可以创建重置按钮,如下面的例如所示。`

````html
 <input type="reset"  value="Reset" />
 <button type="reset">重置</button>
````
`表单重置的时候也会在重置之前触发reset事件--如果阻止默认事件那么会让表单放弃提交,使用form.reset() 方法可以提交表单`
```javascript
formElement.addEventListener("reset",function(event){
  alert("无法重置");
  //this.reset();
  event.preventDefault();//取消浏览器默认事件
},false);
```

#####  <a id="formfiled" href="#formfiled">表单字段：elements </a>  :star2: <a href="#top"> :arrow_up: </a>
`form 的属性elements 属性 可以让你以name字典或者 数组索引的方式访问form表单的所有input textare fieldset button 控件`
```javascript
  console.log(formElement.elements["StudentID"]);
  console.log(formElement.elements[0]);
  
  <input type="radio" name="color" value="Red" /> Red
  <input type="radio" name="color" value="Yellow" /> Yellow
  <input type="radio" name="color" value="Blue" /> Blue
```
**`Radio的问题 `**
```html           	
console.log(formElement.elements["color"]);
//输出了是一个RadioNodelist[input input input] 集合
<input type="radio" name="color" value="Red" /> Red
<input type="radio" name="color" value="Yellow" /> Yellow
<input type="radio" name="color" value="Blue" /> Blue
```
#####  <a id="formfiledProperty" href="#formfiledProperty">表单字段公共属性</a>  :star2: <a href="#top"> :arrow_up: </a>
* Form 表单字段拥有的一些相同的属性
  * `disabled`：`布尔值，表示当前字段是否被禁用。`
  * `form`：`指向当前字段所属表单的指针；只读。`
  * `name`：`当前字段的名称。`
  * `readOnly`：`布尔值，表示当前字段是否只读。`
  * `tabIndex`：`表示当前字段的切换（tab）序号。`
  * `type`：`当前字段的类型，如"checkbox"、 "radio"，等等。`
    * `<select>...</select>`:**`select-one`**
    * `<select multiple>...</select>`:**`select-multiple`**
    * `<button>..</button>`:**`submit`**
  * `value`：`当前字段将被提交给服务器的值。对文件字段来说，这个属性是只读的，包含着文件在计算机中的路径`
```javascript
  console.log("表单字段 value: "+formElement.elements[0].value);
  console.log("表单字段 disabled: "+formElement.elements[0].disabled);
  console.log(formElement.elements[0].tabIndex);
  console.log(formElement.elements[0].name);
  console.log(formElement.elements[0].readOnly);
  console.log(formElement.elements[0].form.id);
```
`有时候在我们提交表单以后,我们就应该将提交按钮设置为disable 以免用户重复提交,为此我们可以监听submit事件,当用户提交按钮以后就禁用按钮,一直到得到返回之后,如果是Ajax 那么就是等ajax 回调函数执行的时候 在重新启用它`

####  <a id="formfiledFunction" href="#formfiledFunction">表单字段公共方法</a>  :star2: <a href="#top"> :arrow_up: </a>
* `公有的方法有两个`
  * `focus()`:`可以将浏览器焦点设置到表单的字段上面 ----请注意是方法  不是 onfocus事件 ，但是html5新增的autofocus 属性`
  * `blur()`：`可以使得字段失去焦点`
  
####  <a id="formfiledEventFunction" href="#formfiledEventFunction">表单字段公共事件</a>  :star2: <a href="#top"> :arrow_up: </a>
* 公共的事件
  * focus 焦点事件： `当浏览器的字段获得焦点的时候触发`
  * blur 失去焦点事件 ：`失去焦点`
  * change : `value的值改变或者 <select> 标签的选项改变`
####  <a id="TextScript" href="#TextScript">文本框脚本</a>  :star2: <a href="#top"> :arrow_up: </a>
* `在HTML中，有两种方式来表现文本框：一种是使用<input>元素的单行文本框，另一种是使用<textarea>的多行文本框。这两个控件非常相似，而且多数时候的行为也差不多。不过，它们之间仍然存在一些重要的区别。`
* `要表现文本框，必须将<input>元素的type特性设置为”text”。而通过设置size特性，可以指定文本框中能够显示的字符数。通过value特性，可以设置文本框的初始值，而maxlength特性则用于指定文本框可以接受的最大字符数。`
* `相对而言，<textarea>元素则始终会显示为一个多行文本框。要指定文本框的大小，可以使用rows和cols特性。其中rows特性指定的是文本框的字符行数，而cols特性指定的是文本框的字符列数。`

#####  <a id="getvaluetext" href="#getvaluetext">获取表单文本的值</a>  :star2: <a href="#top"> :arrow_up: </a>
`要是用value 属性,才能获得input 的value值,获得控件的文本`
```javascript
 var input_text = document.forms[0].elements["userinput"];
 var val = input_text.value;
 console.log("用户输入:"+val);
```
#####  <a id="Shoosetext" href="#Shoosetext">选择文本方法/事件 </a>  :star2: <a href="#top"> :arrow_up: </a>
`文本控件都有哦一个select事件,可以让控件选择整个文本,当然这个时候最好当焦点在文本框的时候才选择文本才好,所有最好按照用的需求来使用这个方法`<br/>
**`select 方法`**
```javascript
 var input_text = document.forms[0].elements["userinput"];
 input_text.select();
```
**`select 事件`**
* `当用户选择了文本的时候触发,并且h5给我们提供了两个有用的属性`
  * `selectionStart`:`用户选择文本的开始位置索引`
  * `selectionEnd`:`用户选择文本的结束位置索引`
```javascript
  window.onload=function(){
    let val;
    document.getElementById("UserInfoSelect").addEventListener("select",function(event){
      val=this.value.substring(this.selectionStart,this.selectionEnd);	
      alert("用户选择:"+val);
    },false);
  }
```
**`选择部分文本:`** `选择部分文本可以使用setSelectionRange() 方法 使用这个访问应该在调用这个方法之前或之后就调用focus方法聚焦到文本框,IE8之前支持的是通过 createTextRange() 方法创建一个范围,并将其放在恰当的位置上,然后在调用moveStart和moveEnd 方法将范围移动到位 在调用这些方法之前
还有调用collapse 方法将范围折叠刀文本框的开始位置`
```javascript
 range.collpase(true);
 range.moveStart("character",0);
 range.moveEnd("character",5);
 range.select()
```
**`IE9/Firefox/Chrome/Opera 都支持的方法`**
```javascript
  var txt= document.getElementById("UserInfoSelect");
  txt.setSelectionRange(1,20);
  txt.focus();
```
#####  <a id="keypressevent" href="#keypressevent">过滤输入</a>  :star2: <a href="#top"> :arrow_up: </a>
`过滤输入最快捷的方式就是监控keypress 事件,然后阻止浏览器的默认事件就可以阻止用户的输入，但是因为输入法的关系用户还是可以输入中文数字和英文
已经不可以输入了`
```C#
 txt.addEventListener("keypress",function(event){
   event.preventDefault();
 },false);
```
##### <a id="copypaste" href="#copypaste">粘贴板事件</a>  :star2: <a href="#top"> :arrow_up: </a> 
* 关于粘贴复制剪切操作的事件
  * `beforecopy`：`在发生复制操作前触发`
  * `copy`：`在发生复制操作时触发`
  * `beforecut`：`在发生剪切操作前触发`
  * `cut`：`在发生剪切操作时触发`
  * `beforepaste`：`在发生粘贴操作前触发`
  * `paste`：`在发生粘贴操作时触发`
* 访问剪切板中的数据
  * `使用clipboardData对象`
  * `1.这个对象有三个方法`
    * `getDate`:`获取数据`
    * `setDate`：``
    * `clearDate`:``
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>





