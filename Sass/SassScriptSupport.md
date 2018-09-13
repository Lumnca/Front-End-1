<a id="top" href="#top">SassScript 语法  :maple_leaf:</a> 
----
`除了普通的CSS属性语法之外，Sass还支持一小组名为SassScript的扩展。SassScript允许属性使用变量，算术和额外函数。SassScript可用于任何属性值。
SassScript还可用于生成选择器和属性名称，这在编写mixins时很有用。这是通过插值完成的。SassScript 是sass变量 数据类型的底层支持`
- [x] :maple_leaf: <a href="#SassScriptLearing">`SassScript 认识`</a>
- [x] :maple_leaf: <a href="#SassScriptDataType">`SassScript 数据类型`</a>
- [x] :maple_leaf: <a href="#mediaCheck">`@media`</a>
- [x] :maple_leaf: <a href="#extendYueShu">`@extend 约束`</a>
- [x] :maple_leaf: <a href="#extendCheckonly">` @extend-Only 选择器 %`</a>
- [x] :maple_leaf: <a href="#optionalShoose">`!optional `</a>
- [x] :maple_leaf: <a href="#debugCoding">`@debug @warn`</a>

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
  
#### 变量默认值： !default
`相当于变量的默认值,如果变量为null 或者不存在之前那就是使用这个值`
```scss

$content: "Second content?" !default;
$content: "First content";
$new_content: "First time reference" !default;

#main {
  content: $content;
  content: $new_content;
}
```
`编译结果: `
```css
#main {
  content: "First content";
  content: "First time reference";
}
```
`具有null值的变量被视为未分配的！default：`
```scss
$content: null;
$content: "Non-null content" !default;

#main {
  content: $content;
} 
```
`编译结果:`
```css
#main {
  content: "Non-null content"; }
```
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
#### `运算`
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
#### <a id="extendCheckonly" href="#extendCheckonly">@extend-Only %选择器</a>  :star2: <a href="#top"> :arrow_up: </a>
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
#### <a id="extendYueShu" href="#extendYueShu">@extend 的约束</a>  :star2: <a href="#top"> :arrow_up: </a>
`@extend在指令中使用有一些限制,下面是有错的,Sass无法使@media块外的CSS规则适用于其中的选择器 通过extend`
```scss
.error {
  border: 1px #f00;
  background-color: #fdd;
}

@media print {
  .seriousError {
    // INVALID EXTEND: .error is used outside of the "@media print" directive
    @extend .error;
    border-width: 3px;
  }
}
```


####  <a id="optionalShoose" href="#optionalShoose">!optional </a>  :star2: <a href="#top"> :arrow_up: </a>
`通常，当您扩展选择器时，如果@extend不起作用则会出错。例如，如果您编写a.important {@extend .notice}，如果没有包含的选择器，则会出错.notice。如果包含的唯一选择器.notice是h1.notice，则也是一个错误，因为h1与之冲突a并且因此不会生成新的选择器` <br/>

`但有时候，您希望允许@extend不生成任何新的选择器。为此，只需!optional在选择器后添加标志即可。例如：`

```scss
#main {
  content: $content;
  content: $new_content;
  @extend .DivFnd !optional //实际上并没有DivFnd 这个class类 但是加上 !optional 不会出现
}
```

####  <a id="debugCoding" href="#debugCoding">@debug @warn</a>  :star2: <a href="#top"> :arrow_up: </a>
* `@debug 指令将SassScript表达式的值打印到标准错误输出流。它对于调试具有复杂SassScript的Sass文件非常有用`
* `@warn 指令将SassScript表达式的值打印到标准错误输出流 `
```scss
  @debug 10em + 12em;
  //输出: Line 1 DEBUG: 22em
```

