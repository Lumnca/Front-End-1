### [Javascript 客户端检测](#top) :grey_exclamation: <b id="top"></b>
`由于各个浏览器对ECMA 标准的执行有所差别,并且各种互不兼容API的原因,逼得各为程序员在使用Javascript API的时候首先要检查一下是否支持某些功能`
:white_check_mark:

------

- [x] [`1.能力检查`](#enable)
- [x] [`2.IE 的各种不支持`](#target2)
- [x] [`3.怪癖检测`](#target3)
- [x] [`4.用户代理检测`](#target4)

------

#####  :octocat: [1.能力检查](#top) <b id="enable"></b> 
`不要万不得已千万不要去检查客户端,去区分Javascript 在那个浏览器执行,除非你面对的是IE,需要提醒用户,求求你不要用IE了下载其他浏览器吧！`
`Javascript 能力监测就很常用,被广泛使用,能力检查的目标不是这是哪一个浏览器,而是,你是否支持这个能力`

```node
if(object.propertyInQuetion){
    //使用 object.propertyInQuetion
}
```
##### 举个栗子
`IE5 不支持 document.getElementById()，它提出的API 是 docuemnt.add[]`
```c#
function getElementByIdCross(id){
    if(document.getElementById){
        return document.getElementById(id);
    }else if(document.all){
        return document.all[id];
    }else{
        throw new Error("No Way To Suppert get Element By Id");
        console.error("No Way To Suppert get Element By Id");
    }
}
```
##### 更加可靠的能力检查
`能力检测本质是想知道某个特性是否会按照适当方式行事,而不是这个特性存不存在`
> `举个栗子`：`检测一下这个对象是否支持排序方法`
```node
function isSortable(object){
  return typeof object.sort == "function";
}
```
* `当然有时候扯鬼的是 IE 会把你看似是 函数的东西 typeof 返回 object 例如 IE8及其之前的 document.createElement 返回 object 而不是 function`
* `就不再说 其他的IE问题了 求求你放弃IE吧`
##### :octocat: [2.IE 的各种不支持](#top) <b id="target2"></b> 
* `IE8 之前的版本不支持 innerWidth 属性`
* `IE5 不支持 document.getElementById`
* `IE8 及其之前版本的 typeof document.createElement 返回 object 而不是 function`
#####  :octocat: [3.怪癖检测](#top) <b id="target3"></b> 
`怪癖检测的目的是,对于相同的ECMA标准我支持了,但是支持方式不一样,我这个浏览器的支持方式,和你们都不一样`
* `IE8 早期版本某个实例属性与[[Enumrable]]标记为 false的某个原型属性同名,那么该属性不会出现在 fon-in属性中`
```node
//检测代码 。。。自己写吧
```

#####  :octocat: [4.用户代理检测](#top) <b id="target4"></b> 
[**`此处要看懂需要知晓 HTTP协议 推荐书籍 <<图解HTTP>>`**](#top)
`通过检测用户代理字符串[navigator.userAgent] 来确定实际使用的浏览器。在每一次HTTP请求中,用户代理字符串都是作为相应首部发送的，在服务端检测用户代理
来确定用户使用的是什么浏览器,浏览器是pc版本,还是移动版本.是一种常用并且广泛使用和接受的做法.但是浏览器端就是一种万不得已采用的做法,优先使用能力检测和
怪癖检测！`

##### 用户代理字符串进过不断发展 [百度百科](https://baike.baidu.com/item/%E7%94%A8%E6%88%B7%E4%BB%A3%E7%90%86/1471005?fr=aladdin)
* `最开始的长度`
```
 世界第一款浏览器的用户代理字符串 1993 NCSA
 Mosaic/0.9  
```
* `现在 请打开浏览器 F12 检测网络HTTP请求中的 User-Agent字段 `

* `火狐的`
```node
"Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:64.0) Gecko/20100101 Firefox/64.0"
```

* `谷歌的`
```node
"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) 
Chrome/72.0.3610.2 Safari/537.36"
```

* `Edge 浏览器`
```node
"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) 
Chrome/64.0.3282.140 Safari/537.36 Edge/17.17134"
```
##### 用户代理的函数太多了 网上一找一大把 自己百度吧
* `核心就一点 他们所有的解析都是依据` `navigator.userAgent` `字符串的`



--------------------
`作者:` `KickGod` 
`完成时间`:`2019年1月1日21:45:43`
`备注信息`: `任意观看使用` 
