---
title: JavaScript异步编程
cover: ../../cover/异(步)客.png

date: 2025-09-13T20:12:52+08:00
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

JavaScript是一门单线程的语言，这意味着同一时刻只能执行一个任务。JavaScript的异步编程模型是基于事件循环的，可以使得我们可以在主线程执行同步代码的同时，处理耗时的异步操作。

# 实现

## 回调函数
可以使用setTimeout(fn, 0) 会把 fn 推入异步任务队列，继续执行后面的函数。
```javascript
    function f1() {
        // 同步阻塞：这个循环会卡住浏览器1秒以上
        let sum = 0;
        for (let i = 0; i < 1000000000; i++) {
            sum += i;
        }
        console.log("f1 完成");
    }

    function f2() {
        console.log("f2 执行了"); // 很快完成
    }
```
本例子中f1是一个耗时及长的函数，会卡住浏览器，因而需要异步操作。
```javascript
    function f1(callback) {
    // 使用 setTimeout 把 f1 的任务推迟到异步队列
        setTimeout(() => {
            let sum = 0;
            for (let i = 0; i < 1000000000; i++) {
                sum += i;
            }
            console.log("f1 完成");
            callback(); // 异步任务完成后通知
        }, 0);
    }

    function f2() {
        console.log("f2 执行了");
    }

    // 调用
    f1(() => {
        console.log("f1 的回调");
    });

    f2();
```
会先输出f2，然后输出f1，最后输出f1的回调。

这里将f1函数体内的任务放到了setTimeout中，并传入一个回调函数，在f1执行完毕后，调用这个回调函数来告知异步操作完成。

## Promise
Promise 在ES6版本引入，是异步编程的一种解决方案，它将回调函数的嵌套问题简化成链式调用。

```javascript
    const myPromise = new Promise((resolve, reject) => {  //只考虑成功则可以只写一个参数 
        // 异步操作写在这里
        // 成功时调用 resolve(数据)
        // 失败时调用 reject(错误)
    });
```
当成功时调用 resolve(数据)，失败时调用 reject(错误)。

resolve函数会在命令行输出参数并会转为完成状态，reject函数会在命令行输出参数并会转为失败状态。

完成状态会触发then方法，失败状态会触发catch方法,finally()方法无论 Promise 最终状态如何都会执行。

```javascript
    const myPromise = new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve("成功");
        }, 1000);
        });

    myPromise.then(data => {
        console.log(data); // 成功 
    }).catch(error => {
        console.log(error); // 失败
    }).finally(() => {
        console.log("Promise 完成");
    });
```
promise的优点可以在后面跟一串then方法，将多个异步操作串联起来，可以实现更复杂的异步操作。

```javascript
    const myPromise = new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve("成功");    
        }, 1000);
    });

    myPromise.then(data => {
        console.log(data); // 成功
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                resolve("成功2");
            }, 1000);
        });
    }).then(data => {
        console.log(data); // 成功2
    }).catch(error => {
        console.log(error); // 失败
    }).finally(() => {
        console.log("Promise 完成");
    });
```

### 常见的Promise方法：

1. Promise.all()：用于将多个 Promise 实例包装成一个新的 Promise 实例。只有当所有 Promise 实例都成功时，才会成功，否则失败。
```javascript
    const p1 = Promise.resolve("A");
    const p2 = fetch('/api/user'); // 网络请求
    const p3 = new Promise(r => setTimeout(() => r("C"), 100));

    Promise.all([p1, p2, p3])
        .then(results => {
            console.log(results); // ["A", response, "C"]
        })
        .catch(err => {
            console.error("有一个失败了", err);
        });
```
2. Promise.race()：用于将多个 Promise 实例包装成一个新的 Promise 实例。只要有一个 Promise 实例完成，就成功，并触发成功者的result。
```JavaScript
    const p1 = new Promise(r => setTimeout(() => r("快"), 500));
    const p2 = new Promise(r => setTimeout(() => r("慢"), 1000));

    Promise.race([p1, p2])
        .then(result => {
            console.log(result); // "快"
        });
```
3. Promise.allSettled()：用于将多个 Promise 实例包装成一个新的 Promise 实例。无论 Promise 实例是成功还是失败，都会触发成功者的result。
```javascript
    Promise.allSettled([p1, p2, p3])
    .then(results => {
        results.forEach((result, index) => {
            if (result.status === 'fulfilled') {
                console.log(`任务${index}成功：`, result.value);
            } else {
                console.log(`任务${index}失败：`, result.reason);
            }
        });
    });
```
4. Promise.resolve(value) 和 Promise.reject(error) 创建成功、失败的 Promise 实例。

# async/await

async/await 是 ES8 引入的异步编程语法，它是 Promise 的语法糖。

传统Promise的写法：
```javascript
function getData() {
    return new Promise(r => setTimeout(() => r("数据"), 1000));
}

function getMore(data) {
    return new Promise(r => setTimeout(() => r(data + " + 更多"), 500));
}

getData()
    .then(data => getMore(data))
    .then(final => console.log(final));
```

async/await的写法：
```JavaScript
    async function fetchData() {
        try {
            const data = await getData();
            const final = await getMore(data);
            console.log(final);
        } catch (error) {
            console.error("出错了：", error.message);
        }
    }

    fetchData()
```

# 参考资料
- [JavaScript Promise](https://www.runoob.com/js/js-promise.html) 
- [Javascript异步编程的4种方法](https://www.cnblogs.com/ToTigerMountain/articles/18846477)
- [详解JS的四种异步解决方案：回调函数、Promise、Generator、async/await（干货满满）](https://blog.csdn.net/lunahaijiao/article/details/124185543)


