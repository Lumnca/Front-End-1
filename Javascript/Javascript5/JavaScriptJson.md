<a id="top"  href="#">:maple_leaf: JavaScript 原生  JSON </a>:arrow_lower_left:
-----
`JSON 现在是一种重要的数据格式,被很多语言支持`

- [x] <a href="#Jsongrammar">`Json 语法`</a>
- [x] <a href="#JsonParsersAndStringif">`解析和序列化`</a>
  * <a href="#eval"> `eval() 解析 JSON`</a>  
  * <a href="#JsonObject">`JSON对象`</a>
    * <a href="#stringify">`JSON.stringify(object,func/array,number/stri)`</a>
    * <a href="#parse">`JSON.perse(jsonStr)`</a> 

#### &nbsp;&nbsp;Json 语法 <a href="#top" id="Jsongrammar" >:arrow_up:</a>
`Json的语法包含下面三种类型的值`
   * 简单值:`可以在Json中表示Json字符串,数值,布尔值和null`
     ```javascript
        //简单值
         var person={
              "name":"Jeke", //字符串
              "Age":15,      //数值
              "sex":true,    //布尔值
              "Node":null    //null
          }  
          var strJsonOfperson=JSON.stringify(person);
          // {"name":"Jeke","Age":15,"sex":true,"Node":null}
     ```
   * 对象:`对象是一种复杂的数据类型,表示一组无序的键值对,键值对可以是简单是也可以是复杂数据类型 例如对象,数组`
   ```javascript
       //对象
        var racer ={
            name:"LiuDeHua",
            Age:31,
            Car:{
                Type:"X-T2100 BENTIAN1180",
                id:"Q12300",
                Name:"BenLieGod",
                ProductTime:"2016/5/8"
            },
            sex:true

        }

        var strJsonOfperson=JSON.stringify(racer,null,4);
        console.info(strJsonOfperson);
        /* 序列化后的结果
        {
              "name": "LiuDeHua",
              "Age": 31,
              "Car": {
                  "Type": "X-T2100 BENTIAN1180",
                  "id": "Q12300",
                  "Name": "BenLieGod",
                  "ProductTime": "2016/5/8"
              },
              "sex": true
          }
          */
   ```
   * 数据:`数组是一种复杂的数据类型,表示一组有序的值的序列,可以通过数值索引来访问其中的值,数组的值可以是任意类型,简单值,对象或数组`
   ```javascript
          var racers ={
              Numbers:[
                  {
                      name:"LiuDeHua",
                      Age:31,
                      Car:{
                          Type:"X-T2100 BENTIAN1180",
                          id:"Q12301",
                          Name:"BenLieGod",
                          ProductTime:"2016/5/8"
                      },
                      sex:true
                  },
                  {
                      name:"GunNan",
                      Age:32,
                      Car:{
                          Type:"E-B2N0M BENCHIX1792",
                          id:"Q12302",
                          Name:"RoalyN",
                          ProductTime:"2013/5/8"
                      },
                      sex:true
                  },
                  {
                      name:"ChengJian",
                      Age:27,
                      Car:{
                          Type:"X-GG77 AODIQQ8888",
                          id:"Q12303",
                          Name:"ShanDianQueen",
                          ProductTime:"2017/2/8"
                      },
                      sex:true
                  }
              ],
              Count:3
          }
          /*也可以直接把数组序列化
            var racers =[
                    {
                        name:"LiuDeHua",
                        Age:31,
                        Car:{
                            Type:"X-T2100 BENTIAN1180",
                            id:"Q12301",
                            Name:"BenLieGod",
                            ProductTime:"2016/5/8"
                        },
                        sex:true
                    },
                    {
                        name:"GunNan",
                        Age:32,
                        Car:{
                            Type:"E-B2N0M BENCHIX1792",
                            id:"Q12302",
                            Name:"RoalyN",
                            ProductTime:"2013/5/8"
                        },
                        sex:true
                    },
                    {
                        name:"ChengJian",
                        Age:27,
                        Car:{
                            Type:"X-GG77 AODIQQ8888",
                            id:"Q12303",
                            Name:"ShanDianQueen",
                            ProductTime:"2017/2/8"
                        },
                        sex:true
                    }
            ]
          */
          var strJsonOfperson=JSON.stringify(racers,null,4);
          console.info(strJsonOfperson);
   ```
#### &nbsp;&nbsp;解析和序列化 <a href="#top" id="JsonParsersAndStringif">:arrow_up:</a>
`早期的JSON解析器基本上都使用JavaScript的eval() 函数,由于JSON是Javascript的子集,因此eval函数可以解析,解释返回Js对象和数组,js5之后增加了全局
对象JSON进行规范,对于某些不支持JSON对象的浏览器可以采用eval解析`
* 使用 **`eval()`** 解析 Json字符串 <a id="eval" href="#top">:arrow_up:</a>
  ```javascript
      
      var rastr='[{"name":"LiuDeHua","Age":31,"Car":{"Type":"X-T2100 BENTIAN1180","id":"Q12301","Name":
      "BenLieGod","ProductTime":"2016/5/8"},"sex":true},{"name":"GunNan","Age":32,"Car":{"Type":"E-B2N
      0M BENCHIX1792","id":"Q12302","Name":"RoalyN","ProductTime":"2013/5/8"},"sex":true},{"name":"Che
      ngJian","Age":27,"Car":{"Type":"X-GG77 AODIQQ8888","id":"Q12303","Name":"ShanDianQueen","Product
      Time":"2017/2/8"},"sex":true}]';
      
      var racer=eval(rastr);
      console.log("决赛总共有"+racer.length+"位选手");
      console.log("----------------------");
      racer.forEach(element => {
          console.log("选手名称:"+element.name);
          console.log("选手年龄:"+element.Age);
          console.log("选手车名称:"+element.Car.Name);
          console.log("----------------------");
      });
      /*
          决赛总共有3位选手
          ----------------------
          选手名称:LiuDeHua
          选手年龄:31
          选手车名称:BenLieGod
          ----------------------
          选手名称:GunNan
          选手年龄:32
          选手车名称:RoalyN
          ----------------------
          选手名称:ChengJian
          选手年龄:27
          选手车名称:ShanDianQueen
          ----------------------      
      */
  ```
 -----
