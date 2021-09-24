

## 一、CSS基础部分

### 1. CSS选择器及其优先级

| 选择器         | 格式                 | 优先级权重 |
| -------------- | -------------------- | ---------- |
| id选择器       | #id                  | 100        |
| 类选择器       | .classname           | 10         |
| 属性选择器     | a[ref=“eee”]         | 10         |
| 伪类选择器     | li:last-child        | 10         |
| 标签选择器     | div                  | 1          |
| 伪元素选择器   | li:after             | 1          |
| 相邻兄弟选择器 | h1+p                 | 0          |
| 子选择器       | ul>li，直接子元素    | 0          |
| 后代选择器     | li a，所有层级子元素 | 0          |
| 通配符选择器   | *                    | 0          |



!important  >  内联样式   >  内部样式  >  外部样式

内部样式： id > （ 类 、伪类、属性）  > （ 标签 、伪元素） >   复合选择器   >   继承



需要注意的是：

- **!important声明的样式的优先级最高**
- 如果优先级相同，则最后出现的样式生效
- 继承得到的样式的优先级最低

  



### 2. CSS中可继承与不可继承属性有哪些

**一、无继承性的属性**

1. **display**：规定元素应该生成的框的类型
2. **文本属性**：

- vertical-align：垂直文本对齐
- text-decoration：规定添加到文本的装饰
- text-shadow：文本阴影效果
- white-space：空白符的处理
- unicode-bidi：设置文本的方向

1. **盒子模型的属性**：width、height、margin 、border、padding
2. **背景属性**：background、background-color、background-image、background-repeat、background-position、background-attachment
3. **定位属性**：float、clear、position、top、right、bottom、left、min-width、min-height、max-width、max-height、overflow、clip、z-index
4. **生成内容属性**：content、counter-reset、counter-increment
5. **轮廓样式属性**：outline-style、outline-width、outline-color、outline
6. **页面样式属性**：size、page-break-before、page-break-after
7. **声音样式属性**：pause-before、pause-after、pause、cue-before、cue-after、cue、play-during

**二、有继承性的属性**

1、字体系列属性

- font-family：字体系列
- font-weight：字体的粗细
- font-size：字体的大小
- font-style：字体的风格

2、文本系列属性

- text-indent：文本缩进
- text-align：文本水平对齐
- line-height：行高
- word-spacing：单词之间的间距
- letter-spacing：中文或者字母之间的间距
- text-transform：控制文本大小写（就是uppercase、lowercase、capitalize这三个）
- color：文本颜色

3、元素可见性：

- visibility：控制元素显示隐藏

4、列表布局属性：

- list-style：列表风格，包括list-style-type、list-style-image等

5、光标属性：

- cursor：光标显示为何种形态

### 3. display的属性值及其作用

| **属性值**   | **作用**                                                   |
| ------------ | ---------------------------------------------------------- |
| none         | 元素不显示，并从文档流中移除。                             |
| block        | 块类型。默认宽度为父元素宽度，可设置宽高，换行显示。       |
| inline       | 行内元素类型。默认宽度为内容宽度，不可设置宽高，同行显示。 |
| inline-block | 默认宽度为内容宽度，可以设置宽高，同行显示。               |
| list-item    | 像块类型元素一样显示，并添加样式列表标记。                 |
| table        | 此元素会作为块级表格来显示。                               |
| inherit      | 规定应该从父元素继承display属性的值。                      |



### 4. 单行、多行文本溢出隐藏

- 单行文本溢出

```css
overflow: hidden;            // 溢出隐藏
text-overflow:ellipsis;      // 文本溢出时发生的事，ellipsis表示用省略号代替溢出的文本
white-space: nowrap;         // 规定段落中的文本不进行换行
复制代码
```

- 多行文本溢出

```css
overflow: hidden;            // 溢出隐藏
text-overflow: ellipsis;     // 溢出用省略号显示
display:-webkit-box;         // 作为弹性伸缩盒子模型显示。
-webkit-box-orient:vertical; // 设置伸缩盒子的子元素排列方式：从上到下垂直排列
-webkit-line-clamp:3;        // 显示的行数
复制代码
```

注意：由于上面的三个属性都是CSS3的属性，没有浏览器可以兼容，所以要在前面加一个`-webkit-`来兼容一部分浏览器。

### 5. 隐藏元素的方法有哪些

- **display:none**：渲染树不会包含该渲染对象，因此该元素不会在页面中占据位置，也不会响应绑定的监听事件。
- **visibility:hidden**：元素在页面中仍占据空间，但是不会响应绑定的监听事件。
- **opacity:0**：将元素的透明度设置为 0，以此来实现元素的隐藏。元素在页面中仍然占据空间，并且能够响应元素绑定的监听事件。
- **position: absolute**：通过使用绝对定位将元素移除可视区域内，以此来实现元素的隐藏。
- **z-index 负值**：来使其他元素遮盖住该元素，以此来实现隐藏。
- **clip/clip-path** ：使用元素裁剪的方法来实现元素的隐藏，这种方法下，元素仍在页面中占据位置，但是不会响应绑定的监听事件。
- **transform:scale(0,0)**：将元素缩放为 0，以此来实现元素的隐藏。这种方法下，元素仍在页面中占据位置，但是不会响应绑定的监听事件。

### 6. link和@import的区别

两者都是外部引用CSS的方式，它们的区别如下：

- link是XHTML标签，除了加载CSS外，还可以定义RSS等其他事务；@import属于CSS范畴，只能加载CSS。
- **link引用CSS时，在页面载入时同时加载；@import需要页面网页完全载入以后加载。**
- link是XHTML标签，无兼容问题；@import是在CSS2.1提出的，低版本的浏览器不支持。
- link支持使用Javascript控制DOM去改变样式；而@import不支持。

### 7. transition和animation的区别

