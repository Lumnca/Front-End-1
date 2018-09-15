<a id="top">:checkered_flag: </a>JavaScript 与XML :smirk:
----
`XML指可扩展标记语言（eXtensible Markup Language)` `已经成为一种无可忽视的村咋,各种文件的配置文件,数据传输,表示都在使用,JavaScript原生也内置了对
XML的支持,对XML进行解析和序列化等特性`

- [x] :sailboat: <a href="#CreateXML">` 创建一个XML`</a>

- [x] :sailboat: <a href="#XMLDomParser">` DOMParser 类型`</a> `Parser：分析器`

- [x] :sailboat: <a href="#XMLSerializerClass">` XMLSerializer 类型`</a> `Serializer 串行`

- [x] :sailboat: <a href="#IEXMLSupport">` IE8及其之前版本中的XML`</a> 

- [x] :sailboat: <a href="#ManyXMLSupportCross">` 跨浏览XML解析序列化`</a> 

#### <a id="CreateXML">`新建一个XML`</a>  :closed_umbrella: 
* `DOM2在 document.implementation 引入了` [createDocument](https://developer.mozilla.org/en-US/docs/Web/API/DOMImplementation/createDocument) `方法,基本上所有浏览器+IE9[IE不算浏览器...垃圾玩意儿]都支持这个方法`
*  **`创建空白的XML文档`**: `var xmldoc=document.implementation.createDocument(namespaceurl,root,doctype);`

    ```xml
     <XMLU name="参数解释">
       <root mean="根节点名称">在通过JavaScript处理XML时,通常只使用参数root,因为这个参数指定的是XML 
       DOM文档元素的标签名称</root>

       <namespaceurl mean="命名空间">namespaceurl参数也很少用 JavaScript中管理命名空间比较困难</namespaceurl>

       <doctype mean="文档类型">  参数就用得更少了 默认为null DOM2 DOM3都没有改变参数 坚持默认为null</doctype>
     </XMLUser>
    ```
* **`使用注意`**:`使用前检查浏览器是否支持DOM2的XML`
* **`检查方式`**:` var hasXMLDOMFeature= document.implementation.hasFeature("XML","2.0");`

  ```JavaScript
      var hasXMLDOMFeature= document.implementation.hasFeature("XML","2.0");
      if(!hasXMLDOMFeature){
          alert("当前浏览器不支持XML解析构造功能");
      }else{
          //根节点名称 XMLroot
          var xmldoc=document.implementation.createDocument("","XMLroot",null);
          console.warn(xmldoc.documentElement.tagName);
          var child=xmldoc.createElement("child");
          var son=xmldoc.createElement("son");
          son.setAttribute("type","person");
          child.appendChild(son);
          xmldoc.documentElement.appendChild(child);
          console.log(xmldoc);
      }
      /* 输出结果:
        <XMLroot>
          <child>
            <son type="person"/>
          </child>
        </XMLroot>
      */
  ```
  
<a href="#top">`  看完一小节.点我置顶`</small> :relaxed:</a> 

#### <a id="XMLDomParser" target="_blank" href="https://developer.mozilla.org/en-US/docs/Web/API/DOMParser">`DOMParser 分析器`</a>  :closed_umbrella: 
`为了将XML解析为DOM文档,Firefox引入了DOMParser类型,后来其他浏览器也都支持了这个类型,在解析XML之前需要创建一个DOMParser实例,然后调用
parseFromString() 方法 接受两个参数,要解析的XML字符串和内容类型` 
* **`解析方法`**:`DOMParser 的实例方法 parseFromString(xmlstring,"text/xml") 方法 第二参数只能是这个,第一个参数是被解析的XML`
* **`错误处理`**:`该有的错误处理要注意严格把控`
    ```JavaScript
        var hasXMLDOMFeature= document.implementation.hasFeature("XML","2.0");
        if(!hasXMLDOMFeature){
            alert("当前浏览器不支持XML解析构造功能");
        }else{            
            var parser=new DOMParser();
            try{
                var docxml=parser.parseFromString(`<root><son id="name">李志明</son></root>`,"text/xml");
                console.log(docxml.documentElement.tagName);
                console.log(docxml.documentElement.firstChild.tagName);    
                var antherchild=docxml.createElement("child");    
                antherchild.textContent="李嘉坤";
                docxml.documentElement.appendChild(antherchild);
                var children=docxml.getElementsByTagName("child");
                var son=docxml.getElementById("name");
                console.log("son name:"+son.textContent);
                console.log("child 标签数量:"+children.length);
                console.log(docxml);
                //检错
                var errors=docxml.getElementsByTagName("parsererror");
                if(errors.length >0){
                    throw new Error("Parsing error!");
                }    
            }catch(error){
                console.log(error.message);
            }
        }
        /*  root
            son
            son name:李志明
            child 标签数量:1
            <root>
                <son id="name">李志明</son>
                <child>李嘉坤</child>
            </root>
         */
    ```
  -------
  `DOMParser 只会解析格式良好的XML,因而不能把HTML解析为HTML文档。在发生解析错误时,parseFromString 会返回一个Document对象,但这个对象的文档元素是
  <parsererror>,而文档元素的内容是对解析错误的概述.parsererror 有些浏览器也只是这个几个错误`
  
  <a href="#top">`  看完一小节.点我置顶`</small> :relaxed:</a> 
  
#### <a id="XMLSerializerClass" target="_blank" href="https://developer.mozilla.org/en-US/docs/Web/API/XMLSerializer/serializeToString">`XMLSerializer 类型`</a>  :closed_umbrella: 
`在引入DOMParser的同时,Firefox还引入了XMLSeralizer类型,提供了相反的功能:将DOM文档序列化为XML字符串。后来,IE9,Opera,Chrome,Safari等等浏览器
都支持了DOMSerializer 要序列化DOM文档,首先必须创建XMLSerializer的实例,然后将文档传入其SerializeToString() 方法`

##### 将整个HTML文档都序列化为XML文档

   ```JavaScript
    
        window.onload=function(){
            var hasXMLDOMFeature= document.implementation.hasFeature("XML","2.0");
            if(!hasXMLDOMFeature){
                alert("当前浏览器不支持XML解析构造功能");
            }else{            
                var parser=new DOMParser();
                try{
                    var serializer=new XMLSerializer();
                    var xml=serializer.serializeToString(window.document);
                    console.log(xml);
                    //返回 xml格式化后的字符串 但是这个字符串不适合打印,因为会显得很乱,但是
                    // XMLSerializer 可以序列化任何的DOM对象,不仅仅包含个别的节点 也包含html文档
                }catch(error){
                    console.log(error.message);
                }
            }
        }
 ```       
<a href="#top">`  看完一小节.点我置顶`</small> :relaxed:</a> 

#### <a id="IEXMLSupport">`IE8及其之前版本中的XML`</a>  :closed_umbrella: 

`IE是第一个原生支持XML的浏览器,而这一支持是通过ActiveX对象实现的。为了便于桌面应用程序开发人员处理XML,微软创建了MSXML库;但微软并没有针对JavaScript创建不同的对象,而是让web开发人员能够通过浏览器访问相同的对象`

* `ActiveXObject 类型,通过这个类型可以在JavaScript中创建ActiveX对象的实例,但是需要XML文档版本微软提供了六种`

    * `Microsoft XmlDom`:`最初随着不同的XML文档版本可以供选择。`
    * `MSXML 2.DOMDocument`:`方便脚本处理的更新版本,建议只是在特殊情况下使用`
    * `MSXML 2.DOMDocument.3.0`:`为了在JavaScript中使用,这是最低的建议版本`
    * `MSXML 2.DOMDocument.4.0`:`通过脚本处理时并不可靠,这个版本可能会导致警告`
    * `MSXML 2.DOMDocument.5.0`:`并不可靠,可能会到时安全警告`
    * `MSXML 2.DOMDocument.6.0`:`目前最可靠的版本`
        
##### 使用for循环迭代了每个可能的版本,知道创建并且返回读写即可        

        function createDocument(){
            if (typeof arguments.callee.activeXString != "string"){
                var versions = ["MSXML2.DOMDocument.6.0", "MSXML2.DOMDocument.3.0",
                                "MSXML2.DOMDocument"];
        
                for (var i=0,len=versions.length; i < len; i++){
                    try {
                        var xmldom = new ActiveXObject(versions[i]);
                        arguments.callee.activeXString = versions[i];
                        return xmldom;
                    } catch (ex){
                        //skip
                    }
                }
            }
        
            return new ActiveXObject(arguments.callee.activeXString);
        }

    
##### IE解析XML字符串
`IE解析字符串之前必须先创建一个dom文档,然后调用loadXml方法,新创建的XML文档完全是一个空文档,因而不能执行任何操作但是可以通过loadXML()方法
传入XML字符串经过解析后填充到DOM文档中`

```javascript
    var xmldom = createDocument();
    xmldom.loadXML("<root><child/></root>");

    alert(xmldom.documentElement.tagName);  //"root"
    alert(xmldom.documentElement.firstChild.tagName); //"child"

    var anotherChild = xmldom.createElement("child");
    xmldom.documentElement.appendChild(anotherChild);

    var children = xmldom.getElementsByTagName("child");
    alert(children.length);   //2        

    alert(xmldom.xml);
```
##### 错误处理
```javascript
    var xmldom = createDocument();
    xmldom.loadXML("<root>");

    if (xmldom.parseError != 0){
        alert("An error occurred:\nError Code: "
              + xmldom.parseError.errorCode + "\n"
              + "Line: " + xmldom.parseError.line + "\n"
              + "Line Pos: " + xmldom.parseError.linepos + "\n"
              + "Reason: " + xmldom.parseError.reason);
    }
```
##### IE 可以通过load方法从js文档所在服务上加载XML文档----没啥用 已经启用IE
```javascript
    var xmldom = createDocument();
    xmldom.async = false;
    xmldom.load("example.xml");

    if (xmldom.parseError != 0){
        alert("An error occurred:\nError Code: "
              + xmldom.parseError.errorCode + "\n"
              + "Line: " + xmldom.parseError.line + "\n"
              + "Line Pos: " + xmldom.parseError.linepos + "\n"
              + "Reason: " + xmldom.parseError.reason);
    } else {
        alert(xmldom.documentElement.tagName);  //"root"
        alert(xmldom.documentElement.firstChild.tagName); //"child"

        var anotherChild = xmldom.createElement("child");
        xmldom.documentElement.appendChild(anotherChild);

        var children = xmldom.getElementsByTagName("child");
        alert(children.length);   //2        

        alert(xmldom.xml);        
    }
```
<a href="#top">`  看完一小节.点我置顶`</small> :relaxed:</a> 

#### <a id="ManyXMLSupportCross">`跨浏览XML解析序列化`</a>  :closed_umbrella: 
`以前函数可以在四个浏览器使用,但是由于IE 已经被放弃,所以可以不需要掌握有关IE的内容`

##### 解析XML 为DOM
```javascript
        function createDocument(){
            if (typeof arguments.callee.activeXString != "string"){
                var versions = ["MSXML2.DOMDocument.6.0", "MSXML2.DOMDocument.3.0",
                                "MSXML2.DOMDocument"];
        
                for (var i=0,len=versions.length; i < len; i++){
                    try {
                        var xmldom = new ActiveXObject(versions[i]);
                        arguments.callee.activeXString = versions[i];
                        return xmldom;
                    } catch (ex){
                        //skip
                    }
                }
            }
        
            return new ActiveXObject(arguments.callee.activeXString);
        }
    
        function parseXml(xml){
            var xmldom = null;
            
            if (typeof DOMParser != "undefined"){
                xmldom = (new DOMParser()).parseFromString(xml, "text/xml");
                var errors = xmldom.getElementsByTagName("parsererror");
                if (errors.length){
                    throw new Error("XML parsing error:" + errors[0].textContent);
                }        
            } else if (typeof ActiveXObject != "undefined"){
                xmldom = createDocument();
                xmldom.loadXML(xml);
                if (xmldom.parseError != 0){
                    throw new Error("XML parsing error: " + xmldom.parseError.reason);
                }
            } else {
                throw new Error("No XML parser available.");
            }
            
            return xmldom;
        }
        // 使用方法
        var xmldom = null;
        try {
            xmldom = parseXml("<root><child/></root>");
        } catch (ex){
            alert(ex.message);
        }
```

##### 序列化dom为XML
```javascript
        function serializeXml(xmldom){
           
            if (typeof XMLSerializer != "undefined"){
                return (new XMLSerializer()).serializeToString(xmldom);
            } else if (typeof xmldom.xml != "undefined"){
                return xmldom.xml;
            } else {
                throw new Error("Could not serialize XML DOM.");
            }
        }
```
#### [XPath](http://www.runoob.com/xpath/xpath-tutorial.html) 
`XML查询节点的一种手段,自从DOM3开始支持,可以使用hasFeature方法检测浏览器是否支持`
* `在DOM3级XPath规范定义的类型中,最重要的两个类型是XPathEvaluator和XPathResult。XPathEvaluator用于在特定的上下文中对XPath表达式求值,这个类型,有下列三个方法.`
    * **`createExpression(expression,nsresolver)`**:`将XPath 表达式及相应的命名空间信息转换成一个XPathExpression,这是查询的编译版本` 
    * **`createNSResolver(node)`**:`根据node的命名创建一个新的XPathNSResolver对象` 
    * **`evaluate(expression,context,nsresolver,type,result);  expression:表达式, 上下文节点,没有哦命名空间则为null,返回类型`
   ```
    ANY_TYPE	0	无论什么类型自然地来自给定的表达。
    NUMBER_TYPE	1	包含单个数字的结果集。例如，在使用该count()函数的XPath表达式中很有用。
    STRING_TYPE	2	包含单个字符串的结果集。
    BOOLEAN_TYPE	3	包含单个布尔值的结果集。例如，使用该not()函数的XPath表达式很有用。
    UNORDERED_NODE_ITERATOR_TYPE	4	包含与表达式匹配的所有节点的结果集。结果集中的节点不一定与它们在文档中出现的顺序相同。
    ORDERED_NODE_ITERATOR_TYPE	五	包含与表达式匹配的所有节点的结果集。结果集中的节点与它们在文档中出现的顺序相同。
    UNORDERED_NODE_SNAPSHOT_TYPE	6	包含与表达式匹配的所有节点的快照的结果集。结果集中的节点不一定与它们在文档中出现的顺序相同。
    ORDERED_NODE_SNAPSHOT_TYPE	7	包含与表达式匹配的所有节点的快照的结果集。结果集中的节点与它们在文档中出现的顺序相同。
    ANY_UNORDERED_NODE_TYPE	8	包含与表达式匹配的任何单个节点的结果集。节点不一定是文档中与表达式匹配的第一个节点。
    FIRST_ORDERED_NODE_TYPE	9	包含文档中与表达式匹配的第一个节点的结果集。
   ```
    
```javascript
        var supportXPath=document.implementation.hasFeature("XPath","3.0");    
        if(!supportXPath){
            console.error("浏览器不支持XPath 功能");
            alert("浏览器不支持XPath 功能");
        }
        var xmldom = (new DOMParser()).parseFromString(
            "<employees>"+
                "<employee title=\"Software Engineer\">"
                    +"<name>Nicholas C. Zakas</name>"+
                "</employee>"
               +"<employee title=\"Salesperson\">"+
                     "<name>Jim Smith</name>"+
                 "</employee>"+
             "</employees>", "text/xml");

        var serializer = new XMLSerializer();
        var result = xmldom.evaluate("employee/name", xmldom.documentElement, null, XPathResult.ORDERED_NODE_ITERATOR_TYPE, null);

        var message = "";
        var count = 0;

        var element = result.iterateNext();
        while (element) {
            message += serializer.serializeToString(element) + "\n";
            count++;
            element = result.iterateNext()
        }

        message = "There are " + count + " matching nodes.\n" + message;

        console.log(message);
```
