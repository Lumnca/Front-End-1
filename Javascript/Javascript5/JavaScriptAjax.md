<a id="top"  href="#">:maple_leaf: Javascript 原生 Ajax </a>:arrow_lower_left:
-----
`Asynchronous JavaScript + XML 这一技术能够向服务器请求额外的数据而无须卸载页面,会带来更好的用户体验,`

- [x] <a href="#XMLHttpRequest2">`XMLHttpRequest2`</a>



```javascript
一、初探浏览器原生Ajax接口
    1、创建XHR对象
       我们整个Ajax技术的接口，核心是通过XMLHttpRequest这个对象（简称XHR对象）来完成！
        XHR对象怎么得到？
            对于IE7+，谷歌，火狐，是通过XMLHttpRequest这个引用类型来创建出XHR对象!
            var xhr=new XMLHttpRequest();//得到XHR对象，变量名随便取
        对于IE7以下的ie浏览器创建出XHR对象的方法我们这边不做介绍，一个原因是jQuery后面为Ajax操作
        提供了兼容各浏览器的方法，另一个原因是IE7以下的极地版本的IE浏览器，使用率已经非常低！
```
#####  XMLHttpRequest对象
`不考虑IE7以下的兼容问题,不管直接使用XMLHttpRequest 对象`

```javascript
      var xhr=new XMLHttpRequest();
      xhr.open("GET","web/a.php",true);
      xhr.send(null);
      xhr.onreadystatechange=function(){
          if(xhr.readyState==4){
              console.info(xhr.status);
              console.info(xhr.statusText);
              console.log(xhr.responseText);
          }
      }
```

```php
  // a.php
  <?php
      echo "<div>来吧小伙子,了解一下Ajax</div>"
  ?>
```

##### 启动请求
`使用open(get/post,url,async= true/false),但是真正发送请求要使用send方法,get方式 使用send(null) 如果是post方法  使用send(urldata),返回的数据会自动填充到对象的属性中`

```javascript    
    2、启用一个请求等待发送
        XHR对象.open('HTTP方法','请求的地址',是否异步发送请求的布尔值,用户名,密码);
        调用open()方法并不会真正发送请求，而只是启动一个请求以备发送
        1）'HTTP方法'
            比如get或者post	大小写无所谓
            GET请求应该用于从服务器端获取数据为目的
            POST方式主要是为了将数据提交给服务器端并且存储（比如将数据提交到服务器端，且写入数据库）！
        2）请求的url地址
           如果该地址指向的是静态内容（比如html等）会直接将指定文件里面的内容返回给客户端！
           如果是动态的脚本（比如PHP）那么会在服务器端执行这个PHP文件，并且将其输出的内容返回给客户端！
        3）是否异步发送请求的布尔值	
           true表示异步请求（默认），false表示同步请求
           同步请求的特点
                客户端提交请求->等待服务器处理（等待服务器端回应之前客户端不能做其他事情）->服务器端处理完毕返回给
                浏览器即：浏览器在得到服务器端的数据回应之前，浏览器不能和用户有任何交互，后面的JavaScript 代码会
                等到服务器响应之后再继续执行！
           异步请求的特点
                客户端提交请求（请求之后，可以继续去做其他事情）
                    ->服务器进行处理（处理过程就像在后台完成一样，用户可能都感觉不到，还可以继续浏览网页中的内容并
                    且交互，后面的JavaScript 代码也会继续执行而不会等待异步请求的响应！）
                处理完毕（处理完毕之后，浏览器会得到这个通知，然后可以执行对应的一些准备好的操作）
                优点：在异步请求的过程中用户依然可以操作我们的页面内容，后面的js代码也会继续执行，而无需等待发起的
                请求的响应！
           把客户端（浏览器）和服务器端比喻两个人，浏览器我们称作A，服务器端称作B
           同步请求：
                A到餐厅吃饭，点了一桌菜，约B来一起吃饭，约完之后，A就坐在餐厅一直等待，直到B到了，坐了下来，两人一
                起吃！
           异步请求：
                A到餐厅吃饭，点了一桌菜，约B来一起吃饭，约完之后，A就直接拿起筷子吃了，边吃边等，B来了之后，拿起
                筷子吃！
        4）最后两个参数是 服务器如果设置了需要认证请求，写上您在服务器端设置的用户名和密码（一般很少使用）
    3、发送请求
        XHR对象.send(要发送的数据);
        传入的参数作为主体内容发送给服务器！
        如果不需要传主体数据，必须传入null，否则有些浏览器无法兼容！
```  

