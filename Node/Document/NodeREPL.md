<a href="#" id="node" >Node REPL交互运行环境 :maple_leaf:</a>
-----
`一个JS代码立即运行时结果`

##### [理解REPL](#)
* `(Read-Eval-Print-Loop) 可交互运行环境 为了方便开发者测试JS代码,提供了一个名为REPL的环境 ,开发者可以在该运行环境中输入任何JS表达式,当用户按下
回车键的时候,REPL运行环境将显示表达式运行结果`
* `如何理解REPL呢? 让我们打开浏览器！ F12 看到里面的Console 没有 对功能就和那个一样,只是区别在与,打开使用Console 需要打开浏览器 按F12,而REPL 需要的是
在命令行输入`

`打开浏览器,输入node 然后敲代码吧`
```javascript
D:\Users\Kick\WebstormProjects\node-wordspace>node
> console.log("kicker");
kicker
undefined
> var user = new object();
ReferenceError: object is not defined
> var user = new Object();
undefined
> var a = 6 + 9
undefined
> console.log(a)

```
##### [REPL 使用下划线 _](#)
`下划线用来访问最近一次的表达式`
```javascript
> a = 3
3
> _ + 5
8
> user = {}
{}
> _.name = "kicker"
'kicker'
> _.age = 17
17
> _.sex = true
true
> console.log(user)
{ name: 'kicker' }
undefined
>
```
