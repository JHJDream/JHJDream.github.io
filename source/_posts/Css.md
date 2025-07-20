---
title: Css
date: 2022-03-28 16:22:37
tags:
---

How CSS works. edit. CSS is a language that defines style structures such as fonts, colors, positions, etc., and is used to describe how information on a web page is formatted and displayed.

## css知识点

##### 与下文css对应

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="/Web/css/style.css">
</head>
<body>
    <div class="red-tag big-tag" >div 1</div>
    <div>div 2</div>
    <div id="mydiv">div 3</div>
    <div class="effect"> div4</div>

    <p id="k">p 1</p>
    <p id="h">p 2</p>
    <p>p 3</p>
    <p>p 4</p>
    

    <a href="/Web/Gift/Gift.html">about</a>
    <a href="/Web/Login/interface.html">about</a>
    <a href="/Web/Gift/Gift2.html">about</a>
    <a href="/Web/Gift/Gift3.html">about</a>
    <button href="/Web/wang/cheng.html">about</button>

    <input type="text">
<br>
    <h2>三国志</h2>
    <h2>追风筝的人</h2>
    <h2>狂人日记</h2>

    <img id="beijing" width="200" src="/Web/Gift/background.2.jpg" alt="pic">

        <br>

    <img width="150" id="yuan" src="/Web/Gift/Me.03.png" alt="pic">

    <br>

    <table>
        <tbody>
            <tr>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <td></td>
                <td></td>
                <td></td>
            </tr>
        </tbody>
    </table>

</body>
</html>
```

## 选择器 

```css
/* 标签选择器 */
div {
    width: 100px;
    height: 100px;
    background-color: lightblue;
    margin-bottom: 10px;
}

p {
    width: 50px;
    height: 70px;
    background-color: lightgreen;
}

/* id选择器   # id名{}  id一般唯一 */

#mydiv {
    background-color: lightcoral;
}

#myp {
    background-color: lightsalmon;
}

/* 类选择器  . class名{}  一个标签可有多个class */

.red-tag {
    background-color: lightpink;
}

.big-tag {
    width: 120px;
    height: 120px;
}


/* 伪类选择器 */

.effect:hover {
    transform: scale(1.1);/*  1.1倍 */
    transition: 200ms;    /* 渐变 */
}

#mydiv:hover {
    background-color: red;/*  变颜色  */
    transition: 200ms;
}


/* 没有点击之前 */
a:link {
    color: red;
}
/* 点击之后的颜色 */
a:visited {
    color: green;
}
/* 鼠标悬停之后的颜色 */
a:hover {
    color: orange;
}
/* 鼠标点击之后的颜色 */
a:active {
    color: purple;
}
/* 光标定位后的聚焦状态 */
input:focus {
    background-color: lightblue;
    width: 100px;/* 聚焦之后加长 */
}

input {
    width: 50px;/* 聚焦之前比较短 */
}

input:hover {
    transform: scale(1.2);
}

button:hover {
    background-color: aquamarine;
}
button:active {
    background-color: chartreuse;
}

/* 位置选择器
找p的父级子类下的第7个标签
（）中可写odd ：所有奇数
        even: 所有偶数
        2n+1
        3n
*/
p:nth-child(7) {
    background-color: deepskyblue;
}

/* 复合选择器 */
#k:hover,#h:hover {
    background-color: aquamarine;
}

/* 伪元素选择器 
改变 p段落每行首个字符或字
*/
p::first-letter {
    color: red;
    font-size: 110%;
}

/*
第一行都变成红色
p::first-line {
    color: red;
    font-size: 110%;
}
选中区域变成紫底 蓝字
p::selection {
    color: aqua;
    background-color: blueviolet;
}
*/

/* 在元素前后插入内容 */
h2::before {
    content: "《";
    color: aqua;
}
h2::after {
    content: "》";
    color: aquamarine;
}

#beijing:hover {
    transform: scale(1.1);
    transition: 200ms;
}

/*  去掉超链接的下划线 */
a {
    text-decoration: none;
}

#yuan:hover {
    border-radius: 50%;
    transform: scale(1.1);
    transition: 200ms;

}


