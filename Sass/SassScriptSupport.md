<a id="top" href="#top">SassScript 语法  :maple_leaf:</a> 
----
`除了普通的CSS属性语法之外，Sass还支持一小组名为SassScript的扩展。SassScript允许属性使用变量，算术和额外函数。SassScript可用于任何属性值。
SassScript还可用于生成选择器和属性名称，这在编写mixins时很有用。这是通过插值完成的。SassScript 是sass变量 数据类型的底层支持`
- [x] :maple_leaf: <a href="#SassScriptLearing">`SassScript 认识`</a>
- [x] :maple_leaf: <a href="#SassScriptDataType">`SassScript 数据类型`</a>
- [x] :maple_leaf: <a href="#mediaCheck">`@media`</a>
- [x] :maple_leaf: <a href="#extendCheckonly">` @extend-Only 选择器 %`</a>

####  <a id="SassScriptLearing" href="#SassScriptLearing">SassScript 认识</a>  :star2: <a href="#top"> :arrow_up: </a>
* `Interactive Shell 可以在命令行中测试 SassScript 的功能。在命令行中输入 sass -i，然后输入想要测试的 SassScript 查看输出结果：` <br/>
* `变量仅在定义它们的嵌套选择器级别内可用。如果它们是在任何嵌套选择器之外定义的，那么它们随处可见。它们也可以用!global旗帜定义，在这种情况
下它们也随处可见。`<br/>
* **`变量: $开头`** `$width: 5em;`

  ```scss
  #main {
    $width: 5em !global;
    width: $width;
  }

  #sidebar {
    width: $width;
  }
  ```
####  <a id="SassScriptDataType" href="#SassScriptDataType">SassScript 数据类型</a>  :star2: <a href="#top"> :arrow_up: </a>
* `Sass 支持八种数据类型`
  * `数字(Number): 1, 2, 13, 10px`
  * `字符串(String):有引号字符串与无引号字符串，"foo", 'bar', baz`
  * `颜色(Color):blue, #04a3f9, rgba(255,0,0,0.5)`
  * `布尔型(Boolean):true, false  SassScript支持and，or和not运算符为布尔值。`
  * `空值(null):null`
  * `数组 (list):由空格或逗号隔开 1.5em 1em 0 2em, Helvetica, Arial, sans-serif`
  * `键值对(Map):相当于 JavaScript 的 object 从一个值映射到另一个值（例如(key1: value1, key2: value2)）`
##### `数组的作用: 数组不支持任何运算方式`
* `margin: 10px 15px 0 0;`  `font-face: Helvetica, Arial, sans-serif;`
```scss
  $height:200px;
  $list-margin: 10px 15px 0 0;

  .lab-div-info{
      width: $height;
      .funky {
          font: {
            family: fantasy;
            size: 30em;
          }
        }
        margin: $list-margin;
  }
```
##### `运算`
`如果需要使用变量，同时又要确保 / 不做除法运算而是完整地编译到 CSS 文件中，只需要用 #{} 插值语句将变量包裹。`
```scss
p {
  $font-size: 12px;
  $line-height: 30px;
  font: #{$font-size}/#{$line-height};
}

.plass{
  $font-size: 12px;
  $line-height: 30px;
  font: $font-size/$line-height;
}
```
```scss
p{
  font: 12px/30px;
}

.plass {
  font: 0.4;
}
```
##### `#{} 插值语句`
`通过 #{} 插值语句可以在选择器或属性名中使用变量：`
```scss
$name: foo;
$attr: border;
p.#{$name} {
  #{$attr}-color: blue;
}
```
####  <a id="mediaCheck" href="#mediaCheck">@media</a>  :star2: <a href="#top"> :arrow_up: </a>
`Sass 中 @media 指令与 CSS 中用法一样，只是增加了一点额外的功能：允许其在 CSS 规则中嵌套。如果 @media 嵌套在 CSS 规则内，编译时，@media 将被
编译到文件的最外层，包含嵌套的父选择器`
```scss
.sidebar {
  width: 300px;
  @media screen  and (max-width:800px) and (orientation: landscape) {
    width: 500px;
  }
}
```
```css
@media screen and (max-width: 800px) and (orientation: landscape) {
  .sidebar {
    width: 500px;
  }
}
```
**`@media 甚至可以使用 SassScript（比如变量，函数，以及运算符）代替条件的名称或者值`**
```scss
$media: screen;
$feature: -webkit-min-device-pixel-ratio;
$value: 1.5;

@media #{$media} and ($feature: $value) {
  .sidebar {
    width: 500px;
  }
}
```
```css
@media screen and (-webkit-min-device-pixel-ratio: 1.5) {
  .sidebar {
    width: 500px;
  }
}
```
####  <a id="extendCheckonly" href="#extendCheckonly">@extend-Only %选择器</a>  :star2: <a href="#top"> :arrow_up: </a>
`有时，需要定义一套样式并不是给某个元素用，而是只通过 @extend 指令使用，尤其是在制作 Sass 样式库的时候，希望 Sass 能够忽略用不到的样式。Sass 
引入了“占位符选择器” (placeholder selectors)，看起来很像普通的 id 或 class 选择器，只是 # 或 . 被替换成了 %。可以像 class 或者 id 选择器
那样使用，当它们单独使用时，不会被编译到 CSS 文件中。`
```scss
%extreme {
  color: blue;
  font-weight: bold;
  font-size: 2em;
}

.notice {
  @extend %extreme;
}

#context a%what {
  color: blue;
  font-weight: bold;
  font-size: 2em;
}

.noticewhat {
  @extend %what;
}
```
`编译结果:`
```css
.notice {
  color: blue;
  font-weight: bold;
  font-size: 2em;
}

#context a.noticewhat {
  color: blue;
  font-weight: bold;
  font-size: 2em;
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







