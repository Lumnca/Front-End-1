### [JavaScript OO 之继承](#top) :grey_exclamation: <b id="top"></b>
:white_check_mark: `继承方法 虽然有很多种 但是 我们一般只用那么一种 因为其他的都是这一种继承方法的垫脚石,推荐使用寄生组合继承`

- [x] [`1.原型链继续`](#proto) 
- [x] [`2.理解一下属性在哪里`](#property) 
- [x] [`3.借用构造函数继承`](#constructor)
- [x] [`4.组合继承`](#useall)
- [x] [`5.原型继承`](#prototype)
----
#####  :octocat: [1.原型链继续](#top) <b id="proto"></b> 
* `原型链-继承,你不会喜欢这个继承方式  原因 你不是继承一个类 而是继承一个 父类的实例 这是不优雅的`
* `constructor`:`构造函数属性 在原型对象中 prototype 中, constructor默认执行构造函数 就是拥有这个原型对象的构造函数 `
* `原型对象继承 类似于 Java/C# 使用 静态属性 静态方法的 来实现继承 不推荐使用`
```node
/* ------ 父类 ------ */
function Person(name,age){
    this.name = name;
    this.age = age;
}
Person.prototype.GetName = function () {
    return this.name.toLowerCase();
}
let p1 = new Person("JxKicker",18);

console.log(p1);
/* ------- 父类 ------- */

/* ------- 子类 ------- */
function Student(stuId){
    this.stuId = stuId;
}
Student.prototype = new Person("JxKicker",18); 
let stu = new Student("2016110418");
/* ------- 子类 ------- */
```
#####  :octocat: [2.理解一下属性在哪里](#top) <b id="property"></b> 
* `-- 读取属性的特性 --`:`Object.getOwnPropertyDescriptor(Object,"PropertyName");`
* `-- in 操作符号 --`：`如果属性在实例中 返回 ture,如果属性在对象的原型中 也返回 ture 否则我返回 false`
* `-- 判断属性在哪里 --`:`let isHave = stu.hasOwnProperty('stuId'); 每一个对象有这个方法 判断属性是否在对象实例中`
* `-- 获得可枚举的属性 --`:`Object.keys() 接受一个对象作为参数 返回一个包含所有可枚举属性字符串数组`

#####  :octocat: [3.借用构造函数继承](#top) <b id="constructor"></b> 
`你了解一下就行了  为啥呢 这种构造函数仍然不完美 因为没有完成函数的复用`
* `使用借用构造函数无法 实现 子类是属于父类的判断 子类 instanceof 父类 会返回 false`
```node
/***************** 父类 *******************/
function Egg(color = "white",typeName ="卵生物种"){
    this.typeName =  typeName ,
    this.color = color
}

Egg.prototype.getType = function(){
    return this.typeName;
}
/***************** 父类 *******************/


/***************** 子类 *******************/

function chicken(MainColor,sex,weight){
    Egg.call(this,MainColor,"鸡"); //借用构造函数
    this.sex = sex;
    this.weight = weight;
}

chicken.prototype.getPrice = function(Meony){
    if (typeof Meony != "number") {
        console.error('Error', 'Meony is not Number Type')
    }
    return  this.weight * Meony;
}

let littleChicken =  new chicken("White",true,2.1);

console.log(littleChicken);
// chicken { typeName: '鸡', color: 'White', sex: true, weight: 2.1 }

console.log(littleChicken instanceof Egg); //而且 并不承认它的继承地位
// false

// littleChicken.getType();
// 这里会报错 没有这个方法
/***************** 子类 *******************/
```

#####  :octocat: [4.组合继承](#top) <b id="useall"></b> 
`它又名为 伪经典继承 同时使用原型继承 和构造函数继承 构造函数继承属性  原型继承原型函数对象`
* `这是非常需要掌握的继承方式 `
* `子类 instanceof 父类 会返回 ture 实现了继承`
```node

function Chicken(MainColor,sex,weight){
    Egg.call(this,MainColor,"鸡"); //借用构造函数
    this.sex = sex;
    this.weight = weight;
}

Chicken.prototype = new Egg();
Chicken.prototype.getPrice = function(Meony){
    if (typeof Meony != "number") {
        console.error('Error', 'Meony is not Number Type')
    }
    return  this.weight * Meony;
}


let littleChicken =  new Chicken("White",true,2.1);
console.log("物种:" + littleChicken.getType());

console.log(littleChicken);
// Egg { typeName: '鸡', color: 'White', sex: true, weight: 2.1 }

console.log(littleChicken instanceof Egg); //而且 并不承认它的继承地位
// true

/***************** 子类 *******************/
```

#####  :octocat: [5.原型继承](#top) <b id="prototype"></b> 
`道格拉斯.克罗克福德 提出的` `使用原型完成继承本身就是一件 失败的事情 就好像让C# Java用静态属性来完成继承一样 天方夜谭`
* `利用一件存在的一个对象作为原型 赋值给一个新的对象 完成继承`
* `要求必须先要有一个对象`
* `放弃它吧 我们需要继承的 不是对象 而是类 从这点看来 这个继承方式就是错误的 `
```node
 function object(o){
  function F() {};
  F.prototype = o;
  return new F();
 }
```
