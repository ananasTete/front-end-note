HTML ：为网页添加内容

<标签  属性们>   
   内容或内部标签们 
</标签>

CSS ：对HTML元素进行样式控制

<标签  属性们>
   HTML元素选择器们
</标签>

CCS由两个部分组成：选择器以及一些声明。











### div与span

|      | <div>                      | <span>                 |
| ---- | -------------------------- | ---------------------- |
|      | 块级元素，自动另起一行     | 内联元素，不会自动     |
|      | 任意元素的容器             | 文本容器               |
|      | 用于大的内容块设置样式属性 | 为部分文本设置样式属性 |
|      | 可以设置宽高               | 不能设置宽高等         |



### head元素

以下标签都可以添加到 head 部分：<title>、<base>、<link>、<meta>、<script> 以及 <style>。

meta提供关于HTML文档的元数据，元数据不会显示在页面上，但对于机器是可读的。典型的情况是，<meta>元素用于对文档的描述关键词，文档的作者最后修改时间以及其他元数据。

meta标签始终用于head元素中。



### HTML字符

HTML中一些特殊符号的表示，最常用的比如空格符号&nbsp代表一个空格。

![](../实例图片/字符表.PNG)





子元素会自动继承父元素的属性。

子元素会在父元素的左上角；子元素在宽或高上超过父元素后会露出；

```html
css
div{ 
weith=100px;
height:100px
}
html
<div>
    哈哈哈哈哈
</div>
```

宽高是对div的设置，是这一块级元素的宽高，与内容“哈哈哈哈哈”无关，文字会在左上角显示。





### CSS选择器

---

<br>

1. 标签选择器  （标签名）
2. id选择器（#）       id只能有一个
3. 类名选择器（ . ）  通过设置相同的class来对不同标签的元素或部分相同标签元素进行相同操作。类名可以有多个。
4. 属性选择器  （ [ ] )  具有相同属性，而不论属性值是什么。



#### 后代选择器：

```html
<!--css部分-->
h1 em {color:red;}
<!--html部分-->
<h1>This is a <em>important</em> heading</h1>
<p>This is a <em>important</em> paragraph.</p>
```

**将h1标签下所有em元素设置为红色。需要注意的是不管em是h1第几级元素，都会设置为红色，即他们之间的层级间隔是无限的。**

#### 子元素选择器：

```html
<!--css部分-->
h1 > strong {color:red;}
<!--html部分-->
<h1>This is <strong>very<strong>very</strong> </strong> important.</h1>
```

**将h1下的所有第一级strong元素设置为红色，而第二级不会**



#### 选择器的混合使用：不同类型的选择器混合使用

```
h1,p,em {
  color: green;
  }
.name,#02,p{
  color:blue;
  }
```

**同时将三种标签元素设置为绿色**



==选择器优先级：选择范围小的，选中元素少的优先级高==





###  设置宽和高

---
```html
width: 50px;
height: 50px;
```
设置元素占用区域大小 。超出元素实体的部分会产生白色背景。



### 边框，内边距，外边距

---




#### 2.2内边距和外边距

|      | 内边距                                  | 外边距                                         |
| ---- | --------------------------------------- | ---------------------------------------------- |
|      | 用于控制元素与边框之间的空白距离        | 为元素边框外创建额外空白距离，用以改变元素位置 |
|      | padding                                 | margin                                         |
|      | padding-top botton left right  上下左右 | margin-top botton left right                   |
|      | padding:5px 5px 6px 7px  上右下左顺时针 | padding:5px 5px 6px 7px                        |

margin可以为负值，且经常为负值。

==padding : 0 auto;在父元素中居中==

==padding：0；==

==margin：0；清空内外边距。==



##### 2.2.1外边距合并

**外边距合并指的是，当两个垂直外边距相遇时，它们将形成一个外边距。**

**合并后的外边距的高度等于两个发生合并的外边距的高度中的较大者。**