```javascript
     //post请求
    <script>        
        function encodeU(data) {
            var str='';
            for (var i in data) {
                str+=encodeURIComponent(i)+'='+encodeURIComponent(data[i])+'&';
            }
            return str.substr(0,str.length-1);
        }
        window.onload=function(){
            var xhr=new XMLHttpRequest();
            var data=encodeU({
                UserPwd:"152123595",
                UserID:"858585",
                UserName:"王俊凯"
            });   
            xhr.open("POST","postdata.php",true);
            xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
            xhr.send(data);
            xhr.onreadystatechange=function(){
                if(xhr.readyState==4){
                    console.info(xhr.status);
                    console.info(xhr.statusText);
                    console.log(xhr.responseText);
                }
            }
        }
    </script>
```


##### 获得数据

```javascript   
    4、如何获取服务器响应的数据
       在收到服务器端响应后，响应的数据会自动填充XHR对象的属性，部分属性和方法简介如下
       1）responseText：作为响应主体被返回的文本
       2）responseXML：如果响应的内容是XML格式的，就根据内容创建XML DOM对象以便操作（XML格式已经很少使用，所以这个属
	               性现在也很少使用了）
       3）status：响应的HTTP状态（200表示成功，404表示未找到）
       4）statusText：HTTP状态的说明
```

* 5）readyState：请求/响应过程的当前活动阶段，可能的值
  * 0：`未初始化。尚未调用open()方法`
  * 1：`启动。已经调用open()方法，但尚未调用send()方法`
  * 2：`发送。已经调用send()方法，但尚未接收到响应`
  * 3：`接收。已经接收到部分响应数据`
  * 4：`完成。已经接收到全部响应数据，而且已经可以在客户端使用了`
  
* 6）readystatechange事件:
  `只要readyState属性的值由一个值变成另一个值，都会触发一次readystatechange事件`  
  `注：必须在调用open()之前指定readystatechange事件处理程序才能确保跨浏览器兼容性。
       对于readystatechange事件处理程序内部最好不要使用this来代表当前的xhr对象，因为有的浏览器会出现不可
       预知的问题，所以我们在处理程序内部就用XHR对象的变量名就好了。`
##### 7）abort()
	  取消当前正在执行的请求