- **transition是过度属性**，强调过度，它的实现需要触发一个事件（比如鼠标移动上去，焦点，点击等）才执行动画。它类似于flash的补间动画，设置一个开始关键帧，一个结束关键帧。
- **animation是动画属性**，它的实现不需要触发事件，设定好时间之后可以自己执行，且可以循环一个动画。他也类似于flash的补间动画，但是他可以设置多个关键帧（用@keyframe定义）完成动画。

### 8. display:none与visibility:hidden的区别

这两个属性都是让元素隐藏，不可见。 **区别：** （1）**在渲染树中**

- `display:none`会让元素完全中渲染树中消失，渲染的时候不会占据任何空间；
- `visibility:hidden`不会让元素从渲染树中消失，渲染的元素还会占据相应的空间，只是内容不可见

（2）**继承**

- `display:none`是非继承属性，他的子孙节点会随着父节点从渲染树消失，通过修改子孙节点的属性也无法显示。
- `visibility:hidden`是继承属性，子孙节点消失是由于继承了`hidden`，通过设置`visibility:visible`可以让子孙节点显示。

（3）修改常规文档流中的元素的`display`通常会造成文档的重排，但是修改`visibility`属性只会造成本元素的重绘 （4）如果使用读屏器，设置为`display:none`的内容不会被读取，设置为`visibility:hidden`的内容会被读取。`visibility:hidden`

### 9. **伪元素和伪类的区别和作用？**

- 伪元素 -- 在内容元素的前后插入额外的元素或样式，但是这些元素实际上并不在文档中生成。它们只在外部显示可见，但不会在文档的源代码中找到它们，因此，称为“伪”元素。例如：

```css
p::before {content:"第一章：";}
p::after {content:"Hot!";}
p::first-line {background:red;}
p::first-letter {font-size:30px;}
复制代码
```

- 伪类 -- 将特殊的效果添加到特定选择器上。它是已有元素上添加类别的，不会产生新的元素。例如：

```css
a:hover {color: #FF00FF}
p:first-child {color: red}
复制代码
```



### 10. 对requestAnimationframe的理解

实现动画效果的方法比较多，Javascript 中可以通过定时器 setTimeout 来实现，css3 可以使用 transition 和 animation 来实现，HTML5 中的 canvas 也可以实现。除此之外，HTML5 还提供一个专门用于请求动画的API，那就是 requestAnimationFrame，顾名思义就是请求动画帧。 先看一下MDN对该方法的描述：

> window.requestAnimationFrame() 告诉浏览器——你希望执行一个动画，并且要求浏览器在下次重绘之前调用指定的回调函数更新动画。该方法需要传入一个回调函数作为参数，该回调函数会在浏览器下一次重绘之前执行

**语法：** `window.requestAnimationFrame(callback);` 其中，callback是**下一次重绘之前更新动画帧所调用的函数**(即上面所说的回调函数)。该回调函数会被传入DOMHighResTimeStamp参数，它表示requestAnimationFrame() 开始去执行回调函数的时刻。该方法属于**宏任务**，所以会在执行完微任务之后再去执行。

**取消动画：** 使用cancelAnimationFrame()来取消执行动画，该方法接收一个参数——requestAnimationFrame默认返回的id，cancelAnimationFrame只需要传入这个id就可以取消动画了。

**优势：**

- **CPU节能**：使用SetTinterval 实现的动画，当页面被隐藏或最小化时，SetTinterval 仍然在后台执行动画任务，由于此时页面处于不可见或不可用状态，刷新动画是没有意义的，完全是浪费CPU资源。而RequestAnimationFrame则完全不同，当页面处理未激活的状态下，该页面的屏幕刷新任务也会被系统暂停，因此跟着系统步伐走的RequestAnimationFrame也会停止渲染，当页面被激活时，动画就从上次停留的地方继续执行，有效节省了CPU开销。
- **函数节流**：在高频率事件( resize, scroll 等)中，为了防止在一个刷新间隔内发生多次函数执行，RequestAnimationFrame可保证每个刷新间隔内，函数只被执行一次，这样既能保证流畅性，也能更好的节省函数执行的开销，一个刷新间隔内函数执行多次时没有意义的，因为显示器每16.7ms刷新一次，多次绘制并不会在屏幕上体现出来。
- **减少DOM操作**： requestAnimationFrame 会把每一帧中的所有DOM操作集中起来，在一次重绘或回流中就完成，并且重绘或回流的时间间隔紧紧跟随浏览器的刷新频率，一般来说，这个频率为每秒60帧。

**setTimeout执行动画的缺点**： 它通过设定间隔时间来不断改变图像位置，达到动画效果。但是容易出现卡顿、抖动的现象；原因是：

- settimeout任务被放入异步队列，只有当主线程任务执行完后才会执行队列中的任务，因此实际执行时间总是比设定时间要晚；
- settimeout的固定时间间隔不一定与屏幕刷新时间相同，会引起丢帧。



### 11. 对盒模型的理解

CSS3中的盒模型有以下两种：标准盒模型、IE盒模型 ![img](images/1603600820746-e10daafa-451a-454e-9705-f8c358769d5b.png) ![img](images/1603600820555-dc6ed390-d47e-412b-942a-857bbe5f280d.png) 盒模型都是由四个部分组成的，分别是margin、border、padding和content。

标准盒模型和IE盒模型的区别在于设置width和height时，所对应的范围不同：

- 标准盒模型的width和height属性的范围只包含了content，
- IE盒模型的width和height属性的范围包含了border、padding和content。

即IE盒模型宽高设置的是左外边框到右外边框，添加内边距或边框：盒子宽高不变，content缩小。

即IE盒模型宽高设置的是content，添加内边距或边框：盒子宽高变大，content不变。



一般来说，我们可以通过修改元素的box-sizing属性来改变元素的盒模型。

- `box-sizeing:content-box`表示标准盒模型（默认值）
- `box-sizeing:border-box`表示IE盒模型（也就是怪异盒模型）