[w3school页面](https://www.w3school.com.cn/css/css_margin_collapsing.asp)



#### 2.3值复制

```
h1 {margin: 0.25em 1em 0.5em;}	/* 等价于 0.25em 1em 0.5em 1em */
h2 {margin: 0.5em 1em;}		/* 等价于 0.5em 1em 0.5em 1em */
p {margin: 1px;}			/* 等价于 1px 1px 1px 1px */
```













### 浮动float

```html
img{
float:right;
margin:0px 0px 15px 20px; 
}
```

![float实例](C:\Users\李子航\Desktop\java前端笔记\float实例.png)

color 文本颜色

background-color  背景颜色



### 文本样式text

---

|                                  | 属性                                        | 选项                                                    |
| -------------------------------- | ------------------------------------------- | ------------------------------------------------------- |
| 文本对齐方式                     | text-align                                  | center, left , right                                    |
| 字母间距(汉字)，单词间距，行间距 | letter-spacing , word-spacing , line-height | 如 letter-spacing：50px;                                |
| 大小写                           | text-transform                              | capitalize 首大写；uppecase 全大写lowercase全小写       |
| 首行缩进                         | text-indent                                 | 如 text-indent:50px;                                    |
| 下划线，上划线，删除线           | text-decoration                             | underline 下划线  line-through 删除线  overline上划线。 |
| 文本阴影                         | text-shadow: 10px 10px 5px red;             | 水平偏移量，竖直~, 模糊程度(选填)，颜色                 |

**text-decoration特别说明：**

1. 可以组合使用：text-decoration：underline  line-through；
2. text-decoration : none 会关闭元素上的所有装饰，可以用来去除链接上的下划线。 



`line-height` 行间距（行高）

<img src="../实例图片/屏幕截图 2021-02-28 150549.png" alt="屏幕截图 2021-02-28 150549" style="zoom:67%;" />

把 line-height 值设置为 height 一样大小的值可以实现单行文字的**垂直居中**；

如果一个标签没有定义 height 属性，那么其最终表现的高度是由 line-height 决定的。



### 字体font

---
|                    | 属性                          | 选项                                           |
| ------------------ | ----------------------------- | ---------------------------------------------- |
| 字体               | font-family : 微软雅黑 ;      |                                                |
| 字体大小           | font-size: 50px;              |                                                |
| 字体样式           | font-style                    | italic 斜体                                    |
| 字体粗细           | font-weight                   | 以100到700整百递增，还有bold粗bolder更粗等选项 |
| 字母小写转小型大写 | font-variant: all-small-caps; | 蒋小写改为小写大小的大写                       |





### 链接



CSS为链接设置样式

```html

  <style type="text/css">
    a:link{color:blue}
    a:visited{color:#b3d4fc}
    a:hover{color:red}
    a:active{color:mediumvioletred}
  </style>


  <a href="www.bilibili.com">这里是B站</a>



```
link未被访问链接；visited已被访问链接；hover鼠标停留；active正在被点击；

**为了使定义生效，他们的顺序不能变！**



### 列表

==list-style:none 将列表项目标记设置为无。==

list-style属性设置列表项目标记

| list-style:                | type position image      |
| -------------------------- | ------------------------ |
| list-style-type:           | 设置项目标记类型         |
| list-style-position:       | 设置在何处放置列表项标记 |
| list-style-image:url("  ") | 将图片设置为列表项目标记 |

**type可能的值**：circle 空心圆圈；square 实心方块；upper-roman 罗马数字；lower-alpha 小写abc。

 **position可能的值**：inside；outside（默认值），inside比outside更靠右一些。





### 鼠标停留过渡

将鼠标移至目标时发生的变化动作。


```html
    p{
      width: 100px;
      height: 100px;
      background-color: red;
    }
    p:hover{
      width: 200px;
      height: 200px;
      background-color: blue;
      transition-duration: 1s;
      transition-duration：1s；
    }
```

|                            | 效果                                                    |               |
| -------------------------- | ------------------------------------------------------- | ------------- |
| transition-delay：1s；     | 1s后开始过渡                                            | 过渡-延迟     |
| transition-duration：1s；  | 过渡开始后1s时间里平滑变化                              | 过渡-持续时间 |
| transition-timing-function | ease-in 先慢后快；ease-out 先快后慢；ease-in-out 快慢快 |               |



### 轮廓

轮廓位于边框边缘的外围，可以起到突出元素的作用。

|                         |          |              |
| ----------------------- | -------- | ------------ |
| outline: 宽度 样式 颜色 |          |              |
| outline-style           | 轮廓样式 | solid dotted |
| outline-color           | 轮廓颜色 |              |
| outline-weight          | 轮廓宽度 | 5px或thin等  |



**提示：**内边距、边框和外边距可以应用于一个元素的所有边，也可以应用于单独的边。

**提示：**外边距可以是负值，而且在很多情况下都要使用负值的外边距。

