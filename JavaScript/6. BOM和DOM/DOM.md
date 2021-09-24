

#### 基础知识



API ：应用编程接口

Web API 大部分都是实现了各种功能的大量函数，开发者只需要简单调用就能实现其功能。



DOM 和 BOM :

文档对象模型（ document object model ），用于操作HTML的API。

浏览器对象模型（browser object model），用于操作浏览器的API。



DOM树：

1. 文档（document），一个页面就是一个文档。
2. 元素（element），文档中所有的**标签**都叫做元素。
3. 节点（node），文档中**所有的内容**（元素、元素的属性、文本、注释等）都叫做节点。



DOM把文档、元素、节点都看作是**对象**。

DOM主要用于操作元素。





#### 概述



1. 获取对象：获取被操作的对象
2. 注册事件：为被操作对象注册事件
3. 操作元素：在事件处理函数中，通过被操作对象和事件对象的属性和方法操作被操作对象。





#### 第1步：获取元素



##### 通用方式

1. `document.getElementById()` ，通过ID获取**单个元素**。输入元素ID字符串，返回一个元素对象。
2. `document.getElementsByTagName()` ，通过标签名获取相同标签名的**元素集合**。输入元素标签名字符串，返回元素对象集合。
3. `document.getElementsByClassName()` ，通过类名获取相同类名**元素集合**。输入元素类名字符串，返回元素对象集合。



##### H5获取元素新的方式

​        通过CSS中选择器的方式来获取元素，可以通过一个函数获取各种类型的元素，不需要像上述各种函数，更加统一。

1. `document.querySelector()`，通过**选择器**获取**单个元素**。输入选择器格式的字符串，返回该该选择器格式下的第一个元素。（所有选择器格式，包括混合、嵌套）
2. `document.querySelectorAll()`，通过选择器获取元素**集合**。输入选择器格式的字符串，返回该该选择器格式下元素集合。



##### 获取`<html><body>` 

​        除了上述方法获取这两个元素外，还有特殊的方式获取。

`document.body`

`document.documentElement`



==使用获取元素集合的方式获取单个元素时，仍返回集合。故需注意单个元素用 `element[0]` 表示，容易写成`element` 这样不会生效。==



##### 通过节点操作获取



页面中所有的内容都是节点，元素当然也是。

```html
<div class="box">
     <nav>
         <ul>
                <li>商品介绍</li>
                <li>规格与包装</li>
                <li>售后保障</li>
                <li>商品评价（1万+）</li>
          </ul>
     </nav>
</div>
```

我们首先用上述方法获取一个元素，然后就可以通过节点操作**直接使用**它的父元素、子元素和兄弟元素，没有对应的元素则返回 `null` 。

```javascript
var nav = document.querySelector('.box nav');

nav.parentNode  //元素的最近父元素节点

nav.children    //元素内的第一层的元素节点集合
nav.children[n]   //元素的第n+1个元素子节点
nav.children.length  //元素的子节点个数
nav.firstElementChild  //第一个元素子节点，可能会有兼容性问题。
nav.lastElementChild  //最后一个元素子节点

nav.nextElementSibling   //元素的下一个元素节点（即兄弟节点）
nav.previousElementSibling  //元素的上一个元素节点（即兄弟节点）
```

其它不常用的

```javascript
nav.childNodes  //元素内第一层的全部子节点集合（包括元素、文本等），不常用一般我们只需要元素节点

nav.firstChild  //第一个子节点（注意不是元素节点）
nav.lastChild   //最后一个子节点（注意不是元素节点）
nav.children[0]       //第一个元素子节点，没有兼容性问题。
nav.children[nav.children.length - 1]  //最后一个元素子节点

nav.nextSibling    //元素的下一个节点（即兄弟节点）
nav.previousSibling  //元素的上一个节点
```

注意换行符、空格符也属于文本节点，所以`console.log(nav.childNodes)` 结果为`NodeList(3) [text, ul, text]` ，即nav  的第一个和最后一个子节点为空格（文本节点）。







#### 第2步：注册事件



##### 常用事件




| 鼠标事件   |                           |
| ---------- | ------------------------- |
| click      | 鼠标点击                  |
| mouseover  | 鼠标覆盖                  |
| mouseout   | 鼠标离开                  |
| focus      | 鼠标焦点（左击）          |
| blur       | 失去焦点                  |
| mousemove  | 鼠标移动                  |
| mousedown  | 鼠标按下                  |
| mouseenter | 鼠标进入，动作同mouseover |
| mouseleave | 鼠标离开，同上            |

