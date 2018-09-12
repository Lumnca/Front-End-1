<a id="top" href="#top">Sass 语法  :maple_leaf:</a> 
----
`Sass语法及其简单,让我们来进入Sass的世界`

- [x] :maple_leaf: <a href="#SassValraible">`Sass 变量 `</a>
- [x] :maple_leaf: <a href="#SassQianTao">`Sass 嵌套`</a>
  - <a href="#CengciProperty" >`sass 层次嵌套`</a>
  - <a href="#Property" >`sass 属性嵌套`</a>
- [x] :maple_leaf: <a href="#P">`部分 scss `</a>
- [x] :maple_leaf: <a href="#">``</a>

####  <a id="SassValraible" href="#SassValraible">Sass 变量</a>  :star2: <a href="#top"> :arrow_up: </a>
* `Sass 变量可以存储颜色，字体堆栈或您认为要重用的任何CSS值等内容 Sass 变量必须以` `$` `开头如果变量需要嵌套到字符串之中，就必须卸载#{}中` 
* `Sass 变量可以参与运算 +-*/ ()都可以`
* `Sass 变量以:` `;` `结尾` 
* `Sass 赋值的方法是使用 ` `:` `左边是变量名称--右边是值`
* `对于定义在全局的变量文件每一个地方都可以访问,如果变量定义在 {} 那么它 的作用域就在 {} 内部 也就是说变量具有作用域`
```css
  $color-red:"red";
  $width: 500px;
  $nav-outter-width:200px;
  $nav-inner-width: $nav-outter-width*0.8;
  
  .nav-outter{
      width: $nav-outter-width;
  }
  .nav-inner{
      width: $nav-inner-width;
  }
  .nav-bar{
      width: $width;
      border:"1px solid #{$width}" //使用变量
  }
  .font-color{
      color:$color_red;
  }
```
**`编译结果:`**
```css
.nav-outter {
  width: 200px;
}

.nav-inner {
  width: 140px;
}

.nav-bar {
  width: 500px;
  border: "1px solid 500px";
}

.font-color {
  color: "red";
}
```
**`运算：有注意的地方`**
* `在乘除运算中, 如果两个变量运算不可以都带上单位,如此则不能够参加乘除运算`:`建议对于参与运算的两个值或者多个值,其中一个带上单位其他不带单位即可
在数值运算中,如下修改所示` 
* `ruby底层在处理运算的时候由需要符号,来确定最后的值的单位是什么`
* `运算支持` `()`
* `sass还支持这样的非变量运算: height: 70px+40px;`
```scss
$zero-up : 20px;
$zero-down : 40px;

.nav-height{
    width:40px+90px;
    height: $zero-down+$zero-up; //支持
}

.nav-title{
    height: $zero-down * $zero-up; //不支持 可以把两个变量定义成
}

00px*px isn't a valid CSS value.
        on line 9 of sass/m:\vscode-workspace\Sass\Arithmatic.scss
>>     height: $zero-down * $zero-up;
```
* `1. 修改方式1`:`可以变量都不带单位最后加上一个值为0 的带单位数`
```scss
$zero-up : 20;
$zero-down : 40;

.nav-height{
    height: ($zero-down+$zero-up)+0px ;
}

.nav-title{
    height: ($zero-down * $zero-up) +0px;
}
```
* `2. 修改方式2`:`这种方式修改更加简洁`
```scss
$zero-up : 20;
$zero-down : 40px;

.nav-height{
    height: $zero-down+$zero-up;
}

.nav-title{
    height: $zero-down * $zero-up;
}
```
####  <a id="SassQianTao" href="#SassQianTao">Sass 嵌套</a>  :star2: <a href="#top" id="CengciProperty"> :arrow_up: </a>
`sass 支持嵌套以,减少css的工作量,请看下面的`
```scss
nav{
    ul {
        width: 200px;
        height:50px;
        font-size: 14px;
        line-height: 18px;
    }  
    div{
        padding: 5px;
        a{
            text-decoration: none;
            padding: 5px;
        }
    } 
    
    .full-left{
        float: left;
        padding-left: 5px;   
    } 
    .full-right{
        float: right;
        padding-right: 5px;
    }

    margin: 5px;
    padding: 5px;
}
```
**`编译结果:`**
* `它具有清晰的嵌套和可视层次结构，scss的层次结构更加的清晰`
```css
nav {
  margin: 5px;
  padding: 5px;
}

nav ul {
  width: 200px;
  height: 50px;
  font-size: 14px;
  line-height: 18px;
}

nav div {
  padding: 5px;
}

nav div a {
  text-decoration: none;
  padding: 5px;
}

nav .full-left {
  float: left;
  padding-left: 5px;
}

nav .full-right {
  float: right;
  padding-right: 5px;
}
```
####  <a id="Property" href="#Property">Sass 属性嵌套</a>  :star2: <a href="#top"> :arrow_up: </a>
```scss
```

####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
`您可以创建包含很少CSS片段的部分Sass文件，您可以将这些片段包含在其他Sass文件中。这是模块化CSS并帮助保持易于维护的好方法。partial只是一个以前导下划线命名的Sass文件。你可能会说出类似的东西_partial.scss。下划线让Sass知道该文件只是一个部分文件，不应该生成CSS文件。Sass partials与@import指令一起使用。`
* `nav.scss`
```scss
body{
    a{
        text-decoration: none;
    }
}
```
* `link.scss`
```scss
nav{
    ul {
        width: 200px;
        height:50px;
        font-size: 14px;
        line-height: 18px;
    }  
}
```
* `lab.scss`
```scss
@import "nav";
@import "link";

$height:200px;

.lab-div-info{
    width: $height;
    .funky {
        font: {
          family: fantasy;
          size: 30em;
        }
      }
}
```
**`编译结果:`**
```css
nav ul {
  width: 200px;
  height: 50px;
  font-size: 14px;
  line-height: 18px;
}

body a {
  text-decoration: none;
}

.lab-div-info {
  width: 200px;
}

.lab-div-info .funky {
  font-family: fantasy;
  font-size: 30em;
}

```

####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>
####  <a id="" href="#"></a>  :star2: <a href="#top"> :arrow_up: </a>