### 12. Canvas和SVG的区别

**（1）SVG：** SVG可缩放矢量图形（Scalable Vector Graphics）是基于可扩展标记语言XML描述的2D图形的语言，SVG基于XML就意味着SVG DOM中的每个元素都是可用的，可以为某个元素附加Javascript事件处理器。在 SVG 中，每个被绘制的图形均被视为对象。如果 SVG 对象的属性发生变化，那么浏览器能够自动重现图形。

其特点如下：

- 不依赖分辨率
- 支持事件处理器
- 最适合带有大型渲染区域的应用程序（比如谷歌地图）
- 复杂度高会减慢渲染速度（任何过度使用 DOM 的应用都不快）
- 不适合游戏应用

**（2）Canvas：** Canvas是画布，通过Javascript来绘制2D图形，是逐像素进行渲染的。其位置发生改变，就会重新进行绘制。

其特点如下：

- 依赖分辨率
- 不支持事件处理器
- 弱的文本渲染能力
- 能够以 .png 或 .jpg 格式保存结果图像
- 最适合图像密集型的游戏，其中的许多对象会被频繁重绘

注：矢量图，也称为面向对象的图像或绘图图像，在数学上定义为一系列由线连接的点。矢量文件中的图形元素称为对象。每个对象都是一个自成一体的实体，它具有颜色、形状、轮廓、大小和屏幕位置等属性。

### 13. CSS中有哪些是空元素？

空元素，即没有内容的HTML元素。空元素是在开始标签中关闭的，也就是说空元素没有闭合标签的。 常见的有：`<br>`、`<hr>`、`<img>`、`<input>`、`<link>`、`<meta>` 鲜见的有：`<area>`、`<base>`、`<col>`、`<colgroup>`、`<command>`、`<embed>`、`<keygen>`、`<param>`、`<source>`、`<track>`、`<wbr>`

### 14. CSS3中有哪些新特性

1. 颜色：新增 RGBA，HSLA 模式 

2. 文字阴影（text-shadow、） 
3. 3.边框： 圆角（border-radius）边框阴影： box-shadow 
4. 盒子模型：box-sizing 
5. 背景：background-size 设置背景图片的尺寸 background-origin 设置背景图片的原点 background-clip 设置背景图片的裁切区域，以”，”分隔可以设置多背景，用于自适应布局
6. 渐变：linear-gradient、radial-gradient 
7. 过渡：transition，可实现动画 
8. 自定义动画 animate @keyfrom 
9. 在 CSS3 中唯一引入的伪元素是 ：：selection.
10.  媒体查询，多栏布局 @media screen and (width:800px){ … }
11. border-image 
12. 2D 转换：transform：translate(x，y) rotate(x，y) skew(x，y) scale(x，y) 
13. 3D 转换 14 字体图标 font-face 15 弹性布局 flex



### 16. 常见的图片格式有哪些，使用场景

（1）**BMP**，是无损的、既支持索引色也支持直接色的、点阵图。这种图片格式几乎没有对数据进行压缩，所以BMP格式的图片通常 具有较大的文件大小。

（2）**GIF**是无损的、采用索引色的、点阵图。采用LZW压缩算法进行编码。文件小，是GIF格式的优点，同时，GIF格式还具 有支持动画以及透明的优点。但，GIF格式仅支持8bit的索引色，所以GIF格式适用于对色彩要求不高同时需要文件体积 较小的场景。

（3）**JPEG**是有损的、采用直接色的、点阵图。JPEG的图片的优点，是采用了直接色，得益于更丰富的色彩，JPEG非常适合用来 存储照片，与GIF相比，JPEG不适合用来存储企业Logo、线框类的图。因为有损压缩会导致图片模糊，而直接色的选用， 又会导致图片文件较GIF更大。

（4）**PNG-8**是无损的、使用索引色的、点阵图。PNG是一种比较新的图片格式，PNG-8是非常好的GIF格式替代者，在可能的 情况下，应该尽可能的使用PNG-8而不是GIF，因为在相同的图片效果下，PNG-8具有更小的文件体积。除此之外，PNG-8还支持透明度的调节，而GIF并不支持。现在，除非需要动画的支持，否则我们没有理由使用GIF而不是PNG-8。

（5）**PNG-24**是无损的、使用直接色的、点阵图。PNG-24的优点在于，它压缩了图片的数据，使得同样效果的图片，PNG-24格 式的文件大小要比BMP小得多。当然，PNG24的图片还是要比JPEG、GIF、PNG-8大得多。

（6）**SVG**是无损的、矢量图。SVG是矢量图。这意味着SVG图片由直线和曲线以及绘制它们的方法组成。当你放大一个SVG图 片的时候，你看到的还是线和曲线，而不会出现像素点。这意味着SVG图片在放大时，不会失真，所以它非常适合用来绘制企 业Logo、Icon等。

（7）**WebP**是谷歌开发的一种新图片格式，WebP是同时支持有损和无损压缩的、使用直接色的、点阵图。从名字就可以看出来它是 为Web而生的，什么叫为Web而生呢？就是说相同质量的图片，WebP具有更小的文件体积。现在网站上充满了大量的图片， 如果能够降低每一个图片的文件大小，那么将大大减少浏览器和服务器之间的数据传输量，进而降低访问延迟，提升访问体验。

- 在无损压缩的情况下，相同质量的WebP图片，文件大小要比PNG小26%；
- 在有损压缩的情况下，具有相同图片精度的WebP图片，文件大小要比JPEG小25%~34%；
- WebP图片格式支持图片透明度，一个无损压缩的WebP图片，如果要支持透明度只需要22%的格外文件大小。

目前只有Chrome浏览器和Opera浏览器支持WebP格式，兼容性不太好。

### 17. 阐述一下 CSSSprites

