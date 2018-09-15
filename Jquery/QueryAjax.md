<a id="top" href="#top">Jquery Ajax :maple_leaf:</a> 
----
`Jquery对Ajax 支持了很多封装和方法,提供了许多的Ajax快捷方法`
- [x] :maple_leaf: <a href="#AjaxFunctionQuick">`jQuery提供的Ajax快捷方法`</a>
  * `$.get()` <a href="#get">:arrow_down:</a> 
  * `$.post()` <a href="#post">:arrow_down:</a> 
  * `$.load()` <a href="#load">:arrow_down:</a> 
  * `$.getScript()` <a href="#getScript">:arrow_down:</a> 
  * `$.getJSON()` <a href="#getJSON">:arrow_down:</a> 
  * `jqXHR` <a href="#getJSON">:arrow_down:</a> 
- [x] :maple_leaf: <a href="#AjaxSupportInterface">`jQuery提供的Ajax底层接口`</a>
  * `$.ajax()`


####  <a id="AjaxFunctionQuick" href="#AjaxFunctionQuick">jQuery提供的Ajax快捷方法</a>  :star2: <a href="#top"> :arrow_up:  :arrow_up:</a>  
`Query定义了一整套操作Ajax的快捷方法，可以方便的执行常见的Ajax任务`

##### :one: <a id="get" href="#get">JQuery.get(url[,data][,success(data,textStatus,jqXHR)][,dataType]);</a> <a href="#top">:arrow_up:</a> 
**解释**: `使用一个HTTP GET请求从服务器加载数据`
* `参数说明:`
   * `url（类型: String） 发送请求的目标URL字符串`
   * `data（类型：对象或者字符串）可选发送给服务器的字符串或Key/value键值对 : {id:10,name:"孙胜利"} 键与值无需进行url编码，jQuery自动帮我们做
   了这些小事情！如果传入的是字符串（查询字符串），为保险起见，请自行将名称和值进行encodeURIComponent()处理！`
   * `success(data,textStatus,jqXHR) 可选 回调函数 接受三个参数`
     * data：`服务器端返回的数据`
     * textStatus：`请求得到的状态`
     * jqXHR：`对象，XHR对象的一个超集:` ` 它里面包含了原生XHR对象的所有成员，并且包含了其他的jQuery方法！`
   * `dataType`:`(类型：字符串) 可以设置的值：html，script，json，jsonp，xml`
     * `从服务器返回的预期的数据格式，不同数据格式，jQuery对它们的默认处理处理起来也是不一样的。`
        * `注：如果要设置该值，我们最好传入上面的回调函数，否则无效！`
        * `默认 智能猜测（可能是html，script，json，xml 中的一种） 根据响应的Content-Type头信息来猜测：`
        * `text/html：html格式`
        * `application/x-javascript 或者text/javascript：js代码`
        * `application/json或者text/json：json格式`
