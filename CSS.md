# CSS
## posititon 几种属性
* relative
  * 不脱离文档流
  * 设置left/right/top/bottom时，相对自身发送偏移，当文档流仍旧保持默认位置
* absolute
  * 脱离文档流
  * 相对于父元素（position不为static的，若没有则继续向上查找父元素直至body）定位
* fixed
  * 脱离文档流
  * 相对于body定位
* static

***
## 垂直水平居中方法
* 
  ```
  //margin: auto法
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    margin: auto
  // margin 一定值法
    position: absolute;
    top: 50%;
    left: 50%;
    margin-top: -自身高度的50%；
    margin-left: -自身宽度的50%;  // 未知宽高度可采用transform: translate(-50%,-50%) 
  // flex布局
    display: flex;
    justify-content: center;
    align-items: center;
  ```
  
***
## BFC(以下都是摘自[mdn](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context))
* 定义
> 块级格式上下文。是Web页面的可视化CSS渲染的一部分，是块盒子的布局过程发生的区域，也是浮动元素与其他元素交互的区域。
* 下列方式会创建块格式化上下文：
  * html
  * float不为none
  * position: absolute; position: fixed
  * display: inline-block; display: flex; display: table-cell; display: table-caption
  * overflow不为visible
* 作用
  ```
  块格式化上下文对浮动定位（参见 float）与清除浮动（参见 clear）都很重要。浮动定位和清除浮动时只会应用于同一个BFC内的元素。浮动不会影响其它BFC中元素的布局，而清除浮动只能清除同一BFC中在它前面的元素的浮动。外边距折叠（Margin collapsing）也只会发生在属于同一BFC的块级元素之间。
  ```
 
 ## 文字环绕图片效果
 *  对图片
  ```
  <html>
    <head>
        <style>
            .img-container {
                word-break: break-all; //主要针对英文数字不环绕问题设置的
            }
            img {
                float: left;
            }
        </style>
    </head>
    <body>
        <div class="container">
            <div class="img-container">
                <img src="./1.png">
                abccccccccccccccabccccccccccccccabccccccccccccccabccccccccccccccababccccccccccccccabccccccccccccccabccccccccccccccabccccccccccccccababccccccccccccccabccccccccccccccabccccccccccccccabccccccccccccccababccccccccccccccabccccccccccccccabccccccccccccccabccccccccccccccababccccccccccccccabccccccccccccccabccccccccccccccabccccccccccccccababccccccccccccccabccccccccccccccabccccccccccccccabccccccccccccccababccccccccccccccabccccccccccccccabccccccccccccccabccccccccccccccababccccccccccccccabccccccccccccccabccccccccccccccabccccccccccccccababccccccccccccccabccccccccccccccabccccccccccccccabccccccccccccccababccccccccccccccabccccccccccccccabccccccccccccccabccccccccccccccab
            </div>
        </div>
    </body>
</html>
  ```
  
  ## 清除浮动
  * 父元素设置height
  * 父元素创建BFC 参考上面提到的BFC
  * 父元素设置伪类
  
  ```
   <html>
    <head>
        <style>
            .container {
                border: 1px solid red;
                height: 300px;
                /* 兼容ie6- */
                zoom: 1; 
            }
            .container::after {
                clear: both;
                display: block;
                height: 0;
                content: '';
            }
            .img-container {
                float: left;
            }
        </style>
    </head>
    <body>
        <div class="container">
            <div class="img-container">
                <img src="./1.png">
                
            </div>
            <div class="second">
                css学习
            </div>
        </div>
    </body>
</html>

  ```
  
  * 最后一个浮动元素后 增加一个空元素 设置该空元素 clear: both
  ## 怎么让Chrome支持小于12px 的文字？(摘抄50道CSS基础面试题)[https://segmentfault.com/a/1190000013325778?utm_source=tag-newest]
  ```
  p{font-size:10px;-webkit-transform:scale(0.8);} //0.8是缩放比例 
  ```
  
  ## 用css 实现一个三角形
  ```
  <html>
    <head>
        <style>
            
            .triangle {
                height: 0;
                width: 0;
                border-left: 20px solid transparent;
                border-top: 20px solid transparent;
                border-right: 20px solid transparent;
                border-bottom: 20px solid red;
            }
        </style>
    </head>
    <body>
        <div class="triangle">

        </div>
    </body>
</html>
  ```
  
  
 