td {
    border-style: solid;
    width: 20px;
    height: 20px;
}
/* 消除表格的重叠 */
table {
    border-style: solid;
    border-collapse: collapse;
}
```



## 文本

```html
<h4>悯农</h4>
<div class = "mydiv">
    <p id= "a">
    锄禾日当午，
    汗滴禾下土。
    谁知盘中餐，
    粒粒皆辛苦。
	</p>
</div>
```



```css
.mydiv {
    whidth: 50vw;//相对于视窗等比缩小放大
    height: 30vw;
    background-color:lightblue;
    
    text-align:center;//标签居中
    //justify左右对齐
}

#a {
    text-indent:2em;//首行缩进2个字符 1em = 1个字
}
```

- 补充知识点：长度单位

  px    设备上的像素点

  %     相对元素的百分比

  em  相对于当前元素的字体大小

  rem 相对于跟元素的字体大小

  vw   相对与视窗宽度的百分比

  vh    相对于视窗高度的百分比

## 字体

1. ```css
   font-size
   ```

    CSS 属性指定字体的大小。因为该属性的值会被用于计算em和ex长度单位，定义该值可能改变其他元素的大小。

2. ```css
   font-style
   ```

    CSS 属性允许你选择 font-family 字体下的 italic 或 oblique 样式.

3. ```css
   font-weight
   ```

    CSS 属性指定了字体的粗细程度。 一些字体只提供 normal 和 bold 两种值。

4. ```css
   font-family
   ```

   CSS 属性 font-family 允许通过给定一个有先后顺序的，由字体名或者字体族名组成的列表来为选定的元素设置字体。
   属性值用逗号隔开。浏览器会选择列表中第一个该计算机上有安装的字体，或者是通过 @font-face 指定的可以直接下载的字体。

## 背景

- ```css
  background-color
  opacity: 0.2;//透明度
  ```

  CSS属性中的background-color会设置元素的背景色, 属性的值为颜色值或关键字”transparent”二者选其一。

- ```css
  background-image
  background-image: url(' ');//引入图片做背景
  ```

  CSS background-image 属性用于为一个元素设置一个或者多个背景图像。  

  渐变色：linear-gradient(rgba(0, 0, 255, 0.5), rgba(255, 255, 0, 0.5))

- ```css
  background-size
  ```

  background-size 设置背景图片大小。图片可以保有其原有的尺寸，或者拉伸到新的尺寸，或者在保持其原有比例的同时缩放到元素的可用空间的尺寸。

- ```css
  background-repeat
  ```

  background-repeat CSS 属性定义背景图像的重复方式。背景图像可以沿着水平轴，垂直轴，两个轴重复，或者根本不重复。

- ```css
  background-position
  ```

  background-position 为背景图片设置初始位置。

- ```css
  background-attachment
  ```

  background-attachment CSS 属性决定背景图像的位置是在视口内固定，或者随着包含它的区块滚动。

## 边框

1. ```css
   border-style//(上右下左)
   ```

   border-style 是一个 CSS 简写属性，用来设定元素所有边框的样式。

2. ```css
   border-width
   ```

   border-width属性可以设置盒子模型的边框宽度。

3. ```css
   border-radius//(50%)圆形
   ```

   CSS 属性 border-radius 允许你设置元素的外边框圆角。当使用一个半径时确定一个圆形，当使用两个半径时确定一个椭圆。这个(椭)圆与边框的交集形成圆角效果。

4. ```css
   border-color//(上右下左)
   ```

   CSS属性border-color 是一个用于设置元素四个边框颜色的快捷属性： border-top-color, border-right-color, border-bottom-color, border-left-color

5. ```css
   border-collapse
   ```

   border-collapse CSS 属性是用来决定表格的边框是分开的还是合并的。在分隔模式下，相邻的单元格都拥有独立的边框。在合并模式下，相邻单元格共享边框。

## 内边距与外边距

*margin*

属性为给定元素设置所有四个（上下左右）方向的外边距属性。

1. 可以接受1~4个值（上、右、下、左的顺序）
   可以分别指明四个方向：margin-top、margin-right、margin-bottom、margin-left

2. 可取值

   - length :固定值
   - percentage：相对于包含块的宽度，以百分比值为外边距。
   - auto：让浏览器自己选择一个合适的外边距。有时，在一些特殊情况下，该值可以使元素居中。

3. 特殊情况

   - 块的上外边距(margin-top)和下外边距(margin-bottom)有时合并(折叠)为单个边距，其大小为单个边距的最大值(或如果它们相等，则仅为其中一个)，这种行为称为边距折叠。
   - 父元素与后代元素：父元素没有上边框和padding时，后代元素的margin-top会溢出，溢出后父元素的margin-top会与后代元素取最大值。

   *padding*

   CSS 简写属性控制元素所有四条边的内边距区域

   1. 以接受1~4个值（上、右、下、左的顺序）
   2. 以分别指明四个方向：padding-top、padding-right、padding-bottom、padding-left

   ## 盒子模型

   *box-sizing*

CSS 中的 box-sizing 属性定义了 user agent 应该如何计算一个元素的总宽度和总高度。

```css
/* box-sizing: content-box;  是默认值，设置border和padding均会增加元素的宽高。 */
    box-sizing: border-box; /*   置border和padding不会改变元素的宽高，而是挤占内容区域 */
    padding: 10px;
    border: 10px solid black;
