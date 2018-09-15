<a id="top" href="#top">Jquery 事件 :maple_leaf:</a> 
----
`我们伟大的jQuery竭尽全力的把浏览器之间的不一致从咱们眼前隐藏起来，从而使我们使用起来更加简单，方便！统一绑定事件的方法`
- [x] :maple_leaf: <a href="#EventBuildingByOn">`通过On绑定事件处理函数`</a>
    -  `on('事件类型'[,选择器][,数据],handler(eventObject) )`
    -  `on(对象[,选择器] [,数据] )`
- [x] :maple_leaf: <a href="#RemoveEventBuildingByOn">`移除on方法绑定的事件处理函数`</a>
    -  `off( events [, selector ] [, handler ] )`
    -  `off( 事件对象 )`
    -  `off()`
- [x] :maple_leaf: <a href="#JqueryEventObject">`Jquery事件对象`</a>
- [x] :maple_leaf: <a href="#EventBuildingBybind">`使用bind绑定事件处理函数`</a>
- [x] :maple_leaf: <a href="#RemoveEventBuildingByBind">`移除bind方法绑定的事件处理函数`</a>
- [x] :maple_leaf: <a href="#CallEventByUserself">`JQuery人工调用事件处理函数`</a>
    -  `trigger( eventType [, extraParameters ] )`
    -  `triggerHandler( eventType [, extraParameters ] )`
- [x] :maple_leaf: <a href="#CallEventByUserself">`JQuery绑定事件处理函数的快捷方法`</a>
    -  `click(function(){})`
    -  `load(function(){})`
    -  `scroll(function(){})`
    -  ...

####  <a id="EventBuildingByOn" href="#EventBuildingByOn">通过On绑定事件处理函数</a>  :star2: <a href="#top"> :arrow_up:</a> 
 ` 从jQuery1.7版本开始，on() 方法是将事件处理程序绑定到文档的首选方法！`
##### :one: jQuery对象.on('事件类型'[,选择器][,数据],handler(eventObject) ) <a href="#top"> :arrow_up:</a> 
* **`事件类型`**： `一个或多个空格分隔的事件类型和可选的命名空间`
* **`选择器`**：`一个选择器字符串，用于过滤出被选中的元素中能触发事件的后代元素。如果选择器是 null 或者忽略了该选择器，那么被选中的元素总是能触发事件，
 传入选择器就代表，在绑定目标的后代范围内，与选择器相匹配的元素在发生指定事件类型时才会执行这个处理函数！,传不传选择器，完全就是两个世界！传入选择器
 会非常的强大！`
* **`数据`**：`如果data参数传给.on()并且不是null 或者 undefined，那么每次触发事件时，data参数都传递给处理程序。data
        参数可以是任何类型，但如果是字符串类型时，那么selector参数必须提供，或明确地传递null，这样的 data 参
        数不会误认为是选择器。最好是使用一个对象（键值对） ，所以可以作为属性传递多个值`       
* **`事件处理函数`**:` 事件被触发时，执行的函数。若该函数只是要执行return false的话，那么该参数位置可以直接简写成 false`        
```javascript
   $(document).ready(function(){
       $("#load").on("click",null,null,function(){
           alert("你点我啊");
       })
   });
```
```javascript
    $(document).ready(function() {
        $("#myDiv").on("click", "p", function(event) {
            alert("你点我啊");
            alert(event.target.tagName);
        });
        $("#myDiv").append("<p>我是你爷爷啊</p>");
    });
```
##### <a href="sendInSelector">传入选择器</a>
`控制器利用了事件委托,规定只要是$("select") 里面的符合选择器的元素都可以加上事件函数,即使是新添加的元素`
* `不选入选择器`
```javascript
  $(document).ready(function() {
      //给ID为myDiv的元素下的所有p标签加上事件
      $("#myDiv p").on("click", function() {
          alert("你点我啊");
      });
      $("#myDiv").append("<p>我是你爷爷啊</p>");
      //新添加的p标签 没有click 事件
  });
```
* `加上选择器可以完美的解决后天元素无事件的问题 利用事件委托 那么新加入的p也具有点击事件处理`
```javascript
  $(document).ready(function() {
      $("#myDiv").on("click", "p", function() {
          alert("你点我啊");
      });
      $("#myDiv").append("<p>我是你爷爷啊</p>");
  });
```
##### <a href="SendDataByJqEvent">传入数据通过jqEvent的data属性获取</a>
`Jquery 支持传入事件对象但是Jquey在原有了Event对象的基础上面有增加了许多的功能方法,启动data就是用来接收我们传入的第三个参数数据`
```javascript
   //当传入的数据是字符串的数据时候,第二个选择器参数需要写上 null也可以
   $(document).ready(function() {
       $("#myDiv").on("click", "p", {
           "name": "JiangXing",
           "Age": 18,
           "Sex": true
       }, function(jqEvent) {
           alert("你点我啊");
           alert(jqEvent.target.tagName);
           console.log(jqEvent.data);
       });
       $("#myDiv").append("<p>我是你爷爷啊</p>");
   });
```
##### <a href="stopDefaultAction">阻止浏览器默认行为</a>
```javascript
  $(document).ready(function() {
      $("#myDiv").on("click", "a", null, false);
  });
```
##### :two: jQuery对象.on(对象[,选择器] [,数据] ) <a href="#top"> :arrow_up:</a> 
`第一个参数是一个事件类型为键 函数为 值的对象 ,选择器效果和上面一样,数据类型`
```javascript
  //同时绑定多个事件类型
  $(document).ready(function() {
     $("#myDiv").on({
         "click": function(jqEvent) {
             alert("你点击了我");
         },
         "mouseenter": function(jqEvent) {
             alert("鼠标进来了");
         },
         "mouseleave": function() {
             alert("鼠标离开了");
         }
     });
  });
```
`为多个事件绑定一个处理函数`
```javascript
  $(document).ready(function() {
      $("#myDiv").on({
          //中间空格分开,并且引号括起来
          "click mouseenter": function(jqEvent) {
              alert("鼠标在我这里");
          },
          "mouseleave": function() {
              alert("鼠标离开了");
          }
      });
  });
```
`传递数据`
```javascript
  $(document).ready(function() {
      $("#myDiv").on({
          "click mouseenter": function(jqEvent) {
              alert("鼠标在我这里");
          },
          "mouseleave": function() {
              alert("鼠标离开了");
          }
      }, null, {
          "name": "李嘉坤",
          "Age": 21
      });
  });
```

