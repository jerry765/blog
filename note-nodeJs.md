---
title: Node.js 笔记
tags:
  - javascript
  - node.js
categories: note
date: 2023-08-26 11:01:52
---

## Timer

### Zero Delay

如果指定超时延迟为 0 ，回调函数将尽快执行，但在当前函数执行之后：
``` js
setTimeout(() => {
  console.log('after ');
}, 0);

console.log(' before ');
```
<!-- more -->
该代码将打印

``` bash
before
after
```

这对于避免在密集型任务上阻塞 CPU 并通过在调度程序中对函数进行排队来让其他函数在执行繁重计算时执行特别有用。

### Recursive setTimeout

`setInterval` 每 n 毫秒启动一个函数，而不考虑函数何时完成执行。如果一个函数总是花费相同的时间，那就没问题；但也许一个长执行会与下一个执行重叠：

![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308261059739.png)

为了避免这种情况，您可以安排在回调函数完成时调用递归 setTimeout：

``` js
const myFunction = () => {
  // do something

  setTimeout(myFunction, 1000);
};

setTimeout(myFunction, 1000);
```

为了实现这个场景：

![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308261100968.png)

Node.js 还提供了 `setImmediate()` ，相当于使用 `setTimeout(() => {}`, 0) ，主要用于与 Node.js 事件循环配合使用。

### setImmediate()

`setImmediate()` 与 `setTimeout(() => {}, 0)` （传递 0 毫秒超时）以及 `process.nextTick() `和 `Promise.then()` 有何不同？

当前操作结束后，传递给 `process.nextTick()` 的函数将在事件循环的当前迭代中执行。这意味着它将始终在 `setTimeout` 和 `setImmediate` 之前执行。

延迟 0 毫秒的 `setTimeout()` 回调与 `setImmediate()` 非常相似。执行顺序将取决于各种因素，但它们都将在事件循环的下一次迭代中运行。

`process.nextTick` 回调被添加到 `process.nextTick queue` 。 `Promise.then()` 回调被添加到 `promises microtask queue` 。 setTimeout 回调被添加到 `macrotask queue` 。

事件循环首先执行 `process.nextTick queue` 中的任务，然后执行 `promises microtask queue` ，然后执行 `macrotask queue` 。

下面是一个显示 `setImmediate()` 、 `process.nextTick()` 和 `Promise.then()` 之间顺序的示例：

``` js
const baz = () => console.log('baz');
const foo = () => console.log('foo');
const zoo = () => console.log('zoo');
const start = () => {
  console.log('start');
  setImmediate(baz);  // 3
  new Promise((resolve, reject) => {
    resolve('bar');
  }).then((resolve) => {
    console.log(resolve);
    process.nextTick(zoo);  // 2
  });
  process.nextTick(foo);  // 1
};
start();

// start foo bar zoo baz

```

此代码将首先调用 `start()` ，然后调用 `process.nextTick queue` 中的 `foo()` 。之后，它将处理 `promises microtask queue` ，打印 `bar` 并同时在 `process.nextTick queue` 中添加 `zoo()` 。然后就会调用刚刚添加的 `zoo()` 。最终调用了 `macrotask queue` 中的 `baz()` 。

## 参考

> 更应该说是摘抄自

[探索 JavaScript 定时器](https://nodejs.dev/en/learn/discover-javascript-timers/)