```javascript
    @section scripts{
       <script type="text/javascript">
           $(function () {
               $.get("/MyAjax/GetJson", function (data, textstatus, jqXHR) {
                   console.log(data);
                   $("h2").text(data.Name);
                   for (var val in data.books) {
                       console.log(data.books[val]);
                       let index = parseInt(val) + 1;
                       let str = "<tr><td>" + index + "</td><td>" + data.books[val].Name + 
                       "</td><td>" + data.books[val].Publisher + "</td></tr >";
                       console.log(str);
                       $("#book tbody").append(str);
                   };

               }, "json");
           }) 
       </script>    
    }
```
* C#控制器方法
```C#
  public String GetJson()
  {
      var book1_ = new JObject();
      book1_["Name"] = "React Natice 6.0实践之路";
      book1_["Publisher"] = "China No.1";
      var book2_ = new JObject();
      book2_["Name"] = "JavaScript5 高级教程";
      book2_["Publisher"] = "China No.1";

      var list = new JArray();
      list.Add(book1_);
      list.Add(book2_);
      var bookRestore = new JObject();
      bookRestore["Name"] = "王者图书馆";
      bookRestore["books"] = list;

      return bookRestore.ToString();
  }
```
##### :two: <a id="post" href="#post">JQuery.post(url[,data][,success(data,textStatus,jqXHR)][,dataType]);</a> <a href="#top">:arrow_up:</a> 
`使用一个HTTP POST 请求从服务器加载数据 	参数，使用方式同上！`
```javascript
   $.post("/MyAjax/ReturnInfo", { id: "2016110999" }, function (data, textstatus, jqXHR) {
       console.log(data);
       for (let val in data) {
           let str = '<li><a href="#">' + val+" : "+data[val] + '</a></li>';
           $(".breadcrumb").append(str);
       }

   },"json");
```
* 控制器方法
```C#
    public String ReturnInfo(string id)
    {
        var person = new JObject();
        person["ID"] = id;
        person["Name"] = "CNM";
        person["Age"] = 19;
        person["sex"] = true;
        return person.ToString();
    }
```
##### :three: <a id="load" href="#load">JQuery.load(url[,data][,complete(responseText, textStatus,jqXHR)])</a> <a href="#top">:arrow_up:</a> 
`从服务器载入数据并且将返回的 HTML 代码替换 匹配的元素 的后代元素`
* `如果提供了 "complete" 回调函数，它将在请求处理完之后，并且 HTML 已经被插入完时被调用。回调函数
会在每个匹配的元素上被调用一次，并且 this始终指向当前正在处理的 DOM 元素`
*	`默认使用 GET 方式 ， 如果data 参数提供一个对象，那么使用 POST 方式`
*	`如果 url 参数的字符串中包含一个或多个空格，那么第一个空格后面的内容，会被当成是 jQuery 的选择器，
    从而决定应该加载返回结果中的哪部分内容`
* 控制器
```C#
    [Route("MyAjax/Part/{i:int}")]
    public ActionResult Part(int i)
    {
        ViewBag.TotalPage = i;
        return PartialView();
    }//返回部分视图
```
```javascript
    $("#downpage").load("/MyAjax/Part", { "i": 5 });
```
* part 部分视图
```html
  <ul class="pagination" style="margin:auto">
      <li><a href="#">&laquo;</a></li>
      @for (int i = 1; i <= ViewBag.TotalPage; i++)
      {
          <li><a href="#">@i</a></li>
      }
      <li><a href="#">&raquo;</a></li>
  </ul>
```
##### :four: <a id="getScript" href="#getScript">JQuery.getScript(url,success(script,textStatus,jqXHR))</a>  <a href="#top">:arrow_up:</a> 
`使用一个HTTP GET请求从服务器加载并拿到当前页来执行一个 JavaScript 代码，js代码拿过来就会执行`
* `url`:`（类型: String） 一个包含发送请求的URL字符串`
*	`success(script,textStatus,jqXHR)`:`当请求成功后执行的回调函数`
* 控制器配置
```C#
public String GetScript()
{
    try {
        String path = Server.MapPath("~/Scripts/App/Validation.js");
        path = Path.GetFullPath(path);

        if (System.IO.File.Exists(path)) {
            String js = System.IO.File.ReadAllText(path);
            return js;
        }
        else {
            String js = "console.log('" + path + "');";
            return js;
        }
    }
    catch (Exception ex)
    {
        throw new Exception(ex.Message);
    }
}
```
* JS代码
```javascript
   <script type="text/javascript">
       $(function () {
           $.getScript("/MyAjax/GetScript"); 
       }) 
   </script>    
```
##### :four: <a id="getJSON" href="#getJSON">JQuery.getJSON(url[,data ][,success(data, textStatus, jqXHR)])</a> <a href="#top">:arrow_up:</a> 
`使用一个HTTP GET请求从服务器加载JSON格式的数据`            
* ` jQuery对于JSONP 跨源请求 的支持相当方便，我们只需要在使用getJSON方法时在URL的查询字符串中添加callback=?即可`
* ` jQuery会自动生成一个随机名字的回调函数，并使用它和服务器进行通信，如此简单的即可实现跨域请求！`
           
