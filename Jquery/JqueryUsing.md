<a id="top" href="#top">Jquery 特效 :maple_leaf:</a> 
----
`Jquery 使用去解决一些小问题`

- [x] :maple_leaf: <a href="#windowsize">`窗口大小问题`</a>
   
####  <a id="windowsize" href="#windowsize">Jquery基础特效</a>  :star2: <a href="#top"> :arrow_up:  :arrow_up:</a>   
* `alert($(window).height());`                    `//浏览器时下窗口可视区域高度`
* `alert($(document).height());`                  `//浏览器时下窗口文档的高度`
* `alert($(document.body).height());`             `//浏览器时下窗口文档body的高度`
* `alert($(document.body).outerHeight(true));`    `//浏览器时下窗口文档body的总高度 包括border padding margin`
* `alert($(window).width());`                     `//浏览器时下窗口可视区域宽度`
* `alert($(document).width());`                   `//浏览器时下窗口文档对于象宽度`
* `alert($(document.body).width());`              `//浏览器时下窗口文档body的高度`
* `alert($(document.body).outerWidth(true));`     `//浏览器时下窗口文档body的总宽度 包括border padding margin`
* `alert($(document).scrollTop()); `              `//获取滚动条到顶部的垂直高度`
* `alert($(document).scrollLeft());`              `//获取滚动条到左边的垂直宽度`   

```javascript
window.onload=function(){
    function setMask(){
        $('.mask').height(0);
        $('.mask').width(0);
        let winHeights =[$(window).height(),$(document).height(),
        $(document.body).height(),$(document.body).outerHeight(true)];
        let winWidths = [$(window).width(),$(document).width(),
        $(document.body).width(),$(document.body).outerWidth(true)]
        var maxHeight = winHeights.sort((one,two)=> one<two)[0];
        var maxWidth = winWidths.sort((one,two)=> one<two)[0];
        $('.mask').height(maxHeight);
        $('.mask').width(maxWidth);
    }
    window.addEventListener("resize",setMask,false);
    setMask();
}
```
