---
title: 前端面试-javascript
date: 2024-04-18 14:22:17
tags: 前端面试
categories: 技术相关
---

#### 使用 promise 实现请求的并发控制

并发控制

#### js 中的事件循环、微任务和宏任务

JS 分为同步任务和异步任务
，同步任务都在主线程上执行，形成一个执行栈
，主线程之外，事件触发线程管理着一个任务队列，只要异步任务有了运行结果，就在任务队列之中放置一个事件。
一旦执行栈中的所有同步任务执行完毕（此时 JS 引擎空闲），系统就会读取任务队列，将可运行的异步任务添加到可执行栈中，开始执行，如此往复循环就是事件循环。任务队列又包括宏任务和微任务，如下

宏任务：

- script(整体代码)
- setTimeout
- setInterval
- I/O
- UI 交互事件
- postMessage
- MessageChannel //管道通信
- setImmediate(Node.js 环境)
- requestAnimationFrame

  微任务：

- Promise.then
- Object.observe //监听 js 对象发生改变
- MutationObserver //监听 dom 发生改变
- process.nextTick(Node.js 环境)

一般来说宿主（浏览器）发起的异步任务为宏任务，js 引擎自身发起的为微任务

运行机制：

- 执行一个宏任务（栈中没有就从事件队列中获取）
- 执行过程中如果遇到微任务，就将它添加到微任务的任务队列中
- 宏任务执行完毕后，立即执行当前微任务队列中的所有微任务（依次执行）
- 当前宏任务执行完毕，开始检查渲染，然后 GUI 线程接管渲染
- 渲染完毕后，JS 线程继续接管，开始下一个宏任务（从事件队列中获取）

#### 普通函数和箭头函数

写法不同
箭头函数是匿名函数，不能作为构造函数，不能使用 new
箭头函数不绑定 arguments，取而代之用 rest 参数...解决
箭头函数不绑定 this，会捕获其所在的上下文的 this 值，作为自己的 this 值
箭头函数不能当做 Generator 函数,不能使用 yield 关键字
箭头函数没有原型属性

#### ES6 ES5 实现继承的方式

js 继承的方式

#### 防抖和节流

防抖和节流

#### 如何判断 this 的指向

① 在全局环境中调用就指向 window。② 作为对象的方法调用就指向该对象。③ 作为构造函数调用就指向这个新创建的对象。④ 可以使用 apply,call,bind 改变 this 指向。⑤ 箭头函数中的 this 与定义时所处的上下文绑定，且不能被改变

#### Symbol ,Set,weakSet,Map,weakMap 的使用场景

Symbol:

作为对象的属性名，不可遍历，可以用 Object.getOwnPropertySymbols()访问，私有属性

Set:

数组去重

WeakSet 没有 size 属性，没有办法遍历它的成员。垃圾回收机制根据对象的可达性（reachability）来判断回收，如果对象还能被访问到，垃圾回收机制就不会释放这块内存。结束使用该值之后，有时会忘记取消引用，导致内存无法释放，进而可能会引发内存泄漏。WeakSet 里面的引用，都不计入垃圾回收机制，所以就不存在这个问题。因此，WeakSet 适合临时存放一组对象，以及存放跟对象绑定的信息。只要这些对象在外部消失，它在 WeakSet 里面的引用就会自动消失。

Map:

Map 是一个纯哈希结构，而 Object 不是(它拥有自己的内部逻辑)。Map 在频繁增删键值对的场景下表现更好，性能更高。因此当你需要频繁操作数据的时候也可以优先考虑 Map

weakMap

首先，WeakMap 只接受对象作为键名（null 除外），不接受其他类型的值作为键名。其次，WeakMap 的键名所指向的对象，不计入垃圾回收机制。
总之，WeakMap 的专用场合就是，它的键所对应的对象，可能会在将来消失。WeakMap 结构有助于防止内存泄漏。
WeakSet 和 WeakMap 是基于弱引用的数据结构，ES2021 更进一步，提供了 WeakRef 对象，用于直接创建对象的弱引用。

#### 什么是闭包，使用场景是什么

闭包-阮一峰 ，可以封装私有变量，只暴露一些接口来修改内部的值

#### js 中的下文和作用域

上下文和作用域

#### js 模块化方案有哪些

javascript 模块 化，umd

#### 原型和原型链

Object.setPrototypeOf()，为现有对象设置原型，返回一个新对象
Object.getPrototypeOf() 是 ES5 中用来获取 obj 对象的原型对象的标准方法。
Object.hasOwnProperty()表示是否有自己的属性。这个方法会查找一个对象是否有某个属性，但是不会去查找它的原型链。
Object.create(pro,obj) 创建一个挂载 obj 的属性的，并且原型对象为 pro 的新对象

#### for of 和 for in 的区别

for...in 是 ES5 的标准，该方法遍历的是对象的属性名称(key：键名)。一个 Array 对象也是一个对象，数组中的每个元素的索引被视为属性名称，所以在使用 for...in 遍历 Array 时，拿到的是每个元素索引
for...of 是 ES6 的标准，该方法遍历的是对象的属性所对应的值(value：键值)。所以它用来遍历数组时得到每个元素的值