```

## 位置

*position*

CSS position属性用于指定一个元素在文档中的定位方式。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="/Web/css/style.css">
</head>
<body style="margin: 0;">
    <div class="div-outer">
        <div class="div-inner-1">
            1
        </div>
        <div class="div-inner-2">
            回到顶部
        </div>
        <div class="div-inner-3">
            3
        </div>
    </div>
</body>
</html>
```



#### 定位类型：

定位元素 ，是其计算后位置属性为 relative, absolute, fixed 或 sticky 的一个元素（换句话说，除static以外的任何东西）。

相对定位元素，是计算后位置属性为 relative 的元素。

绝对定位元素，是计算后位置属性为 absolute 或 fixed 的元素。

粘性定位元素，是计算后位置属性为 sticky 的元素。



```css
.div-outer {
    width: 300px;
    height: 3000px;
    background-color: lightblue;
    margin: 100px;
    /* position: absolute; */
    /* padding: 20px 0 0 30px; */
    /*padding-top: 1px;
    border-top: 1px solid;  solid 实心 */
    /* overflow: hidden; */
    /* 子元素距父元素的像素*/
}

div-inner-1 {
    width: 100px;
    height: 100px;
    background-color: red;
    margin: 10px;
    color: white;
    display: inline-block;
    /* z-index: 2;
    position: relative; 把压在下面的 显现出来 */
}

.div-inner-2 {
    width: 30px;
    height: 100px;
    background-color: green;
    /* margin: 10px; */
    color: white;
    display: inline-block;
    position: fixed; /* 固定定位 */
    /*position: absolute ; 绝对定位 */
    top: 100px; /* 相对与上边的线（边界）向下偏移30px */
    /*  left: 20px;相对与左边的线（边界）向下偏移30px */
    right: 0;
}
```



#### 取值

- static：该关键字指定元素使用正常的布局行为，即元素在文档常规流中当前的布局位置。此时 top, right, bottom, left 和 z-index 属性无效。

- relative：该关键字下，元素先放置在未添加定位时的位置，再在不改变页面布局的前提下调整元素位置（因此会在此元素未添加定位时所在位置留下空白）。top, right, bottom, left等调整元素相对于初始位置的偏移量。

- absolute：元素会被移出正常文档流，并不为元素预留空间，通过指定元素相对于最近的非 static 定位祖先元素的偏移，来确定元素位置。绝对定位的元素可以设置外边距（margins），且不会与其他边距合并。

- fixed：元素会被移出正常文档流，并不为元素预留空间，而是通过指定元素相对于屏幕视口（viewport）的位置来指定元素位置。元素的位置在屏幕滚动时不会改变。

- sticky：元素根据正常文档流进行定位，然后相对它的最近滚动祖先（nearest scrolling ancestor）和 containing block (最近块级祖先 nearest block-level ancestor)，包括table-related元素，基于top, right, bottom, 和 left的值进行偏移。偏移值不会影响任何其他元素的位置。

  ```css
  .div-inner-3 {
      width: 100px;
      height: 100px;
      background-color: red;
      margin: 10px;
      color: white;
      position: sticky;/* 粘性定位  */
      bottom: 10px;
  }
  ```

  

## 浮动

*float*

常取值 left：表明元素必须浮动在其所在的块容器左侧的关键字。
             right：表明元素必须浮动在其所在的块容器右侧的关键字

**左右浮动最常用的地方是  把不同的div放在同一行且不想有间距**

```css
float: left;
```

***clear***

