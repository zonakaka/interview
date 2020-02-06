# interview
1. React-router  实现原理
是基于html5 特性 history.pushState实现的
history.pushState & history.replaceState 都是添加或修改历史记录条目，
在不刷新页面的情况下

使用方法
```
let stateObj = {
    foo: "bar",
};
history.pushState(stateObj, "page 2", "bar.html");

```
