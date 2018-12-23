### [JavaScript 函数](#top) :grey_exclamation: <b id="top"></b>
:white_check_mark: `Javascript 函数有很多的其他深层次的东西`

- [x] [`1.递归`](#proto) 

----
#####  :octocat: [1.递归](#top) <b id="proto"></b> 
`函数名的本质是什么啊？ 引用 存储着一个执行函数本身的引用地址,既然是引用那么就可以传递,一个函数名可以只要改变引用就可以代表不同的函数,那么如何递归呢？`
* `使用函数名完成递归的潜在威胁`
```node
function test(num){
    if(num <= 1){
        return 1;
    }else{
        return num * test(num-1);
    }
}

let run = test; //吧递归函数的引用传递一下

//修改text的引用
test = function(){
    return 0;
}

console.log(run(10));//跑递归
// 0
```
* `arguments.callee 执行函数本身的指针,严格模式下不允许使用 可以通过它来保证 但是在js严格模式下 不允许使用这个指针`
```node
function factorial(end){
    if(end <= 1){
        return 1;
    }else{
        return end * arguments.callee(end - 1);
    }
}

let run_f = factorial;

factorial = function () {
    return 0;
}

console.log(run_f(10));//跑递归
// 3628800
```
##### `ES6 语法保证递归的正确性`
* `上诉两种方法都有缺陷,第一种递归有函数引用改变的威胁,第二种有严格模式不支持的危险 那么使用第三种吧`
* `通过const 直接不允许改变改变引用 就可以了并且严格模式也支持`
```node
 const test = function(num){
    if(num <= 1){
        return 1;
    }else{
        return num * test(num-1);
    }
}

console.log(test(10));//跑递归
//3628800

```
