<a id="top" href="#top">Sass 运行环境安装  :maple_leaf:</a> 
----
`	Sass是世界上最成熟，最稳定，最强大的专业级CSS扩展语言。Bootstrap4.0 也是基于Sass 编写的,使用Sass构建了无数的框架。Compass，Bourbon和Susy..。`

- [x] :maple_leaf: <a href="#WindowsInstallSass">`Windows 10 安装Sass`</a>
- [x] :maple_leaf: <a href="#CodingFileSass">`编译文件`</a>
- [x] :maple_leaf: <a href="#vscodeUseSass">`使用vscode 实现自动编译 / 自由开发`</a>

#####  <a id="WindowsInstallSass" href="#WindowsInstallSass">安装Sass</a>  :star2: <a href="#top"> :arrow_up: </a>
`Sass 是基于Ruby的扩展语言,所以需要安装Ruby`
* 1.[`Ruby 安装地址`](http://rubyinstaller.org/downloads)
  * `安装完后 在windos dos 中 输入` `ruby -v` `输出版本 信息输出后安装成功`
* 2.`安装ruby gem源 才能安装Sass`

  ```shell
    //1.删除原gem源 因为下载太慢了  除非你能够翻墙
    gem sources --remove https://rubygems.org/

    //2.安装 切换gem 源 腾讯支持gem源 https://gems.ruby-china.com  淘宝的gem源已经不行了
    // 如果实在不行 请安装 Shadowsocks 翻墙 然后服务器代理到 tokyo 然后就用原来的下载也行
    gem sources -a https://gems.ruby-china.com/

    //3.打印是否替换成功
    gem sources -l

    //4.更换成功后打印如下
    *** CURRENT SOURCES ***
    https://gems.ruby-china.org/
  ```
* 3.`安装Sass`
  * `gem install sass`
  * `gem install compass`
* 4.`Sass 设置`
  * `sass -v  查看Sass 版本`
  * `gem update sass 更新Sass版本`
#####  <a id="CodingFileSass" href="#CodingFileSass">编译文件</a>  :star2: <a href="#top"> :arrow_up: </a>
`一旦你开始修改Sass，它将采用你的预处理Sass文件并将其保存为您可以在您的网站中使用的普通CSS文件。`
* `实现这一目标的最直接方法是在您的终端。安装Sass后，您可以使用该sass命令将Sass编译为CSS 。您需要告诉Sass要构建哪个文件，以及将CSS输出到何处。例如，sass input.scss output.css从终端运行将获取单个Sass文件input.scss，并将该文件编译为output.css。`

* `您还可以使用该--watch标志查看单个文件或目录。watch标志告诉Sass要查看源文件的更改，并在每次保存Sass时重新编译CSS。如果您想观看（而不是手动构建）您的input.scss文件，您只需将watch标志添加到您的命令中，如下所示：` `sass --watch input.scss output.css`

* `您可以使用文件夹路径作为输入和输出来观察和输出到目录，并使用冒号分隔它们。在这个例子中：` `sass --watch app/sass:public/stylesheets` `Sass会查看文件app/sass夹中的所有文件以进行更改，并将CSS编译到该public/stylesheets文件夹。`

`通过命令行编译`
```C#
 //单文件转换命令
 sass input.scss output.css

 //单文件监听命令
 sass --watch input.scss:output.css

 //如果你有很多的sass文件的目录，你也可以告诉sass监听整个目录：
 sass --watch app/sass:public/stylesheets
 
 //编译格式
 sass --watch input.scss:output.css --style compact

 //编译添加调试map
 sass --watch input.scss:output.css --sourcemap

 //选择编译格式并添加调试map
 sass --watch input.scss:output.css --style expanded --sourcemap

 //开启debug信息
 sass --watch input.scss:output.css --debug-info
```
**`编译格式`**
```C#
  //未编译样式
 .box {
   width: 300px;
   height: 400px;
   &-title {
     height: 30px;
     line-height: 30px;
   }
 }
```
**`nested 编译排版格式`**
```css
 /*命令行内容*/
 sass style.scss:style.css --style nested

 /*编译过后样式*/
 .box {
   width: 300px;
   height: 400px; }
   .box-title {
     height: 30px;
     line-height: 30px; }
```
**`compressed 编译排版格式`**
```css
 /*命令行内容*/
 sass style.scss:style.css --style compressed

 /*编译过后样式*/
 .box{width:300px;height:400px}.box-title{height:30px;line-height:30px}
```
**`可以使用Koala 编译 单开具有scss类型的文件 点击编译就可以了`** <br/>
* `这里推荐koala&codekit,它们是优秀的编译器，界面清晰简洁，操作起来也非常简单`
* [`koala 下载`](https://www.sass.hk/skill/koala-app.html)
#####  <a id="vscodeUseSass" href="#vscodeUseSass">使用vscode 实现自动编译 / 自由开发</a>  :star2: <a href="#top"> :arrow_up: </a>
`sass 编译 使用vscode 安装一个插件那么在编辑 sass之后 ` `ctrl+s ` `保存的时候就自定吧scss 文件编译为 .css .min.css css.map 三种文件类型`
* `插件列表`：
  * `EasySass`:`自动编译Sass  但是需要先配置好安装环境 就是前面讲的ruby sass 等等环境...`
  * `Sass`：`vscode Sass语法支持`
  * `Sass Formatter`:`支持对Sass 代码的格式化`
`安装好这些插件后,打开一个文件夹,添加一个scss 文件 然后写上代码 点击保存,就自动编译了`
```scss
  $color_red:"red";
  $width: 500px;

  .nav-bar{
      width: $width
  }

  .font-color{
      color:$color_red;
  }
```