mouseover和mouseenter的区别：mouseenter不会冒泡




| 常见键盘事件 |                                                |
| ------------ | ---------------------------------------------- |
| keyup        | 某个按键抬起                                   |
| keydown      | 某个按键按下                                   |
| keypress     | 某个按键按下，不识别功能键如ctrl ,shift,箭头等 |

响应优先级：keydown > keypress > keyup，与定义顺序无关。



| 滚动条事件 |                  |
| ---------- | ---------------- |
| scroll     | 鼠标滚动时触发。 |
|            |                  |
|            |                  |









##### 注册和删除事件

注册事件由三部分组成：事件源、事件类型、事件监听器（事件处理函数）。

```javascript
<button>按钮测试</button>
    
<script>
     var but = document.querySelector('button');

     but.addEventListener('click', clickBut1);      //为一个事件注册了两个处理函数
     but.addEventListener('click', clickbut2);

     function clickBut1() {
         alert('234');
         but.removeEventListener('click', clickBut1);     //删除事件的一个处理函数
     }
     function clickbut2() {
         alert('678');
     }
</script>

//第一次触发弹出234，确定后弹出678.而第二次触发只弹出678，因为第一次触发执行clickBut1()弹出234后，为But删除了clickBut1()事件监听器
```



`eventTarget.addEventListener(type, listener，[useCaptrue] );`        注册事件

`eventTarget.removeEventListener(type, listener，[useCaptrue] );`  删除事件

- eventTarget      事件源
- type                    事件类型，**字符串形式**
- listener              事件监听器
- [useCaptrue]    可选的布尔值，下面的DOM事件流会讲到。



==可以给事件源的一个事件添加多个事件处理函数，触发事件后按添加顺序自动依次执行。（只触发一次即可，不是触发一次执行一个）==



##### DOM事件流

当我们发生事件触发动作时，并不是直接在此元素上判断是否注册了此事件并响应事件监听器。事件按一定的顺序在对象中传播。判断每个对象是否注册了该事件。如果注册了会执行事件监听器，继续判断下一个对象。事件有两种传播方式，称之为DOM事件流。

```javascript
<div class="father">
        <div class="son"></div>
</div>
```

- 捕获事件流：document对象、HTML对象、div.father对象、div.son对象

- 冒泡事件流：div.son对象、div.father对象、HTML对象、document对象 （默认为冒泡事件流）

1. 我们没有给`.father` 或`.son` 注册事件，当我们点击 `.son` 时，判断 `.son` 是否注册了点击事件，没有则判断`.father` 是否注册了点击事件，继续往上没有对象注册了点击事件则没有任何效果。

2. **我们给`.father` 注册了点击事件。当我们点击 `.son` 时，判断 `.son` 是否注册了点击事件，没有则判断`.father` 是否注册了点击事件，这时显示点击效果。继续往上没有对象注册了点击事件。而我们直接点击`.father` 也会有同样的效果。**

3. 我们给`.father` 或`.son` 都注册事件，点击`.son` 时，会先执行`.son` 的处理函数，再执行`.father`的处理函数。直接点击`.father` 则会再执行`.father`的处理函数，而不会执行`.son` 的处理函数

==并不是一个元素注册了该事件，在这个元素上发生该事件时才会出现事件流，没有注册这个事件也会触发事件流。任何元素都会触发事件流。==



```javascript
<div class="father">
        <div class="son"></div>
</div>

<script>
     var father = document.querySelector('.father');

     father.addEventListener('click', alertNun1, true);
     father.firstElementChild.addEventListener('click', alertNum2, false);

     function alertNun1() {
          alert('father');
     }
     function alertNum2() {
          alert('son');
     }
</script>

//.son盒子为冒泡事件流，onclick事件会在冒泡事件流中传播，判断每个对象是否为onclick注册了事件监听器。点击.son盒子，弹出"son",确定后弹出"father"
//点击.father盒子，只弹出"father",因为捕获事件流只执行到.father盒子
//事件在事件流中传播时，只判断该对象是否注册了该事件，而不管事件在该对象是什么事件流。
```



注意：

1. 当`[useCaptrue]` 为 `true` 时，响应事件执行捕获事件流；当`[useCaptrue]` 为 `false` 时，响应事件执行冒泡事件流。默认不写为`false`。

