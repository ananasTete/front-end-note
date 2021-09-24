#### window对象



window对象是js访问浏览器的接口。



##### 窗口加载事件



```javascript
window.addEventListener('load', 函数名)；
```



1. `load` 事件，等页面内容（DOM元素，图片，CSS等）全部加载完毕再执行`load` 事件的处理函数。
2. `DOMContentLoaded` 事件，等DOM元素加载完毕再执行`load` 事件的处理函数，比`load` 响应更快速



##### 调整浏览器窗口大小事件



`resize` 事件，浏览器窗口大小发生变化时执行 `resize`  事件处理函数。

`window.innerWidth` 返回浏览器宽度。

`window.innerHeight` 返回浏览器高度。



##### 定时器方法



setTimeout(函数名，时间)           只执行一次函数后定时器自动失效，毫秒

clearTimeout(定时器名)

setInterval(函数名，时间);       循环执行函数，不会自动失效，毫秒

clearInterval(定时器名);





#### location对象



location对象是 window对象的一个属性，用于获取和设置窗口的URL。



##### URL

统一资源定位符，互联网上每一个文件都有一个唯一的URL，包含的信息指出文件的位置以及浏览器应该怎么处理它。

语法：`protocol://host[:port]/path/[?query]#fragment`

```javascript
https://www.bilibili.com/video/BV1k4411w7sV?p=91
```

| protocol | 通信协议                          |
| -------- | --------------------------------- |
| host     | 域名                              |
| port     | 端口号                            |
| path     | 路径，以/的形式分隔开             |
| query    | 参数，以键值对的形式，通过&分割开 |
| fragment | 片段                              |



##### 常用属性

![屏幕截图 2021-02-24 214825](https://gitee.com/li_zihang/typora-drawing-bed/raw/master/图片/屏幕截图 2021-02-24 214825.png)



##### 常用方法

![屏幕截图 2021-02-25 093100](https://gitee.com/li_zihang/typora-drawing-bed/raw/master/图片/屏幕截图 2021-02-25 093100.png)

`assign()` 可以回退页面也就是浏览器左上角可以回退页面。而`replace` 左上角不能回退页面。

前两个方法参数为URL字符串。







#### navigator对象





#### history对象



history对象是window对象的一个属性，与浏览器历史记录进行交互，该对象包含用户访问过的URL。



##### 常用方法

![屏幕截图 2021-02-25 095419](https://gitee.com/li_zihang/typora-drawing-bed/raw/master/图片/屏幕截图 2021-02-25 095419.png)

- 前两个方法没有参数，`history.back()` ,直接调用。

- 实现了浏览器左上角的前进后退功能。
- `location` 对象的方法是跳转到指定页面，`history` 对象的方法是前进后退页面。





