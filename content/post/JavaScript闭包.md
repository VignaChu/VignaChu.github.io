---
title: JavaScript闭包
cover: ./cover/closure.jpg

date: 2025-09-13T20:23:52+08:00
lastmod: 2025-09-13T20:12:50+08:00

tags:
  - JavaScript
  - 前端学习
  - Study
categories:
  - Study

math: true
mermaid: true

---

# 引言

通常函数内部作用域的变量外部是读取不了的，且在函数生命周期结束后会被销毁。但通过闭包可以访问函数内部的变量，从而对函数的生命周期进行延长，且能够更好的封装变量。

# 语法

**闭包**是一个函数内部的函数，能够访问该函数内部的变量，并作为该函数的返回值，在函数执行完毕后仍然存在，仍能读取父函数的变量。

闭包的原理是JS特有的作用域链机制:在当前执行环境下访问某个变量时，如果不存在就一直向外层寻找，最终寻找到最外层。

```javascript 
    function person(){
        var name = '有鱼';
        function cat(){
            console.log(name);
        }
        return cat;
    }
    var per = person();// per的值就是return后的结果，即cat函数
    per();// 有鱼 per()就相当于cat()
    per();// 同上，而且变量name没有销毁，一直存在内存中，供函数cat调用
    per();// 有鱼
```
另一种基于setTimeout的闭包：
```javascript
    function foo(a) {
        setTimeout(function timer(){
            console.log(a)
        }, 1000)
    }
    foo(2);
```
在1000ms后，foo的a仍没被销毁，timer函数仍保有对foo作用域的引用，所以可以读取到变量a的值。

# 利用闭包对变量进行封装

闭包的一个作用是对变量进行封装，使得函数的内部变量不被外界访问到，从而隐藏变量，实现更好的封装。

```javascript
    function person(){
        var age = 18;
        function old(){
            age++;
            console.log(age);
        }
        return old;
    }

    var per = person();//per相当于函数old
    per();// 19 即old() 
    // 这样每次调用不在经过age的初始值，这样就可以一直增加了。
    // 不然每次都得从person开始调用，会将age的值重置。
    per();// 20
    per();// 21

```

# 闭包作缓存

由于函数一旦被执行完毕，其内存就会被销毁，而闭包可以保持函数作用域，所以可以用闭包先保持函数状态，等合适的时候在调用。

```javascript
    function lazy_sum(arr) {
        let sum = function () {
            return arr.reduce(function (x, y) {
                return x + y;
            });
        }
        return sum;
    }
```
这里当调用return的函数时才会计算求和，实现了惰性求值。延迟到真正需要结果的时候才求值，能够实现性能优化。

同时需要注意，在循环与闭包同时存在时，如果要输出循环不同状态的值，需要再创建一个函数绑定函数的值。否则会输出最终的状态，原因和上面一样，闭包只是返回了函数，并没执行，所以会在全部返回之后调用的时候在执行，状态变量就会位于最后的状态。

```javascript
    function count() {
        let arr = [];
        for (var i=1; i<=3; i++) {
            arr.push(function () {
                return i * i;
            });
        }
        return arr;
    }

    let results = count();
    let [f1, f2, f3] = results;
```

这里输出的值均为16(因为i=4的时候退出循环)

通过再包一层函数进行修正。

```javascript
function count() {
    let arr = [];
    for (var i=1; i<=3; i++) {
        arr.push((function (n) {
            //这里用输入的n储存状态变量，闭包在保持这一状态变量。
            return function () {
                return n * n;
            }
        })(i));
    }
    return arr;
}

let [f1, f2, f3] = count();

f1(); // 1
f2(); // 4
f3(); // 9
```
# 注意

*由于闭包会保持原作用域内的变量不被销毁，导致变量不会被垃圾回收机制回收，造成内存消耗。不恰当的使用闭包可能会造成内存泄漏的问题。*

# 参考资料
- [封面图片来源](https://safebooru.org/index.php?page=post&s=view&id=5178673) 
- [JavaScript中闭包的概念、原理、作用及应用](https://zhuanlan.zhihu.com/p/106287246)
- [深入理解JavaScript闭包之什么是闭包](https://segmentfault.com/a/1190000023356598)
- [廖雪峰的官方网站|闭包](https://liaoxuefeng.com/books/javascript/function/closure/index.html)


