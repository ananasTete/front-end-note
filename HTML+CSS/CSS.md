



宽高设计思路：父盒子只设置宽，由子盒子们设置高，这样父盒子多大由子盒子撑起，不用每个div都要设置宽高，动一个就要动很多盒子。



[MDN的css文档](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Reference)



几部分：

1. 布局：flex，position，浮动，margin，padding
2. 盒模型：padding，border，margin
3. background
4. 字体处理：颜色，行高，对齐方式
5. 属性的继承性



## 继承与非继承属性









## 尺寸



绝对尺寸表示

- `px `       像素单位



相对尺寸表示

- `%`            
  1. 设置宽高时，是相对于父元素的宽高的百分比，父元素为\<body>时，宽度有效，高度无效
  2. 设置`margin padding` 时，根据父元素的宽度的百分比
  3. `border-radius` 中的百分比：`border-radius:25% /50%;` 每个角横向半径为宽度的25%，纵向半径为高度的25%；`border-radius:25% 50% 30% 10%;` 左上角横向半径为宽度的25%，纵向半径为高度的25%，其它角同理。
  4. [csdn %](https://blog.csdn.net/qq_40832236/article/details/88785184)
- `em`          
  1. 用于字体大小：子元素`font-size`使用em时是**父元素**这一属性的n倍，如果父元素没有设置字体大小且无更大的父元素则父元素的字体大小为浏览器默认字体大小,一般为`16px`
  2. 用于`width height margin padding border`中的尺寸，为**当前元素**的`font-size` 的n倍。当前元素没有`font-size`属性则为父元素`font-size`的n倍。
- `rem`   css3 
  1. 在css中为\<html>元素设置`font-size` ，
  2. 此页面上应用`rem` 的单位都是相对这一尺寸的n倍，不再相对父元素全部相对于这一`font-size`，字体是这样，其他的如`width height margin`等也是相对于\<html>的字体大小的n倍
- `vh， vw， vmin， vmax`
  1. 视口高度、宽度。50vh表示视口高度的 50%
  2. vmin、vmax指vh、vw中较小以及较大的哪个作为单位 。30vmin



calc计算函数css3

```css
width: calc(100% - 96px);
```

也属于相对尺寸。

注意！运算符两侧必须有空格！如 `calc(100%-96px)` 不生效





## 颜色



#### 单色表示



- 颜色名称表示



- 十六进制表示（#RRGGBB)
  1. RRGGBB：红绿蓝；
  2. #后跟6位十六进制数字 00~FF (即0~255)



- `rgb(r,g,b)`
  1. 每个参数都为 0~255



- `hsl(色调,饱和度,亮度)`
  1. Hue 是色盘上的度数（从 0 到 360） - 0 (或 360) 是红色，120 是绿色，240 是蓝色。
  2. Saturation 是百分比值；饱和度越高色彩越浓、饱和度越低色彩越淡；0% 意味着灰色，而 100% 是全彩。
  3. Lightness 同样是百分比值；0% 是黑色，100% 是白色。亮度度决定照射在颜色上的白光有多亮。



#### 半透明颜色 css3



1. `rgba(r,g,b,alpha)`          

   - alpha为不透明度，0.0~1.0

   

2. `hsla(色调,饱和度,亮度,alpha) `            

   - 同上



#### opacity

opacity属性指定了一个元素的**不透明度**

一个元素和它包含的所有子元素都会具有和元素背景相同的透明度，哪怕这个元素和它的子元素有不同的opacity属性值。（不是继承）

```
/* 完全不透明 */
opacity: 1;
opacity: 1.0;

/* 半透明 */
opacity: 0.6;

/* 完全透明 */
opacity: 0.0;
opacity: 0;

opacity: inherit;
```



rgba()和 opacity 的透明效果有什么不同？

 rgba()和 opacity 都能实现透明效果，但最大的不同是 opacity 作用于元素，以及元素内的所有 内容的透明度。

 rgba()只作用于元素的颜色或其背景色。（设置 rgba 透明的元素的子元素不会继承透明效果！）





#### 特殊表示



```css
currentColor       //一个变量，存储着当前HTML元素的color值。
```

- 一个HTML元素设置了color后，可以将currentColor用在该元素的其它css属性中。

- 如果HTML元素没有设置color，由于color元素具有继承性，将从父元素继承这一属性。

```css
 <div class="b"> hahahhah </div> 
```

```css
.b{
      color: red;
      border: currentColor 1px solid;
}
```



#### 收集盒



[颜色名称-16进制-rgb对照表](https://tool.oschina.net/commons?type=3)

[rgb、rgba预览](https://www.qianbo.com.cn/Tool/Rgba/)







## 样式




|        |                    |
| ------ | ------------------ |
| solid  | 普通边框           |
| double | 双边框             |
| dotted | 点边框             |
| groove | 类似相框质感的边框 |
| dashed | 虚线边框           |










## 背景



`background` 是一种CSS简写属性，用于一次性集中定义各种背景属性。

- 可以按**任意顺序**放置，空格隔开。

- 对于所有简写属性，任何没有被指定的值都会被设定为它们的初始值。



`backgroud-image` 属性用于为一个元素设置**一个或者多个**背景图像。

- 先定义的图像在上面，后定义的图像在下面。用逗号隔开。
- 可能的取值：`none`(初始值)  



`background-color`设置元素的背景色, 属性的值为颜色值或关键字"transparent"二者选其一。

- transparent 是`background-color`未设定时的初始值，表示全透明色，相当于相当于 rgba(0,0,0,0)
- 颜色可以以各种颜色表示法表示，纯色表示，半透明色表示等，详见颜色。



`background-clip` 设置元素的背景（背景图片或颜色）是否**延伸**到边框、内边距盒子、内容盒子下面。

- border-box ：默认值，背景延伸到边框外沿
- padding-box：背景延伸到内边距外沿
- content-box：背景延伸到内边距内沿，即内容区





#### 1. 背景图片


|                                  |                                              |
| -------------------------------- | -------------------------------------------- |
| backgroud-image : url ("地址")； | 设置背景图片                                 |
| background-size                  | 设置背景图片尺寸                             |
| background-repeat :              | 设置背景图片重复方式                         |
| background-attachment : fixed;   | 设置背景图片固定在屏幕某个位置，不随页面滚动 |
| background-position              | 设置背景图片在容器中的位置                   |



##### （1）backgroud-size

|         |                                                              |
| ------- | ------------------------------------------------------------ |
| auto    | 默认，背景图片尺寸<空间尺寸时，自动重复背景填满空间          |
| cover   | 背景图片等比例缩放到覆盖整个空间，可能会显示不全             |
| contain | 背景图片等比例缩放到能在盒子中显示完全的最大尺寸（宽或高到达边缘停止） |
| 如50px  | 手动设置背景图片尺寸。背景尺寸<空间尺寸时，自动重复背景填满空间 |



##### （2）background-repeat

|           |                   |      |
| --------- | ----------------- | ---- |
| repeat-x  | 图片只在x方向重复 |      |
| repeat-y  | 图片只在y方向重复 |      |
| no-repeat | 图片不重复        |      |



##### （3）background-position

```css
background-position: x y ;
//
```







#### 2. 背景颜色



```css
background-color                   //不可继承
```



有两种取值：transparent 和 颜色

- transparent 是`background-color`未设定时的初始值，表示全透明色，相当于相当于 rgba(0,0,0,0)
- 颜色可以以各种颜色表示法表示，详见颜色。



可能的值：

```css
background-color: red;                          //颜色名称表示

background-color: #bbff00;                      //十六进制表示

background-color: rgb(255, 255, 128);           //rgb表示
background-color: hsl(50, 33%, 25%);            //hsl表示

background-color: rgba(255, 255, 128, 0.4);      //半透明色
background-color: hsla(50, 33%, 25%, 0.75);      

background-color: currentColor;                 //currentColor变量表示
background-color: transparent;                  //初始值，表示全透明色

background-color: inherit;                     //表示继承的三个关键字用于颜色
background-color: initial;
background-color: unset;
```

（详见颜色）



#### 背景在盒子中的填充

背景颜色、背景图片会填充元素的content、padding、border区域





## 边框



边框会扩张元素的大小，`div`设置为200*200，若边框设置为50，`div`就变成了300 *300。



#### border


|                          |                                      |                                                              |
| ------------------------ | ------------------------------------ | ------------------------------------------------------------ |
| border-style             | 边框样式                             |                                                              |
| border-width             | 边框宽度                             |                                                              |
| border-color             | 边框颜色                             | 还可以设置border-color: blue yellow yellow red;分别设置颜色；其他boder-xxx同理 |
| border:宽度  样式 颜色； | 上述三者的简写，但是这样写没有提示。 |                                                              |
|                          |                                      |                                                              |
| border-top-style         | 上边框样式                           | 单独设置上边框，同理还有 left, right,botton                  |
| border-top-width         | 上边框宽度                           | 其它border-xxx同理                                           |
| border-top-color         | 上边框颜色                           |                                                              |


- boder-style选项


|        |                    |
| ------ | ------------------ |
| solid  | 普通边框           |
| double | 双边框             |
| dotted | 点边框             |
| groove | 类似相框质感的边框 |
| dashed | 虚线边框           |





#### 圆角边框



**四角同弧度：**

```css
border-radius: 35px / 30px ;
```

前者是侧边框外沿到圆心的距离，后者是上或下边框外沿到圆心的距离。

当距离相同时可以写为一个。

```css
border-radius: 50px ;
```

**四角不同弧度：**

```css
border-radius: 10px 20px 30px 40px ; //分别为左上、右上、右下、左下设置圆角

border-radius: 10px 20px ； //左上、右下为10px;右上左下为20px
```



1. 这个距离是边框==**外沿**==到圆心的距离，当边框足够宽以至于圆心不在盒子里而在边框里时，边框内沿不会有圆角

<img src="../实例图片/image-20210111213828016.png" alt="image-20210111213828016" style="zoom:33%;" />

2. 当圆角的幅度比较大时，会显示到盒子里去。只是看起来这样，实际的边框还在盒子之外

<img src="../实例图片/image-20210111214216245.png" alt="image-20210111214216245" style="zoom: 50%;" />

如下图：

<img src="..//实例图片/image-20210111215300279.png" alt="image-20210111215300279" style="zoom: 50%;" />



#### 边框与背景



边框与背景的关系：

- `div`设置为200*200，若边框设置为50，`div`就变成了300 *300，即边框在盒子外。
- 默认状态下，背景会延伸到边框的下方，背景色、背景图片都会。



#### 半透明边框



由边框和背景的关系可知，当我们设置半透明边框时，背景会延伸到半透明边框之下。

<img src="../实例图片/image-20210111211655754.png" alt="image-20210111211655754" style="zoom: 33%;" />

背景设置为颜色时，也会跟半透明边框颜色重叠，边框会形成新的颜色。

那我们如何改变这一困局呢？

```css
 background-clip: border-box(默认) | padding-box;
```

- `border-box` 意为用边框外沿来切割背景。
- `padding-box` 意为用边框内沿来切割背景

<img src="../实例图片/image-20210111212421316.png" alt="image-20210111212421316" style="zoom:33%;" />

#### 多重边框

1. `box-shadow` 方案

```css
box-shadow:  0px 0px 0px 10px  yellow,
               0px 0px 0px 20px   palevioletred;
```

<img src="../实例图片/image-20210115205227318.png" alt="image-20210115205227318" style="zoom:50%;" />

2. `outline` 方案

当我们只需要两层边框时，可以先添加一层`border` 再添加一层`outline` ，实现两层边框的效果。由于轮廓可以设置样式，我们就能得到比`box-shadow` 方案更多元化的多重边框效果。

```css
 border: 5px solid yellow;
 outline: 5px dotted palevioletred;
```

<img src="../实例图片/image-20210115215656230.png" alt="image-20210115215656230" style="zoom:50%;" />





#### 收集盒



##### 白色半透明边框

```css
div{
    border:10px solid hsla(0,0%,100%,.5);
    background-clip: padding-box;
}
```





## 轮廓



#### outline



边框与轮廓的区别：

1. 边框会扩展div的大小，轮廓不会
2. 轮廓位于边框外沿之外



| outline: 宽度 样式 颜色 |          |
| ----------------------- | -------- |
| outline-width           | 轮廓宽度 |
| outline-style           | 轮廓样式 |
| outline-color           | 轮廓颜色 |





## 阴影



#### box-shadow



```javascript
box-shadow : (inset)  offset-x  offset-y  (blur-radius)  (spread-radius)  (color) ;
```

- `inset` 可选的，加入此关键字将成为内阴影；不加则默认外阴影。
- `offset-x` 必选的，阴影在x轴偏移距离。0为不偏，外阴影：正值向右偏；负值向左偏。内阴影相反。
- `offset-y` 必选的，阴影在y轴偏移距离。0为不偏，外阴影：正值向下偏；负值向上偏。内阴影相反。
- `blur-radius` 可选的，阴影模糊半径，只能取正值，如5px,阴影各边扩张5px，扩张的面积显示为模糊效果，值越大，扩张面积越大，越模糊。
- `spread-radius` 可选的，阴影传播半径，默认阴影与被阴影对象一样大，可以接收负值。各边可以扩大或缩小指定长度。
- `color` 颜色，可设成半透明色。



##### 1. 基本例子：



```css
box-shadow: 5px 5px 5px black;          //右下外阴影
```

<img src="../实例图片/image-20210115201037491.png" alt="image-20210115201037491" style="zoom:50%;" />

```css
 box-shadow: 0px 0px 10px black;    //四周外阴影
```

<img src="../实例图片/image-20210115201539995.png" alt="image-20210115201539995" style="zoom:50%;" />

```css
 box-shadow: 0px 0px 10px 5px black;    //四周扩大外阴影
```

<img src="../实例图片/image-20210115201306501.png" alt="image-20210115201306501" style="zoom:50%;" />

```css
 box-shadow: inset 0px 0px 10px  black;  //四周内阴影
```

<img src="../实例图片/image-20210115201731376.png" alt="image-20210115201731376" style="zoom:50%;" />

```css
box-shadow: inset 10px 10px  20px black;  //左上内阴影
```

<img src="../实例图片/image-20210115202208554.png" alt="image-20210115202208554" style="zoom:50%;" />

##### 2. 多重阴影



`box-shadow` 可以设置多个阴影，用逗号隔开。

```css
 box-shadow:  5px 5px 5px  black,
               0px -5px 5px black;           //三边外阴影
```

<img src="../实例图片/image-20210115203940281.png" alt="image-20210115203940281" style="zoom:50%;" />

```css
box-shadow:  20px 0px 20px -20px black,
               -20px 0px 20px -20px black;    //两侧外阴影
//因为模糊半径会使没有偏移的上下两边也会出现阴影，所以通过负值使其收缩起来
```

<img src="../实例图片/image-20210115204530913.png" alt="image-20210115204530913" style="zoom:50%;" />

```css
box-shadow:  0px 0px 0px 10px  yellow,
               0px 0px 0px 20px   palevioletred;
```

<img src="../实例图片/image-20210115205227318.png" alt="image-20210115205227318" style="zoom:50%;" />



#### text-shadow





## 继承



三个关键字：`inherit`      `initial`      `unset`



**表示继承的关键字可用于任何HTML元素的任何属性。**



**inherit关键字:** 

表示继承父元素这一属性的值。用于子元素中不具有继承性的属性设置为父元素相应属性的值。

**initial关键字:**

表示不继承父元素这一属性的值。用于子元素中具有继承性的属性不继承父元素相应属性的值，而是该属性的初始值。

**unset关键字：** 













