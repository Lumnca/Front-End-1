
<a id="top" href="#top">JavaScript 原生Event  :maple_leaf:</a> 
----
`JS与HTML之间的交互式通过事件实现的,事件就是文档或浏览器窗口发生的一些特点交互瞬间,可以使用侦听器来预订事件,由于不同的DOM版本 又有不同DOM级别的事件,比如DOM0级事件
DOM1 级事件,现在主要浏览器已经实现了DOM2级事件`

- [x] :maple_leaf: <a href="#EventStream">事件流</a>
  - <a href="#EventMaoPao">`事件冒泡`</a>
  - <a href="#EventCatch">`事件捕获`</a>
  - <a href="#DomEventStream">`DOM事件流`</a>
- [x] :maple_leaf: <a href="#EventDealWith">`事件处理程序`</a>
  - <a href="#HTMLEventBuilder">`HTML事件处理程序`</a>
  - <a href="#DOM1EventBuilder">`Dom0级事件处理程序`</a>
  - <a href="#DOM2EventBuilder">`Dom2级事件处理程序`</a>
  - <a href="#IEEventBuilder">`IE事件处理程序`</a>
- [x] :maple_leaf: <a href="#EventObject">`事件对象`</a>
  - <a href="#DOMEventObject">`DOM中的事件对象`</a>  
  - <a href="#IEEventObject">`IE中的事件对象`</a>
- [x] :maple_leaf: <a href="#EventType">事件类型</a>
  - <a href="#UIEvent">`UI事件`</a>
  - <a href="#FocusEvent">`焦点事件`</a>
  - <a href="#MouseEvent">`鼠标事件`</a>
  - <a href="#wheelEvent">`鼠标滚轮事件`</a>
  - <a href="#TextEvent">`文本事件`</a>
  - <a href="#KeyboardEvent">`键盘事件`</a>
  - <a href="#MulEvent">`合成事件`</a>
  - <a href="#DOMChangeEvent">`DOM结构变得事件`</a>
  - <a href="#HTMLEventType">`HTML5事件`</a>
  - <a href="#DevieceEvent">`设备事件[现代移动响应开发的需求产生]`</a>
  - <a href="#TouchAndGestureEvent">`触摸与手势事件[现代移动响应开发的需求产生]`</a>
- [x] :maple_leaf: <a href="#MemoreEngine">`内存和性能`</a>
  - <a href="#EventDelegate">`事件委托[基于事件冒泡]`</a>
- [x] :maple_leaf: <a href="#StartEventByMe">`模拟事件`</a>


