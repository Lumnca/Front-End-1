
<a id="top" href="#top">Jquery 特效 :maple_leaf:</a> 
----
`Jquery包含一些简单的特效,但是可以实现很多复杂的功能`
- [x] :maple_leaf: <a href="#JiChutexiao">`基础特效`</a>
   * `hide`
   * `show`
   * `toggle`
- [x] :maple_leaf: <a href="#SlideDownUp">`滑动特效`</a>
   * `slideDown`
   * `slideUp`
   * `slideToggle`
- [x] :maple_leaf: <a href="#fadeoutIn">`淡入淡出特效`</a>
   * `fadeOut`
   * `fadeIn`
   * `fadeTo`
   * `fadeToggle`
- [x] :maple_leaf: <a href="#CreateByYourself">`定制特效`</a>
   * `animate`
- [x] :maple_leaf: <a href="#CreateQueneManger">`创建并管理队列`</a>
   * `queue`
   * `dequeue`
   * `clearQueue`
   * `stop`   
- [x] :maple_leaf: <a href="#PZDL">`配置动画特效`</a>
   * `$.fx.interval`
   * `$.fx.off`
   
####  <a id="JiChutexiao" href="#JiChutexiao">Jquery基础特效</a>  :star2: <a href="#top"> :arrow_up:  :arrow_up:</a>
`基础特效包含消失,`
##### :one: `hide( [duration ] [, easing ] [, complete ] )`
`解释`:`隐藏匹配的元素,可传参数说明,不传参数表示立刻隐藏`
* **`duration`** :`一个字符串或者数字决定动画将运行多久(如果不传第一个参数，但是传了后面的参数那么该参数默认值为400)
                      字符串 'fast' 和 'slow' 分别代表200和600毫秒`
* **`easing`** :`一个字符串，表示过渡使用哪种缓动函数(默认: swing) jQuery自身提供"linear" 和 "swing" 其他过渡效果可以使用相关的插件实现`
* **`complete`** :`在动画完成时执行的函数,函数内部的this指向执行动画的DOM元素`
##### :two: `show( [duration ] [, easing ] [, complete ] )`
`解释`:`显示匹配的元素,可传参数说明和ide一样,不传参数表示立刻隐藏`   
##### :three: `toggle( [duration ] [, easing ] [, complete ] )`
`解释`:`显示或隐藏匹配元素 来回切换`<br/>
`toggle(Boolean)`：`一个布尔值，使用 true 来显示元素，或者 false 隐藏它`

##### 总结:基础特效显[show]藏[hide]切[toggle],三个动作三参数,时长运动与回掉,默认时间400毫 不传参数立即做
     
####  <a id="SlideDownUp" href="#SlideDownUp">滑动特效 </a>  :star2: <a href="#top"> :arrow_up:  :arrow_up:</a>
`滚动来滚动去,向下向上铺展.`
#####  :one: **`slideDown( [duration ] [, easing ] [, complete ] )`**:
`解释`:`用滑动动画显示匹配元素`
#####  :two: **`slideUp( [duration ] [, easing ] [, complete ] )`**:
`解释`:`用滑动动画隐藏匹配元素`
#####  :three: **`slideToggle( [duration ] [, easing ] [, complete ] )`**:
`解释`:`用滑动动画显示或隐藏匹配元素 切换`
##### 总结:滑上滑下相切换 三个参数不能换,时长运动加回掉 个个都可不需要

####  <a id="fadeoutIn" href="#fadeoutIn">淡入淡出特效</a>  :star2: <a href="#top"> :arrow_up:  :arrow_up:</a>
:fast_forward: `fadeOut方法,fadeIn方法,fadeTo方法,fadeToggle方法` :rewind:

##### :one: fadeOut( [duration ] [, easing ] [, complete ] ) 
`解释`:`通过淡出的方式隐藏匹配元素`       
##### :two: fadeIn( [duration ] [, easing ] [, complete ] )
`解释`:`通过淡入的方式显示匹配元素`
##### :three: fadeTo( duration, opacity [, easing ] [, complete ] )
`解释`:`调整匹配元素的透明度`
*  可传参数说明：opacity
   * 类型: Number 0和1之间的数字表示目标元素的不透明度
