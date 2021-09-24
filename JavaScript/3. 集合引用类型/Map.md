### Map



map 是用于存储 "键/值" 类型数据的类。

所谓 ”键/值“ 是一种每组数据都是一对一的数据结构。与object中的属性名-属性类似。

那为什么不直接使用object保存 ”键/值“ 类型的数据呢？

1. object的键只能使用数值、字符串或符号，值无限制；map键、值类型都无限制。
2. object中的属性名-属性是无序的；map中的”键/值“是有序的。



#### 创建map



```javascript
const m = new Map();
```



#### 创建的同时初始化



```javascript
// 使用嵌套数组初始化映射
const m1 = new Map([
 ["key1", "val1"],
 ["key2", "val2"],
 ["key3", "val3"]
]);
alert(m1.size); // 3

// 使用自定义迭代器初始化映射
const m2 = new Map({
 [Symbol.iterator]: function*() {
 yield ["key1", "val1"];
 yield ["key2", "val2"];
 yield ["key3", "val3"];
 }
});
alert(m2.size); // 3
```



#### 操作map的方法

可以使用 set()方法再添加键/值对。可以使用 get()和 has()进行查询，可 以通过 size 属性获取映射中的键/值对的数量，还可以使用 delete()和 clear()删除值。

```javascript
let test = new Map();
test.set('name','lizihang').set('age',21); //可以连续调用.set(键，值)
alert(test.get('name'));  //参数为键，返回对应的值，lizihang，没有返回undefined
alert(test.has('name'));  //参数为键，返回布尔值，true
test.delete('name');  //参数为键，将键对应的键/值组删除
test.clear();         //将map中所有的键/值组删除
document.write(test.size);  //返回map中键/值组的个数
```

