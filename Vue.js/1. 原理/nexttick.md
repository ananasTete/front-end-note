## nexttick





```html
<span ref="numref"> {{num}} </span> <br>
<button @click="add">+</button>
```

```js
import { ref } from "vue"

setup() {
  const num = ref("");
  const numref = ref(null);

  function add() {
    num.value += "呼";
    console.log(numref.value.offsetWidth);
  }

  return {
    num,
    numref,
    add,
  }
}
```

先看一个案例，有一个 span，值为空字符串。按下一次按钮添加一个 “呼”字，即字符串长度不断变长。我们想要在改变长度后获取新的字符串长度。但这里打印出来的都是改变前的长度。因为 add()方法中的两条语句都是同步语句立即执行，但数据改变后重新生成虚拟DOM重新渲染成真实DOM却是异步事件。所以在真实DOM重新渲染完成之前就打印了字符串的长度，打印的自然就是改变前的长度。



可以通过 nexttick在真实DOM重新渲染完成后再打印长度，原理：nexttick会将函数添加到微任务队列的最后。

```js
import { ref, nextTick } from "vue"

function add() {
  num.value += "呼";
  nextTick(() => {
    console.log(numref.value.offsetWidth);
  })  
}
```

