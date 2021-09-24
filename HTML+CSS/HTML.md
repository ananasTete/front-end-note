





### 块级元素和行内元素



| 块级元素                                 | 行内元素                             |
| ---------------------------------------- | ------------------------------------ |
| 自占一行                                 |                                      |
| 默认宽度是它本身父容器的100%，与内容无关 | 不能设置元素宽高，完全靠内容撑开宽高 |

块级元素和行内元素转换：设置元素的display属性

| none         | 元素不会被显示                                     |
| ------------ | -------------------------------------------------- |
| block        | 此元素将显示为块级元素，此元素前后会带有换行符。   |
| inline       | 默认。此元素会被显示为行内元素，元素前后没有换行符 |
| inline-block | 既可以设置长宽，又可以和其他行内元素并排。         |
| inhert       | 继承父元素的display                                |

常见的块级和行内元素

|              |                                        |
| ------------ | -------------------------------------- |
| 行内元素     | a,b,span,button,strong,select,textarea |
| 块级元素     | div,ul,ol,table                        |
| 行内块级元素 | img，input                             |



### 替换元素和非替换元素



### 一些简单标签
---
|          |               |                      |
| -------- | ------------- | -------------------- |
| 加粗     | <b></b>       |                      |
| 斜体     | <em></em>     |                      |
| 删除线   | <s></s>       |                      |
| 换行     | <br>          |                      |
| 段落     | <p></p>       | 段落前后自动空出一行 |
| 标题     | <h1>~<h6>     | ；六种层次标题       |
| 分割线   | <hr>          |                      |
| 行内文本 | <span></span> |                      |



### 表格
---
表格：<table>   行 <tr>  单元格 <td>   
```html
<table>
<!--  第一行-->
  <tr>
    <td>用户名</td>   <!--<th>为加粗并居中-->
    <td>性别</td>
    <td>密码</td>
    <td>年龄</td>
  </tr>

<!--  第二行-->
  <tr>
    <td>李子航</td>
    <td>男</td>
    <td>01</td>
    <td>20</td>
  </tr>


</table>
```

![](../实例图片/捕获.PNG)

合并单元格：

```html
<table>
  <!--  第一行-->
  <tr>
    <td rowspan="2">用户名</td>   <!--纵向合并单元格，将用户名与李子航合并-->
    <td>性别</td>                 <!--<th>为加粗并居中-->
    <td>密码</td>
    <td>年龄</td>
  </tr>

  <!--  第二行-->
  <tr>

    <td colspan="2">男</td>     <!--横向合并单元格，将男与01合并-->
    <td>20</td>
  </tr>

</table>
```

![](../实例图片/捕获2.PNG)



可以设置表头，表体，表尾。用于设置不同的CSS：

```html
<table>
  <thead>                               <!-表头-->
    <tr>
	    <th>姓名</th>
	    <th>性别</th>
	  </tr>
  </thead>
    
  <tbody>                               <!-表体-->
	  <tr>
	    <td>kevin</td>
	  <td>男</td>
	</tr>
	<tr>
	  <td>anne</td>
	  <td>女</td>
	</tr>
  </tbody>
    
  <tfoot>                              <!-表尾-->
	<tr>
	  <td>Footer content 1</td>
	  <td>Footer content 2</td>
	</tr>
  </tfoot>
</table>
```







### 列表



有序列表
```html
<ol>
  <li>处理图像</li>
  <li>处理表格</li>
</ol>
```
倒序排列
```html
<ol reversed>
  <li>处理图像</li>
  <li>处理表格</li>
</ol>
```
默认为123排列，可以用type选择不同排列方式有5种
```html
<ol type="a">
  <li>处理图像</li>
  <li>处理表格</li>
</ol>
```
可以进行列表嵌套
```html
<ol >
  <li>处理图像</li>
  <ol type="a">
    <li>插入图片</li>
    <li>裁剪图片</li>
  </ol>
  <li>处理表格</li>
</ol>
```
无序列表
```html
<ul>
  <li>处理图像</li>
  <li>处理表格</li>
</ul>
```





### 图片
---
```html
<img  src="图片地址" alt="文本">   <!--图片无法显示时的替代文字-->
```







### 文字链接和图片链接

```html
 <a  href="https://www.bilibili.com/">bilibili</a> 
 
 <a href="https://www.bilibili.com/">
  <img src="maozhuxi.jpg">
</a>
```

| 常用属性         |                                                |
| ---------------- | ---------------------------------------------- |
| target="__blank" | 在新标签页打开链接，不写则默认本标签页打开链接 |

去除链接下划线见CSS文本样式text



#### 为图片不同位置添加不同链接