2. **一个元素的一个事件，捕获和冒泡事件流只能存在一个。**
3. DOM事件流的核心是事件的传播，一个元素不同的事件可以有不同的事件流。
4. 有些事件不支持冒泡事件流，如`focus、blur、mouseenter、mouseleave`
5. 阻止冒泡事件流只让被绑定元素执行事件处理函数，详见事件对象。







##### 事件对象

为一个元素注册事件，**事件被触发之后，执行事件处理函数之前**，会自动生成一个事件对象。保存了事件相关的属性（如触发元素、事件类型等）和一些操作触发事件元素的方法。

鼠标事件会产生 `MouseEvent` 对象，键盘事件会产生 `KeyboardEvent` 对象。不同的事件对象有通用的属性和方法，也有不同的属性和方法。这些对象默认都用 `event` 调用。

| 通用的事件对象属性和方法 |                                                 |
| ------------------------ | ----------------------------------------------- |
| event.target             | 触发事件的元素                                  |
| event.type               | 事件类型                                        |
| event.preventDefault()   | 阻止触发对象的默认行为(如<a>不跳转，按钮不工作) |
| event.stopPropagation()  | 阻止触发对象冒泡事件流                          |

注意上述属性和方法针对的是触发事件的元素，触发事件的元素不一定为事件绑定元素。



1. ==触发事件的元素不一定为事件绑定元素。（事件流原理）==

```javascript
<div class="father">
     <div class="son"></div>
     <button>点击测试</button>
</div>

<script>
      var father = document.querySelector('.father');

      father.addEventListener('click', changeCol, false);

      function changeCol() {
           father.style.backgroundColor = 'blue';
           console.log(event.target);           //直接调用event即可
           console.log(event.type);
      }
</script>
//我们为.father盒子绑定了点击事件。当我们点击.father盒子时，target返回.father盒子，type为click
//当我们点击.son盒子和按钮时，也会触发click事件，但target返回的是.son盒子或按钮,type为click
```

2. 阻止触发对象的默认行为

```javascript
<a href="https://www.bilibili.com/">bilibili</a>

<script>
     var a = document.querySelector('a');

     a.addEventListener('click', no);      //'contextmenu'禁止鼠标右键，'selectstart'

     function no(){
          event.preventDefault();
     }
</script>
//点击链接后，不再跳转。（可以用于链接、按钮）
//'contextmenu'禁止鼠标右键，'selectstart' 禁止鼠标选中
```

3. 阻止冒泡事件流

将 `event.stopPropagation()` 添加到事件处理函数中。





##### 鼠标事件对象



| 鼠标事件对象常用属性 |                                     |
| -------------------- | ----------------------------------- |
| event.clientX        | 返回鼠标相当于浏览器可视窗口的x坐标 |
| event.clientY        | 返回鼠标相当于浏览器可视窗口的y坐标 |
| event.pageX          | 返回鼠标相对于文档页面的x坐标       |
| event.pageY          | 返回鼠标相对于文档页面的y坐标       |
| event.screenX        | 返回鼠标相当于屏幕的x坐标           |
| event.screenY        | 返回鼠标相当于屏幕的y坐标           |



##### 键盘事件对象



| 键盘事件对象常用属性 |                       |
| -------------------- | --------------------- |
| event.keyCode        | 返回对应按键的ASCII值 |

只要判断返回的ASCII值是否是我们需要的按键的ASCII值就可以给指定按键添加操作。



```javascript
document.addEventListener('keydown', down);       //给文档对象注册keydown事件

function down() {
    if( event.keyCode == 65){                 
         alert('a');
    }
}
//每次按键按下都会判断是否是按下了a，这样是否是太没效率了
```

- keydown、keyup不区分大小写。（a和A都是65)
- keypress区分大小写，但它不识别功能键。





##### 事件委托

冒泡事件流的应用。









#### 第3步：操作元素



##### 获取和改变元素的内容

`element.innerHTML` ：识别HTML标签，识别空格和换行。（推荐）

`element.innerText` ：不识别HTML标签，不识别空格和换行（即会去除）。



##### 获取和改变元素的属性



`element.属性名`

如：`element.className` `element.id` `element.src`

应用场景：

当我们触发事件后需要修改元素的大量属性时，可以不用在函数中一个一个修改元素的属性，而是在css中专门定义一个类名选择器，在里面修改它的样式，这样只要在事件函数改变类名，即className即可。

修改地址src即可起到切换图片的效果。



`element.style.属性名` 

属性采用驼峰命名法，如 `background-color` 写为 `element.style.backgroundColor`