####  <a id="RemoveEventBuildingByOn" href="#RemoveEventBuildingByOn">移除on方法绑定的事件处理函数</a>  :star2: <a href="#top"> :arrow_up:</a> 
`使用说明：`
##### off( events [, selector ] [, handler ] )
* `events`：`一个或多个空格分隔的事件类型和可选的命名空间，或仅仅是命名空间`
* `selector`：`一个选择器，当绑定事件处理程序时匹配最初传递给 .on()的那个`
* `handler`：`事件处理函数`
##### off( 事件对象 )
`将事件对象传入，此方法适合在事件处理函数内部，移除自己`
##### off()
`移除匹配结果集，所有的事件处理函数`
```javascript
  $(document).ready(function() {
      $("#myDiv").on({
          "click mouseenter": function(jqEvent) {
              alert("鼠标在我这里");
          },
          "mouseleave": function() {
              alert("鼠标离开了");
          }
      }, null, {
          "name": "李嘉坤",
          "Age": 21
      });
      $("#myDiv").off("click mouseenter");
  });
```
`移出所有事件`
```javascript
   $(document).ready(function() {
       $("#myDiv").on({
           "click mouseenter": function(jqEvent) {
               alert("鼠标在我这里");
           },
           "mouseleave": function() {
               alert("鼠标离开了");
           }
       }, null, {
           "name": "李嘉坤",
           "Age": 21
       });
       $("#myDiv").off();
   });
```
`移出自己`
```javascript
   $(document).ready(function() {
       $("#myDiv").on({
           "click mouseenter": function(jqEvent) {
               alert("鼠标在我这里");
               $("#myDiv").off(jqEvent); //移出自己
               return null;
           },
           "mouseleave": function() {
               alert("鼠标离开了");
           }
       }, null, {
           "name": "李嘉坤",
           "Age": 21
       });
   });
```
####  <a id="JqueryEventObject" href="#JqueryEventObject">Jquery事件对象</a>  :star2: <a href="#top"> :arrow_up:</a> 
 `Jquery 事件对象`
* `jQuery`:`事件对象作为事件处理程序的参数，对原生事件对象中最常用的属性以及事件对象中常用的方法进行规范化`
* 成员如下：
  * `currentTarget`:	`这个属性总是等于函数的this`
  * `target`:	`触发事件的事件目标`
  * `data`:`返回绑定事件时传递给绑定方法的可选数据参数`
  * `pageX`:`相对于页面左上角的鼠标位置`
  * `pageY`:`相对于页面左上角的鼠标位置`
  * `preventDefault()`:	`阻止当前时间的默认行为`
  * `stopImmediatePropagation()`:	`阻止剩余的事件处理函数执行并且防止事件冒泡到DOM树上`
  * `stopPropagation()`:		`防止事件冒泡到DOM树上，也就是不触发的任何前辈元素上的事件处理函数`
  * `originalEvent`:		`未经jQuery加工的原始的DOM Event对象`
  * `isDefaultPrevented()		若已经调用过preventDefault()方法则返回true`
  * `isImmediatePropagationStopped()	若已经调用过stopImmediatePropagation()方法则返回true`
  * `isPropagationStopped()		若已经调用stopPropagation()方法则返回true`
  * `relatedTaregt		仅对鼠标事件有效，返回该鼠标事件有关的元素`
  * `result			事件被触发的一个事件处理程序的最后返回值`
  * `timeStamp`:	`这个属性返回事件触发时距离1970年1月1日的毫秒数`
  * `type`:	`事件类型`
  * `which`:	`针对键盘和鼠标事件，这个属性能确定你到底按的是哪个键 对于keydown返回键码，对于keypress返回ASCII码`
