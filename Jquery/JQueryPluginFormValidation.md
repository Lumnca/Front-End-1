### :checkered_flag: <a href="#top" id="top">Jquery 表单验证插件</a>
----
- [x] ::herb:: <a href="#liezi">`简单介绍`</a>
- [x] ::herb:: <a href="#validateUseIt">`validate()方法使用例子`</a>
- [x] ::herb:: <a href="#ruleValidation">`validate() 内置的验证规则`</a>
- [x] ::herb:: <a href="#messageValidation">`提示信息修改`</a>
- [x] ::herb:: <a href="#callbacksfireIndex">`callbacks.fire()`</a>
- [x] ::herb:: <a href="#callbacksfirewithIndex">`callbacks.fireWith([context ] [, args ])`</a>



##### <a href="#top" id="liezi" >简单介绍</a>
`Validation是一个十分优秀的表单验证插件，它历史悠久，全球使用率超高，好评不断,学习jq 掌握这个插件是非常有必要的`
* `这个插件有3个主要方法`
  * `validate()`:`用于验证表单，也是该插件最核心的方法`
  * `valid()`:`验证表单是否通过验证`
  * `rules()`:`为一个表单控件，查看、新增、移除规则`
* `增加了一些选择器`
  * `:blank`:`选择所有没有值或者值为空白的表单控件`
  * `:filled`:`选择所有填写了非空值的表单控件`
  * `:unchecked`:`与jQuery提供的:checked选择器相反`
  
##### <a href="#top" id="validateUseIt" >validate()方法使用例子</a>
```javascript
<script>
$(function () {
  $("form[name='login']").validate({
    //错误提示信息
    messages: {
      Userid: "请填写你的用户名",//此方法在username控件上的所有验证规则提示都是设置的这个字符串
      Userpwd: {
        required: "请填写你的密码",
        minlength: "密码长度不得小于10"
      }
    },
    //验证规则
    rules: {
      //使用空间 name 名称
      Userid: {
        required: true
      },
      Userpwd:{
        required:true,
        minlength:10
      }
    }
  });
});
</script>
<form action="/homr/login" method="POST" name="login">
  <input type="text" name="Userid" id="id" />
  <br/>
  <input type="password" name="Userpwd" id="pwd" />
  <br/>
  <button type="submit">立即提交</button>
</form>
```
##### <a href="#top" id="ruleValidation">validate() 内置的验证规则</a>
* `required`:`必须输入的字段` `使用`:`required:true`
* `minlength`:`最小字符长度` `使用`:`minlength:10`
* `maxlength`:`最大字符长度` `使用`:`maxlength:20`
* `rangelength`:`字符长度必须介于某个区间` `使用`: `rangelength:[5,10]` 
* `min`:`输入值被允许的最小值` `使用`:`min：5`
* `max`:`输入值被允许的最大值` `使用`:`max：5`
* `range`:`输入值必须介于某个区间` `使用`:`range：[5,10]`
* `number`:`必须输入合法的数字` `使用`:`number:true`
* `number`:`必须输入合法的数字` `使用`: `number:true`
* `digits`:`必须输入整数` `使用`: `digits:true`
* `email`:`必须输入正确格式的电子邮件` `使用`: `email:true`
* `url`:`必须输入正确格式的网址` `使用`: `url:true`
* `equalTo`:`输入值必须和给定选择器的字段的值相同` `使用`: `equalTo:"选择器"`
* `remote`:`使用 ajax 方法调用 服务器端脚本 验证输入值 `
```javascript
remote:"check.php"
remote: {
   url: "check-email.php",
   type: "post",
   data: {
            username:'sunshengli'
    }
}
// 服务器返回一个 true /false 的字符串
//默认会提交当前验证的值到远程地址，如果需要提交其他的值，可以使用 data 选项 参数与值与$.ajax方法相同
```
* `extension`:`限定能是限定的后缀名,多个用|分隔`
```javascript
UserFile:{
  required:true,
  extension:"png|jpg|jpeg"
}
文件 <input type="file" name="UserFile" />
```
```javascript
官方里的additional-methods.js里的包含了一些常用的验证方法
maxWords：最多输入的字符个数

minWords：最少输入的字符个数

rangeWords：输入两个数之间的个数

letterswithbasicpunc：只能输入字母和标点符号

alphanumeric：只能输入数字、字母和下划线

lettersonly：只能输入字母

nowhitespace:不能输入空白符，空格

ziprange：邮政编码范围

zipcodeUS：指定编码无效

integer：一个正数或负非十进制数字
```
##### <a href="#top" id="messageValidation">提示信息修改</a>
`提示消息,有中文版,英文版,各种语言的版本,如果你不填写,修改默认的提示信息最简单的办法引入messages_zh.js文件即可！ 默认是英文,当然你可以自己配置
messages 属性,如果你不配置就需要使用默认的提示信息`
```javascript
$("form[name='login']").validate({
   messages: {
     Userid: "请填写你的用户名",//此方法在username控件上的所有验证规则提示都是设置的这个字符串
     Userpwd: {
       required: "请填写你的密码",
       minlength: "密码长度不得小于{0}",
       maxlength:"密码长度超过规定的{0}位",
       //rangelength:"密码长度应该在{0}到{1}之间"
       nowhitespace:"不能输入空白符，空格"
     },
     UserEmail:{
       required:"请填写你的邮箱",
       email:"请输入正确的邮箱地址"
     }
   },
   rules: {
     Userid: {
       required: true
     },
     Userpwd:{
       required:true,
       minlength:10,
       maxlength:20,
       //rangelength[10,20]
       nowhitespace:true
     },
     UserEmail:{
       required:true,
       email:true
     },
     UserFile:{
       required:true,
       extension:"png|jpg|jpeg"
     }
   }
 });
});
```
`你可以通过messages 属性配置设置所有的提示信息 {0} 使用属性对象的第一个值 {1} 使用属性对应的第二个值`
<a href="#top" id="messageValidation">validation 常用配置选项</a> 
