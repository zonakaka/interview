# interview
# 一、Vue
## 1. React-router/Vue-Router  实现原理
   * 路由
简单来说路由就是用来跟后端服务器进行交互的一种方式，通过不同的路径，来请求不同的资源，请求不同的页面是路由的其中一种功能。
   * 实现原理
是基于html5 特性 history.pushState实现的
history.pushState & history.replaceState 都是添加或修改历史记录条目，
在不刷新页面的情况下

  * 使用方法
  ```
  let stateObj = {
      foo: "bar",
  };
  history.pushState(stateObj, "page 2", "bar.html");

  ```
  在前端使用路由要有个前提，那就是后端要将全部的路径都指向首页，即 index.html。否则后端会出现 404 错误。
***
## 2. nextTick
   * 定义（引用[官网](https://cn.vuejs.org/v2/api/#Vue-nextTick)
> 原文：当你设置 vm.someData = 'new value'，该组件不会立即重新渲染。当刷新队列时，组件会在下一个事件循环“tick”中更新。
个人理解：dom更新是异步的，nextTick为该次事件循环后的回调钩子，确保了dom更新完毕，可以在nextTick中对更新后的dom进行操作
```
vm.someData = 'new value'
//someData 未更新
Vue.nextTick(function(){
    //someData更新了
})
```
（ps: $nextTick 返回一个Promise对象）
   * 异步更新队列

数据变化时，Vue开启一个队列，缓存同一循环事件中所有的dom更新，即同一watcher更新多次时，有且仅有一个入队列，避免了不必要的计算和dom更新
   * 源码
```
/**
 * Defer a task to execute it asynchronously.
 */
export const nextTick = (function () {
  const callbacks = []
  let pending = false
  let timerFunc

  function nextTickHandler () {
    pending = false
    const copies = callbacks.slice(0)
    callbacks.length = 0
    for (let i = 0; i < copies.length; i++) {
      copies[i]()
    }
  }

  // the nextTick behavior leverages the microtask queue, which can be accessed
  // via either native Promise.then or MutationObserver.
  // MutationObserver has wider support, however it is seriously bugged in
  // UIWebView in iOS >= 9.3.3 when triggered in touch event handlers. It
  // completely stops working after triggering a few times... so, if native
  // Promise is available, we will use it:
  /* istanbul ignore if */
  if (typeof Promise !== 'undefined' && isNative(Promise)) {
    var p = Promise.resolve()
    var logError = err => { console.error(err) }
    timerFunc = () => {
      p.then(nextTickHandler).catch(logError)
      // in problematic UIWebViews, Promise.then doesn't completely break, but
      // it can get stuck in a weird state where callbacks are pushed into the
      // microtask queue but the queue isn't being flushed, until the browser
      // needs to do some other work, e.g. handle a timer. Therefore we can
      // "force" the microtask queue to be flushed by adding an empty timer.
      if (isIOS) setTimeout(noop)
    }
  } else if (!isIE && typeof MutationObserver !== 'undefined' && (
    isNative(MutationObserver) ||
    // PhantomJS and iOS 7.x
    MutationObserver.toString() === '[object MutationObserverConstructor]'
  )) {
    // use MutationObserver where native Promise is not available,
    // e.g. PhantomJS, iOS7, Android 4.4
    var counter = 1
    var observer = new MutationObserver(nextTickHandler)
    var textNode = document.createTextNode(String(counter))
    observer.observe(textNode, {
      characterData: true
    })
    timerFunc = () => {
      counter = (counter + 1) % 2
      textNode.data = String(counter)
    }
  } else {
    // fallback to setTimeout
    /* istanbul ignore next */
    timerFunc = () => {
      setTimeout(nextTickHandler, 0)
    }
  }

  return function queueNextTick (cb?: Function, ctx?: Object) {
    let _resolve
    callbacks.push(() => {
      if (cb) {
        try {
          cb.call(ctx)
        } catch (e) {
          handleError(e, ctx, 'nextTick')
        }
      } else if (_resolve) {
        _resolve(ctx)
      }
    })
    if (!pending) {
      pending = true
      timerFunc()
    }
    if (!cb && typeof Promise !== 'undefined') {
      return new Promise((resolve, reject) => {
        _resolve = resolve
      })
    }
  }
})()
```
   * callbacks 存放 nextTick 回调函数

   * nextTickHandler 用于挨个触发callbacks里的每个回调

   * timerFunc 根据浏览器支持情况（Promise/MutationObserver/setTimeout）将nextTickHandler封装延时函数（会在同步任务以及更新DOM的异步任务之后回调具体函数。）

   * queueNextTick 作为钩子函数对外暴露，接受callback、context(上下文执行环境)，如若不传入任何参数，则返回一个新的Promise对象

***
## 3 compute 和 watch 
> 这篇写的很详细 [Vue的computed和watch的细节全面分析](https://segmentfault.com/a/1190000012948175?utm_source=tag-newest)
***
# TODO computed 和 watch 源码理解
