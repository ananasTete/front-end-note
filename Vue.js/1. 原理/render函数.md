## render函数

通过compiler或@vue/compiler-sfc编译模板，在组件配置对象中生成一个render函数。

如：

```html
<div class="why">
   <h2>当前计数：100</h2>
   <button @click="">+1</button>
</div>
```

```js
export default {
  
  render() {
    return h("div", {class: "why"}, [
      h("h2", null, "当前计数：100"),
      h("button", {onClick: () => {console.log("button点击");}}, "+1"),
    ])
  },

  //调用 render函数时，return的是h函数的调用，h函数接收三个参数返回 vnode
  
  //元素标签名字符串，如"div"；或者组件名，如Home
  //元素的属性组成的对象，没有属性时可以为null
  //元素的内容，可以为字符串，或者子元素的vnode组成的数组
};
```



调用 render函数返回vnode，是一个JS对象，如

```js
{
  tag: "div",
  props: { class: "why" },
  children: [
    {
       tag: "h2",
       props: null,
       children: "当前计数：100",
    },
    {
       tag: "button",
       props: { onClick: () => {console.log("button点击");}},
       children: "+1",
    }
  ]
};
```

由于vue应用是一颗组件树，其中的模板也会一层层嵌套，对应的vnode也会一层层嵌套形成一个大的JS对象，即虚拟DOM。



反正模板也会被编译为一个render函数，我们可以干脆可以不写模板直接在组件配置对象中自己定义render函数。就像上面的例子中展示的那样，但需要引入h函数

```js
import { h } from "vue";
```