CSSSprites（精灵图），把多个小的图片整合到一张大的图片上，然后利用CSS的background-image，background-repeat，background-position的组合进行背景定位。利用CSSSprites能很好地减少网页的http请求，从而很好的提高页面的性能；CSSSprites能减少图片的字节。

**优点：**

- 减少HTTP请求数，极大地提高页面加载速度
- 增加图片信息重复度，提高压缩比，减少图片大小
- 更换风格方便，只需在一张或几张图片上修改颜色或样式即可实现

**缺点：**

- 图片合并麻烦
- 维护麻烦，修改一个图片可能需要重新布局整个图片，样式



### 18. 什么是物理像素，逻辑像素和像素密度，为什么在移动端开发时需要用到@3x, @2x这种图片？

物理像素：屏幕的分辨率。屏幕上真实存在的像素点的个数。

逻辑像素：css中的像素单位，px。

PC端，1px对应一个物理像素。

移动端，不一定，由像素密度决定。

以 iPhone XS 为例，当我们在写 CSS 代码时，针对于我们的单位 px，其宽度为 414px & 896px，也就是说当我们赋予一个 DIV 414px，这个 DIV 就会填满手机的宽度；而实际测量这部手机的物理像素，实际为 1242*2688 物理像素；经过计算可知，1242/414=3，也就是说，在单边上，一个逻辑像素=3个物理像素（1px对应3个物理像素点），我们就说这个屏幕的像素密度为 3，也就是我们常说的 3 倍屏。

为什么会需要这样呢？因为同等尺寸的手机有 1080p、2K甚至4K的分辨率，通过让像素点变小使同样大小的尺寸上塞入了更多的像素点，屏幕更加清晰锐利。

<img src="images/image-20210524161035660.png" alt="image-20210524161035660" style="zoom:80%;" />

如果都是1px对应一个像素点，CSS中 2px的线在1倍屏上比2倍屏上的线要长一倍。为了在不同手机上展示相同大小，就需要在2倍屏手机上，1px对应两个像素点才能让 2px的线在两个屏幕上长度相同。

图片大小采用的是逻辑像素。为了和1倍屏显示相同大小的尺寸，一张 2 * 2px的图片在2倍屏上被拉伸为 4 *4px大小，图片会被拉伸模糊失真。

所以就有了2倍图概念，在2倍屏上使用2倍图。如在1倍屏上使用 2*2px的图片，在2倍屏上使用 4 *4px的图片，手动将其缩小为 2 *2px，这样在屏幕上被拉伸为 4 *4px大小时因为其本身就是这么大就不会模糊

使用 CSS 媒体查询来判断不同的像素密度，从而选择不同的图片:

```javascript
my-image { background: (low.png); }
@media only screen and (min-device-pixel-ratio: 1.5) {
  #my-image { background: (high.png); }
}
```





### 20. 对**line-height 的理解及其赋值方式**

**（1）line-height的概念：**

- line-height 指一行字的高度，包含了字间距，实际上是下一行基线到上一行基线距离
- **如果一个标签没有定义 height 属性，那么其最终表现的高度是由 line-height 决定的**
- 一个容器没有设置高度，那么撑开容器高度的是 line-height 而不是容器内的文字内容
- 把 line-height 值设置为 height 一样大小的值可以实现单行文字的垂直居中
- line-height 和 height 都能撑开一个高度，height 会触发 haslayout，而 line-height 不会

**（2）line-height 的赋值方式：**

- 带单位：px 是固定值，而 em 会参考父元素 font-size 值计算自身的行高
- 纯数字：会把比例传递给后代。例如，父级行高为 1.5，子元素字体为 18px，则子元素行高为 1.5 * 18 = 27px
- 百分比：将计算后的值传递给后代



### 21. li 与 li 之间有看不见的空白间隔是什么原因引起的？有什么解决办法？

通过将 li设置 `display: inline-block | inline `，可以将 ul中所有的 li标签置为一行，但每个 li标签之间都有空白间隔，这是为什么？

因为HTML中的 li标签原本是块级元素，现在变成了行内块级元素，**浏览器会把inline元素间的空白字符（空格、换行、Tab等）渲染成一个空格。**

**解决办法：**

（1）将所有`<li>`写在同一行。不足：代码不美观。

```html
<ul>
  <li class="part1"></li><li class="part2"></li><li class="part3"></li><li class="part4"></li>
</ul>
```

（2）为`<li>`设置float:left。不足：有些容器是不能设置浮动，如左右切换的焦点图等。

（3）将`<ul>`内的字符尺寸直接设为0，即font-size:0。不足：`<ul>`中的其他字符尺寸也被设为0，需要额外重新设定其他字符尺寸，且在Safari浏览器依然会出现空白间隔。

（4）消除`<ul>`的字符间隔letter-spacing:-8px，不足：这也设置了`<li>`内的字符间隔，因此需要将`<li>`内的字符间隔设为默认letter-spacing:normal。

### 22. CSS 优化、提高性能的方法有哪些？

**加载性能：**

（1）css压缩：将写好的css进行打包压缩，可以减少很多的体积。

（2）css单一样式：当需要下边距和左边距的时候，很多时候选择:margin:top 0 bottom 0;但margin-bottom:bottom;margin-left:left;执行的效率更高。

（3）减少使用@import,而建议使用link，因为后者在页面加载时一起加载，前者是等待页面加载完成之后再进行加载。

**选择器性能：**

（1）关键选择器（key selector）。选择器的最后面的部分为关键选择器（即用来匹配目标元素的部分）。CSS选择符是从右到左进行匹配的。当使用后代选择器的时候，浏览器会遍历所有子元素来确定是否是指定的元素等等；

（2）如果规则拥有ID选择器作为其关键选择器，则不要为规则增加标签。过滤掉无关的规则（这样样式系统就不会浪费时间去匹配它们了）。

（3）避免使用通配规则，如*{}计算次数惊人！只对需要用到的元素进行选择。

