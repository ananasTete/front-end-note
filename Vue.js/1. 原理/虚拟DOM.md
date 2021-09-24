## vnode和虚拟DOM

virtual node 虚拟节点。



模板中的每一个组件或元素，在Vue中表现出来的都是一个个js对象，称作VNode。

![image-20210518105426328](https://gitee.com/li_zihang/typora-drawing-bed/raw/master/图片/image-20210518105426328.png)

子元素对应的对象会成为父元素对象中children属性的一个对象属性，模板中的所有元素最终形成一个嵌套而成的大对象，称为虚拟DOM。



为什么需要转化为虚拟DOM？因为操作 JS对象比直接操作DOM要更加简单和灵活。在Vue中操作DOM时操作的是虚拟DOM。

