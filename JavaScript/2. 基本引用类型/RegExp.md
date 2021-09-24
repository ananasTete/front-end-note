## 正则表达式



正则表达式是一种引用类型。

```javascript
let test = /pattern/flags ；   //模式，标记（是可选的）
```

```javascript
let test = new RegExp('pattern','flags');  //标记参数是可选的。
```



### 语法



#### 1. 标记：

每个正则表达式可以有0个或多个标记。

| g    | 查找字符串的全部内容，而不是找到第一个匹配项就结束 |
| ---- | -------------------------------------------------- |
| i    | 不区分大小写                                       |
| m    | 多行模式，查找到一行文本末尾时会继续查找           |
| y    | 黏附模式，只从字符串的lastIndex之后的内容匹配模式  |
| u    |                                                    |
| s    |                                                    |

g和m有什么区别？



#### 2. 模式：



1.  英文句号`.`匹配**任意单个**字符，不会匹配换行符。
2. 字符集：中括号`[ ]` 匹配括号内范围的**单个**字符。
   1. `[^ ]` 匹配**非**括号内范围的单个字符。
   2. `[.]` 匹配点而不是任意字符，相当于`.`的转义字符。


| .    | 任意单个字符 |
| ---- | ------------ |
| \w   | [A-Za-z0-9]  |
| \W   | [^\w]        |
| \d   | [0-9]        |
| \D   | [^\d]        |
| \s   | 空格符       |
| \S   | [^\s]        |

3. 重复`* + ?`
   1. `*`表示将上一个匹配规则重复0次或多次。
   2. `+`表示将上一个匹配规则重复1次或多次。
   3. `?` 表示上一个匹配规则可有可无，即匹配0次或1次。

```javascript
let test = /cat*/;  //表示ca(0次),cat,catt,,,,,,
let test = /[a-z]*/; //表示任意数量的a-z内的任意字符

let test = /cat+/;  //表示cat(1次),catt,cattt,,,,,,,
let test = /c.+t/;  //表示c开头，中间有一个或一个以上的任意字符，以t结尾

let test = /[Tt]?he/; //表示he,The,the
```

4. 花括号`{}` 指定重复次数

```javascript
let test = /t{2}/   //表示tt
let test = /t{2,}/   //表示重复两次或两次以上，tt,ttt,tttt,,,,
let test = /t{2,4}/  //表示tt,ttt,tttt三种
```

5. 字符组`()` 

```javascript

```

6. 分支结构`|`

```javascript
let test = /the|ar/ ;   //the或ar
```

7. 断言

- 正向先行断言`(?=...)`

```javascript
let test = /(T|t)he(?=\sfat)/ ;  //表示后面跟着 fat的The或the。\s表示空格符
```

- 负向先行断言`(?!...)`

```javascript
let test = /(T|t)he(?!\sfat)/ ;   //表示后面不跟着 fat的The或the。\s表示空格符
```

- 正向后行断言`(?<=...)`

```javascript
let test = /(?<=(T|t)he\s)(fat|mat)/ ;  //表示前面跟着The 或the 的fat或mat
```

- 负向后行断言`(?<!..)`

```javascript
let test = /(?<!(T|t)he\s)(fat|mat)/ ;  //表示前面不跟着The 或the 的fat或mat
```



#### 3. 转义字符：

当需要匹配形如`( [ { \ ^ $ | ) ] } ? * + . ` 等字符时为了加以区分，需要对其进行转义。

```javascript
// 匹配第一个"[bc]at"，忽略大小写
let pattern2 = /\[bc\]at/i;

// 匹配所有".at"，忽略大小写
let pattern4 = /\.at/gi; 
```

当我们通过`new RegExp('pattern','flags');`方式定义正则时，需要进一步转义，即\翻倍。

```javascript
// 匹配第一个"[bc]at"，忽略大小写
let pattern2 = /\[bc\]at/i;
let pattern2 = new RegExp('\\[bc\\]at','i')

//匹配第一个字符是[A-Za-z0-9]中的一个，后跟\hello\123
let pattern3 = /\w\\hello\\123/;
let pattern3 = new RegExp('\\w\\\\hello\\\\123')
```







### 正则表达式的实例方法



1. `exec()`       表示在字符串上运用此正则。接收一个参数，即被匹配的字符串。
2. `test()`



#### exec()



1. 主要用于配合捕获组使用。
2. 找到匹配项会返回一个动态数组；没有找到匹配项返回 `null` 。
3. 数组有两个属性`index` 和`input` 分别返回 字符串中的此次起始匹配位置 和 被匹配的字符串。



**捕获组**

当正则表达式中包含字符组即 `()` 时，执行`exec()` 后返回的数组第0个元素保存整个正则的匹配结果，第1，第2，等等元素按从左到右，从外到里的顺序保存各字符组的匹配结果。此时各字符组被称为捕获组。

可以利用这一特性在定义正则表达式时，通过字符组对其进行有意识地拆分，用以获取和使用各捕获组的匹配结果。

- 正则表达式没有捕获组，返回的数组只包含一个元素即第0个元素保存整个正则的匹配结果。

```javascript
let text = 'cat, bat, sat, fat';
let test = /bat/;
let result = test.exec(text);
document.write(result[0]);
```

- 正则表达式中有捕获组，按从左到右，从外到里的顺序分别匹配各捕获组并保存。

```javascript
let text = 'cat, bat, sat, fat';
let test = /(b)(at)/;
let result = test.exec(text);
document.write(result.index+'\t');
document.write(result[0]+'\t');
document.write(result[1]+'\t');  
document.write(result[2]);
//结果为5 bat b at 
//result[0]匹配/(b)(at)/
//result[1]匹配/(b)/
//result[2]匹配/(at)/
```

- 非捕获组：用于匹配模式但不保存匹配结果

```javascript
(?:pattern)     //形如此式
断言             //特殊的非捕获组
```





**全局搜索g**

- 正则表达式使用全局搜索g标记：每次执行`exec()` 会依次返回匹配结果。即执行一次返回第一个匹配结果，执行第二次返回第二个匹配结果，以此类推。
- 正则表达式不使用全局搜索g标记：每次执行`exec()` 只会返回第一个匹配结果。



#### test()



- 接受一个字符串参数，判断此字符串是否符合此正则。
- 返回一个布尔值即`true flase`
- 主要用于验证用户输入。

```javascript
let text = "000-00-0000";
let pattern = /\d{3}-\d{2}-\d{4}/;
if (pattern.test(text)) {
 console.log("The pattern was matched.");
} 
```







