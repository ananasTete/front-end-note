###  Array



- 数组是对象，属性`length`保存数组的长度。

特殊的 `length` 属性：通过主动修改 `length` 属性添加或删除数组的末尾元素

```javascript
let colors = ["red", "blue", "green"]; 
colors.length = 2;
alert(colors[2]); // undefined
//"green"元素被删除

colors.length = 3;
alert(colors[2]); // undefined
//为数组新增了一个元素，其值为undefined
```

- Array与Java中的数组不同，一个array可以保存不同数据类型的数据。



#### 创建数组



```javascript
let colors = new Array(); 
colors[0]='red';    //赋值
colors[1]='blue';
let colors = new Array(20);  //下面的代码会创建一个初始 length 为 20 的数组：
let colors = new Array("red", "blue", "green"); 
```

字面量表示法

> 与对象一样，在使用数组字面量表示法创建数组不会调用 Array 构造函数。

```javascript
let colors = ["red", "blue", "green"]; // 创建一个包含 3 个元素的数组
let names = []; // 创建一个空数组
let values = [1,2,]; // 创建一个包含 2 个元素的数组
```



Array 构造函数还有两个 ES6 新增的用于创建数组的静态方法：`map()`和 `of()`





#### 数组空位



```javascript
let test = [,,,,];
//这表示创建了一个含有4个元素的数组，每个元素的值为Undefined;
let test = [1,,,5];
```

> 由于行为不一致和存在性能隐患，因此实践中要避免使用数组空位。如果确实需要 空位，则可以显式地用 undefined 值代替。



#### 检测数组



即检测一个对象是不是数组对象。

```javascript
//在只有一个网页时（即只有一个全局上下文）
if (value instanceof Array){
 // 操作数组
} 
//网页中有多个框架时（可能有多个全局上下文）
if (Array.isArray(value)){
 // 操作数组
} 
```



### 对Array操作的方法



#### 迭代器方法



#### 复制和填充方法



- 使用 `fill()` 方法可以将一个已有的数组中全部或部分的元素变为开发者指定的值。

- 使用`copyWithin()`方法将数组中的全部或部分元素复制到指定位置，并覆盖原值。



1. `fill()`方法，可以接收3个参数（指定值，起始位置，结束位置）

```javascript
const zeroes = [0, 0, 0, 0, 0];

// 用 5 填充整个数组
zeroes.fill(5);
console.log(zeroes); // [5, 5, 5, 5, 5]
zeroes.fill(0); // 重置

// 用 6 填充索引大于等于 3 的元素
zeroes.fill(6, 3);
console.log(zeroes); // [0, 0, 0, 6, 6]
zeroes.fill(0); // 重置

// 用 7 填充索引大于等于 1 且小于 3 的元素即[1,3)
zeroes.fill(7, 1, 3);
console.log(zeroes); // [0, 7, 7, 0, 0];
zeroes.fill(0); // 重置

// 用 8 填充索引大于等于 1 且小于 4 的元素
// (-4 + zeroes.length = 1)
// (-1 + zeroes.length = 4)
zeroes.fill(8, -4, -1);
console.log(zeroes); // [0, 8, 8, 8, 0];
```

`fill()` 静默忽略超出数组边界、零长度及方向相反的索引范围：

```javascript
const zeroes = [0, 0, 0, 0, 0];
// 索引过低，忽略
zeroes.fill(1, -10, -6);
console.log(zeroes); // [0, 0, 0, 0, 0]
// 索引过高，忽略
zeroes.fill(1, 10, 15);
console.log(zeroes); // [0, 0, 0, 0, 0]
// 索引反向，忽略
zeroes.fill(2, 4, 2);
console.log(zeroes); // [0, 0, 0, 0, 0]
// 索引部分可用，填充可用部分
zeroes.fill(4, 3, 10)
console.log(zeroes); // [0, 0, 0, 4, 4]
```

2. `copyWithin()`方法，可以接收3个参数

```javascript
let ints =  [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

ints.copyWithin(5);
console.log(ints); // [0, 1, 2, 3, 4, 0, 1, 2, 3, 4]；

// 从 ints 中复制索引 5 开始的内容，插入到索引 0 开始的位置，到数组边界为止
ints.copyWithin(0, 5);
console.log(ints); // [5, 6, 7, 8, 9, 5, 6, 7, 8, 9]

// 从 ints 中复制索引 0 开始到索引 3 结束的内容
// 插入到索引 4 开始的位置
ints.copyWithin(4, 0, 3);
alert(ints); // [0, 1, 2, 3, 0, 1, 2, 7, 8, 9]

// 支持负索引值，与 fill()相对于数组末尾计算正向索引的过程是一样的
ints.copyWithin(-4, -7, -3);
alert(ints); // [0, 1, 2, 3, 4, 5, 3, 4, 5, 6]
```

`copyWithin()`静默忽略超出数组边界、零长度及方向相反的索引范围：

```javascript
ints.copyWithin(1, -15, -12);
alert(ints); // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

// 索引过高，忽略
ints.copyWithin(1, 12, 15);
alert(ints); // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

// 索引反向，忽略
ints.copyWithin(2, 4, 2);
alert(ints); // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

// 索引部分可用，复制、填充可用部分
ints.copyWithin(4, 7, 10)
alert(ints); // [0, 1, 2, 3, 7, 8, 9, 7, 8, 9]; 
```