####  <a id="EventBuildingBybind" href="#EventBuildingBybind">使用bind绑定事件处理函数</a>  :star2: <a href="#top"> :arrow_up:</a> 
` 在之前的jQuery版本里面，bind的方法是最常用的用来绑定事件处理函数的方法！相当于是on方法的弱化版，on方法是bind方法的加强版！
bind方法不可以传入选择器，这个方法的内部本身并没有 事件委托的思路在里面！你了解一下就好,以后看到这个函数 知道它的意思就行,与On的区别就是不可以
传递选择器`
##### Query对象.bind('事件类型',[数据,]事件处理函数)
* `事件类型`：`一个或多个空格分隔的事件类型和可选的命名空间`
* `事件处理函数`：`事件被触发时，执行的函数。若该函数只是要执行return false的话，那么该参数位置可以直接简写成 false`
* `数据`：`传入的的对象可用jqEvent.data属性接受`
##### jQuery对象.bind('事件类型',布尔值)
`用来阻止事件默认行为，以及冒泡`
##### jQuery对象.bind(对象,[数据,] )
`移除匹配结果集，所有的事件处理函数`
####  <a id="RemoveEventBuildingByBind" href="#RemoveEventBuildingByBind">移除bind方法绑定的事件处理函数</a>  :star2: <a href="#top"> :arrow_up:</a> 
##### unbind( [eventType ] [, handler(eventObject) ] )
* `events`：`一个或多个空格分隔的事件类型和可选的命名空间，或仅仅是命名空间`
* `handler`：`事件处理函数`
##### unbind(事件对象)
`将事件对象传入，此方法适合在事件处理函数内部，移除自己`
##### unbind()
`移除匹配结果集，所有的事件处理函数`
####  <a id="CallEventByUserself" href="#CallEventByUserself">JQuery人工调用事件处理函数</a>  :star2: <a href="#top"> :arrow_up:</a> 
##### trigger( eventType [, extraParameters ] )
`通过trriger触发函数`
```javascript
 $(document).ready(function() {
     $("#myDiv").on("click", "p,a", null, function() {
         alert("我被摸了");
     })
     $("#myDiv>a").trigger("click");
 });
```
`第二个参数就是绑定函数传入的data`
```javascript
  $(document).ready(function() {
      $("#myDiv").on("click", "p,a", {
          "name": "JiangXing",
          "Age": 18,
          "Sex": true
      }, function(jqEvent) {
          alert("我被摸了");
          console.log(jqEvent.data);
      });

      $("#myDiv>a").trigger("click", {
          "name": "帝王",
          "Age": 25,
          "Sex": true
      });
  }); //好像还是显示的前面的数据 ,如果一开始的data传入为null 还是为null 所以第二个参数不用就好
```
##### 触发自定义事件 利用trigger 
`无法使用triggerHandler 触发非系统定义事件`
```javascript
  $(document).ready(function() {
      $("#myDiv").on("JiangXingDefineShijian", "p,a", null, function(jqEvent) {
          alert("这是自己定义吃事件");
      })
      $("#myDiv>a").trigger("JiangXingDefineShijian");
  });
```

##### triggerHandler( eventType [, extraParameters ] )
`和真实的事件发生不一样，仅仅是触发绑定的函数执行，至于其他的默认行为都会忽略，并且也不会事件传播,冒泡也不会有`

####  <a id="CallEventByUserself" href="#CallEventByUserself">JQuery绑定事件处理函数的快捷方法</a>  :star2: <a href="#top"> :arrow_up:</a> 
 
` blur, focus, focusin, focusout, load, resize, scroll, unload, click, dblclick, mousedown, mouseup, mousemove, mouseover,
mouseout, mouseenter, mouseleave, change, select, submit, keydown, keypress, keyup, error使用方法，直接对选中的元素：
调用对应的快捷方法即可！`
```javascript
  $(document).ready(function() {
      $("#myDiv").click(function(jqEvent) {
          console.log("点击我啊!");
          console.log("来触发我啊");
          console.log(this.id);
      });

      $("#myDiv").trigger("click");
  });
```
