### [JavaScript 面向对象](#top) <b id="top"></b> :maple_leaf:

----
:white_check_mark: `JavaScript5 没有类 但是有对象，JS对象是一个非常有趣的东西 它就是无序属性的集合 属性可以为基本值 对象 和函数`

- [x] :maple_leaf: [`Object 属性类型/特性`](#object)
   * `数据属性`
       * `特性` `Object.defineProperty`
   * `访问器属性`
       * `特性` `Object.defineProperties`
###### [Object 属性类型/特性](#top)  :maple_leaf:
`ECMA 在第五版定义了只有内部采用的特性 描述了属性的各种特性,ECM-262 定义这些特性是否了实现JavaScript 是为了实现JavaScripty殷勤用的,因此Js代码中无法访问他们
为了表示特性是内部值 规范用双中括号表示 [[Enumerable]]`

- [x] (1). ECMA中有两种属性:数据属性和访问器属性

##### 数据属性
`包含一个数据值的位置，这个位置可以读取 数据属性有四个描述其行为的特性`

- [x] `(1)`. `[[Configurable]]`:`是否能够通过delete 删除属性从而重新定义属性 默认值为true`
- [x] `(2)`. `[[Enumerable]]`: `表示能否通过for-in循环返回属性默认为true`
- [x] `(3)`. `[[Writeable]]`:`表示能否修改属性的值 默认为 true`
- [x] `(4)`. `[[Value]]`:`包含这个属性的数据值，读取属性值的时候 从这个位置读取 写入属性值的 吧新值保存在这个位置`

```javascript
var person = {
  Name:"Jxkicker" //前三个特性值为 true [[Value]] 为 "Jxkicker"
}
```
#####  :maple_leaf::[Object.defineProperty(obj,propertyName,obj_desc)](#top)
`如果要修改属性默认的特性,必须使用defineProperty方法 接收三个参数 属性所在对象 属性名称 和一个描述符对象 描述符对象的属性必须是  configurable,enumerable
writeable,value 设置一个或者多个值`
* `注意`:`那么不设置的特征值是 默认值 可以多次调用 此方法修改同一个属性但是 但是在吧configurable设置 为false之后就会有错误了 `
```javascript
var person = {} ; 

Object.defineProperty(person,"name",{
    configurable:true,
    writable:false,
    value:"JxKicker"
});

person.name = "Kicker";

console.log(person.name); //JxKicker
```

##### 访问器属性
`它不包含值;他们包含一堆getter setter 函数 在读取属性值的时候调用getter属性 在设置属性值的时候 掉setter值 这个函数负责决定如何处理函数,访问属性有如下四个
特性值`

- [x] `(1)`. `[[Configurable]]`:`是否能够通过delete 删除属性从而重新定义属性 默认值为true`
- [x] `(2)`. `[[Enumerable]]`: `表示能否通过for-in循环返回属性默认为true`
- [x] `(3)`. `[[Get]]`:`在读取属性的时候调用的函数 默认值 undefined`
- [x] `(4)`. `[[Set]]`:`在设置属性的时候调用的函数 默认值 undefined`

```javascript
var user = {
    _birth_year:1998,
    age:20
}

Object.defineProperty(user,"birthYear",{
    get:function(){
        return this._birth_year;
    },
    set:function(newValue = 1998){
        this._birth_year = newValue;
        var date = new Date();
        this.age = date.getFullYear() - this._birth_year;
    }
});

user.birthYear = 1997;

console.log(user.age);
console.log(user.birthYear);
```

##### :maple_leaf: [Object.defineProperties()](#top)
`一次性定义多个属性`

```node
var book = {};

Object.defineProperties(book,{
    _year:{
        writable:true,
        value:2004
    },
    edition:{
        writable:true, //一定要有 不然要出错 使用 defineProperties 默认值为
        value:1
    },
    year:{
        get: function(){
            return this._year;
        },
        set: function(newValue){
            if(newValue >= 2004  ){
                this._year = newValue;
                this.edition = newValue - 2003;
            }
            
        }
    }
});
book.year = 2008;

console.log(book.edition);
```