`使用` **`JSON对象解析和序列化`** `JSON对象有两个方法 stringify()[将对象序列化为字符串] 和parse()[将JSON字符串解析为对象] ` <a id="JsonObject" href="#top">:arrow_up:</a>
* parse: <a href="#atnow" id="atnow">` 如果传入的字符串不是有效的JSON,这个方法就会抛出错误`</a>
* 1.序列化  1.1 String stringify(Object) <a id="stringify" href="#top">:arrow_up:</a>
 ```javascript
       var racers ={
          Numbers:[
              {
                  name:"LiuDeHua",
                  Age:31,
                  Car:{
                      Type:"X-T2100 BENTIAN1180",
                      id:"Q12301",
                      Name:"BenLieGod",
                      ProductTime:"2016/5/8"
                  },
                  sex:true
              },
              {
                  name:"GunNan",
                  Age:32,
                  Car:{
                      Type:"E-B2N0M BENCHIX1792",
                      id:"Q12302",
                      Name:"RoalyN",
                      ProductTime:"2013/5/8"
                  },
                  sex:true
              },
              {
                  name:"ChengJian",
                  Age:27,
                  Car:{
                      Type:"X-GG77 AODIQQ8888",
                      id:"Q12303",
                      Name:"ShanDianQueen",
                      ProductTime:"2017/2/8"
                  },
                  sex:true
              }
          ],
          Count:3
      }
      var strJsonOfperson=JSON.stringify(racers);
      /* 结果
      {"Numbers":[{"name":"LiuDeHua","Age":31,"Car":{"Type":"X-T2100 BENTIAN1180","id":"Q12301","Name":"BenLie
      God","ProductTime":"2016/5/8"},"sex":true},{"name":"GunNan","Age":32,"Car":{"Type":"E-B2N0M BENCHIX1792"
      ,"id":"Q12302","Name":"RoalyN","ProductTime":"2013/5/8"},"sex":true},{"name":"ChengJian","Age":27,"Car":{
      "Type":"X-GG77 AODIQQ8888","id":"Q12303","Name":"ShanDianQueen","ProductTime":"2017/2/8"},"sex":true}],"C
      ount":3}      
      */
 ```
* 1.序列化  1.2 过滤结果 String stringify(Object,Array[] / function(key,value)) 

    ```javascript
       第二个参数可以传递一个数组也可以传递一个函数
       传递的字符串会按照名称除掉对象的属性,函数为
       function(key,value) 两个参数
       
       // 传递数组
       var person={
            "name":"Jeke", //字符串
            "Age":15,      //数值
            "sex":true,    //布尔值
            "Node":null    //null
        }  
        var strJsonOfperson=JSON.stringify(person,["Age","Node"]);
        console.info(strJsonOfperson);
        // 结果返回:{"Age":15,"sex":true}       
        
        //传递函数
        var person={
            "name":"Jeke", //字符串
            "Age":15,      //数值
            "sex":true,    //布尔值
            "Node":null    //null
        }  
        var strJsonOfperson=JSON.stringify(person,function(key,value){
            switch(key){
                case "Age":
                    return person.Age-1;
                case  "name":
                case  "Node":
                    return undefined;
                default:
                    return value;    
            }
        });
        
        // 结果返回:{"Age":14,"sex":true}
    ```
-----

* 1.序列化  1.3 字符串缩进 String stringify(Object,Array[] / function(key,value),number/string)  
`一般情况下序列化的字符串可读性不高,没有缩进空格之类的那么第三个传输可以数字知道使用多少个空白字符串 缩进JSON字符串,最大缩进倍数为10`

    * 第三个参数为数字
    
    ```javascript
          var person={
              "name":"Jeke", //字符串
              "Age":15,      //数值
              "sex":true,    //布尔值
              "Node":null    //null
          }  
          var strJsonOfperson=JSON.stringify(person,null,4);
          console.info(strJsonOfperson);
          /* 输出
            {
                "name": "Jeke",
                "Age": 15,
                "sex": true,
                "Node": null
            }      
          */
    ```
    
    * 第三个参数为字符串
    
    ```javascript
          var person={
              "name":"Jeke", //字符串
              "Age":15,      //数值
              "sex":true,    //布尔值
              "Node":null    //null
          }  
          var strJsonOfperson=JSON.stringify(person,null,"----");
          console.info(strJsonOfperson);
          /* 输出:
          {
            ----"name": "Jeke",
            ----"Age": 15,
            ----"sex": true,
            ----"Node": null
          }
          */
    ```
* 2.解析  2.1 JSON.perse(jsonStr) <a href="#top" id="parse" >:arrow_up:</a>   

  ```C#
      var strJson=`{"name":"Jeke","Age":15,"sex":true,"Node":null}`;

      var XiaoMing=JSON.parse(strJson);

      console.log("----------------------");
      console.log("姓名:"+ XiaoMing.name);
      console.log("年龄:"+ XiaoMing.Age);
      console.log("性别:"+ (XiaoMing.sex?"男":"女"));
      console.log("----------------------");
  ```
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
