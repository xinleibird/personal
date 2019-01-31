
# JavaScript 的异步机制

## 1.1 单线程模型

单线程模型, 指的是 JavaScript 脚本只在一个线程上运行.

> 值得注意的是, JavaScript 引擎进程并非只有一个线程在运行. 事实上, 引擎中有多个线程同时运行, 其中 JavaScript 脚本只在主线程运行, 其他线程在后台配合.

## 1.2 同步任务和异步任务

可以简单看做同步任务 (synchronous) 即传统的自顶向下排队执行的模式, 而异步任务 (asynchronous) 则不进入主线程.

## 1.3 任务队列和事件循环

异步任务不放入主线程, 引擎将其放入事件队列 Task Queue (可以看做是另一个或者多个线程). 当引擎认为异步任务可以执行了, 则将其放入主线程执行. 异步任务明显是非阻塞的, 同步的代码不会等待其执行而是会直接运行后面的同步代码. 而当异步任务可执行时, 会将其移出任务队列, 放入主线程中依次执行. (注意, 队列中如果有多个异步任务, 事实上它们会同时被监听而不存在顺序问题. 谁先被翻牌子谁先滚蛋)

当主线程中的任务执行完毕, 引擎会查看任务队列中是否有任务, 如果有, 则会不停循环的检查任务队列是否可执行了. 一旦有任务可执行, 则将其移入主线程执行, 直至任务队列清空, 退出程序. 这种轮询检查的机制, 就叫做事件循环 (Even Loop).

# 2 异步操作模式

## 2.1 回调函数

明确的讲, 回调函数和异步没有直接关联. 有关联的是异步回调函数

## 2.2 事件监听

引擎中的各种 on 事件, 就是事件监听的代表

## 2.3 发布订阅 / 观察者模式

```javascript
const observe = {
  subs: new Set(),
  subscribe(sub) {
    this.subs.add(sub);
  },
  unsubscribe(sub) {
    this.subs.delete(sub);
  },
  publish(event) {
    this.subs.forEach((sub) => {
      const s = sub;
      s.event = event;
      new Promise((resolve, reject) => {
        // ...
        // 各种获取数据
        s.data = 'something data';
        if (true) {
          resolve(s.data);
        } else {
          reject();
        }
      }).then((data) => {
        console.log(event, data);
      });
    });
  },
};

// 订阅者类
class Subject {
  constructor() {
    // 向观察者注册自身
    observe.subscribe(this);
    this.event = '';
    this.data = '';

    // 向观察者取消自身订阅
    this.unsubscribe = function unsubscribe() {
      observe.unsubscribe(this);
      this.event = '';
    };
  }
}

const s1 = new Subject();
const s2 = new Subject();

observe.publish('something event and');

console.log(s1, s2);
```

# 3 异步操作的流程控制

## 3.1 串行执行

用某种方式控制其进入事件队列的时机, 从而能够依次执行而不是并行执行

```javascript
const asyn = new Promise((resolve) => {
  console.log('a');
  resolve(this);
});

asyn
  .then(console.log('b'))
  .then(console.log('c'))
  .then(console.log('d'));
```

## 3.2 并行执行

只要进入事件队列, 其中的事件都是并行执行的. 这种方式高效, 但是并行规模过大时会提高 cpu 占用率

```javascript
function asyn(callback) {
  setTimeout(callback, 1000);
  return asyn;
}

function a() {
  console.log('a');
}

function b() {
  console.log('a');
}

function c() {
  console.log('a');
}

asyn(a)(b)(c);
```

## 3.3 并行与串行结合

用某种方式控制并行的规模, 降低 cpu 占用

```javascript
const asyn = new Promise((resolve) => {
  console.log('a');
  resolve(this);
});

asyn
  .then(console.log('b'))
  .then(console.log('b'))
  .then(console.log('b'));

asyn
  .then(console.log('c'))
  .then(console.log('c'))
  .then(console.log('c'));
```

# 4 定时器

## 4.1 定时器方法

1. setTimeout()
2. setInterval()
3. clearTimeout()
4. clearInterval()

## 4.2 运行机制

setTimeout 和 setInterval 方法是将当前代码移出主线程加入任务队列, 并且踢出本轮的事件循环. 在设定的时间结束后等待回调. 如果主线程内相应的代码 (同步) 未运行结束, 则继续等待其结束再进行.

> setTimeout(something, 0), 意味着移出主线程, 本轮事件循环不参与, 等待主线程任务完成, 可以用来调整代码的执行顺序.

# 5 Promise 对象

```javascript
new Promise(step1)
  .then(step2)
  .then(step3)
  .then(step4);
```

## 5.1 Promise 对象的状态

1. pending
2. fulfiled
3. rejected

## 5.2 Promise 构造函数

```javascript
const promise = new Promise(resolve, reject) {
  if(/* 异步操作成功 */) {
    resolve(value); // value 就是成功后获取到数据
  } else {
    reject(new Error())
  }
}
```
