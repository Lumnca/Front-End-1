<a id="top"  href="#">:maple_leaf: JavaScript数据存储 </a>:arrow_lower_left:
----

- [x] <a href="#CookieInfo">`Cookie 信息`</a>
- [x] <a href="#SubCookie">`Sub Cookie`</a>
- [x] <a href="#NoticeCookie">`Cookie 注意`</a>

### [1.Cookie](#) <span id="CookieInfo"></span>
`用于在客户端存储信息`
* Cookie的构成
  * `名称`:`key ,cookie不区分大小写,但是实践中最好当做区分大小写,因为某些服务会这样处理,Cookie的名称必须进过URL编码的。`
  * `值`:`存储信息`
  * `域`:`所有想改域发送的请求都会包含这个cookie信息`
  * `路径`:`指定域的那个路径,可以向服务器发送Cookie，例如可以指定只有在http://www.wangzhe.com/book/ 才能访问,那么http://www.wangzhe.com 就
          不能发送cookie信息,即使请求来着同一个域`
  * `失效时间`:`什么时候浏览器删除掉的时间戳, 这个值是GMT时间格式 Wdy,DD-Mon-YYYY HH:MM:SS`    
     
     * 1.**`GMT转普通格式`**
     
     ```javascript
       GMTToStr(time){
            let date = new Date(time)
            let Str=date.getFullYear() + '-' +
            (date.getMonth() + 1) + '-' + 
            date.getDate() + ' ' + 
            date.getHours() + ':' + 
            date.getMinutes() + ':' + 
            date.getSeconds()
            return Str
        }
     ```
     * 2.**`普通格式转GMT`**
     
     ```javascript
       StrToGMT(time){
            let GMT = new Date(time)
            return GMT
        }
     ```
     
     
     
  * `安全标志`:`指定后,cookie只有在使用SSL链接的时候才能发送到服务器`
  <br/>
  
  ```http
    HTTP/1.1 200 OK
    Content-type: text/html
    Set-Cookie: name=value; expires=Mon， 22-Jan-07 07:10:24 GMT; domin=.www.com
    Other-header: other-header-value
  ```
* 设置Cookie 使用Cookie 
  ```javascript
      //设置一个cookie键值对: "name":"JiangXing"
      document.cookie=encodeURIComponent("name")+"="+encodeURIComponent("JiangXing");
  ```
  
* Cookie 操作对象 <a href="#top">置顶</a>
  
  ```javascript
    var CookieUtil = {
          get: function (name){
              var cookieName = encodeURIComponent(name) + "=",
                  cookieStart = document.cookie.indexOf(cookieName),
                  cookieValue = null,
                  cookieEnd;     
              if (cookieStart > -1){
                  cookieEnd = document.cookie.indexOf(";", cookieStart);
                  if (cookieEnd == -1){
                      cookieEnd = document.cookie.length;
                  }
                  cookieValue = decodeURIComponent(document.cookie.substring(cookieStart + 
                  cookieName.length, cookieEnd));
              } 
              return cookieValue;
          },

          set: function (name, value, expires, path, domain, secure) {
              var cookieText = encodeURIComponent(name) + "=" + encodeURIComponent(value);
              if (expires instanceof Date) {
                  cookieText += "; expires=" + expires.toGMTString();
              }
              if (path) {
                  cookieText += "; path=" + path;
              }
              if (domain) {
                  cookieText += "; domain=" + domain;
              }
              if (secure) {
                  cookieText += "; secure";
              }
              document.cookie = cookieText;
          },

          unset: function (name, path, domain, secure){
              this.set(name, "", new Date(0), path, domain, secure);
          }
    };
  ```
* 使用 CookieUtil  <a href="#top">置顶</a>

  ```javascript
        //document.cookie=encodeURIComponent("name")+"="+encodeURIComponent("JiangXing");
        if(CookieUtil.get("name")!=null){
            let Name=CookieUtil.get("name");
            console.info(Name);
            CookieUtil.unset("name",null,null,null);
        }else{
            console.log("cookie 不存在!");

        }
  ```
### <a href="#ttp" id="ttp"> 2.子 Cookie </a>  <a href="#top" id="SubCookie" >置顶</a> 

`子Cookie一般格式`:`name=name1=value1&name2=value2&name3=value3`

* 操作 子Cookie

```javascript
    var SubCookieUtil = {

    get: function (name, subName){
        var subCookies = this.getAll(name);
        if (subCookies){
            return subCookies[subName];
        } else {
            return null;
        }
    },

    getAll: function(name){
        var cookieName = encodeURIComponent(name) + "=",
            cookieStart = document.cookie.indexOf(cookieName),
            cookieValue = null,
            cookieEnd,
            subCookies,
            i,
            parts,
            result = {};

        if (cookieStart > -1){
            cookieEnd = document.cookie.indexOf(";", cookieStart)
            if (cookieEnd == -1){
                cookieEnd = document.cookie.length;
            }
            cookieValue = document.cookie.substring(cookieStart + cookieName.length, cookieEnd);

            if (cookieValue.length > 0){
                subCookies = cookieValue.split("&");

                for (i=0, len=subCookies.length; i < len; i++){
                    parts = subCookies[i].split("=");
                    result[decodeURIComponent(parts[0])] = decodeURIComponent(parts[1]);
                }

                return result;
            }  
        } 

        return null;
    },

    set: function (name, subName, value, expires, path, domain, secure) {

        var subcookies = this.getAll(name) || {};
        subcookies[subName] = value;
        this.setAll(name, subcookies, expires, path, domain, secure);

    },

    setAll: function(name, subcookies, expires, path, domain, secure){

        var cookieText = encodeURIComponent(name) + "=",
            subcookieParts = new Array(),
            subName;

        for (subName in subcookies){
            if (subName.length > 0 && subcookies.hasOwnProperty(subName)){
                subcookieParts.push(encodeURIComponent(subName) + "=" + encodeURIComponent(subcookies[subName]));
            }
        }

        if (subcookieParts.length > 0){
            cookieText += subcookieParts.join("&");

            if (expires instanceof Date) {
                cookieText += "; expires=" + expires.toGMTString();
            }

            if (path) {
                cookieText += "; path=" + path;
            }

            if (domain) {
                cookieText += "; domain=" + domain;
            }

            if (secure) {
                cookieText += "; secure";
            }
        } else {
            cookieText += "; expires=" + (new Date(0)).toGMTString();
        }

        document.cookie = cookieText;        

    },

    unset: function (name, subName, path, domain, secure){
        var subcookies = this.getAll(name);
        if (subcookies){
            delete subcookies[subName];
            this.setAll(name, subcookies, null, path, domain, secure);
        }
    },

    unsetAll: function(name, path, domain, secure){
        this.setAll(name, null, new Date(0), path, domain, secure);
    }

    };
```
* 操作
```javascript
    function StrToGMT(time){
        let GMT = new Date(time);
        return GMT;
    }
    SubCookieUtil.set("data","name","JiangXing");
    SubCookieUtil.set("data","book","JavaScript5 高级教程",StrToGMT("2018-8-5 20:24"));
    console.log(SubCookieUtil.get("data","book"));    
```
### <a id="NoticeCookie">`Cookie 注意`</a>
`还有一类Cookie被称为` `HTTP 专有Cookie 可以从浏览器或者服务器设置,但是只能在服务器端读取,因为Js无法获取HTTP专有 Cookie的值`
