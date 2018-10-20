### :checkered_flag: <a href="#top" id="top">Jquery 表单验证插件</a>
----
- [x] ::herb:: <a href="#liezi">`简单介绍`</a>
- [x] ::herb:: <a href="#validateUseIt">`validate()方法使用例子`</a>
- [x] ::herb:: <a href="#ruleValidation">`validate() 内置的验证规则`</a>
- [x] ::herb:: <a href="#otherFunction">`validate() 其他配置对象`</a>
- [x] ::herb:: <a href="#ValidatorObject">`Validator对象`</a>
- [x] ::herb:: <a href="#OtherSomeThing">`其他方法`</a>

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

##### :herb: <a  href="#top"  id="otherFunction">`validate() 其他配置对象`</a>
* `submitHandler:Function(form)`:`表单验证合理之后,默认添加该函数则不会再提交除非手动提交或者使用return true;`
  * `该函数接受一个参数表示当前表单 DOM对象`
```javascript
  <script>
    $(function () {
      $("form[name='login']").validate({
        messages: {
          Userid: {
              required:"请填写你的用户名"
          }
        },
        rules: {
          Userid: {
            required: true
          }
        },
        submitHandler:function(form){
            alert("提交成功");
            // 当验证成功后悔打印出字符串 但是不会自动提交表单 需要自动提交表单需要 
            // 调用方法 form.submit()
        }
      });
    });
  </script>
```
* `invalidHandler:类型: Function(event,validator)`
  * `当前验证的表单validator对象,当表单验证失败的时候执行`
```javascript
 $(function () {
   $("form[name='login']").validate({
     messages: {
       Userid: {
           required:"请填写你的用户名"
       }
     },
     rules: {
       Userid: {
         required: true
       }
     },
     invalidHandler:function(event,validator){
         alert("表单验证失败");
     }
   });
 });
```
* `errorClass (默认值: error) String`
   * `指定错误提示与验证不通过的控件的 css 类名 会作用在errorElement控件和input/..空间上面`
* `validClass (默认值: "valid") String`
   * `在验证成功的控件上加上传入的css类`
* `errorElement (默认值: "label") String 用什么标签标记错误`
* `errorPlacement Function(error, element) (默认值: 在无效的元素之后)`
   * `自定义错误信息放到哪里 error 是错误信息提示标签  element 是输入验证控件`
* `errorContainer String 选择器字符串`
   * `有错误信息出现时把选择器匹配的元素变为显示，无错误时隐藏`