##### :four: fadeToggle( [duration ] [, easing ] [, complete ] )
`解释`:`通过匹配的元素的不透明度动画，来显示或隐藏它们`
        
        
####  <a id="CreateByYourself" href="#CreateByYourself">定制特效   </a>  :star2: <a href="#top"> :arrow_up:  :arrow_up:</a>
`根据一组 CSS 属性，执行自定义动画`
##### animate( properties [, duration ] [, easing ] [, complete ] )
`可传参数说明：`
* **`properties`**:`一个CSS属性和值的对象,动画将根据这组对象移动值也可以是：+= 或 -=开始的值，那么目标值就是以这个属性的
        当前值加上或者减去给定的数字来计算的比如：left: '+=50'
```
    注意：
        .所有用于动画的属性必须是数字的（例如，width, height或者left可以执行动画），除非另有说明.除了样式属性， 一
        些非样式的属性，如scrollTop 和 scrollLeft，以及自定义属性，也可应用于动画！要设置整个页面的滚动条不可以将
        document或者window传入$函数，必须将html,body一起传入才可得到各个浏览器 的兼容即：$('html,body')，这就是
        规定，这么用就ok了！CSS简写属性（例如font,  border等）没有得到充分的支持，即设置时不要用简写方式！并且， 对
        于这些属性预设值最好不要是"auto" 。
  ```
* **`duration`**:` 一个字符串或者数字决定动画将运行多久(默认: 400) 默认值: "normal"， 三种预定速度的字符串("
              slow", "normal", 或 "fast")或表示动画时长的毫秒数值(如：1000)`
              
* **`easing`**:` 一个字符串，表示过渡使用哪种缓动函数(默认: swing)jQuery自身提供"linear" 和 "swing"`

* **`complete`**:`在动画完成时执行的函数 函数内部的this指向执行动画的DOM元素`:minibus:

```javascript
    $("#ClickController").click(function(){
        $("div:first-of-type").animate({
            "width":'-=50px',
            "height":"-=50px"
        },1000,"swing",function(){
            alert( $(this).width());
        });
    });
```
####  <a id="CreateQueneManger" href="#CreateQueneManger">创建并管理队列</a>  :star2: <a href="#top"> :arrow_up:  :arrow_up:</a>
` 函数在排队，优点，第一个全部执行完成了，第二个才会开始执行，依次，后面都是一样的，不会混乱！`
##### `queue()`
`在匹配的元素上创建函数队列（替换已有队列），或向函数队列中添加函数，queue方法用于，在匹配的元素上，创建队列、替
换已有队列、向已有队列中继续添加函数！`
* `怎么在匹配的元素上创建函数队列 `
  * `jQuery对象.queue('sunshengli',函数数组);`
* `替换已有队列`
  * `jQuery对象.queue('已有队列名称',函数数组);`
* `向已有队列中继续添加函数`
  * `jQuery对象.queue('已有队列名称',function(next){});`
* `获取，指定元素上指定队列中函数的个数（包括正在执行的方法）`
  * `jQuery对象.queue('已有的队列名称').length;`
  * `正在执行的动画方法显示形式为："inprogress"`
```javascript
   //创建一个名为:ConsoleNumber 的队列
   $("#ClickController").queue("ConsoleNumber",[
       function(next){
           console.log("1");
           next();//next表示下一个函数 这里执行下一个函数
       },
       function(next){
           console.log("2");
           next();//next表示下一个函数
       },
       function(next){
           console.log("3");
       }   
   ]);
   //执行队列
   $("#ClickController").click(function(){
       $("#ClickController").dequeue("ConsoleNumber"); //执行队列
   });
```
##### dequeue( [queueName ] )
`执行匹配元素队列的下一个函数`
* `当dequeue()被调用的时候，列队中的下一个函数将从这个列队中被移除，然后再执行。`
* 参数： queueName：一个含有队列名的字符串。（默认是fx，标准的效果队列）

##### clearQueue( [queueName ] )
**`解释`**: :fast_forward:`当clearQueue()方法被访问的时候，所有在这个列队中未执行的函数将被移除 。`:rewind:
* queueName：一个含有队列名的字符串。默认是fx，标准的效果队列
* `这个方法类似stop(true)然而stop()方法只适用在动画中,clearQueue()还可以用来移除用queue()方法添加到队里中的任何函数`
##### `stop( [queue ] [, clearQueue ] [, jumpToEnd ] )`
`停止匹配元素当前 正在运行 的 动画方法`
 * `参数：`
   * **`queue`** ：`停止动画队列的名称（默认值为标准的该元素上面的fx这个动画队列）`
   * **`clearQueue`** ： ` 一个布尔值，指示是否取消已列队动画。默认 false `
   * **`jumpToEnd`** ： ` 一个布尔值指示是否当前动画方法立即完成。默认false`
 * `使用stop方法的传参不同情况：`
``` 
    1）jQuery对象.stop(['fx',]false,false);
       简写方式：jQuery对象.stop();
       作用：停止当前正在运行的动画方法，然后继续执行当前动画队列中的接下来的动画方法！

    2）jQuery对象.stop(['fx',]false,true);
       作用：立刻完成当前正在执行的动画方法，然后继续执行队列中下面的动画方法！

    3）jQuery对象.stop(['fx',]true,false);
       简写方法：jQuery对象.stop(['fx',],true);
       作用：停止正在执行的动画方法，清除队列中其他的动画方法！
    4）jQuery对象.stop(['fx',]true,true);
       作用：立刻完成当前正在执行的动画方法，清除除列队中其他的所有动画方法！
``` 
##### `finish( [queue ] )`
`停止当前正在运行的动画，删除所有排队的动画，并完成匹配元素所有的动画`
* `参数：queue：停止动画队列中的名称(默认: 'fx')`
* `当finish()在一个元素上被调用，立即停止当前正在运行的动画和所有排队的动画（如果有的话），并且他们的CSS属性设置为它们的
 目标值。所有排队的动画将被删除。`
        
####  <a id="PZDL" href="#PZDL"> 配置动画特效 </a>  :star2: <a href="#top"> :arrow_up:  :arrow_up:</a>

##### $.fx.interval
`这个属性可以设置每隔多少毫秒绘制一帧图像。默认是13毫秒。该属性值越小，在速度较快的浏览器中（例如，Chrome），动画执行的越流畅，但是会影响程序的性能并且占用更多的 CPU 资源`
##### $.fx.off
`全局的禁用所有动画当这个属性设置为true的时候，调用时所有动画方法将立即设置元素为他们的最终状态`

```
  补充：
      默认情况下，我们在同一个元素上执行的动画方法，会被自动的放入该元素下的fx队列中！
      fx队列会自动执行里面的第一个方法，当前的动画方法执行完之后还会自动执行fx队列中的下一个方法。
      非动画方法，并不会被放入fx队列中！
```