（4）尽量少的去对标签进行选择，而是用class。

（5）尽量少的去使用后代选择器，降低选择器的权重值。后代选择器的开销是最高的，尽量将选择器的深度降到最低，最高不要超过三层，更多的使用类来关联每一个标签元素。

（6）了解哪些属性是可以通过继承而来的，然后避免对这些属性重复指定规则。

**渲染性能：**

（1）慎重使用高性能属性：浮动、定位。

（2）尽量减少页面重排、重绘。

（3）去除空规则：｛｝。空规则的产生原因一般来说是为了预留样式。去除这些空规则无疑能减少css文档体积。

（4）属性值为0时，不加单位。

（5）属性值为浮动小数0.**，可以省略小数点之前的0。

（6）标准化各种浏览器前缀：带浏览器前缀的在前。标准属性在后。

（7）不使用@import前缀，它会影响css的加载速度。

（8）选择器优化嵌套，尽量避免层级过深。

（9）css雪碧图，同一页面相近部分的小图标，方便使用，减少页面的请求次数，但是同时图片本身会变大，使用时，优劣考虑清楚，再使用。

（10）正确使用display的属性，由于display的作用，某些样式组合会无效，徒增样式体积的同时也影响解析性能。

（11）不滥用web字体。对于中文网站来说WebFonts可能很陌生，国外却很流行。web fonts通常体积庞大，而且一些浏览器在下载web fonts时会阻塞页面渲染损伤性能。

**可维护性、健壮性：**

（1）将具有相同属性的样式抽离出来，整合并通过class在页面中进行使用，提高css的可维护性。

（2）样式与内容分离：将css代码定义到外部css中。



## 二、页面布局

### 1. 常见的CSS布局单位

常用的布局单位包括像素（`px`），百分比（`%`），`em`，`rem`，`vw/vh`。

**（1）像素**（`px`）是页面布局汇总的基础，一个像素表示终端（电脑、手机、平板等）屏幕所能显示的最小的区域，像素分为两种类型：CSS像素和物理像素。两者区别如下：

- **CSS像素**：为web开发者提供，在CSS中使用的一个抽象单位；
- **物理像素**：只与设备的硬件密度有关，任何设备的物理像素都是固定的。

**（2）百分比**（`%`），当浏览器的宽度或者高度发生变化时，通过百分比单位可以使得浏览器中的组件的宽和高随着浏览器的变化而变化，从而实现响应式的效果。一般我们的直观理解都会认为子元素的百分比完全相对于直接父元素。

**（3）em和rem**相对于px更具灵活性，它们都是相对长度单位，而它们之间的区别可以用一句话来概括：**em相对于父元素，rem相对于根元素。**

- **em：** 文本相对长度单位。相对于当前对象内文本的字体尺寸`font-size`。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸(默认16px)。(相对父元素的字体大小倍数)
- **rem：** rem是CSS3新增的一个相对单位（root em，根em），相对于根元素(即html元素)font-size计算值的倍数只相对于根元素的大小。**作用**：利用rem可以实现简单的响应式布局，可以利用html元素中字体的大小与屏幕间的比值设置font-size的值实现当屏幕分辨率变化时让元素也变化。

**（4）vw/vh**是与视图窗口有关的单位，vw表示相对于视图窗口的宽度，vh表示相对于视图窗口高度，除了vw和vh外，还有vmin和vmax两个相关的单位。

- vw：相对于视窗的宽度，视窗宽度是100vw，30vw表示视窗宽度的30%
- vh：相对于视窗的高度，视窗高度是100vh
- vmin：vw和vh中的较小值
- vmax：vw和vh中的较大值

**vw/vh** 和百分比很类似，但是还是有区别的：

- 百分比（`%`）：大部分相对于祖先元素，也有相对于自身的情况比如（border-radius、translate等)
- vw/vm：相对于视窗的尺寸

### 3. 两栏布局的实现

一般两栏布局指的是左边一栏宽度固定，右边一栏宽度自适应，两栏布局的具体实现：

- 利用浮动，将左边元素宽度设置为200px，并且设置向左浮动。将右边元素的margin-left设置为200px，宽度设置为auto（默认为auto，撑满整个父元素）。

```css
.outer {
  height: 100px;
}

.left {
  float: left;

  height: 100px;
  width: 200px;

  background: tomato;
}

.right {
  margin-left: 200px;

  width: auto;
  height: 100px;

  background: gold;
}
复制代码
```

- 利用flex布局，将左边元素的放大和缩小比例设置为0，基础大小设置为200px。将右边的元素的放大比例设置为1，缩小比例设置为1，基础大小设置为auto。

```css
.outer {
  display: flex;

  height: 100px;
}

.left {
  flex-shrink: 0;
  flex-grow: 0;
  flex-basis: 200px;

  background: tomato;
}

.right {
  flex: auto;
  /*11auto*/

  background: gold;
}
复制代码
```

- 利用绝对定位布局的方式，将父级元素设置相对定位。左边元素设置为absolute定位，并且宽度设置为

200px。将右边元素的margin-left的值设置为200px。

```css
.outer {
  position: relative;
  height: 100px;
}
.left {
  position: absolute;
  width: 200px;
  height: 100px;
  background: tomato;
}
.right {
  margin-left: 200px;
  height: 100px;
  background: gold;
}
复制代码
```

- 利用绝对定位的方式，将父级元素设置为相对定位。左边元素宽度设置为200px，右边元素设置为绝对定位，左边定位为200px，其余方向定位为0。

```css
.outer {
  position: relative;
  height: 100px;
}
.left {
  width: 200px;
  height: 100px;
  background: tomato;
}
.right {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 200px;
  background: gold;
}
复制代码
```



### 4. 三栏布局的实现

三栏布局一般指的是页面中一共有三栏，左右两栏宽度固定，中间自适应的布局，三栏布局的具体实现：