```Html
<style>
    .errorInfo{
        display: block;
        display: block;
        font-size: 14px;
        color: brown;
    }
    .validaSuccess{
        border-color: green;
        border-radius: 5px;
        width: 200px;
        height: 30px;
    }
    .validaSuccess:focus{
        outline: none;
    }
</style>
<script>
$(function () {
    $("form[name='login']").validate({
    messages: {
        Userid: {
            required:"请填写你的用户名",
            minlength:"密码长度不合法"
        }
    },
    rules: {
        Userid: {
        required: true,
        minlength:8
        }
    },
    invalidHandler:function(event,validator){
        alert("表单验证失败");
    },
    errorClass:"errorInfo" ,
    validClass :"validaSuccess",
    errorElement:"div",
    errorPlacement:function(error,element){
        $(error).insertBefore(element);
        //把错误信息提示放到控件前面去
    }, 
    errorContainer:"#info",
    debug:true
    });
});
</script>
</head>
<body>
  <div id="info" style=" display: none; ">
    验证信息错误
  </div>
  <form  method="POST" name="login">
    <div>
        账号：
    </div>
    <input type="text" name="Userid" id="id" />
    <br/><br/>  
    <button type="submit">立即提交</button>
  </form>
</body>
```
* `errorLabelContainer String 选择器字符串 把错误信息统一放在一个容器里面`
* `wrapper String 用什么标签再把上边的 errorELement 包起来`
```html
<style>
    .errorInfo{
        display: block;
        display: block;
        font-size: 14px;
        color: brown;
    }
    .validaSuccess{
        border-color: green;
        border-radius: 5px;
        width: 200px;
        height: 30px;
    }
    .validaSuccess:focus{
        outline: none;
    }
</style>
<script>
$(function () {
  $("form[name='login']").validate({
    messages: {
        Userid: {
            required:"请填写你的用户名",
            minlength:"密码长度不合法"
        }
    },
    rules: {
        Userid: {
        required: true,
        minlength:8
        }
    },
    errorLabelContainer:"#errorList",//把错误信息统一放在一个容器里面
    debug:true
    });
});
</script>
</head>
<body>
  <div id="info" style=" display: none; ">
    验证信息错误
  </div>
  <form  method="POST" name="login">
    <div>
        账号：
    </div>
    <input type="text" name="Userid" id="id" />
    <br/><br/>  
    <button type="submit">立即提交</button>
  </form>
  <div id="errorList">

  </div>
</body>
```
* `wrapper 类型：String 说明：用什么标签再把上边的 errorELement 包起来`
```javascript
$(function () {
  $("form[name='login']").validate({
    messages: {
        Userid: {
            required:"请填写你的用户名",
            minlength:"密码长度不合法"
        }
    },
    rules: {
        Userid: {
        required: true,
        minlength:8
        }
    },
    errorClass:"errorInfo",
    debug:true,
    wrapper:"div"
    });
});
```
* `success 类型：String or Function(label,element) 每个字段验证通过执行函数`
  * `函数参数：label：信息提示标签的jQuery对象。 element：当前验证成功的DOM元素对象 如果跟一个字符串,会作为css类加在提示信息的标签上`
```javascript
<style>
    .errorInfo{
        font-size: 14px;
        color: brown;
    }
    .validaSuccess{
        border-color: green;
        border-radius: 5px;
        width: 200px;
        height: 30px;
    }
    .validaSuccess:focus{
        outline: none;
    }
</style>
<script>
$(function () {
  $("form[name='login']").validate({
    messages: {
        Userid: {
            required:"请填写你的用户名",
            minlength:"密码长度不合法"
        }
    },
    rules: {
        Userid: {
        required: true,
        minlength:8
        }
    },
    errorClass:"errorInfo",
    debug:true,
    wrapper:"div",
    success:function(label,element){
        console.log(label);
    }
    });
});
</script>
</head>
<body>
  <div id="info" style=" display: none; ">
    验证信息错误
  </div>
  <form  method="POST" name="login">
    <div>
        账号：
    </div>
    <input type="text" name="Userid" id="id" />
    <br/><br/>  
    <button type="submit">立即提交</button>
  </form>
  <div id="errorList">

  </div>
</body>
```
* `highlight(默认值: 添加errorClass到验证失败的表单控件) Type: Function(element, errorClass, validClass)`
  * `传入的函数会在每个控件验证不通过时执行，我们可以通过这个配置属性，给不通过的控件加写效果`
  * `函数参数：element：当前未通过验证的控件DOM元素对象`
  * `errorClass：错误时给错误提示标签的css类名称`
  * `validClass：validClass属性的当前值`
