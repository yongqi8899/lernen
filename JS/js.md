# VSCode插件和配置
code -> 首选项 -> 设置 -> 打开设置Json
```
"editor.bracketPairColorization.enabled": true, "editor.guides.bracketPairs":"active"
```
# JavaScript变量和数据类型
◼ JavaScript 中有八种基本的数据类型(前七种为基本数据类型，也称为原始类型，而 object 为复杂数据类型，也称为引用类
型)。  

number 用于任何类型的数字:整数或浮点数。  

string 用于字符串:一个字符串可以包含 0 个或多个字符，所以没有单独的单字符类型。 boolean 用于 true 和 false。  

undefined 用于未定义的值 —— 只有一个 undefined 值的独立类型。  

object 用于更复杂的数据结构。  

null 用于未知的值 —— 只有一个 null 值的独立类型。  
## 数据类型的转换
1. 字符串String的转换
-  "字符串"+其他=>"字符串"
- String()函数;
- toString()方法
2. 数字类型Number的转换
- 乘除
- Number()函数
3. 布尔类型Boolean的转换
- Boolean(value) 
- 直观上为“空”的值(如 0、空字符串、null、undefined 和 NaN)将变为 false。
- 包含 0 的字符串 "0" 是 true
- 其他值变成 true。

# JavaScript基础运算符
1. " =" 赋值运算符   
 - 语句 x = value 将值 value 写入 x 然后返回 x。
 - 链式赋值(Chaining assignments): 从右到左进行计算
 ```js
let a,b,c;
a=b=c=2+2;
console.log(a,b,c);
 ```
2.  ** 幂(ES7) 如：2 ** 3 =>8
3. ++和—的位置
- 运算符 ++ 和 -- 可以置于变量前，也可以置于变量后。 - 当运算符置于变量后，被称为“后置形式”(postfix form):counter++。 
- 当运算符置于变量前，被称为“前置形式”(prefix form):++counter。 - 两者都做同一件事:将变量 counter 与 1 相加。  

◼ 他们有什么区别吗?
- 有，但只有当我们使用 ++/-- 的返回值时才能看到区别;
-  如果自增/自减的值不会被使用，那么两者形式没有区别; 
- 如果我们想要对变量进行自增操作，并且 需要立刻使用自增后的值，那么我们需要使用前置形式; 
- 前置形式返回一个新的值，但后置返回原来的值;