---------
##### :five:<a id="jqXHR" href="#jqXHR">jqXHR对象</a>  <a href="#top">:arrow_up:</a> 
`知识补充：从jQuery 1.5开始，jQuery提供的所有的Ajax方法（比如我们上面讲的方法，以及后面还没有讲到的jQuery提供的Ajax方法）都会返回一个XHR对象的超集，我们可以简称为jqXHR对象，它里面不仅包含了XHR对象的成员，还包含一些jQuery添加的其他方法，比如：`
* `done(function(data, textStatus, jqXHR) {})` `传入请求成功之后执行的函数`
* `fail(function(jqXHR, textStatus, errorThrown) {})` `传入请求失败之后执行的函数`
* `always(function(data|jqXHR, textStatus, jqXHR|errorThrown) { })` `传入请求完成之后执行的函数`

```javascript
  let jqXHR=  $.get("/MyAjax/GetJson", function (data, textstatus, jqXHR) {console.log(data);}, "json");
  jqXHR.done(function((data, textStatus, jqXHR){
     alert("调用成功!");
  });
```
####  <a id="AjaxSupportInterface" href="#AjaxSupportInterface">jQuery提供的Ajax底层接口</a>  :star2: <a href="#top"> :arrow_up:  :arrow_up:</a>  
`jQuery还提供了底层Ajax方法，底层是相对于上面的快捷方法而言的，意味着我们可以对发起的Ajax请求进行更详细的配置！`