- 利用绝对定位的方式，左右两栏设置为绝对定位，中间设置对应方向大小的margin的值。

```css
.outer {
  position: relative;
  height: 100px;
}

.left {
  position: absolute;

  width: 100px;
  height: 100px;
  background: tomato;
}

.right {
  position: absolute;
  top: 0;
  right: 0;

  width: 200px;
  height: 100px;
  background: gold;
}

.center {
  margin-left: 100px;
  margin-right: 200px;
  height: 100px;
  background: lightgreen;
}
复制代码
```

- 利用flex布局的方式，左右两栏的放大和缩小比例都设置为0，基础大小设置为固定的大小，中间一栏设置为auto

```css
.outer {
  display: flex;
  height: 100px;
}

.left {
  flex: 00100px;
  background: tomato;
}

.right {
  flex: 00200px;
  background: gold;
}

.center {
  flex: auto;
  background: lightgreen;
}
复制代码
```

- 利用浮动的方式，左右两栏设置固定大小，并设置对应方向的浮动。中间一栏设置左右两个方向的margin值，注意这种方式，中间一栏必须放到最后

```css
.outer {
  height: 100px;
}

.left {
  float: left;
  width: 100px;
  height: 100px;
  background: tomato;
}

.right {
  float: right;
  width: 200px;
  height: 100px;
  background: gold;
}

.center {
  height: 100px;
  margin-left: 100px;
  margin-right: 200px;
  background: lightgreen;
}

复制代码
```

- 圣杯布局，利用浮动和负边距来实现。父级元素设置左右的 padding，三列均设置向左浮动，中间一列放在最前面，宽度设置为父级元素的宽度，因此后面两列都被挤到了下一行，通过设置 margin 负值将其移动到上一行，再利用相对定位，定位到两边。

```css
.outer {
  height: 100px;
  padding-left: 100px;
  padding-right: 200px;
}

.left {
  position: relative;
  left: -100px;

  float: left;
  margin-left: -100%;

  width: 100px;
  height: 100px;
  background: tomato;
}

.right {
  position: relative;
  left: 200px;

  float: right;
  margin-left: -200px;

  width: 200px;
  height: 100px;
  background: gold;
}

.center {
  float: left;

  width: 100%;
  height: 100px;
  background: lightgreen;
}
复制代码
```

- 双飞翼布局，双飞翼布局相对于圣杯布局来说，左右位置的保留是通过中间列的 margin 值来实现的，而不是通过父元素的 padding 来实现的。本质上来说，也是通过浮动和外边距负值来实现的。

```css
.outer {
  height: 100px;
}

.left {
  float: left;
  margin-left: -100%;

  width: 100px;
  height: 100px;
  background: tomato;
}

.right {
  float: left;
  margin-left: -200px;

  width: 200px;
  height: 100px;
  background: gold;
}

.wrapper {
  float: left;

  width: 100%;
  height: 100px;
  background: lightgreen;
}

.center {
  margin-left: 100px;
  margin-right: 200px;
  height: 100px;
}
复制代码
```



### 5. 水平垂直居中的实现

水平垂直居中的具体实现：

- 利用绝对定位，先将元素的左上角通过top:50%和left:50%定位到页面的中心，然后再通过translate来调整元素的中心点到页面的中心。该方法需要**考虑浏览器兼容问题。**

```css
.parent {
    position: relative;
}
 
.child {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50%);
}
复制代码
```

- 利用绝对定位，设置四个方向的值都为0，并将margin设置为auto，由于宽高固定，因此对应方向实现平分，可以实现水平和垂直方向上的居中。该方法适用于**盒子有宽高**的情况

```css
.parent {
    position: relative;
}
 
.child {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto;
}
复制代码
```

- 利用绝对定位，先将元素的左上角通过top:50%和left:50%定位到页面的中心，然后再通过margin负值来调整元素的中心点到页面的中心。该方法适用于**盒子宽高已知**的情况

```css
.parent {
    position: relative;
}
 
.child {
    position: absolute;
    top: 50%;
    left: 50%;
    margin-top: -50px;     /* 自身 height 的一半 */
    margin-left: -50px;    /* 自身 width 的一半 */
}
复制代码
```

- 使用flex布局，通过align-items:center和justify-content:center设置容器的垂直和水平方向上为居中对齐，然后它的子元素也可以实现垂直和水平的居中。该方法要**考虑兼容的问题**，该方法在移动端用的较多

```css
.parent {
    display: flex;
    justify-content:center;
    align-items:center;
}
复制代码
```



### 6. 如何根据设计稿进行移动端适配？

移动端适配主要有两个维度：

- **适配不同像素密度**。这一部分比较简单，针对不同的像素密度，使用 CSS 媒体查询，选择不同精度的图片，以保证图片不会失真
- **适配不同屏幕大小**。由于不同的屏幕有着不同的逻辑像素大小，所以如果直接使用 px 作为开发单位，会使得开发的页面在某一款手机上可以准确显示，但是在另一款手机上就会失真。为了适配不同屏幕的大小，应按照比例来还原设计稿的内容。

为了能让页面的尺寸自适应，可以使用 rem，em，vw，vh 等相对单位。

### 7. 对Flex布局的理解及其使用场景

Flex是FlexibleBox的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。

任何一个容器都可以指定为Flex布局。行内元素也可以使用Flex布局。注意，设为Flex布局以后，子元素的float、cl ear和vertical-align属性将失效。

采用Flex布局的元素，称为Flex容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为Flex 项目（flex item），简称"项目"。

容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis），项目默认沿主轴排列。

以下6个属性设置在**容器上**：

- flex-direction属性决定主轴的方向（即项目的排列方向）。
- flex-wrap属性定义，如果一条轴线排不下，如何换行。
- flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。
- justify-content属性定义了项目在主轴上的对齐方式。
- align-items属性定义项目在交叉轴上如何对齐。
- align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

