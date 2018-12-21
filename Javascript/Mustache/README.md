### [Mustache 前端模板引擎](#top) <b id="top"></b> :star:

-----

- [x] [`1.简单的用一用`](#into) 
- [x] [`2.编译说明`](#parse) 
- [x] [`3.条件和循环`](#ifelsefor) 
- [x] [`4.其他用途`](#other) 

-----
##### :triangular_flag_on_post: [`1.简单的用一用`](#top)  <b id="into"></b>
`来我们编译一个吧 下面的模板编译成具有数据的 html`
* `{{!}} 表示注释`
```html
<script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.min.js"></script>
<script src="https://cdn.bootcss.com/mustache.js/3.0.1/mustache.js"></script>
<div id="BookInfo" >
    {{!这是注释}}
    <h4>书名称:{{bookName}}</h4>
    <p><small>作者：{{Author.name}} </small></p>
    <p><span>价格：{{price}}</span></p>
    <p>作者地址:{{Author.address}}</p>
</div>
```
`这里结合Jquery 来获取HTML 方便一点 也可以直接使用原生JS`
```node
let Person = {
    name:"JxKicker",
    address:"四川师范大学"
}

let data = {
    bookName:"Java核心卷8 第十版 I和II",
    price:186.2,
    Author:Person
}

var booinfo_template = $('#BookInfo').html();         //1.获得 BookInfo 的html文本 
Mustache.parse(booinfo_template);                     //2.将文本进行编译
var result = Mustache.render(booinfo_template,data);  //3.加载数据
$('#BookInfo').html(result);                          //4.将结果用于重新load 到 html中
```
------`结果如下:`------
<div id="BookInfo">
    <h4>书名称:Java核心卷8 第十版 I和II</h4>
    <p><small>作者：JxKicker </small></p>
    <p><span>价格：186.2</span></p>
    <p>作者地址:四川师范大学</p>
</div>

##### :triangular_flag_on_post: [`2.编译说明`](#top)  <b id="parse"></b>
* `HTML字符转移`
  * `如果你数据对象里面带有 html标签 那么最终会编译成 html转移字符 而不会被解析为 html标签`
```html
<h2 id="hello">
    Hello {{name}}!
</h2>
```
`来我们编译吧！`
```node
let obj = { name :"<b>JxKicker</b>"};

let template = $('#hello').html();
Mustache.parse(template);
result = Mustache.render(template, obj);

$("#hello").html(result);
```

------`结果如下:`------
<h2 id="hello">
    Hello &lt;b&gt;JxKicker&lt;/b&gt;!
</h2>

---
`Hello &lt;b&gt;JxKicker&lt;/b&gt;!`


##### :triangular_flag_on_post: [`3.条件和循环`](#top)  <b id="ifelsefor"></b>
`通过{{#param}} {{/param}} 我们可以完成很多的功能`

##### 一. if 判断
`如果变量 isLogin 是 true 那么就显示 否则 isLogin 是空或者null，或者是false 都不显示`
```html
<div id="Login">
    <p> {{#isLogin}}你已登录了{{/isLogin}}</p>
</div>
```

```node
let data = {
    "isLogin":true,
    "loginInfo":"Http2.0 Requset Right"
}

var template = $('#Login').html();
Mustache.parse(template);
let result = Mustache.render(template,data)
$('#Login').html(result);
```
* `如果你需要取反怎么办呢？ 那么使用 {{^parame}}`
------`结果如下:`------
<p> 你已登录了</p>

-----
##### 二. for 循环
`对象的循环`
```html
<div id="users">
    <p>老师: {{name}}</p>
   {{#persons}}
        <div>
            <p>姓名:{{name}}</p>
            <p>年龄:{{age}}</p>
        </div>
   {{/persons}}
 </div>
```
`那么我们来编译一下 发现没有呀 {{#person}} 里面的 {{name}} 的对象作用域 是 数组里面的对象`
```node
var data = {
    name:"JxKicker",
    persons: [
        {"name": "Moe"  ,age:17}, 
        {"name": "Larry",age:21}, 
        {"name": "Curly",age:19}
    ]
};
let template = $('#users').html();
Mustache.parse(template);
var output = Mustache.render(template,data);
$('#users').html(output);
```
------`结果如下:`------

<div id="users">
  <p>老师: JxKicker</p>
 <div>
   <p>姓名:Moe</p>
   <p>年龄:17</p>
 </div>
 <div>
   <p>姓名:Larry</p>
   <p>年龄:21</p>
 </div>
 <div>
   <p>姓名:Curly</p>
   <p>年龄:19</p>
 </div>
</div>

##### 如果是简单数组呢？
`用 . 表示当前元素`
```html
<div id="names">
    {{#name}}<p>{{.}}</p> {{/name}}
</div>
```

```node
var $odata = {
    name : [ "wangsi", "JxKicker", "kick", "tim" ]
}
template = $('#names').html();
Mustache.parse(template);
var output = Mustache.render(template,$odata);
$('#names').html(output);
```

------`结果如下:`------
<div id="names">
    <p>wangsi</p> <p>JxKicker</p> <p>kick</p> <p>tim</p> 
</div>


-----

##### :triangular_flag_on_post: [`4.其他用途`](#top)  <b id="other"></b>

* `函数变量的情况`
```node
var data = {
    "beatles": [{
        "firstName": "John",
        "lastName": "Lennon"
    }, {
        "firstName": "Paul",
        "lastName": "McCartney"
    }, {
        "firstName": "George",
        "lastName": "Harrison"
    }, {
        "firstName": "Ringo",
        "lastName": "Starr"
    }],
    "name": function () {
        return this.firstName + " " + this.lastName;
    }
};
var output = Mustache
    .render("{{#beatles}} *{{name}}{{/beatles}}", data);
console.log(output);
```

* `{{^}}与{{#}}相反，如果变量是null、undefined、 false、和空数组讲输出结果`

##### 例子
```html
<ul id="enum-list" class="admin-narbar clearStyle border-light-down">

</ul>
<script id="template" type="x-tmpl-mustache">
{{#types}}
    <li>
        <a href="#" data-value-store-typeId='{{typeID}}' >{{typeName}}</a>
    </li>
{{/types}}
</script>


<script>
let jqXHRresult = $.get("product/getType",function (data,status,jqXhr) {
    console.log(data);
    let typeList = {
        types:data
    }
    var template = $('#template').html();
    Mustache.parse(template);
    let result =  Mustache.render(template,typeList);
    console.log(result);
    $('#enum-list').html(result);
},"json");
</script>
```















