# 1. 单线程模型

单线程模型, 指的是 JavaScript 脚本只在一个线程上运行.

> 值得注意的是, JavaScript 引擎进程并非只有一个线程在运行. 事实上, 引擎中有多个线程同时运行, 其中 JavaScript 脚本只在主线程运行, 其他线程在后台配合.

# 2. 同步任务和异步任务

可以简单看做同步任务 (synchronous) 即传统的自顶向下排队执行的模式, 而异步任务 (asynchronous) 则不进入主线程.

# 3. 任务队列和事件循环

异步任务不放入主线程, 引擎将其放入事件队列 Task Queue (可以看做是另一个或者多个线程). 当引擎认为异步任务可以执行了, 则将其放入主线程执行. 异步任务明显是非阻塞的, 同步的代码不会等待其执行而是会直接运行后面的同步代码. 而当异步任务可执行时, 会将其移出任务队列, 放入主线程中依次执行. (注意, 队列中如果有多个异步任务, 事实上它们会同时被监听而不存在顺序问题. 谁先被翻牌子谁先滚蛋)

当主线程中的任务执行完毕, 引擎会查看任务队列中是否有任务, 如果有, 则会不停循环的检查任务队列是否可执行了. 一旦有任务可执行, 则将其移入主线程执行, 直至任务队列清空, 退出程序. 这种轮询检查的机制, 就叫做事件循环 (Even Loop).

# 4. 异步操作模式

1. 回调函数

回调函数式异步操作的基本方法

```javascript
function fn(callback) {
  callback();
  // ...
}

fn(() => console.log(2));
```

2. 事件监听

基本上浏览器中的所有 onXX 操作都是事件监听操作, 当该属性指向自定义的函数后, 当该属性所代表的事件发生后, 引擎会调用指向的函数.

```javascript
window.onload = () => console.log('hello');
```

3. 发布订阅 (观察者模式)

```javascript
// 观察者
const observe = {
  subs: new Set(),
  subscribe(sub) {
    this.subs.add(sub);
  },
  unsubscribe(sub) {
    this.subs.delete(sub);
  },
  publish(even) {
    this.subs.forEach((sub) => {
      const s = sub;
      s.even = even;
    });
  },
};

// 订阅者类
class Subject {
  constructor() {
    // 向观察者注册自身
    observe.subscribe(this);
    this.even = null;
    
    // 向观察者取消自身订阅
    this.unsubscribe = function unsubscribe() {
      observe.unsubscribe(this);
      this.even = () => {};
    };
  }
}

const s1 = new Subject();
const s2 = new Subject();
const s3 = new Subject();
const s4 = new Subject();

observe.publish(() => console.log('hello'));
console.log(observe);

s1.even(); // hello
s2.even(); // hello
s3.even(); // hello
s4.even(); // hello

s1.unsubscribe();
s2.unsubscribe();
s3.unsubscribe();
s4.unsubscribe();

s1.even(); // 空
s2.even(); // 空
s3.even(); // 空
s4.even(); // 空
```

# 异步操作的流程控制

1. 串行执行  
   用某种方式控制其进入事件队列的时机, 从而能够依次执行而不是并行执行
2. 并行执行  
   只要进入事件队列, 其中的事件都是并行执行的. 这种方式高效, 但是并行规模过大时会提高 cpu 占用率
3. 并行与串行结合  
   用某种方式控制并行的规模, 降低 cpu 占用