以下6个属性设置在**项目上**：

- order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。
- flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。
- flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。
- flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。
- flex属性是flex-grow，flex-shrink和flex-basis的简写，默认值为0 1 auto。
- align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

**简单来说：**

flex布局是CSS3新增的一种布局方式，我们可以通过将一个元素的display属性值设置为flex从而使它成为一个flex 容器，它的所有子元素都会成为它的项目。

一个容器默认有两条轴，一个是水平的主轴，一个是与主轴垂直的交叉轴。我们可以使用flex-direction来指定主轴的方向。 我们可以使用justify-content来指定元素在主轴上的排列方式，使用align-items来指定元素在交叉轴上的排列方式。还 可以使用flex-wrap来规定当一行排列不下时的换行方式。

对于容器中的项目，我们可以使用order属性来指定项目的排列顺序，还可以使用flex-grow来指定当排列空间有剩余的时候，项目的放大比例。还可以使用flex-shrink来指定当排列空间不足时，项目的缩小比例。



## 三、定位与浮动



### 1. 为什么需要清除浮动？清除浮动的方式

**浮动的定义：** 非IE浏览器下，容器不设高度且子元素浮动时，容器高度不能被内容撑开。 此时，内容会溢出到容器外面而影响布局。这种现象被称为浮动溢出。



**清除浮动的方式如下：**

- 给父级div定义大于浮动框的`height`属性

- 最后一个浮动元素之后添加一个空的div标签，并添加`clear:both`样式

- 容器使用 `::after` 在容器的最后创建伪元素，并添加`clear:both`样式

- 包含浮动元素的父级标签变为BFC，一般使用 `overflow:hedden`方式

  



### 2. 使用 clear 属性清除浮动的原理？

使用clear属性清除浮动，其语法如下：

```css
clear:none|left|right|both
```

还需要注意的一点是clear属性指的是元素盒子的边不能和前面的浮动元素相邻，注意这里“**前面的**”3个字，也就是clear属性对“后面的”浮动元素是不闻不问的。所以设置 `clear`的元素需要定义在容器的最后，保证前面的所有浮动元素都被作用到。

一般使用伪元素的方式清除浮动：

```css
.clear::after{
  content:'';
  display:block;
  clear:both;
}
```

clear属性只有块级元素才有效的，而::after等伪元素默认都是内联水平，这就是借助伪元素清除浮动影响时需要设置display属性值的原因。



### 3. 对BFC的理解，如何创建BFC

块格式化上下文（Block Formatting Context，BFC）

通俗来讲：

具有 BFC 特性的元素可以看作是一个与外界隔离的独立容器，容器内的布局不会影响到外面。同样外面的布局上影响到容器里面。如：

- 具有 BFC 特性的元素不会与浮动的容器发生重叠

- 计算 BFC 的高度时，浮动元素也参与计算

- 每个元素的左margin值和容器的左border相接触



**创建BFC的条件：**

- 根元素：body
- 元素设置浮动：float 除 none 以外的值
- 元素设置绝对定位：position (absolute、fixed)
- display 值为：inline-block、table-cell、table-caption、flex等
- overflow 值为：hidden、auto、scroll



**BFC的作用：**

- **解决两个元素margin的重叠问题**：相邻父子元素的外边距重叠问题：将父元素变为BFC，父子元素就不会有外边距重叠问题。相邻元素的上下外边距重叠问题：将其中一个元素或两个都变为BFC的子元素或将底部元素变为BFC。
- **解决高度塌陷的问题**：我们在父元素没有设置高度，对子元素设置浮动后，父元素会发生高度塌陷，也就是父元素的高度变为0。解决这个问题，只需要把父元素变成一个BFC就行了。常用的办法是给父元素设置`overflow:hidden`。
- **创建自适应两栏布局**：可以用来创建自适应两栏布局：左边的宽度固定，右边的宽度自适应。

```css
.left{
     width: 100px;
     height: 200px;
     background: red;
     float: left;
 }
 .right{
     height: 300px;
     background: blue;
     overflow: hidden;
 }
 
<div class="left"></div>
<div class="right"></div>
复制代码
```

左侧设置`float:left`，右侧设置`overflow: hidden`。这样右边就触发了BFC，BFC的区域不会与浮动元素发生重叠，所以两侧就不会发生重叠，实现了自适应两栏布局。



### 4. 什么是margin重叠问题？如何解决？

**问题描述：** 两个块级元素的上外边距和下外边距可能会合并（折叠）为一个外边距，其大小会取其中外边距值大的那个，这种行为就是外边距折叠。需要注意的是，**浮动的元素和绝对定位**这种脱离文档流的元素的外边距不会折叠。重叠只会出现在**垂直方向**。

**计算原则：** 折叠合并后外边距的计算原则如下：

- 如果两者都是正数，那么就去最大者
- 如果是一正一负，就会正值减去负值的绝对值
- 两个都是负值时，用0减去两个中绝对值大的那个

**解决办法：**

对于折叠的情况，主要有两种：**兄弟之间重叠**和**父子之间重叠**

（1）兄弟之间重叠

- 底部元素变为行内盒子：`display: inline-block`
- 底部元素设置浮动：`float`
- 底部元素的position的值为`absolute/fixed`

（2）父子之间重叠

- 父元素加入：`overflow: hidden`
- 父元素添加透明边框：`border:1px solid transparent`
- 子元素变为行内盒子：`display: inline-block`
- 子元素加入浮动属性或定位



### 5. 元素的层叠顺序

层叠顺序，英文称作 stacking order，表示元素发生层叠时有着特定的垂直显示顺序。下面是盒模型的层叠规则：

![img](images/1603553952688-ad155942-9d1d-4e4b-86a7-0f7dca46e6d1.png)

对于上图，由上到下分别是：

（1）背景和边框：建立当前层叠上下文元素的背景和边框。