* `unhighlight(默认值: 移除验证失败控件的errorClass) function(element, errorClass, validClass)`
* `debug (默认值: false)  类型: Boolean 设置为true之后则表单不会真正的提交，仅仅是验证！ 使用方法以及参数同上，作用相反`
* `ignore  类型：Selector 说明：忽略某些元素不验证`
```javascript
  highlight:function(element, errorClass, validClass){
      element.addClass("valid");
  },
  unhighlight:function(element, errorClass, validClass){
     element.removeClass("valid");
  }
```
##### :herb: <a id="ValidatorObject" href="#top">`Validator对象`</a>
` validate方法返回一个 Validator 对象，我们可以称这个对象为Validator对象`   
* `Validator.form() 返回：Boolean` :`验证 form 返回成功还是失败`
* `Validator.element() 返回：Boolean`:`验证单个元素是成功还是失败`
* `Validator.resetForm() 把前面验证的 FORM 恢复到验证前原来的状态`  
* `Validator.showErrors()`:`显示特定的错误信息`
* `Validator.numberOfInvalids()`:` 返回验证不通过的字段数`
```html
<body>
  <div id="info" style=" display: none; ">
    验证信息错误
  </div>
  <form  method="POST" name="login">
    <div>
        账号：
    </div>
    <input type="text" name="Userid" id="id" />
    <br/>
    <div>
        密码
    </div>
    <input type="password" class="input_pwd" id="password" name="password"  >
    <button type="submit">立即提交</button>
  </form>
  <br/><br/>  
  <div>
      <button id="Check" type="button">检查一下</button>
      <button id="resetForm" type="button">删除验证信息</button>
  </div>
</body>
```
```javascript
$(function () {
  var validater =  $("form[name='login']").validate({
    messages: {
        Userid: {
            required:"请填写你的用户名",
            minlength:"密码长度不合法"
        }
    },
    rules: {
        Userid: {
        required: true,
        minlength:8
        }
    },
    errorClass:"errorInfo",
    debug:true,
    wrapper:"div",
    });
    $('#Check').on("click",null,null,function(){
        console.log(`表单验证：${validater.form()}`);
        console.log(`账号验证: ${validater.element("form input:eq(0)")}`);
    });
    $('#resetForm').on("click",null,null,function(){
        validater.resetForm();
    });
 });
```
###### 静态方法
* `$.validator.setDefaults() 改变默认的设置`         
* `$.validator.addClassRules() 增加组合验证类型，可以在一个css类里面用多种验证规则`           
* `$.validator.format() 用参数代替模板中的 {n}`
* `$.validator.addMethod("MethodName",Function(value,element,args),"ErrorMessage") 添加一个新的验证方法 自定义验证规则`  
  * `第一个参数：规则名称`
  * `第二个参数: 验证函数(输入值,输入控件,是否启用 true/false)`
  * `第三个参数: 错误提示信息`
  * `返回值: false 失败  返回true 验证成功`
```javascript
  $.validator.addMethod("RemoteServer",function(value,element,args){
      //用户输入的值
      if(args){
            if(value != "123456789"){
            return false;
            }else{
                return true;
            }
      };
      return true;
      console.log(args);//true / false  如果是true 则启用规则 否则不启用规则
  },"服务器验证失败,你不能登陆");
```
```javascript
 $.validator.addClassRules({
   input_pwd:{
       required: true,
       minlength:8
   },
   userName:{
       required: true,  //凡是有.userName类的标签 都必须填写
   }
 });
```
```javascript
 var template = $.validator.format("{0} is {1}  ");
 console.log(template("My age","18"));  //My age is 18 
```
##### :herb: <a href="#ruleFunction">`rule() 方法`</a> 
* `rules()` `返回元素的验证规则`
* `rules("add",rules)` `增加验证规则`
* `rules("remove",rules)` `删除验证规则 多个验证规则用空格隔开`
```javascript
  //需要调用validate 方法 之前
  $('form input:eq(1)').rules('add',{
       required: true,
       minlength:8
  });
  $('form input:eq(1)').rules('remove',"required minlength");
```
##### :herb: <a id="OtherSomeThing" href="#top">`其他方法`</a>   
```
五、valid()方法
    1、介绍
        说明：检查表单是否验证通过
    2、使用
        表单jQuery对象.valid()
六、jQuery Validation提供的选择器
    1、增加的选择器
    这个插件还提供了几个选择器
   :blank
     选择所有没有值或者值为空白的表单控件
   :filled
     选择所有填写了非空值的表单控件
   :unchecked
     与jQuery提供的:checked选择器相反        
```
            
                
            
                
            
                
            
                
