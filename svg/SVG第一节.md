# 什么是SVG
+ 在网页中绘制图形
+ 与Canvas的区别
 1. canvas 是位图
 2. svg 是矢量图
## 位图和矢量图
    1、先从概念说起：矢量图是根据几何特性来绘制图形，是用线段和曲线描述图像，矢量可以是一个点或一条线，矢量图只能靠软件生成，矢量图文件占用内在空间较小，因为这种类型的图像文件包含独立的分离图像，可以自由无限制的重新组合；位图图像也称为点阵图像，位图使用我们称为像素的一格一格的小点来描述图像。

    2、最大的区别，矢量图形与分辨率无关，可以将它缩放到任意大小和以任意分辨率在输出设备上打印出来，都不会影响清晰度，而位图是由一个一个像素点产生，当放大图像时，像素点也放大了，但每个像素点表示的颜色是单一的，所以在位图放大后就会出现咱们平时所见到的马赛克状。

    3、位图表现的色彩比较丰富，可以表现出色彩丰富的图象，可逼真表现自然界各类实物；而矢量图形色彩不丰富，无法表现逼真的实物，矢量图常常用来表示标识、图标、Logo等简单直接的图像。

    4、由于位图表现的色彩比较丰富，所以占用的空间会很大，颜色信息越多，占用空间越大，图像越清晰，占用空间越大；由于矢量图形表现的图像颜色比较单一，所以所占用的空间会很小。

    5、经过软件矢量图可以很轻松的转化为位图，而位图要想转换为矢量图必须经过复杂而庞大的数据处理，而且生成的矢量图质量也会有很大的出入。

## xml 文件
> \<?xml version="1.0" standalone="no" encoding="utf-8" ?>
+ standalone="no" 意味着 SVG 文档会引用一个外部文件
> \<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd".................. >
+ 引用了这个外部的 SVG DTD。该 DTD 位于 "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd"。该 DTD 位于 W3C，含有所有允许的 SVG 元素。
> \<svg xmlns="http://www.w3.org/2000/svg">

## html引入svg
1. 图片 image
 > \<img src="./circle.svg" alt="">
2.  背景 background 
 > \<div class="div"></div>
3.  框架 iframe
 > \<iframe src="./circle.svg"></iframe>
4. html中直接添加
 >  \<svg xmlns="http://www.w3.org/2000/svg" width="100%"height="100%"> 
 >  <br>\<circle cx="500" cy="500" r="100" fill="#09f09f"></circle> <br>
 >  \</svg>
## html 和 xml 的区别

## 绘制基本图形
1. circle 圆形
    cx x轴
    cy y轴
    r   半径
    fill 填充
    stroke 边框
    style 内联元素

2. rect 矩形
    width height
    x y
    rx ry
## 直接添加svg到html中
    创建div
        直接引入svg 添加命名空间

## svg 基本图形
    1. circle
        cx cy r （坐标 半径）
        fill stroke 设置边框 stroke-width设置宽度 transparent （透明）
        style  （可以用css的方法编写）
    2. rect 
        width height x y （款高 坐标）
        rx ry  （边角x y）
    3. line
      x1 y1 x2 y2  （坐标点）
      stroke 线颜色
      stroke-opacity 线透明度
    4. ellipse 椭圆
    5. polyine 折线
    6. ploygon 多边形
    7. path 路径

## \<g>标签
+ 是一个容器分组标签，用来组合元素的
+ 例子:做个靶心
    + transForm = "translate(a,b)"


## 在SVG中添加文本
1. \<text>文本
  1. x y fill （坐标）
  2. text-anchor="middle"
    // star middle end
 - 文字居中 文字大小/2-2 + y
2. \<image>标签

## css 补充
- 划入变为手型
    - cursor:pointer

## 利用JS生成SVG代码
1. 创建代码
> document.createElementNS(参数一,参数二)  //NS代表需要指定命名空间
+ 参数一：命名空间
+ 参数二：创建标签的标签名
2. 获取代码dom 节点
> document.getElementById("")
3. 追加节点
> document.appendChild()


## 封装createTag函数
~~~javascript
    var svgNS = "http://www.w3.org/2000/svg"
        window.onload = function () {
            var oParent = document.getElementById("div1");

            function createTag(tag, objAttr) {
                var oTag = document.createElementNS(svgNS, tag);
                for (var attr in objAttr) {
                    oTag.setAttribute(attr, objAttr[attr]);
                }
                return oTag;
            }
            var oSvg = createTag('svg', { 'xmlns': svgNS, "width": "100%", "height": "100%" })
            var oG = createTag('g', { "style": "cursor:pointer" });
            var oLine1 = createTag('line', { "x1": "100", "y1": "100", "x2": "390", "y2": "200", "stroke": "#ccc", "stroke-width": "1" })
            var oLine2 = createTag('line', { "x1": "100", "y1": "100", "x2": "390", "y2": "200", "stroke": "transparent", "stroke-width": "10" })
            oG.appendChild(oLine1);
            oG.appendChild(oLine2);
            oSvg.appendChild(oG);
            oParent.appendChild(oSvg);
        }
~~~

## 获取中心点坐标
> var centerX = oParent.offsetWidth/2;
> var centerY = oParent.offsetHeight/2;

## 动态获取数据
~~~JavaScript
var data = {
    centerNode:"text:'科鲁兹'",
    otherNode:[{
        x:100,
        y:100,
        text:"易车网"
    }]
}
~~~