####  <a id="EventStream" href="#EventStream">事件流</a>  :star2: <a href="#top"> :arrow_up:  :arrow_up:</a>
**`事件的拥有问题`**:`就像数个同心圆一样,当你手指触碰到了中心的圆,相当于所有的圆你都触碰到了,事件也是一样的当一个Button 产生了点击事件那么
是否Button 所在的Div也产生了点击事件呢!事件流就是讨论Div到底该不该有点击事件,那些页面部分应该接受事件` <br/>
**`事件流`**:`描述从页面接受事件的顺序,但是又有当年的两位天神IE和Netscape提出了两个相反的事件流概念,IE采用事件冒泡,Netscape采用事件捕获流`
##### <a href="#top" id="EventMaoPao">事件冒泡</a> <a href="#top">:arrow_up:</a>  
`IE采用,事件开始时由最具体的元素(文档嵌套层次最深的那个节点接受),然后逐级向上传播`
```html
<!DOCTYPE html>
<html>
  <head>
      <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
      <meta charset="utf-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Index</title>
  </head>
  <body>
      <div class="panel">
          <button id="ClickMe">惦记我</button>
      </div>
  </body>
</html>
```
`当button被点击过后,发生点击事件,然后事件向上传播到 div 然后 到body发生点击事件,最后到Html发生点击事件`
```html
    
   document 发生事件
     /|\
      |
      body 发生事件 向上传播到document 
       /|\
        |
        div 发生事件 向上传播到div
         /|\
          |
         button 发生事件 向上传播到div
```
**`总结`**:`事件冒泡已经被所有现代浏览器所支持,具体实现由细微的差别,IE5.5 会的事件冒泡会跳过html直接到document IE9/Safari/Firefox/Chrome/ 则将事件一直冒泡到
window对象`
##### <a href="#top" id="EventCatch">事件捕获</a> <a href="#top">:arrow_up:</a> 
`事件捕获和事件冒泡正好相反,它的思想是最不具体的节点应该更早的接受到事件,最具体的节点应该最后接受事件`
```html
     document 发生事件 向下传播到body
       ⬇️
       ⬇️
       body 发生事件 向下传播到div
         ⬇️
         ⬇️
        div 发生事件 向下传播到button
           ⬇️
           ⬇️
          button 发生事件
```
**`总结`**:`现在大多数现代浏览器也都支持这种事件模型,虽然规定要求从document传播但是这些浏览器都是从window对象开始捕获事件,很少有人使用事件捕获`
##### <a href="#top" id="DomEventStream">DOM事件流</a> <a href="#top">:arrow_up:</a> 
`Dom2级事件,规定的事件流包含上个阶段,事件捕获阶段,处于目标阶段,事件冒泡阶段 简短来说就是  先捕获在 冒泡`
```html
     document 发生事件 向下传播到body
       ⬇️                  ⬆️
       ⬇️ 1                ⬆️ 6
       body 发生事件 向下传播到div
         ⬇️             ⬆️ 
         ⬇️ 2           ⬆️ 5
        div 发生事件 向下传播到button
           ⬇️        ⬆️
           ⬇️ 3      ⬆️ 4
          button 发生事件
```
####  <a  id="EventDealWith" href="#EventDealWith">事件处理程序</a>  :star2: <a href="#top"> :arrow_up:  :arrow_up:</a>
`响应事件的函数就是事件处理程序(事件侦听器),事件处理程序的名字以` **`on`** `开头因此click 事件的事件处理程序就是onclick,load事件的处理程
序就是onload,为事件处理程序制定处理函数的方式有好多种`
##### <a href="#top" id="HTMLEventBuilder">HTML事件处理程序</a> <a href="#top">:arrow_up:</a> 
`HTML事件处理程序将Js代码嵌入到HTML标签中,可以在点击的时候执行一段js代码 ,或者执行一个函数,当然绑定的函数要声明在HTML渲染之前才有效`
```html
<!DOCTYPE html>
<html>
  <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Page Title</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
      <script src="js/jquery-3.3.1.min.js"></script>
      <script src="js/bootstrap.min.js"></script>
      <link href="css/bootstrap.min.css" rel="stylesheet">
      <script>
          function Deal(){
              console.log("你点击了我Button");
          }
      </script>
  </head>
  <body>
      <button onclick="Deal()" class="btn btn-danger">点我吧</button>
      <button onclick="console.log(confirm(`你确定要删除吗`))" class="btn btn-danger">点我吧Html事件</button>
  </body>
</html>
```
**`总结`**:`缺点很大将JS代码和HTML代码紧密耦合,不方便改动前端代码`
##### <a href="#top" id="DOM1EventBuilder">Dom0级事件处理程序</a> <a href="#top">:arrow_up:</a> 
`DOM0级事件处理,简单跨浏览器所有浏览器都支持这种绑定事件的方式,使用JS给HTML元素指定事件处理程序,首先要取得操作对象的引用,每个元素都有自己的事件处理
程序` [`HTML事件属性`](http://www.w3school.com.cn/tags/html_ref_eventattributes.asp) `这些属性通常全部小写,例如onclick 将这种属性的值设置为
一个函数`
```html
<!DOCTYPE html>
<html>
  <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Page Title</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
      <script src="js/jquery-3.3.1.min.js"></script>
      <script src="js/bootstrap.min.js"></script>
      <link href="css/bootstrap.min.css" rel="stylesheet">
      <script>
          //window.onload 在整个页面渲染后才执行js代码,不加这个 需要把js代码放到最下面
          window.onload=function(){
              //获得引用
              var btn=document.getElementById("clkmy");
              var btnDom0=document.getElementById("mybutton");
              //绑定事件侦听器
              btn.onclick=function(){
                  var str=btn.innerText;
                  if(str=="点我吧")
                  btn.innerText="我被点了";
                  else{
                      btn.innerText="点我吧";
                  }
              }
              btnDom0.onclick=function(){
                  alert("我被点了怎么办!");
              }    
          }
      </script>
  </head>
  <body>
      <button  id="clkmy" class="btn btn-danger">点我吧</button>
      <button id="mybutton"  class="btn btn-danger">Dom0事件处理程序</button>
  </body>
</html>
```
* 取消事件的方法
```js
   btnDom0.onclick=null; //这样就没有了
```
**`总结`**:`跨浏览器且简单大家都支持`
##### <a href="#top" id="DOM2EventBuilder">Dom2级事件处理程序</a>
`DOM2级事件,提供了两个方法,用于处理指定和删除事件处理程序的操作,所以节点都包含这两种方法,并且它们都接受三个参数,要处理的事件名,作为事件处理程序的函数和一个
布尔值,true 表示在捕获阶段使用时间处理程序, 如果是false表示在冒泡阶段调用时间处理程序,一般都是false`
* addEventListener("EventName",function(){//etc},false)
* removeEventListener("EventName",function(){//etc},false)
**`注意`**:`DOM2级事件 使用addEventListener 添加的事件就必须使用removeEventListener移除,移除传入的参数与添加处理程序时使用的参数相同,这就
意味着通过addEventListener添加的匿名函数无法移除`
* 正常格式
```HTML
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>Page Title</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="js/jquery-3.3.1.min.js"></script>
    <script src="js/bootstrap.min.js"></script>
    <link href="css/bootstrap.min.css" rel="stylesheet">
    <script>
        window.onload=function(){
            //书写引用
            var btn=document.getElementById("clkmy");
            var btnDom0=document.getElementById("mybutton");
            //写好处理函数
            function hander(){
                console.log("你神经病啊!没事儿点我");
            }
            function handerdel(){
                //解除绑定
                btn.removeEventListener("click",hander,false);
                console.log("第一个按钮已经废了");
            }
            //绑定
            btn.addEventListener("click",hander,false)
            btnDom0.addEventListener("click",handerdel,false);
        }
    </script>
</head>
<body>
    <button  id="clkmy" class="btn btn-danger">点我吧</button>
    <button id="mybutton"  class="btn btn-danger">Dom2取消前面的</button>
</body>
</html>
```
----
**`总结`**:`不错 标准写法,如果不需要remove那么直接第二个参数 传递一个函数也是可以的`
 ##### <a href="#top" id="IEEventBuilder">Dom2级事件处理程序</a>
 `IE实现了两个与DOM类似的方法attachEvent() detachEvent() 这两个方法接受相同的两个参数,IE8.0之前只支持冒泡所以没有第三个参数, 事件处理程序会在全局作用域中运行,因此this等于window`
 **`总结`**:`跨浏览器事件的解决方法,本人认为放弃兼容IE浏览器,一切完美,否则用框架吧,JQ VUE....之类的`
 
####  <a id="EventObject" href="#EventObject">事件对象</a>  :star2: <a href="#top"> :arrow_up:  :arrow_up:</a>
`在触发DOM上的某个事件的时候,都会产生一个事件对象Event，这个对象包含着所有与事件有关的信息,包括导致事件的元素,事件的类型,例如鼠标操作导致的事件
会有包含鼠标位置的信息,键盘操作有关于键盘的信息`

##### <a id="DOMEventObject" href="#top">`DOM中的事件对象 `</a><a href="#top">:arrow_up:</a> 
`兼容DOM的浏览器会将一个event对象传入到时间处理程序中,无论指定事件处理程序使用的什么方式(DOM0,dom2),都会传入一个event对象` [`Event对象 官方文档`](https://developer.mozilla.org/en-US/docs/Web/API/Event)
```html
<!DOCTYPE html>
<html>
  <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Page Title</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
      <script src="js/jquery-3.3.1.min.js"></script>
      <script src="js/bootstrap.min.js"></script>
      <link href="css/bootstrap.min.css" rel="stylesheet">
      <script>
          window.onload=function(){
              var btn=document.getElementById("clkmy");
              var btnDom0=document.getElementById("mybutton");
              btn.onclick=function(event){
                  console.info("事件类型:"+event.type); 
                  console.log("事件是否支持冒泡:"+event.bubbles);   
                  console.log("事件是否支持冒泡:"+event.cancelable);  
                  console.log("当前正在处理事件的元素:"+event.currentTarget);   
                  console.log("是否取消的事件的默认行为:"+event.defaultPrevented);   
                  console.log("事件详细信息:"+event.detail);   
                  console.log("调用事件处理程序的阶段:"+event.eventPhase); 
                  // 1.捕获 2:处于目标 3:冒泡  
                  console.log("时间目标:"+event.target); 
              }
          }
      </script>
  </head>
  <body>
      <button  id="clkmy" class="btn btn-danger">点我吧</button>
      <button id="mybutton" onclick="alert(event.type)"  class="btn btn-danger">Dom2取消前面的</button>
  </body>
</html>
```
`Event事件对象中包含许多的属性和方法`

----

|属性/方法|类型|读写|说明|
|:---|:----:|:---:|:-----|
| bubbles|Boolean | 只读|一个布尔值，指示事件是否通过DOM冒泡。|
| cancelable|Boolean | 只读|表明是否可以取消事件的默认行为|
| currentTarget |Element | 只读|对当前注册的事件目标的引用。这是当前要发送事件的对象; 通过重新定位，这可能会发生变化。|
| defaultPrevented |Boolean|只读|指示是否event.preventDefault()已在事件上调用。|
|[eventPhase](https://developer.mozilla.org/en-US/docs/Web/API/Event/eventPhase) |int |只读 |指示正在处理事件流的哪个阶段。|
|detail|Int |只读 |只读信息,事件的详细信息 |
|type|string|只读|事件类型|
|createEvent()  |Event|`方法可执行` |创建一个新事件，然后必须通过调用其initEvent() 方法对其进行初始化  。  |
|stopPropagation() |Function |`方法可执行` |阻止事件进一步捕获或冒泡,如果bubbles |
|preventDefault() |Function |`方法可执行` |取消事件的默认行为 如果cancelable是true 就可以使用这个方法 |
|stopImmediatePropagation() |Function |`方法可执行` |取消事件的默认行为|

----
`通过这些属性,可以完成一些功能`
##### 1.一个函数完成过个事件

```javascript
    window.onload=function(){
        var btn=document.getElementById("clkmy");
        var btnDom0=document.getElementById("mybutton");

        let hander=function(event){
             if(event.type=="click"){
                 let targetID=event.target.id;
                 switch(targetID){
                     case "clkmy":{
                         console.log("这里处理clkmy的事件");
                     } break;
                     case "mybutton":{
                        console.log("这里处理mybutton的事件");
                     }
                     default:{

                     } break;
                 }
             }   
        }
        btn.onclick=hander;
        btnDom0.onclick=hander;r
    }
```
##### 2.阻止浏览器默认的障碍事件
```C#
    document.ontouchstart=function(event){
        event.preventDefault(); //手机上浏览器 手指滑动时  组织浏览器默认切换页面是事件
    }
```
##### <a id="IEEventObject" href="#top">`IE中的事件对象`</a><a href="#top">:arrow_up:</a> 
`你以为我还会考虑IE这个浏览器吗?不存在的不可能的,IE事件对象  不考虑 放弃`

#### <a id="EventType" href="#top">`事件类型`</a><a href="#top">:arrow_up:</a> 
`Web浏览器中的事件有很多的类型二DOM3级事件规定了一下几类事件`</br>
##### <a href="#top" id="UIEvent">UI事件</a> <a href="#top">:arrow_up:</a> 
`不介绍已经废弃的例如DOMActivate 表示元素已经被用户操作(通过鼠标或者键盘)激活 已经废除`
* 0.确定浏览器是否支持DOMativateDOM2级事件</br>
```javascript
    //浏览器是否支持DOM2 HTML事件
    let isSupport=document.implementation.hasFeature("HTMLEvent","2.0");
    alert(isSupport);
    //浏览器是否支持DOM2 UI事件
    let isSupportUiD3=document.implementation.hasFeature("UIEvent","3.0");
    alert(isSupportUiD3);
```
* 1.load 事件</br>
`当页面完全加载后(包含完全加载后Css文件 JS文件 html渲染完成后执行)`
```javascript
  window.onload=function(){
     //执行代码 通常放在head里面是js代码就写在这个里面
  }
```
* `图像也可以触发onload事件`
```html
  <img src="resource/img/wang.jpg" onload="alert(`这张图像加载完成`)">
```
* 2.unload 事件</br>
`事件在用户退出页面时发生。当页面完成卸载后再window上面触发,当所有框架都卸载后再框架上面触发,谷歌/Safira 浏览器并不支持 `
```javascript
 <body  onload="alert("请问要将此页面设置为主页吗？");" onunload="alert("再见");"></body>
```
* 3.abort 事件</br>
`在用户停止下载过程时,如果嵌入的内容没有加载完,则在<object> 元素上面触发`
* 4.error 事件</br>
`当发生JavaScript错误时在window上面触发,例如无法加载图像时候`
* 5.select 事件</br>
`当用户选择文本框<input> /<textare> 中的一个或者多个字符时触发`
* 6.resize 事件</br>
`当窗口或框架的大小变化时在window或框架上面触发`
* 7.scroll 事件</br>
`当用户滚动滚动条的元素的内容时,在该元素上面触发 body元素包含所在家的滚动条`
##### <a href="#top" id="FocusEvent">焦点事件</a> <a href="#top">:arrow_up:</a> 
`焦点事件会在页面元素获得或者失去焦点的时候触发`
* 0.牵扯浏览器是否支持一下事件
```javascript
  <script>
      let isSupport=document.implementation.hasFeature("FoucsEvent","2.0");
      alert(isSupport);
  </script>
```
* 1.blur 事件 <br>
`当页面元素失去焦点的时候触发,这个事件不会冒泡,所有浏览器都支持它`
* 2.DOMFocusIn 事件[废弃 不用看] </br>
`当得到焦点的时候触发,支持冒泡与HTML事件focus等价,,只有Opera支持这个事件,已经废除在DOM3 选择了focusin`
* 3.DOMFocusOut 事件[废弃 不用看] </br>
`当元素失去焦点的时候触发,这个事件是HTML事件bulr的通用版本,只有Opera支持这个事件DOM3已经废弃 选择focusout`
* 4.focus 事件</br>
`当元素获得焦点的时候触发,不会冒泡,全支持`
* 5.focusin 事件</br>
`当元素获得焦点的时候触发,会冒泡,基本上全支持`
* 5.focusout 事件</br>
`当元素失去焦点的时候触发,基本上全支持`
##### <a href="#top" id="MouseEvent">鼠标事件</a> <a href="#top">:arrow_up:</a> 
`最常见的事件了`
* 0.测试支持性
```javascript
    let isSupport=document.implementation.hasFeature("MouseEvents","2.0");//注意一个s的区别
    alert(isSupport);
    let isSupportDom3=document.implementation.hasFeature("MouseEvent","3.0");//注意一个s的区别
    alert(isSupportDom3);
```
* 1.click 事件 </br>
`当鼠标单击鼠标或者按下回车键的时候触发 ,如果把 dblclick 和 click 事件应用于同一元素，可能会产生问题。 `
* 2.mousedown 事件</br>
`当鼠标按下的时候触发`
* 3.mouseup 事件</br>
`当鼠标释放的时候触发`
```javascript
  document.onmousedown=function(event){
      console.log(" 鼠标按下了 鼠标位置:");
      console.log(`(${event.clientY},${event.clientY})` );

  }
  document.onmouseup=function(event){
      console.log(" 鼠标抬起了 鼠标位置:");
      console.log(`(${event.clientY},${event.clientY})` );
  }
 只有在一个元素上面相继触发 mousedown mouseup才会触发click 只有两次触发click事件才能触发dblclick,一般不使用dblclick 
```

* 4.dblclick 事件</br>
`当用户双击的时候触发，我没有触发成功过!`
* 5.mouseenter 事件</br>
`当鼠标从元素外部首次移动到元素范围之内时触发,不冒泡,切光标移动到后代元素上面不会触发Dom3级事件`
* 6.mouseleave 事件</br>
`当鼠标在元素上分移动出去的时候触发,这个事件不冒泡,移动到后代元素不触发`
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>Page Title</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="js/jquery-3.3.1.min.js"></script>
    <script src="js/bootstrap.min.js"></script>
    <link href="css/bootstrap.min.css" rel="stylesheet">
    <script>
        window.onload=function(){
            let btn=document.getElementById("load");
            let pan=document.getElementById("panel_data");
            pan.onmouseenter=function(){
                console.log("鼠标进来了");
                pan.classList.remove("panel-primary");
                pan.classList.add("panel-default");
            }
            pan.onmouseleave=function(){
                console.log("鼠标出去了");
                pan.classList.remove("panel-default");
                pan.classList.add("panel-primary");
            }
        }
    </script>
</head>
<body class="container">
     <div class="panel panel-primary" id="panel_data">
         <div class="panel-heading">
            我是一个美好的面板
         </div>
         <div class="panel-body">
            <button class="btn btn-default" id="load">点击加载</button>
         </div>
     </div>
</body>
</html>
```
* 7.mousemove 事件</br>
`鼠标指针在元素内部移动时反复触发`

* 8.mouseover  事件</br>
`当鼠标指针为与元素外部然后用户移入另一个元素边界之内时候时触发,和mouseenter 一样`

* 9.mouseout 事件</br>
`鼠标移出元素的时候触发,和mouseleave一样`

##### 鼠标事件存储的鼠标位置
* 页面位置 
	* X：event.clientX
	* Y：event.clientY
* 视口位置
	* X：event.pageX
	* Y：event.pageY
* 屏幕位置
	* X：event.screenX
	* Y：event.screenY
```javascript
let pan=document.getElementById("panel_data");
pan.onclick=function(event){
//页面位置
	console.log(`视口位置:${event.clientX},${event.clientY}`);
	//视口位置
	console.log(`视口位置:${event.pageX},${event.pageY}`);
	//屏幕坐标
	console.log(`视口位置:${event.screenX},${event.screenY}`);
}
```
##### detail Event熟悉
`鼠标事件对象 Event 中的属性 detail提供了新的信息,这个detail表示的意思,鼠标在一个地方点击的次数,一开始从1开始计数,如果鼠标在mousedown
和mouseup之间移动了位置 则detail会被重置为0`
```javascript
  document.getElementById("clickTime").textContent="点击次数:"+event.detail;
```
##### 触摸设备
* `触摸设备不支持双击 dblclick事件,双击会放大屏幕,而且这个行为无法改变`
**`总结`**:`鼠标移动的触发事件只有三个 mouseleave mouseenter mousemove 都是DOM3级事件`
##### <a href="#top" id="wheelEvent">鼠标滚轮事件</a> <a href="#top">:arrow_up:</a> 
`大家都实现了一个事件mousewheel,并且对于这个事件的Event对象提供了一个 wheelDelta熟悉`
* `wheelDelta 正常为120的倍数 向上滑动为正 向下滑动为负数,但是在Opera9.5以前的版本 正负号正好相反`
*  1.mousewheel 事件</br>
`当鼠标滚动的时候触发`
```javascript
window.onload=function(){
   let isContinue=true;
   function docmouseWheel(event){
   if(isContinue){
      let direction=event.wheelDelta;
      console.log("鼠标滚动了"+direction);                    
   if(direction>0){
      console.log("向上运动");
    }else{
      console.log("向下运动");
    }
   }
  }
  document.addEventListener("mousewheel",docmouseWheel,false);
}
```
##### 触摸设备
* `触摸设备手指移动而滚动时会触发mousewheel和scroll事件`
* `屏幕阅读器的问题 需要开发这个的时候再考虑吧`

##### <a href="#top" id="TextEvent">文本事件</a> <a href="#top">:arrow_up:</a> 
`文本事件只有一个,textInput,这个事件是对keypress的补偿,在文本插入文本框之前会触发这个事件`
*  1.textInput 事件</br>
`在文本插入文本框之前会触发这个事件`
`IE支持一个 inputMethod属性表名文字来源; 不喜欢IE`
* 监控用户输入字体的数量
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>Page Title</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="js/jquery-3.3.1.min.js"></script>
    <script src="js/bootstrap.min.js"></script>
    <link href="css/bootstrap.min.css" rel="stylesheet">
    <script>
        window.onload=function(){
            let tb=document.getElementById("ip_resource");
            function textChange(event){
                $("#showText").text(` 字数: ${this.value.length} `);
            }
            tb.addEventListener("textInput",textChange,false);
            tb.addEventListener("focusout",function(){
                $("#showText").text(` 字数: ${this.value.length} `);
            },false);
            tb.addEventListener("focusin",function(){
                $("#showText").text(` 字数: ${this.value.length} `);
            },false);
            tb.addEventListener("keyup",function(){
                $("#showText").text(` 字数: ${this.value.length} `);
            },false);
        }
    </script>
</head>
<body class="container">
     <div class="panel panel-primary" id="panel_data">
         <div class="panel-heading">
            我是一个美好的面板
         </div>
         <div class="panel-body">
            <input id="ip_resource" type="text" placeholder="请输入资源名称!"
									 class="form-control">
            <br/>
            <button class="btn btn-default" id="load">点击加载</button><span 
						class="text-danger" id="showText"></span>
         </div>
     </div>
</body>
</html>
```

##### <a href="#top" id="KeyboardEvent">键盘事件</a> <a href="#top">:arrow_up:</a> 
* `用户在使用键盘时会出发键盘事件,DOM2级事件,最初规定了键盘事件,但在最终定稿之前删除了相应的内容,所以主要遵循的是DOM0级`
* `DOM3级时间为键盘事件制定了规范,IE率先实现了该规范`
*  1.keydown 事件</br>
`当用户按下键盘上的任意键的时候触发,而且如果按住不放会重发触发这个事件`
*  2.keypress 事件</br>
`当用户按下键盘上的字符键的时候触发,而且如果按住不放会重发触发这个事件 按ECS键也会触发这个事件`
*  3.keyup 事件</br>
`当用户释放按下的键的时候触发`
> 所有元素都支持以上三个事件,但是只有在用户通过文本框出入文本时才最常用到
##### keycode 键码 charCode 按键字符
`当发生keydown keyup事件的时候 event对象的keycode 属性会包含一个代码 数字`
[`1.键码列表`](https://jingyan.baidu.com/article/fec7a1e5d6700a1190b4e725.html)
[`2.键码列表`](http://www.t086.com/article/4315)
* charCode:`貌似不被支持 返回按键的Ascii码`
* key:`DOM3支持取代keyCode新增的返回字符串`
```javascript
	document.onkeydown=function(event){
		console.log("DOM3键码："+event.key);
		console.log("键码："+event.keyCode);
		console.log("ASCII："+event.charCode);    
	}
```
##### <a href="#top" id="MulEvent">合成事件</a> <a href="#top">:arrow_up:</a> 
`复合事件是DOM3事件中新添加了一类事件,用于处理IME输入序列,IME(Input Method Editor 输入法编辑器),可以让用户输入物理键盘上找不到的字符,例如,使用拉丁文键盘的用户通过IME照样能输入日文字符.IME通常需要按住多个键,但最终只输入一个字符,复合事件就是针对检测和处理这类输入而设计的`
*  1.compositionstart 事件</br>
`在IME的文本复合系统打开时触发,表示要开始输入`
*  2.compositionupdate 事件</br>
`在想输入字段中插入新字符时触发`
*  3.compositionsend 事件</br>
`IME的文本复合系统关闭时触发,表示返回正常键盘输入状态`
##### <a href="#top" id="DOMChangeEvent">DOM结构变得事件</a> <a href="#top">:arrow_up:</a> 
`DOM2级的变动事件能够在DOM中的某一部分发生变化的时候提示`
1. `DOMSubtreeModified：在DOM结构中发生任何变化时触发；`
2. `DOMNodeInserted：在一个节点作为子节点被插入到另一个节点中时触发； `
3. `DOMNodeRemoved：在节点从其父节点中被移除时触发； `
4. `DOMNodeInsertedIntoDocument：在一个节点被直接插入文档中或者通过子树间接插入文档后触发。在DOMNodeInserted之后触发； `
5. `DOMNodeRemovedFromDocument：在一个节点被直接从文档中删除或通过子树间接从文档中移除之前触发。在DOMNodeRemoved之后触发。 `
6. `DOMAttrModified：在特性被修改之后触发;`
7. `DOMCharacterDataModified：在文本节点的值发生变化的时候触发。 `
##### <a href="#top" id="HTMLEventType">HTML5事件</a> <a href="#top">:arrow_up:</a> 
* 1.`contextmenu` 事件[`我人笨用不来,或无用的事件`] </br>
`上下文事件,没有什么用`
* 2.`beforeunload` 事件[`我人笨用不来,或无用的事件`] </br>
`下面有三种方法绑定这个事件,然而都不起作用!`
```html
    /*
    window.addEventListener("beforeunload",function(event){
          event.returnValue="你要退出了吗?";
          return "你要退出了吗？";
    },false);
    */
    /*
    window.onbeforeunload=function(event){
       confirm("是否要退出");
       event.returnValue="你要退出了吗?";
       return "你要退出了吗？";
    }
    */
    $(window).on('beforeunload',function(){return'Your own message goes here...';});
```
* 3.`readystatechange` 事件 [`非常有用的事件`]</br>
`支持readystatechange 事件的对象都有一个readyState属性,这个事件的目的是提供与文档或元素的加载状态有关的信息,但这个事件的行为有时候也很难预料`
* `readyState` 的五个值
	* `uninitialized(未初始化)` `对象存在但是尚未初始化`
	*  `loading(载入中)` `对象正在加载`
	*  `loaded(加载完毕)` `对象加载数据完成`
	*  `interactive(已经加载完毕,可以交互) ` `可以操作对象了,但还没有完全加载`
	*  `complete(完成)` `对象已经加载完毕`
```javascript
  //这种代码就不要放到window.onload里面了 
   document.addEventListener("readystatechange",function(event){
     if(document.readyState =="interactive"){
        alert("Content loaded")
     }
   },false)
```
##### <a href="#top" id="DevieceEvent">设备事件</a> <a href="#top">:arrow_up:</a> 
* 1.`orientationchange` 事件</br>
`苹果公司为移动Safari中添加了orientationchange事件，以便开发人员能够确定用户何时将设备由横向查看模式。移动Safari的window.reientation属性可能包含3个值：0表示肖像模式，90表示向左旋转的横向模式，-90表示向右旋转的横向模式。相关文档中还提到一个值，即180表示iPhone头朝下；但这种模式至今尚未得到支持。 
只要用户改变了设备的查看模式，就会触发 orientationchange 事件。此时的 event 对象不包含任何有价值的信息，因为唯一相关的信息可以通过 window.orientation 访问到。下面是使用这个事件的典型示例。`
```javascript
 window.addEventListener("load", function(event){
    var div = document.getElementById("myDiv");
    div.innerHTML = "Current orientation is " + window.orientation;
    window.addEventListener("orientationchange", function(event){
    div.innerHTML = "Current orientation is " + window.orientation;
  });
 },false);
```
* 2.`MozOrientation `事件
`Firefox 3.6 为检测设备的方向引入了一个名为 MozOrientation 的新事件。（前缀 Moz 表示这是特定于浏览器开发商的事件，不是标准事件。）当设备的加速计检测到设备方向改变时，就会触发这个事件。但这个事件与 iOS 中的 orientationchange 事件不同，该事件只能提供一个平面的方向变化。由于 MozOrientation 事件是在 window 对象上触发的，所以可以使用以下代码来处理。`</br> </br>
`此时event对象包含三个属性：x,y和z。这几个属性的值都介于-1到1之间，表示不同坐标轴上的方向。在静止状态下，x值为0，y值为0，z值为1（表示设备处于竖直状态）。如果设备向右倾斜，x值会随之减小；反之向左倾斜会随之增大。类似的如果设备向远离用户的方向倾斜，y值会减小，向接近用户的方向倾斜，y值会增大。z轴检测垂直加速度，1表示静止不动，在设备移动式值会减小（失重状态下值为0）.以下是输出这三个值的一个简单的例子.`<br/><br/>
`触发 deviceorientation 事件时，事件对象中包含着每个轴相对于设备静止状态下发生变化的信息。事件对象包含以下 5 个属性。 
alpha ：在围绕 z轴旋转时（即左右旋转时），y 轴的度数差；是一个介于 0 到 360 之间的浮点数 
beta ：在围绕 x轴旋转时（即前后旋转时），z轴的度数差；是一个介于180到 180之间的浮点数。 
gamma ：在围绕 y轴旋转时（即扭转设备时），z轴的度数差；是一个介于90到 90之间的浮点数。 
absolute ：布尔值，表示设备是否返回一个绝对值。 
compassCalibrated ：布尔值，表示设备的指南针是否校准过。`
```javascript
  window.addEventListener("MozOrientation", function(event){
	   //响应事件
  },false);
```
* 3.`deviceorientation ` 事件 <br/>
`本质上，DeviceOrientation Event 规范定义的 deviceorientation 事件与MozOrientation 事件类似。它也是在加速计检测到设备方向变化时在 window 对象上触发，而且具有与 MozOrientation 事件相同的支持限制。不过，deviceorientation 事件的意图是告诉开发人员设备在空间中朝向哪儿，而不是如何移动。 
设备在三维空间中是靠 x、y 和 z 轴来定位的。当设备静止放在水平表面上时，这三个值都是 0。x轴方向是从左往右，y 轴方向是从下往上，z 轴方向是从后往前.`
```javascript
EventUtil.addHandler(window, "deviceorientation", function(event){
  var output = document.getElementById("output");
  output.innerHTML = "Alpha=" + event.alpha + ", Beta=" + event.beta +
  ", Gamma=" + event.gamma + "<br>";
});
```
* 4.`devicemotion `事件 <br/>
`DeviceOrientation Event 规范还定义了一个 devicemotion 事件。这个事件是要告诉开发人员设备什么时候移动，而不仅仅是设备方向如何改变。例如，通过 devicemotion 能够检测到设备是不是正在往下掉，或者是不是被走着的人拿在手里。 
触发 devicemotion 事件时，事件对象包含以下属性。 
acceleration ：一个包含 x 、 y 和 z 属性的对象，在不考虑重力的情况下，告诉你在每个方向上的加速度。 
accelerationIncludingGravity ：一个包含 x 、 y 和 z 属性的对象，在考虑 z 轴自然重力加速度的情况下，告诉你在每个方向上的加速度。 
interval ：以毫秒表示的时间值，必须在另一个 devicemotion 事件触发前传入。这个值在每个事件中应该是一个常量。 
rotationRate ：一个包含表示方向的 alpha 、 beta 和 gamma 属性的对象。 
如果读取不到 acceleration 、 accelerationIncludingGravity 和 rotationRate 值，则它们的值为 null 。因此，在使用这三个属性之前，应该先检测确定它们的值不是 null 。例如：`
```javscript
EventUtil.addHandler(window, "devicemotion", function(event){
 var output = document.getElementById("output");
 if (event.rotationRate !== null){
   output.innerHTML += "Alpha=" + event.rotationRate.alpha + ", Beta=" +
   event.rotationRate.beta + ", Gamma=" +
   event.rotationRate.gamma;
  }
});
```
**`总结`**:`与 deviceorientation 事件类似，只有 iOS 4.2+中的 Safari、Chrome 和 Android 版 WebKit 实现了devicemotion 事件。`
##### <a href="#top" id="TouchAndGestureEvent">触摸和手势事件</a> <a href="#top">:arrow_up:</a> 
* 1.`touchstart` 事件<br/>
`当手指触摸屏幕时触发；即使已经有一个手指放在了屏幕上也会触发。`
* 2.`touchmove` 事件<br/>
`当手指在屏幕上滑动时连续地触发。在这个世界发生期间，调用preventDefault()可以阻止滚动。`
* 3.`touchend` 事件<br/>
`当手指在屏幕上移开时触发。`
* 4.`touchcancel` 事件<br/>
`当系统停止跟踪触摸时触发。关于此事件的确切触发时间，文档中没有明确说明。`
**`总结`**:`上面这几个事件都会冒泡，也都可以取消。虽然这些触摸事件没有在DOM规范中定义，但它们却是以兼容DOM的方式实现的。因此，每个触摸事件的event对象都提供了鼠标事件中常见的属性：`
* `touches`:`表示当前跟踪的触摸操作的Touch对象的数组。`
* `targetTouches`:`特定于事件目标的Touch对象的数组。`
* `changedTouches`:`表示字上次触摸以来发生了什么改变的Touch对象的数组。`
* `每个Touch对象包含下列属性：`
  * `clientX`:`触摸目标在视口中的x坐标。`
  * `clientY`：`触摸目标在视口中的y坐标。`
  * `identifier`:`标识触摸的唯一ID。`
  * `pageX`：`触摸目标在页面中的x坐标。`
  * `pageY`：`触摸目标在页面中的y坐标。`
  * `screenX`：`触摸目标在屏幕中的x坐标。`
  * `screenY`：`触摸目标在屏幕中的y坐标。`
  * `target`：`触摸的DOM节点目标。`
```javascript
function handlerTouchEvent(event){
    //只跟踪一次触摸
    if(event.touches.length==1 || event.touches.length==0){//书上这里有错
        var output=document.getElementById("output");
        switch(event.type){
            case "touchstart":
                output.innerHTML="Touch started ( "+event.touches[0].clientX+",
								"+event.touches[0].clientY+")";
                break;
            case "touchend":
                output.innerHTML+="<br/>Touch ended ("+event.changedTouches[0].clientX+", 
								"+event.changedTouches[0].clientY+")";
                break;
            case "touchmove":
                event.preventDefault(); //阻止滚动
                output.innerHTML+="<br/>Touch moved ("+event.changedTouches[0].clientX+",
								"+event.changedTouches[0].clientY+")";
        }
    }
}
EventUtil.addHandler(document,"touchstart",handlerTouchEvent);
EventUtil.addHandler(document,"touchend",handlerTouchEvent);
EventUtil.addHandler(document,"touchmove",handlerTouchEvent);
```
* `gesturestart`:`当一个手指已经按在屏幕上而另一个手指又触摸屏幕时触发。`
* `gesturechange`:`当触摸屏幕的任何一个手指的位置发生变化时触发。`
* `gestureend`:`当任何一个手指从屏幕上移开时触发。`
####  <a id="MemoreEngine" href="#MemoreEngine">内存和性能</a>  :star2: <a href="#top"> :arrow_up:  :arrow_up:</a>
`给事件绑定函数,而函数的本质是对象,给页面绑定的事件越多那么对象就越多,占用的内存就越多,页面的交互效果就越差,所以要进来减少绑定事件的个数,这里JS利用事件冒泡实现事件委托,通过一个绑定处理多个元素的一个事件,例如一个button click事件 会一直冒泡到 document 所有我们只需要给document 绑定一个click事件然后利用event事件的target属性,针对不同元素处理不同的事件`
##### <a href="#top" id="EventDelegate">事件委托[基于事件冒泡]</a> <a href="#top">:arrow_up:</a> 
```javascript
function handdegeter(event){
   let target= event.target;
   switch(target.id){
      case "load":{
        alert("点我button了 太高兴了");
      }break;
     case "ip_resource":{
     alert("你要开始填写了吗?");
     }break;
     case "panel_data":{
     alert("你点我panel干嘛")
     }break;
  }
}
document.addEventListener("click",handdegeter,false);
```
####  <a id="StartEventByMe" href="#StartEventByMe">模拟事件 </a>  :star2: <a href="#top"> :arrow_up:  :arrow_up:</a>
`模拟事件的目的就是可以让用户通过js在任何时刻来出发特定的事件`
[`Javascript模拟事件`](https://www.baidu.com/s?wd=Javascript%E6%A8%A1%E6%8B%9F%E4%BA%8B%E4%BB%B6&rsv_spt=1&rsv_iqid=0xb461733200052139&issp=1&f=8&rsv_bp=1&rsv_idx=2&ie=utf-8&rqlang=cn&tn=baiduhome_pg&rsv_enter=1&oq=%25E6%25A8%25A1%25E6%258B%259F%25E4%25BA%258B%25E4%25BB%25B6&rsv_t=c1fetBvpicr0FtMJFi6M15VefazQVqLWNNQcshpZLrsMe5MNBUkKamxcmXnRga2z7zCV&inputT=3081&rsv_sug3=28&rsv_sug1=15&rsv_sug7=000&rsv_pq=af968581000544a5&rsv_sug2=0&rsv_sug4=3458&rsv_sug=1)


