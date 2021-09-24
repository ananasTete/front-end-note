1. 选择器及其优先级
2. 行内元素和块级元素
3. 盒子模型
4. 隐藏元素的方法有哪些
5. 垂直水平居中
6. link和@import的区别
7. 清除浮动
8. position
9. 过渡和动画
10. line-height和height
11. 说说 CSS3新增属性
12. 文本溢出
13. 外边距重叠
14. calc
15. BFC



### link和@import的区别

两者都是外部引用CSS的方式，它们的区别如下：

- link是XHTML标签，除了加载CSS外，还可以定义RSS等其他事务；@import属于CSS范畴，只能加载CSS。
- **link引用CSS时，在页面载入时同时加载；@import需要页面网页完全载入以后加载。**
- link是XHTML标签，无兼容问题；@import是在CSS2.1提出的，低版本的浏览器不支持。
- link支持使用Javascript控制DOM去改变样式；而@import不支持。