注意：此种方法相当于HTML元素属性的行内样式，优先级要比在`<style>` 标签中设置的属性高。

隐藏/显示元素：`element.style.display = 'block' | 'none' ;`

 



##### 自定义属性



`element.getAttribute( '属性名' )`

在实际应用中，开发者也可以为元素自定义属性（格式为`data-`开头，如`data-index` ），而这些自定义属性的获取，由这种方式完成。

输入属性名字符串，返回属性值。

`element.setAttribute( '属性名', '值' )`

设置自定义属性。

`element.removeAttribute( '属性名' )`

移除自定义属性。





##### 操作表单元素



`element.type`         表单类型

`element.value`       表单内容

`element.disabled`     （ true 或 false ）禁用该表单元素

`element.checked`

`element.selected`



##### 创建元素

```javascript
//创建元素
var li = document.createElement('li');     //创建了<li>
//添加元素的两种方法
nav.appendChild(li);                      //添加到父元素中（子元素列表的最后）
nav.insertBefore(li, 指定元素);            //添加到父元素中指定元素的前面
```



##### 删除元素

```javascript
nav.removeChild( 子节点 );             //返回被删除的子节点
```



##### 复制元素

```javascript
nav.children[0].cloneNode();        //克隆了nav中的第一个li，只复制标签，不复制内容
nav.children[0].cloneNode(true);    //克隆了nav中的第一个li,复制标签和内容

nav.appendChild(li);                      //添加到父元素中（子元素列表的最后）
nav.insertBefore(li, 指定元素);            //添加到父元素中指定元素的前面
```





##### offset系列属性



使用元素的 `offset` 系列属性可以**动态的**得到该元素相对于（带有定位的）父级元素的位置、大小。

- 如果没有父级属性或父级属性不带定位，则是相对与 `<body>`也就是整个页面的位置。
- 返回的数值没有单位。



常用属性

![屏幕截图 2021-02-25 102422](https://gitee.com/li_zihang/typora-drawing-bed/raw/master/图片/屏幕截图 2021-02-25 102422.png)

高度和宽度不包含 `margin`  外边距。



想要获取元素的宽度和高度时，`offset` 和 `style` 有什么区别？

`element.offsetWidth / element.offsetHeight`    和   `element.style.width / element.style.height`

1. 前面讲到过，`style` 方式设置的是CSS的行内样式，优先级比表头样式要高。那么它获取的也是行内样式中的宽高，如果宽高没有在行内设置则无法获取。`offset` 可以获取任意位置的样式。
2. `offset` 返回值没有单位，`style` 返回值有单位。
3. `offset` 获取宽高为 元素内容区宽高+内边距+边框；`style`  获取宽高只有元素内容区宽高。
4. `offset` 属性是只读属性，`style`  属性可读写。



##### client系列属性



可以通过client系列属性**动态的** 获取元素的边框大小，元素大小。

![屏幕截图 2021-02-26 094226](https://gitee.com/li_zihang/typora-drawing-bed/raw/master/图片/屏幕截图 2021-02-26 094226.png)





##### scroll系列属性



动态地获取元素的滚动距离，元素大小。

![屏幕截图 2021-02-26 102821](https://gitee.com/li_zihang/typora-drawing-bed/raw/master/图片/屏幕截图 2021-02-26 102821.png)

当内容的宽高大于容器的内容区时，容器常常会设置滚动属性，可以设置上下滚动，也可以设置左右滚动。

- `element.scrollTop` 从内容顶部向下滚动时，被卷去的距离。
- `element.scrollWidth` 内容自身的宽度 + 内边距（不是内容区的宽度）。

例如当我们的盒子向下滚动到底部时：

![屏幕截图 2021-02-26 104434](https://gitee.com/li_zihang/typora-drawing-bed/raw/master/图片/屏幕截图 2021-02-26 104434.png)





##### 三系列总结



- `offset` 系列**动态地**得到该元素相对于（带有定位的）父级元素的位置
- `client`系列属性**动态地** 获取元素的边框大小
- `scroll` 系列属性**动态地**获取元素的滚动距离



三个系列可以获得不同的元素宽高：

- `element.style.width / element.style.height` 获取元素内容区宽高
- `element.offsetWidth / element.offsetHeight` 获取元素内容区宽高 + 内边距 + 边框
- `element.clientWidth / element.clientHeight` 获取元素内容区宽高 + 内边距 
- `element.scrollWidth / element.scrollHeight` 获取元素内容本身的宽高 +内边距