为图片不同位置设置不同超链接，不同位置可以为方形，圆形，多边形等
```html
<form>
  <input type="image" src="yingyong.jpg">
</form>
<!--可以点击查看图片中点的坐标-->
```
为一图片中多个矩形区域设置超链接
```html
<img src="yingyong.jpg" usemap="#map1">
<map name="map1">
  <area href="http://www.weather.com.cn/" shape="rect" coords="36,9,117,90" target="_blank">
  <area href="https://naozhong.net.cn/shijian/" shape="rect" coords="154,9,232,90" target="_blank">
</map>
<!--shape设置可点击形状为矩形，coords为左上右下的xyxy坐标即各边到左上边框的距离从而确定矩形位置-->
```
为一图片中多个圆形区域设置超链接,图片中的圆形时钟部分添加超链接
```html
<img src="yingyong.jpg" usemap="#map2">
<map name="map2">
  <area href="https://naozhong.net.cn/shijian/" shape="circle" coords="192,48,34" target="_blank">
</map>
<!--  croods三元素为图片左端到圆心的距离，图片上端到圆心的距离，园的半径前两步确定圆的位置，后一步确定圆的大小即点击范围-->
```



### 表单
表单 <from>  基本格式 <input type="各种类型"> 


##### 1.新建单行输入文本框
```html
  <input type="text">
  <input type="text" value="靠谱学院"><!--默认填入，删除才能填入新内容-->
  <input type="text" placeholder="请输入账号"><!--填入提示，例如账号密码框会有文字背景提示-->
  <input type="text" maxlength="6"><!--限制填入字符长度，汉字数字字母都只能填六个-->
  <input type="text" size="50"><!--设置输入框大小-->
  <input type="text" value="请输入密码" readonly><!--输入框只读，不能填充-->
```


###### 1.1.新建带有多个提示的可输入文本框

```html
  <input type="text" list="datalist1">
  <datalist id="datalist1">
    <option>苹果</option>
    <option>橘子</option>
    <option>菠萝</option>
  </datalist>
```
###### 1.2.新建多行输入文本框
```html
  <textarea>
    aaa
  </textarea> <!--此处aaa相当于默认填充-->
  表单的关键字为input,改变input中的type属性，改变表单的类型。
```
##### 2.密码文本框
```html
  <input type="password" placeholder="请输入密码"><!--自动隐藏内容-->
  <input  placeholder="请输入密码">
```
##### 3.数字滑动条
```html
  <input type="range"  min="-100" max="100"   >
  <input type="range"  min="-100" max="100" step="100"  >
  <input type="range" min="-100" max="100" step="100" value="-100">
  <!--  min,max设置滑动条最小最大值，step设置滑动单位，如以100为单位滑动，value设置起始位置-->
  <!--  浏览器中没有显示数字-->
```
##### 4.按钮
```html
  <butten>提交</butten>
```
##### 5.数字条

```html
  <input type="number" min="-100" max="100"  value="0">
```
##### 6.选择栏
```html
  <select>
    <option>苹果</option>
    <option>橘子</option>
    <option>菠萝</option>
  </select>
```
##### 7.方形勾选框

```html
  请选择正确的选项：
  <input type="checkbox">选项1
  <input type="checkbox">选项2
  <input type="checkbox">选项3
```
##### 8.圆形勾选框

```html
请选择正确的选项：
<input type="radio" name="a" checked>选项一
<input type="radio" name="a">选项二
<input type="radio" name="a">选项三
<!--name的内容可以是任意但所有name内容都必须相同,添加了name后，就只能选中一个，否则可以选择多个-->
<!--  checked作用是默认选择，放在哪就默认选择那个-->
<label for="nan">男</label><input type="radio" id="nan">
<!--点击男，也可以选中-->
```
##### 9.选择时间,比如设置生日
```html
  <input type="date">
```
##### 10.上传文件

会弹出文件资源管理器，可以上传文档，图片，视频，音频等文件。

```html
  <input type="file">
```

##### 11.音频
```html
<audio src=" "   controls  autoplay  loop></audio>
<!--autoplay自动播放-->
<!--loop重复播放-->
```


##### 12.视频
```html
<video src=" "  controls  autoplay></video>
```







### 框架

---
**1.令一个页面展示多个HTML页面，每个HTML称为一个框架，每个框架都独立于其他框架，且不同框架之间的边际可以通过鼠标拖动来改变它的大小**
**2.<frameset>不能与<body>同时出现，使用<frameset>需要删除<body>**

横向，纵向

```html
<frameset rows="50%,50%">
  <frame src="lizi.html" noresize="noresize">
  <frame src="person.html">
</frameset>
<!--rows为纵向排列，cols为横向排列，noresize属性设置不可拖动框架大小
百分比为HTML在页面中的比例-->
```

横纵混合

```html
<frameset rows="30%,70%">
  <frame src="lizi.html" >
  <frameset cols="50%,50%">
    <frame src="person.html">
    <frame src="personnal.html">
  </frameset>
</frameset>
```

![](../实例图片/capture_20200925195656571.bmp)