清除浮动 。有时，想要强制元素移至任何浮动元素下方。比如说，你可能希望某个段落与浮动元素保持相邻的位置，但又希望这个段落从头开始强制独占一行。此时可以使用clear。

**取值：**

left：清除左侧浮动。

right：清除右侧浮动。

both：清除左右两侧浮动。

```css
clear: left;/* 以左为例 */
```

## flex布局

#### 1.定义在容器上

flex CSS简写属性设置了弹性项目如何增大或缩小以适应其弹性容器中可用的空间。

```css
flex-direction /*指定内部元素如何在flex容器中布局的，定义主轴的方向 */
```



**可取值**

- row：flex容器的主轴被定义为与文本方向相同。 主轴起点和主轴终点与内容方向相同。

- row-reverse：表现和row相同，但是置换了主轴起点和主轴终点

- column：flex容器的主轴和块轴相同。主轴起点与主轴终点和书写模式的前后点相同

- column-reverse：表现和column相同，但是置换了主轴起点和主轴终点

  ------

  

```css
flex-wrap: wrap;   /*指定flex元素单行显示还是多行显示，若允许换行，这个属性允许堆叠的方向 */
```

**取值**

- nowrap：默认值。不换行。

- wrap：换行，第一行在上方。

- wrap-reverse：换行，第一行在下方。

  ------

  

```css
justify-content: center;  /*水平居中*/
align-items: center;   /*竖直居中*/
```

justify-content 属性定义了浏览器之间，如何分配顺着弹性容器主轴(或者网格行轴) 的元素之间及其周围的空间。

**取值**

- flex-start：默认值。左对齐
- flex-end：右对齐
- space-between：左右两段对齐
- space-around：在每行上均匀分配弹性元素。相邻元素间距离相同。每行第一个元素到行首的距离和每行最后一个元素到行尾的距离将会是相邻元素之间距离的一半。
- space-evenly：flex项都沿着主轴均匀分布在指定的对齐容器中。相邻flex项之间的间距，主轴起始位置到第一个flex项的间距，主轴结束位置到最后一个flex项的间距，都完全一样。



lign-items属性将所有直接子节点上的align-self值设置为一个组。 align-self属性设置项目在其包含块中在交叉轴方向上的对齐方式。

​	**取值**

- flex-start：元素向主轴起点对齐。
- flex-end：元素向主轴终点对齐。
- center：元素在侧轴居中。
- stretch：弹性元素被在侧轴方向被拉伸到与容器相同的高度或宽度。

------

```css
align-content  /*属性设置了浏览器如何沿着弹性盒子布局的纵轴和网格布局的主轴在内容项之间和周围分配空间。 */
```

**取值**

- flex-start：所有行从垂直轴起点开始填充。第一行的垂直轴起点边和容器的垂直轴起点边对齐。接下来的每一行紧跟前一行。
- flex-end：所有行从垂直轴末尾开始填充。最后一行的垂直轴终点和容器的垂直轴终点对齐。同时所有后续行与前一个对齐。
- center：所有行朝向容器的中心填充。每行互相紧挨，相对于容器居中对齐。容器的垂直轴起点边和第一行的距离相等于容器的垂直轴终点边和最后一行的距离。
- stretch：拉伸所有行来填满剩余空间。剩余空间平均地分配给每一行。

#### 2.定义在flex布局的元素

order :定义flex项目的顺序，值越小越靠前

```css
flex-grow: 1;  /*等比例缩放，负值无效，默认为0*/
flex-shrink: 1;
/*CSS flex-shrink 属性指定了 flex 元素的收缩规则。flex 元素仅在默认宽度之和大于容器的时候才会发生收缩，其收缩的大小是依据 flex-shrink 的值。*/
```

**flex-basis** :CSS 属性 flex-basis 指定了 flex 元素在主轴方向上的初始大小。

**取值**

width 值可以是 [HTML_REMOVED]; 该值也可以是一个相对于其父弹性盒容器主轴尺寸的百分数 。负值是不被允许的。默认为 auto。

*flex*:     flex-grow、flow-shrink、flex-basis的缩写。

**可取**

auto：flex: 1 1 auto

none：flex: 0 0 auto

## 响应式布局

[Bootstrap](https://v5.bootcss.com/docs/getting-started/introduction/)

用于构建响应式、移动设备优先的网站。

