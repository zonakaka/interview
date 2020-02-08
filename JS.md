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

