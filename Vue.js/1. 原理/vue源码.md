## vue源码



1. Compiler模块：编译模板
2. Runtime模块：也可以称之为 Renderer模块，渲染虚拟DOM
3. Reactivity模块：响应式模块



### 编译与渲染

vue有两种版本，runtime+compiler和 runtime-only：



```javascript
// runtime+compiler的 main.js
new Vue({
  el: '#app',
  components: { App },
  template: '<App/>'
})
```

compiler会将组件配置对象中的 template选项编译成一个render函数，创建组件实例时调用 render函数生成成 vnode最终组成虚拟dom，最后渲染成真实DOM

template  -> render -> 虚拟DOM -> 真实DOM



```javascript
// runtime-only的 main.js
new Vue({
  el: '#app',
  render: h => h(App)
})

//h指代createElement, render: h=>h(App)为箭头函数
render: function(createElement) {
  return createElement(App);               //传入一个组件构造器
}

//render->虚拟dom->ui
```

runtime-only没有 compiler，不会解析所有组件配置对象中的 `template`选项。那如何编译组件的模板呢？

组件配置对象中不再写 template选项，在根组件中直接通过 render函数编译 App.vue；在普通组件中通过 webpack的 @vue/compiler-sfc包解析 `<template>`编译成一个render函数，创建组件实例时调用 render函数形成 vnode最终组成虚拟dom，最后渲染成真实DOM

template  -> render -> 虚拟DOM -> 真实DOM。



runtime+webpack 效率比runtime+compiler更高。





### 响应式原理



1. 为什么改变 data中的数据模板中相应的数据会响应式地改变？

```js
const app = new Vue({
  data: {
       message: 'hola'
  }
}).$mount('#app')
```

新建一个 vue对象时传入一个对象参数，其中就有data对象，传进去以后将data对象中每一个属性都重新通过 `Object.defineProperty()` 的方式新建为一个访问器属性替换掉原来的属性。

```js
Object.defineProperty(data, message, {        //在data对象中定义属性message
      set(newValue) {
        value = newValue;
      },
      get() {
        return value;
      }
})
```

在读取访问器属性时，会自动调用`get()` 方法重新写入message的值；在写入访问器属性时，会自动调用`set()` 方法获取 message的值。这样 vue对象中 message的值就可动态变化了。

2. 将 vue对象中的值动态绑定到模板中数据

