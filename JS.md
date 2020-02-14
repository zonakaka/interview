# JS
## [如何修复输出值中的 undefined ？(阿里)](https://github.com/nieyafei/front-end-interview-js/blob/master/docs/basic/js-1-13.md#%E5%A6%82%E4%BD%95%E4%BF%AE%E5%A4%8D%E8%BE%93%E5%87%BA%E5%80%BC%E4%B8%AD%E7%9A%84-undefined-%E9%98%BF%E9%87%8C)
```
function LateBloomer(){
    this.petalCount = Math.ceil(Math.random()*2 + 1);
}
LateBloomer.prototype.bloom = function(){
    window.setTimeout(this.declare, 1000);
}
LateBloomer.prototype.declare = function(){
    console.log('I am a beautiful flower with ' + this.petalCount + ' petals');
}
var flower = new LateBloomer();
flower.bloom();

```
> 结果： I am a beautiful flower with undefined petals
* 解析:
原因是window.setTimeout后this指向了window，为了矫正该this指向我们可以动态为this.declare绑定this
```
window.setTimeout(this.declare, 1000);改为
window.setTimeout(this.declare.bind(this), 1000);
```
***
## 严格模式 this指向 [from JavaScript 严格模式下this的几种指向](https://segmentfault.com/a/1190000010108912)
* 全局作用域下 this指向window
```
"use strict";
this === window   //true
this.document === document //true
this.a === window.a //true
```
* 全局作用域下的函数 this指向undefined
即禁止this指向全局对象
```
"use strict";
function f() {
    console.log(a)
}
f()
// Uncaught TypeError: Cannot read property 'a' of undefined
```
* 对象的函数 this指向该对象
```
"use strict";
var obj = {
    a: 1,
    f: function(){
        console.log(this.a)
    }
}
obj.f() // 1
```
* 构造函数的this 指向该构造函数的实例

* 事件处理函数的this 指向触发该事件的对象目标
* 内联事件处理函数中的this(以下为摘抄)
> 在严格模式下，在内联事件处理函数中，有以下两种情况：
 ```<button onclick="alert((function(){'use strict'; return this})());">
      内联事件处理1
    </button>
    <!-- 警告窗口中的字符为undefined -->
    
    <button onclick="'use strict'; alert(this.tagName.toLowerCase());">
      内联事件处理2
    </button>
    <!-- 警告窗口中的字符为button -->
 ```
 ***
 ## 任务队列事件循环机制
 > [JavaScript 运行机制详解：再谈Event Loop](http://www.ruanyifeng.com/blog/2014/10/event-loop.html)
 * 任务队列
 ```
（1）所有同步任务都在主线程上执行，形成一个执行栈（execution context stack）。

（2）主线程之外，还存在一个"任务队列"（task queue）。只要异步任务有了运行结果，就在"任务队列"之中放置一个事件。

（3）一旦"执行栈"中的所有同步任务执行完毕，系统就会读取"任务队列"，看看里面有哪些事件。那些对应的异步任务，于是结束等待状态，进入执行栈，开始执行。

（4）主线程不断重复上面的第三步。

 ```
 
 
 该过程是不断循环的，即该运行机制为事件循环机制

 
 
 
 ## 宏任务和微任务
 一般的宏任务有script脚本、setTimeout、setInterval，微任务有promise、async/await、process.nextTick
 ## promise实现
 ## async/await
    * async/await 和promise
 ## es6
 ## babel
 ## wepack
 ## react 
 ## redux
 ## vue 双绑定实现
 ## http
 ## 提高性能的方法
 ## 缓存
 ## 继承
 ## 原型及原型链
 ## 判断数据类型
 ```
  typeof 'str' //string
  typeof false //boolean
  typeof 123 //number
  typeof undefined //undefined
  typeof function(){} //function
  typeof {} //object
  typeof [] //object
  typeof null //object
  typeof new RegExp() //object
 ```
 * 准确判断类型方法
 ```
 Object.prototype.toString.call(this).toLowerCase()
 ```
***
## 数组的方法
    ```
    concat()	连接两个或更多的数组，并返回结果。
    join()	把数组的所有元素放入一个字符串。元素通过指定的分隔符进行分隔。
    pop()	删除并返回数组的最后一个元素
    push()	向数组的末尾添加一个或更多元素，并返回新的长度。
    reverse()	颠倒数组中元素的顺序。
    shift()	删除并返回数组的第一个元素
    slice(begin, end)	从某个已有的数组返回选定的元素 (包括begin,不包括end；如果该参数为负数，则表示从原数组中的倒数第几个元素开始提取,一直取到最后一个元素包括最后一个元素)
    sort()	对数组的元素进行排序
    splice()	删除元素，并向数组添加新元素。
    toSource()	返回该对象的源代码。
    toString()	把数组转换为字符串，并返回结果。
    toLocaleString()	把数组转换为本地数组，并返回结果。
    unshift()	向数组的开头添加一个或更多元素，并返回新的长度。
    valueOf()	返回数组对象的原始值
    
    改变原数组的方法有
    
    pop()
    push()
    reverse()
    shift()
    sort()
    splice()
    unshift()
    
    ```
   ***
   ## 字符串方法
   ```
   length //返回字符串长度
   indexOf() //方法返回字符串中指定文本首次出现的索引（位置）
   lastIndexOf() //方法返回指定文本在字符串中最后一次出现的索引
   search() //方法搜索特定值的字符串，并返回匹配的位置
   
   3种提取字符串 方法
   
   slice(start, end) // 包括start，不包括end。为负数时从字符串结尾开始计数
   substring(start, end) // 类似slice， 不接受负数
   substr(start, length) //类似slice, 第二个参数为接受的长度， 若省略第二个参数，则剪裁字符串剩余的部分
   
   
   relpace(oldstr, newstr) // 替换字符串中指定的值
   toUpperCase()
   toLowerCase()
   concat() //连接两个或多个字符串
   trim() //删除字符串两端的空白字符串
   
   提取字符串字符的方法
   charAt(pos) //返回指定位置的字符
   charCodeAt(pos) //返回指定位置的字符unicode编码
   
 
   split() //字符串转数组
   ```
   * 所有的字符串方法都不改变原字符串
   ***
   ## 深拷贝
   * 第一种方法：JSON.parse(JSON.stringfy(obj))
   * 第二种方法：递归
   ```
   var _type = (t)=> Object.prototype.toString.call(t).toLowerCase().slice(8,-1)
   function deepCopy(sourse,target) {
        for (var prop in sourse) {

            if (sourse.hasOwnProperty(prop)) {
                if (_type(sourse[prop]) === 'array') {
                    target[prop] = []
                    deepCopy(sourse[prop], target[prop])
                } else if (_type(sourse[prop]) === 'function') {
                    target[prop] = sourse[prop]
                } else if (_type(sourse[prop]) === '{}') {
                    target[prop] = {}
                    deepCopy(sourse[prop], target[prop])
                } else {
                     target[prop] = sourse[prop]
                }
            }
        }
        return target
    }
    var a = {
        a: [1,2],
        b: {a: 'a', b:{a:1}},
        c: true,
        d: null,
        e: undefined,
        f: function a(){},
        g: NaN
    }
    var b = deepCopy(a,{})
```
   
    