```
	jQuery为Ajax提供的底层API中核心方法就是ajax方法
	1）使用$.ajax()方法发起请求
           $.ajax('请求的url地址',{
                success:function(){}
           });
           第一个参数我们传了请求的url地址
           第二个参数是键值对象可以为本次请求进行配置
                这个键值对象可以配置的选项比较多，我们接下来和大家一起讲解！
                我们只传了一个success选项表示请求成功完成时执行的回调函数
                类型: Function(data,textStatus,jqXHR)
	2）设置请求的url
           $.ajax()方法第一个参数即可设置请求的url地址
           我们还可以省略第一个参数，直接将url地址传入配置对象
           url (类型: 字符串；默认: 当前页面地址)
           $.ajax({
                url:'请求的url地址',
                success:function(){}
           });
	3）设置请求的HTTP方式
           配置对象中传入type属性或者method属性来设置请求的HTTP方式
           type（类型: 字符串）
           method（类型: 字符串）
           注：如果你使用jQuery 1.9.0 之前的版本，你必须使用type选项而不能使用method选项
	4）设置向服务器传递的数据
           配置对象中传入data属性
           发送到服务器的数据。对象将自动进行url编码且转换为查询字符串格式！
           如果传入的是字符串（查询字符串），为保险起见，请自行将名称和值进行encodeURIComponent()处理！
	5）设置在Ajax请求发起之前执行回调函数
           配置对象中传入beforeSend属性指定在Ajax请求发起之前执行的函数
           作用：它提供了在请求发出前，最后配置本次请求的机会！
           类型: Function( jqXHR, settings)
           第二个参数一个配置对象，可以传入修改的配置属性以及值从而覆盖之前的配置对象对应的属性
           若在beforeSend函数中返回false将取消这个请求
	6）设置Ajax请求完成后（无论是否成功）执行的回调函数
           配置对象中传入complete属性来设置
           类型: Function(jqXHR,textStatus)
                    textStatus描述请求状态的字符串
           可以接受一个函数数组。每个函数将被依次调用
	7）设置Ajax请求失败之后执行的回调函数
           配置对象中传入error属性
           类型: Function(jqXHR,textStatus,errorThrown)
                    textStatus描述请求状态的字符串
                    errorThrown 接收HTTP状态的文本部分，比如： "Not Found"（没有找到）
           注意：此处理程序在跨域脚本和JSONP形式的请求时不被调用
           可以接受函数组成的数组。每个函数将被依次调用    
	8）设置Ajax请求成功之后执行的回调函数
           配置对象中传入success属性
           类型: Function( data,textStatus,jqXHR)
                    data：从服务器返回的数据（且根据dataType参数进行处理后的数据）
           可以接受函数组成的数组。每个函数将被依次调用
	9）设置服务器返回数据的预期数据格式
           配置对象中传入：dataType属性（可设置值："xml"、"html"、"script"、"json"、"jsonp"、"text"）
           如果不指定，jQuery 将自动根据 HTTP 头信息Content-Type来智能判断
           如果设置了此属性，jQuery就会将服务器返回的数据看成是这个格式的数据进行一些对于的转换操作，而忽略服务器响应数据声
           称的数据格式，若设置为"jsonp"则：会自动在所请求的URL最后添加 "callback=?"，?就是客户端回调函数的名字，是自动的我
           们无需另外设置，在服务器端只需要返回调用该函数并传入json格式数据的的js代码即可！
	10）设置Ajax请求相关回调函数的上下文
	    配置对象传入：context
	    这个属性的值会成为事件处理函数内this变量的值
	11）设置Ajax请求超时时间
	    配置对象传入：timeout（类型: Number）
	    指定请求超时选项（单位ms）。若请求超时，则jQuery自动调用error回调函数，并把status参数的值设置为timeout
	12）设置Ajax请求是否以异步方式发出
	    配置对象中传入：async
	    指定Ajax请求是否以异步方式发出，默认值为true
	    注意，同步请求将锁住浏览器，用户其它操作必须等待请求完成才可以执行
	13）设置是否缓存服务器返回的数据
	    配置对象中传入：cache（类型：布尔值）
	    若设置为false，则不缓存服务器响应的数据。
	    默认情况下，只有在请求script或者json数据时默认值是false，其他情况默认值都是true
	14）设置处理服务器返回数据的回调函数
	    配置对象中传入：dataFilter属性
	    类型: Function( String data, String type ) => Anything
			  data是Ajax返回的原始数据
			  type是调用jQuery.ajax时提供的dataType参数
	    将处理好的数据，return即可,若不将数据return则其他的事件处理函数（比如success）接受不到数据！
	    该属性通常用在，如果服务器返回的数据格式与我们需要的不匹配（比如包含一些不需要的数据），这功能就派上用场了
	15）控制数据格式转换
	    配置对象中传入：converters（类型：对象）
	    默认: 返回的是html格式则不做处理，若是json格式则转为对象，xml格式则转为xml对象！
		     传入对象内：设置"text html"属性，传入函数来设置对服务器返回的html格式的数据进行转换
		设置"text json"属性，传入函数来设置对服务器返回的json格式的数据进行转换
		函数接受一个参数，是服务器返回的未经转换过的数据(或是由dataFilter修改过的数据)，我们转换成的数据
		直接return即可,若不将数据return则其他的事件处理函数（比如success）接受不到数据！
	16）设置是否触发全局Ajax事件处理函数
	    配置对象中传入：global (默认: true)
	    类型: Boolean
	    设置为 false 将不会触发全局 AJAX 事件
	$.ajax()方法还有其他的一些配置选项，几乎很少使用，这边不作介绍！
2、Ajax请求全局设置
    1）$.ajaxSetup()方法
	为以后要用到的Ajax请求设置默认的值
	参数：一个用来配置Ajax请求的"{键:值}"对，属性同$.ajax()方法的配置对象中的属性
    2）全局Ajax事件方法
	直接在$.ajax()方法内设置的事件处理函数仅对当时ajax请求有效，我们还可以设置一系列“全局”（针对所有Ajax请求）的处理函数
	以下方法仅允许在document对象上调用
	ajaxComplete：
	    在Ajax请求完成之后执行的函数
	    Function(event,jqXHR,ajaxOptions )
        ajaxError：
	    在Ajax请求失败后执行的函数
	    Function( event, jqXHR, ajaxOptions, thrownError )
        ajaxSend：
	    在Ajax请求开始之前执行的函数
	    Function(event, jqXHR, ajaxOptions)
        ajaxStart：
	    在Ajax请求开始时执行的函数
	    Function()
        ajaxStop：
	    在Ajax请求完成之后执行的函数
	    Function()
	ajaxSuccess：
	    在Ajax请求成功完成之后执行的函数
	    Function(event,jqXHR,ajaxOptions,data)
四、jQuery提供的Ajax辅助方法
    1、$.param()方法
	返回用于URL查询字符串或Ajax请求（即会自动url转码，序列化）
	$.param()
    2、serialize()方法
	表单jQuery对象.serialize()
	一次性得到表单的所有数据,且对名称和值url编码，序列化，用于Ajax请求发生非常方便！
    3、serializeArray()方法
	表单jQuery对象.serializeArray()
	将表单转换成数据对象！
```