（2）负的z-index：当前层叠上下文中，z-index属性值为负的元素。

（3）块级盒：文档流内非行内级非定位后代元素。

（4）浮动盒：非定位浮动元素。

（5）行内盒：文档流内行内级非定位后代元素。

（6）z-index:0：层叠级数为0的定位元素。

（7）正z-index：z-index属性值为正的定位元素。 **

**特别说明:** 当定位元素z-index:auto，生成盒在当前层叠上下文中的层级为 0，不会建立新的层叠上下文，除非是根元素。



### 7. **display、float、position的关系**



总的来说，可以把它看作是一个类似优先级的机制，

1. display属性为none，position和float属性的值不影响元素最后的表现。
2. "position:absolute"和"position:fixed"存在的时候浮动不起作用，'display'的值也需要调整为block；注意，如果position的值为relative并且float属性的值存在，则relative相对于浮动后的最终位置定位。
3. 元素的'float'特性的值不是"none"的时候或者它是根元素的时候，调整'display'的值为block；
4. 非根元素，并且非浮动元素，并且非绝对定位的元素，'display'特性值同设置值。





## 四、场景应用

### 1. 实现一个三角形

CSS绘制三角形主要用到的是border属性，也就是边框。 我们平时在给盒子设置边框的时候，往往都设置很窄，就可能误以为边框是由矩形组成的。实际上，border属性是右三角形组成的，下面我们看一个例子：

```css
div {
    width: 0;
    height: 0;
    border: 100px solid;
    border-color: orange blue red green;
}
```

我们将元素的长宽都设置为0，显示出来的效果是这样的： ![img](images/1603636245125-d60dca78-0577-4aa1-8809-f1d38594889a.png) 所以我们就可以根据border这个特性来绘制三角形：

**（1）三角1**

```css
div {
    width: 0;
    height: 0;
    border-top: 50px solid red;
    border-right: 50px solid transparent;
    border-left: 50px solid transparent;
}
复制代码
```

![img](images/1603636245420-28c28277-5074-4725-9386-ffc955cf950a.png)

**（2）三角2**

```css
div {
    width: 0;
    height: 0;
    border-bottom: 50px solid red;
    border-right: 50px solid transparent;
    border-left: 50px solid transparent;
}
复制代码
```

![img](images/1603636245172-36f955bd-075b-442a-b88b-6c084c66ed25.png)

**（3）三角3**

```css
div {
    width: 0;
    height: 0;
    border-left: 50px solid red;
    border-top: 50px solid transparent;
    border-bottom: 50px solid transparent;
}
复制代码
```

![img](images/1603636245082-84a06746-dfc7-4782-a0d4-27d521aecac7.png)

**（4）三角4**

```css
div {
    width: 0;
    height: 0;
    border-right: 50px solid red;
    border-top: 50px solid transparent;
    border-bottom: 50px solid transparent;
}
复制代码
```

![img](images/1603636245064-ecd01197-99fc-476e-897f-a4165b55792a.png)

**（5）三角5**

```css
div {
    width: 0;
    height: 0;
    border-top: 100px solid red;
    border-right: 100px solid transparent;
}
复制代码
```

![img](images/1603636245095-5b40d585-7e68-4bb0-aaef-6c8fce7d36b8.png) 还有很多，就不一一实现了，总体的原则就是通过上下左右边框来控制三角形的方向，用边框的宽度比来控制三角形的角度。

### 2. 实现一个扇形

用CSS实现扇形的思路和三角形基本一致，就是多了一个圆角的样式，实现一个90°的扇形：

```css
div{
    border: 100px solid transparent;
    width: 0;
    heigt: 0;
    border-radius: 100px;
    border-top-color: red;
}
复制代码
```

![img](images/1603636444767-26da7bbe-5479-44e2-9088-50c9211d6c0d.png)

### 3. 实现一个宽高自适应的正方形

- 利用vw来实现

```css
.square {
  width: 10%;
  height: 10vw;
  background: tomato;
}
复制代码
```

- 利用元素的margin/padding百分比是相对父元素width的性质来实现

```css
.square {
  width: 20%;
  height: 0;
  padding-top: 20%;
  background: orange;
}
复制代码
```

- 利用子元素的margin-top的值来实现

```css
.square {
  width: 30%;
  overflow: hidden;
  background: yellow;
}
.square::after {
  content: '';
  display: block;
  margin-top: 100%;
}
复制代码
```



### 4. 画一条0.5px的线

- **采用transform: scale()的方式**，该方法用来定义元素的2D 缩放转换：

```css
transform: scale(0.5,0.5);
```

- **采用meta viewport的方式**

```css
<meta name="viewport" content="width=device-width, initial-scale=0.5, minimum-scale=0.5, maximum-scale=0.5"/>
```

这样子就能缩放到原来的0.5倍，如果是1px那么就会变成0.5px。viewport只针对于移动端，只在移动端上才能看到效果



### 5. 设置小于12px的字体

在谷歌下css设置字体大小为12px及以下时，显示都是一样大小，都是默认12px。

解决办法：

- 使用Webkit的内核的-webkit-text-size-adjust的私有CSS属性来解决，只要加了-webkit-text-size-adjust:none;字体大小就不受限制了。但是chrome更新到27版本之后就不可以用了。所以高版本chrome谷歌浏览器已经不再支持-webkit-text-size-adjust样式，所以要使用时候慎用。
- 使用css3的transform缩放属性-webkit-transform:scale(0.5); 注意-webkit-transform:scale(0.75);收缩的是整个元素的大小，这时候，如果是内联元素，必须要将内联元素转换成块元素，可以使用display：block/inline-block/...；
- 使用图片：如果是内容固定不变情况下，使用将小于12px文字内容切出做图片，这样不影响兼容也不影响美观。


作者：CUGGZ
链接：https://juejin.cn/post/6905539198107942919
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。