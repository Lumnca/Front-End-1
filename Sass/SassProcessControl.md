<a id="top" href="#top">Sass 语法 Over  :maple_leaf:</a> 
----
`Sass的语法即将结束.当sass语法更新的时候,笔记也将持续更新`

- [x] :maple_leaf: <a href="#ifelse">`控制指令`</a>
- [x] :maple_leaf: <a href="#eachList">`@each `</a>
- [x] :maple_leaf: <a href="#whilelist">`@while`</a>
- [x] :maple_leaf: <a href="#mixinclude">`@Mixin @inlude 指令 `</a>
- [x] :maple_leaf: <a href="#functioncode">`@function 指令 `</a>

####  <a id="ifelse" href="#ifelse">控制指令</a>  :star2: <a href="#top"> :arrow_up: </a>
`SassScript支持基本控制指令，仅在某些条件下包含样式，或者在变化时多次包含相同的样式。`<br/>

**`@if`** 
```scss
p {
  @if 1 + 1 == 2 { border: 1px solid;  }
  @if 5 < 3      { border: 2px dotted; }
  @if null       { border: 3px double; }
}
```
**`@else @else if`**
```scss
$type: monster;
p {
  @if $type == ocean {
    color: blue;
  } @else if $type == matador {
    color: red;
  } @else if $type == monster {
    color: green;
  } @else {
    color: black;
  }
}
```
`编译结果:`
```css
p {
  border: 1px solid;
}
p {
  color: green;
}
```
**`@for`**:`该指令有两种格式:` `for $var from <start> through <end>` 和 `@for $var from <start> to <end>`
```scss
@for $i from 1 through 3 {
  .item-#{$i} { width: 2em * $i; }
}
```
`编译结果:`
```css
.item-1 {
  width: 2em;
}

.item-2 {
  width: 4em;
}

.item-3 {
  width: 6em;
}
```
####  <a id="eachList" href="#eachList">@each</a>  :star2: <a href="#top"> :arrow_up: </a>
```scss
@each $var in succces,danger,info,default,warning {
  .text-#{$var}{
    background-image: url('/images/#{$var}.png');
  }
}
```
```css
.text-danger {
  background-image: url("/images/danger.png");
}

.text-info {
  background-image: url("/images/info.png");
}

.text-default {
  background-image: url("/images/default.png");
}

.text-warning {
  background-image: url("/images/warning.png");
}
```

####  <a id="whilelist" href="#whilelist">@while</a>  :star2: <a href="#top"> :arrow_up: </a>
`该@while指令采用SassScript表达式并重复输出嵌套样式，直到语句求值为止false。这可以用来实现比@for语句更复杂的循环，尽管这很少是必要的。例如：`
```scss
$count : 3;
@while $count > 0 {
  .list-item-#{$count}{
     width: $count * 10px;
  }
  $count : $count - 1  //注意要有空格隔开 不然报错哦
}
```
`编译结果：`
```css
.list-item-3 {
  width: 30px;
}

.list-item-2 {
  width: 20px;
}

.list-item-1 {
  width: 10px;
}

```
####  <a id="mixinclude" href="#mixinclude">@Mixin @inlude 指令</a>  :star2: <a href="#top"> :arrow_up: </a>
`Mixins允许您定义可以在整个样式表中重复使用的样式`
* `无参数mixin`
```scss
@mixin large-text {
  font: {
    family: Arial;
    size: 20px;
    weight: bold;
  }
  color: #ff0000;
}

.page-title {
  @include large-text;
  padding: 4px;
  margin-top: 10px;
}
```
```css
.page-title {
  font-family: Arial;
  font-size: 20px;
  font-weight: bold;
  color: #ff0000;
  padding: 4px;
  margin-top: 10px;
}
```
* `@mixin 代码块`
```scss
@mixin silly-links {
  a {
    color: blue;
    background-color: red;
  }
}

@include silly-links;
```
`编译结果:`
```css
a {
  color: blue;
  background-color: red;
}
```
* `@minxin 带参数`:`参数可以带默认值`
```scss
@mixin sexy-border($color, $width:2in) {
  border: {
    color: $color;
    width: $width;
    style: dashed;
  }
}
p { @include sexy-border(blue, 1in); }
```
`编译结果:`
```css
p {
  border-color: blue;
  border-width: 1in;
  border-style: dashed; }
```
* `参数个数不定...`
```scss
@mixin box-shadow($shadows...) {
  -moz-box-shadow: $shadows;
  -webkit-box-shadow: $shadows;
  box-shadow: $shadows;
}
.shadows {
  @include box-shadow(0px 4px 5px #666, 2px 6px 10px #999);
}
```
`编译结果:`
```css
.shadows {
  -moz-box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
  -webkit-box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
  box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
}
```
####  <a id="functioncode" href="#functioncode">@function 指令</a>  :star2: <a href="#top"> :arrow_up: </a>
`scss 用户可以自定义函数,然后在脚本中自由使用它`:`@return以设置函数的返回值。`:`@function 定义函数` `可以传递参数`
```scss
$grid-width: 40px;
$gutter-width: 10px;

@function grid-width($n) {
  @return $n * $grid-width + ($n - 1) * $gutter-width;
}

#sidebar { width: grid-width(5); }
```
`编译结果:`
```css
#sidebar {
  width: 240px;
}

```








