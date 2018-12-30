### [JavaScript BOM](#top) :grey_exclamation: <b id="top"></b>
 `Javascript BOM提供了很多对象,用于访问浏览器的功能,这些功能与任何网页内容无关 ES5的BOM 具有浏览器各种不兼容的地方,好在H5 已经在逐渐规范了`
 :white_check_mark: 

---
> - [x] [`1.window 对象`](#window) 
> - [x] [`2.窗口关系和框架`](#frame) 
> - [x] [`3.窗口位置`](#place) 
>   * [`3.1浏览器相对于屏幕的位置`](#screen)

----

#####  :octocat: [1.window 对象](#top) <b id="window"></b> 
`它是全局作用域 有两个身份`
* :one: `它是通过JavaScript 访问浏览器窗口的一个借口`
* :two: `ECMAScript 规定的Global对象`
```node
var index = 0;

function addItem(num){
    this.index += num;
    return this.index;
}

window.addItem(10);
window.addItem(20);

console.log(window.index);//30

```
#####  :octocat: [2.窗口关系和框架](#top) <b id="frame"></b> 
`如果页面中包含框架 [frame 标签] 则每一个框架都拥有自己window 对象,并且保存在 frame集合中,在frames集合中,可以通过数值索引【从0 开始 从左向右 自上而下】 或者通过 框架名称访问相应的 windo对象`
```html
<body>
    <frameset>
        <iframe src="./frameTop.html" name="top" frameborder="0"></iframe>
        <iframe src="./frameBottom.html" name="bottom" frameborder="0"></iframe>
    </frameset>
</body>
```
* :arrow_lower_left: `1.每个 window对象都有一个name属性 其中包含框架的名称`
* :arrow_lower_left: `2.window.frames[0].parent 执行框架的上层框架 `
* :arrow_lower_left: `3.window.frames[0].window 每一个框架都有自己的 window对象`
```javascript
console.log(window.index);//30

console.log(window.frames.length); //具有两个 frame
console.log(window.frames["bottom"]); // 第二个 
console.log(window.frames[0]); // 第一个top

console.log(window.frames[0].window);//每个frame 都有自己的window 对象

console.log(window.frames[0].parent == window.frames[1].parent); //true
```
----
`请注意 都 9102年了，就不要再你的html文档里面是有 iframe 这种过时的玩意儿了 `

#####  :octocat: [3.窗口位置](#top) <b id="place"></b>
`窗口分好多类, 浏览器窗口 可视区域 页面位置....眼花缭乱的！！！！！并且各个浏览器兼容性还不一样`

##### :one:  [ 3.1 浏览器相对于屏幕的位置](#top) <b id="screen"></b>
`screenLeft screenTop`:`IE Safari Opera Chrome 都支持` <br/>
`screenX ScreenY`:`FireFox Chrome 支持`<br/>
```node
/**
 *  浏览器和屏幕的距离 左上角的距离
 */
 function getScreenPosition(){
    let left = (typeof window.screenLeft == "number") ? window.screenLeft:window.screenX;
    let top = (typeof window.screenTop == "number") ? window.screenTop:window.screenY;
    return [left,top];
 }
```