#### 转换方法



即将数组转换为字符串的方法。

- 所有对象中都有`toLocaleString()、toString()、 valueOf()` 方法。

> toString()返回由数组中每个值的等效字符串拼接而成的一个逗号分隔的 字符串。也就是说，对数组的每个值都会调用其 toString()方法，以得到最终的字符串。

```javascript
let test = [1,2,3];

document.write(test+'\t');
document.write(test.toLocaleString()+'\t');
document.write(test.toString()+'\t');
//以上都返回1，2，3 其中第一式子相当于第三式子。
```

- 继承的方法 `toLocaleString()`以及 `toString()`都返回数组值的逗号分隔的字符串。如果想使 用不同的分隔符，则可以使用 `join()`方法。join()方法接收一个参数，即字符串分隔符，返回包含所 有项的字符串。

```javascript
let colors = ["red", "green", "blue"];
alert(colors.join(",")); // red,green,blue
alert(colors.join("||")); // red||green||blue
```



#### 栈方法



`push()`可接收任意参数，并将他们添加到数组末尾，并返回新的数组长度。

`pop()` 方法可以不接受参数，可以删除数组最后一项元素，并返回被删除的最后一项元素。

这两种方法对数组的操作都是在数组末尾进行，与栈的出栈入栈“后进先出”类似，故以此得名。

```javascript
let test = [1,2,3];
let length=test.push(4,5);
document.write(test+'\t'+length);//1，2，3，4，5 5
let last = test.pop();
document.write(test+'\t'+last);//1，2，3，4 5

let test = [1, 2, 3];
let test1 = [4, 5];
test.push(...test1);  //遍历test1中的元素添加到test
//1,2,3,4,5
```



#### 队列方法



与栈方法正好相反。

`unshift()`可接收任意参数，并将他们添加到数组开头，并返回新的数组长度。

`shift()` 方法可以不接受参数，可以删除数组第一项元素，并返回被删除的第一项元素。

与队列的“先进先出”类似。

```javascript
let test = [1,2,3];
test.unshift(4);
document.write(test);
//4,1,2,3

let test = [1,2,3];
test.shift();
document.write(test);
//2,3
```



#### 排序方法



`reverse()`方法将数组倒序。

```javascript
let test = [1,2,3];
test.reverse();
document.write(test);
//3，2，1
```





#### 操作方法



`slice()` 方法**遍历出**数组的全部或部分元素，返回一个新数组。

```java
let test = [1,2,3,4,5,6,7];
let test3 = test.slice(0); 
document.write(test3);
//1,2,3,4,5,6,7

let test = [1,2,3,4,5,6,7];
let test2 = test.slice(1,4);  
document.write(test2);
//2,3,4 不包括第四项元素，相当于[1,4)
```



`splice()` 方法

- 删除：接收两个参数，起始位置和删除元素个数，将被删除元素组成数组返回。

```javascript
let colors = ["red", "green", "blue"];
let removed = colors.splice(0,2); 
document.write(colors);  //blue
document.write(removed);  //green,blue
```

- 插入或替换：接收2+n个参数，起始位置、删除元素个数和任意个插入数据。将被删除元素组成数组返回，若不删除元素设为0，返回空数组。

```javascript
let colors = ["red", "green", "blue"];
let removed = colors.splice(0,1,"pink","black"); 
document.write(colors);  //pink,black,green,blue
document.write(removed);  //red
```



#### 搜索和位置方法



`indexOf()、lastIndexOf()` 正向和反向搜索指定元素位置。没有则返回-1

`includes()` 判断是否含有该元素，返回布尔值。使用全相等（===）进行比较。

```javascript
let numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];
document.write(numbers.indexOf(4)); // 3
document.write(numbers.lastIndexOf(4)); // 5
document.write(numbers.includes(4)); // true
document.write(numbers.indexOf(4)); // 3
//只能查找第一个匹配项
```



#### 迭代方法



`every()`：对数组每一项都运行传入的函数，如果对每一项函数都返回 true，则这个方法返回 true。

`some()`：对数组每一项都运行传入的函数，如果有一项函数返回 true，则这个方法返回 true。 

`filter()`：对数组每一项都运行传入的函数，函数必须返回布尔值，函数返回 true 的项会组成数组之后返回。

`forEach()`：对数组每一项都运行传入的函数，没有返回值。 

如：

```js
let arrInfo = [4,6,6,8,5,7,87];
arrInfo.forEach((item,index,arr)=>{
    //遍历逻辑
})
//item代码遍历的每一项,
//index:代表遍历的每项的索引，
//arr代表数组本身
```

item、index、arr都是可选的。filter函数也有这几个选项

`map()`：对数组每一项都运行传入的函数，返回由每次函数调用返回的结果构成的数组。 



`find()和 findIndex()`，findIndex：返回指定数据在数组中的索引值

![image-20210904165307958](https://gitee.com/li_zihang/typora-drawing-bed/raw/master/图片/image-20210904165307958.png)



`reduce()`，累加

```js
friends.reduce((preValue, item) => {  
  return preValue + item
}, 0)

//遍历数组friends中的每一项执行传入的函数，preValue表示函数上一次return的值,item表示数组中的当前项。0表示第一次执行函数时(item为数组中第一个数据)的preValue
```



#### 并归方法







