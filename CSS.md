# CSS
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
 
