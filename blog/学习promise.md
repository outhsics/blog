## 学习Promise

### 理解 Promise
Promise 简介: 

一个 Promise 有3个状态。他们分别是：

1. Promise 是待定的（pending）： 不确定当前任务是否满足条件
2. Promise 是已解决的（resolved）：当前任务满足条件
3. Promise 是被拒绝的（rejected）: 当前任务不满足条件

### 创建一个 Promise

``` javascript
/* ES5 */ var Result = false; 
// Promise
var isFulfil = new Promise(
    function (resolve, reject) {
        if (fulfil) {
            var value = 1;  (result用value表示)
            resolve(value); // 完成了
        } else {
            var reason = new Error('不满足条件');（result用reason表示）
            reject(reason); // reject
        }

    }
);
```

1. 我们用一个布尔值`isfulfil`，来定义条件是否满足。

2. 我们有一个命名为`isfulfil`的Promise。这个 Promise 可以是 已完成的（resolved）（满足条件）或者 被拒绝的（rejected） （没有满足条件）。

3. 这里有一个标准的语法来新建一个 Promise，参考[MDN 文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)，一个 promise 语法看上去像这样。

支持的快捷键有：
``` javascript
// promise 语法看上去像这样
new Promise(/* executor*/ function (resolve, reject) { ... } );
```
1. 当条件满足， promise调用 resolve 函数和  结果变量value。如果不满足用 reject 函数和一个理由（reason）reject(reason)；

## 使用 Promise

现在，我们有一个 Promise。来看看怎么使用它：

``` javascript
/* ES5 */
...
// 调用我们的 Promise
var p = function () {
   isFulfil
        .then(function (fulfilled) {
            // 满足条件
            console.log(fulfilled);
         // output: value
        })
        .catch(function (error) {
            // 不满足条件
            console.log(error.message);
         // output: 'reson'
        });
};
p();
```

1. 我们有一个名为p的函数。在这个函数中，我们会使用 Promise isFulfil。
2. 一旦 Promise 被解决（resolved）或者被拒（rejected），我门希望采取些措施。我们用 `.then` 和 `.catch` 来实现。
3. 在我们的例子中，`.then` 之中有个 `function(fulfilled) { ... }` 。`fulfilled` 是什么？`fulfilled` 就是是你传入 Promise 的 `resolve(your_success_value)`.因此，在我们例子中就是 `value`。
4. 我们在 `.catch` 中有 `function(error){ ... }`。error 是什么？正如你猜测的，`error` 正是你传入 Promise 中的 `reject(your_fail_value)`。因此，在我们的例子中就是 `reason`。

让我们看看例子运行之后的结果吧！

Demo: https://jsfiddle.net/8qyfhyLt/7/

![](https://user-gold-cdn.xitu.io/2018/3/19/1623e5b603a9973f?w=1554&h=1420&f=png&s=228449)


## 串联 Promise

Promiss 是可串联的。

也就是说，一个条件满足了可以判断下一个条件是否满足

这就是另一个 Promise 啦。我们来写一个！

说明:

* 在这个例子中，你可能意识到我们没有调用 reject。因为这个是可选的参数。

* 我们可以简化这个样例就像用 Promise.resolve 代替。

``` javascript

    // 简略
    ...

    // 第二个 promise
    var second = function (value) {
        var message = 'second new value';
        return Promise.resolve(message);
    };

```

 让我们串联 Promise。你，宝宝只能在isFulfil Promise 实现之后，才能开始 second Promise。

``` javascript

    ...
    // 调用 Promise
    var p = function () {
        isFulfil
        .then(second) // 在这里串联
        .then(function (fulfilled) {
                console.log(fulfilled);
            // output: 'second new value'
            })
            .catch(function (error) {
                // 不满足条件
                console.log(error.message);
            // output: '不满足条件'
            });
    };

```

## Promises 是异步的

 Promise 是异步的。让我们在调用 Promise 之前和之后各打印一个信息。

```javascript

    // 调用我们的Ppromise
    var p = function () {
        console.log('判断条件之前'); // 运行之前打印
        isFulfil
            .then(second)
            .then(function (fulfilled) {
                console.log(fulfilled);
            })
            .catch(function (error) {
                console.log(error.message);
            });
        console.log('判断条件之后'); // 运行之后打印
    }

```

输出顺序是这样的：

```
    1. 判断条件之前
    2. 判断条件之后
    3. second new value
```

#### 因为JavaScript不等判断条件。

 第一次条件判断的时候等待着p的承诺（promise 这个我们称之为 异步（asynchronous）, 代码不会因为阻塞或等待结果而不运行. 任何想等待 Promise 之后再运行的, 你需要把他们放入 .then