```javascript
    5、设置http头部信息
	我们在浏览器与服务器之间来回的传递数据，这些数据除了我们传递的主体数据之外，还会动加上一些http头信息
	http头部信息
	    为什么要传头部信息？主要就是告诉对方自己的能力，告诉对方主体内容的类型格式！
	    1）请求的头部信息(由浏览器发送给服务器端的http头部信息)
		不同浏览器实际发送的头部信息会有所不同，下面列出的是常见的请求头部信息
		Accept：浏览器能够处理的内容类型
		Accept-Encoding：浏览器能够处理的压缩编码
		Accept-Language：浏览器当前设置的语言
		Accept-Charset：浏览器能够显示的字符集
		Host：发出请求的页面所在的域
		Referer：发出请求的页面的URI
		User-Agent：浏览器的用户代理字符串，通过它我们在服务器端可以大致知道客户端是用的什么类型的浏览器
		设置本次请求的头信息：
                 XHR对象.setRequestHeader()
                 这个方法接受两个参数：头部字段的名称和头部字段的值（也可以发送自定义的头信息）
                 注：要成功发送请求头部信息，必须在调用open()方法之后且调用send()方法之前调用
                 setRequestHeader()
	    2）响应头部信息（由服务器端发送给客户端的http头部信息）
		XHR对象.getResponseHeader()
		    传入头部字段名称，可以取得相应的响应头部信息
		getAllResponseHeaders()
		    包含所有头部信息的长字符串
	    
    6、向服务器发送数据
	1）GET方式的请求
	    请求的url地址?参数1&参数2&参数3&.........
			  每个参数的格式：参数名称=参数值
			  符合?后面的格式的这个字符串，我们可以称作 查询字符串！
	    注：查询字符串中每个参数的名称和值都必须使用encodeURIComponent()进行编码，否则可能会出现乱码的情况！
	2）对于post请求，需将要传的数据传入send方法，并且符合相应的格式（这个符合格式的字符串我们称作查询字符串）
           比如：username=%E5%AD%99%E8%83%9C%E5%88%A9&sex=true，传入send方法！
                     和查询字符串一样，多个参数用&隔开，每个参数的名称和值也经过了encodeURIComponent()进行编码！
           注：我们使用ajax技术发起POST请求并且传递给服务器数据时，需要手动的做一些设置，服务器端才能顺利的接受到
                  数据！将请求的Content-Type头部信息设置为application/x-www-form-urlencoded
                  请求的Content-Type头部信息，表示告诉服务器发送的主体数据的内容类型（我们用post方式提交表单时默认
                  就是采用这个内容类型）！只有这样明确的告诉服务器端我们发送的主体数据的内容类型，服务器端才能合理的
                  识别解析它们，且放入$_POST变量中！
                  application/x-www-form-urlencoded这种内容类型形式上是这样子的：
                  username=%E5%AD%99%E8%83%9C%E5%88%A9&sex=true
           注：直接使用表单提交时这些操作，浏览器都帮我们自动做了，所以我们感觉不到！
    7、处理服务器响应的数据
	服务器端可以返回各种各样格式的数据，不同的数据格式，处理起来也是各不相同！
	首先我们需要知道一点：
	    服务器端响应数据，存放在XHR对象内的responseText这个属性里面，这个属性的数据类型是字符串！
	    但是我们一个字符串里面的数据格式可以有许多种不同的形式（数据格式）
	1）html格式的数据
	    html格式的数据即返回的数据本身就是html代码，这种数据使用起来比较直接，可以直接将其通过append之类
      的方法放到当前页面中   
	2）script格式的数据
	    字符串内直接就是js代码
	    即返回的数据直接就是javascript代码，可以使用js的eval函数来执行这个字符串中的代码
	3）xml格式的数据
	    是Ajax技术刚被提出是最常用的服务器端与客户端交互的数据格式，甚至ajax中的x指的就是xml，但是这种格式的
      数据书写麻烦，
            使用不便，目前已经很少使用这个格式的数据进行交互。
	4）json格式的数据
	    JSON格式的数据形式：
	    形式一：{"键名":值,...}
	    形式二：[{"键名":值},...]
	    JSON数据格式非常严格，主要的注意点：
		键名称必须是用双引号括起来的字符串
		值如果是字符串类型，那么也必须使用双引号括起来而不是单引号！
		对于JSON格式的字符串，我们可以通过JSON.parse()方法将其转换为对象
		    注意：字符串必须符合JSON格式！
		    如果浏览器不支持JSON.parse这个方法可以使用eval函数来投机取巧一下！
	    注意：JSON格式的数据，大家要养成良好的习惯，将其写的标准！
    8、跨源请求
	默认情况下，浏览器只允许向与本页面同源的服务器发起请求
	JSONP（JSON with padding简写，参数式JSON的意思）技术
	跨源 请求的目的：从不同的url下面的脚本请求数据！
	在不同源的php文件那边将JSON格式的数据作为参数传给要调用的函数！
	    注意：只能是get方式
	<script type="text/javascript">
	    function sunshengli(data){
		console.log(data);
	    }
	</script>
	<script type="text/javascript" src="http://127.0.0.1/ajax/demo9_4/test/c.php?callback=sun
  shengli"></script>
 ``` 
 #### <a id="XMLHttpRequest2" href="#XMLHttpRequest2">XMLHttpRequest2 级</a>
 
 ##### 数据序列化 FromData <a href="#top">置顶</a>
 
 ```Javascript
       window.onload=function(){
          var xhr=new XMLHttpRequest();  
          xhr.open("POST","postdata.php",true);
          var data_fromdata=new FormData();
          data_fromdata.append("UserPwd","152123595psd");
          data_fromdata.append("UserID","858585");
          data_fromdata.append("UserName","王俊凯");    
          xhr.send(data_fromdata);
          xhr.onreadystatechange=function(){
              if(xhr.readyState==4){
                  console.info(xhr.status); //Http状态码
                  console.info(xhr.statusText);
                  console.log(xhr.responseText);
              }
          }
      }
 ```
##### OverrideMineType 设置返回数据的类型
`Serve返回的MIME类型是text/plain,但数据中实际包含的是XML,根据MIME类型,即使数据是XML，response属性中任然是null,通过此方法可以保证报相应
当做XML而非存文本来处理`
<br/>
** 可能没什么用 **
```javascript
    window.onload=function(){
        var xhr=new XMLHttpRequest();  
        xhr.open("GET","suser.xml",true);
        xhr.overrideMimeType("text/xml");
        xhr.setRequestHeader("Content-Type","text/xml");
        xhr.send(null);
        xhr.onreadystatechange=function(){
            if(xhr.readyState==4){
               var xmlper=xhr.responseText;
               console.log(xmlper);
            }
        }
    }
```
