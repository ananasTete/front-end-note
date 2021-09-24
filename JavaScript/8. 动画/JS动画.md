前提：元素有position属性，才能设置left / right / top /button

1. 获取元素当前位置（offset）

2. 让盒子在当前位置+n（element.style.left/top = offsetWidth/Height + n）

3. 设置定时器重复上一步

4. 加一个定时器结束条件

   