# 简单语句

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/second-week-1.jpg)

这是基于C++ Primer的第二周笔记，主要内容为C++的控制语句。包括简单语句，条件语句，迭代语句和跳转语句。详细请见C++ Primer的5.1节至5.5节，跳过5.4.3节。

通常情况下，语句都是按顺序执行，但除非是最简单的程序，不然仅仅执行顺序语句对于程序是远远不够的。所以C++语言提供了一组**控制流**（flow-of-control）语句以支持复杂的语句。

一个表达式末尾加上分号就变成了**表达式语句（expression statement）**。其作用是执行表达式并丢弃求值结果。

## 空语句

最简单的语句就是**空语句（null statement）**，只含有一个分号。

```c++
;  // 空语句
```

空语句被用作于：**语法上需要一条语句，但逻辑上不需要**。一种常见的情况是，当循环的全部工作在条件部分就可以完成时，通常会用到空语句。

```c++
// 重复读如数据直至某次输入的值等于sought
while (cin >> s && s != sought)
    ;  // 空语句
```

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/second-week-2.png)

## 别漏写分号，也别多写分号

因为空语句是一条语句，可以用在任何地方。由于这个原因，很多看起来是非法的语句，往往都是空语句。

```c++
v = v1 + v2;;  // 正确：第二个分号表示一条多余的空语句
```

一般来说空语句是无害的，但如果出现在 if 或者 while 之后，就会改变程序的初衷。

```c++
while (iter != svec.end()) ;  // 循环空语句
    ++iter;
```

**多余的空语句并非总是无害的**

## 复合语句 / 块

**复合语句（compound statement）**是指用花括号括起来的语句和声明的序列。复合语句也被叫做**块（block）**。在块中引入的名字只能在块中内访问。

如果在程序中：**语法上需要一条语句，但逻辑上需要多条语句**。则应该使用复合语句。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/second-week-3.png)

所谓空块，是指内部没有任何语句的一对花括号，空块作用等价于空语句。

# 语句的作用域

可以在 if，switch，while 和 for 语句的控制结构内定义变量。定义在控制结构内的变量只在相应语句的内部可见，一旦语句结束，变量也就超出其作用范围了。

# 条件语句

C++语言提供了两种按条件执行的语句。一种是 if 语句，它根据条件决定控制流。另一种是 switch 语句，它计算一个整型表达式的值，然后根据这个值从几条执行路径中选择一条。

## if 语句（if statement）

**作用：判断一个指定的条件是否为真，根据判断结果决定是否执行另外一条语句。**

if 语句包含两种形式

```c++
if (condition)
    statement
```

```c++
if (condition)
    statement
else
    statement
```

其中 condition 必须使用圆括号括起来。condition 可以是一个表达式，也可以是一个初始化了的变量声明。但不管是表达式还是变量，其类型都必须能转化成布尔类型。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/second-week-4.png)

### 使用 if else 语句

```c++
const vector <string> scores = {"F", "D", "C", "B", "A", "A++"};

// 如果 grade 小于60 对应的字母是 F 否则计算其下标
string = letter;
if (grade < 60)
    letter = scores[0];
else
    letter = scores[(grade - 50) / 10];
```

### 嵌套 if 语句

```c++
if (grade % 10 > 7)
    letter += '+';
else if (grade % 10 < 3)
    letter += '-';
```

### 注意使用花括号

有一种常见的错误：**本来程序中有几条语句应该作为一个块来执行，但是我们忘了用花括号把这些语句包围**。这会违背程序的初衷。

为了避免此类问题，有些代码风格要求在 if 或者 else 之后必须写上花括号（对 while 和 for 语句也有同样的要求）这么做的好处是可以避免代码混乱不清，以后修改代码时如果想添加别的语句，也可以很容易的找到正确的位置。

### 垂悬 else

当一个 if 语句嵌套在另一个 if 语句内部时，很可能 if 分支会多于 else 分支。事实上，这时候问题出现了：**怎么知道某个给定的 else 是和哪个 if 匹配呢？**

这个问题通常称作**悬垂 else（dangling else）**，对于这个问题不同的语言有着不同的解决方式，对于C++而言，它规定 else 与离它最近的尚未匹配的 if 匹配，从而消除了程序的二义性。

### 使用花括号控制执行路径

要想使 else 分支和外层的 if 语句匹配，可以在内层 if 语句的两端加上花括号，使其成为一个块。

## switch 语句（switch statement）

此语句提供了一条便利的途径使得我们能够在若干固定选项中做出选择。

举个例子，统计五个元音字母在一篇文章中出现的次数，程序逻辑应该是：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/second-week-5.jpg)

switch 语句首先对括号里的表达式求值，该表达式紧跟在关键词 switch 的后面，可以是一个初始化的变量声明。表达式的值转换成整数类型，然后与每个 case 标签的值比较。

如果表达式和某个 case 标签的值匹配成功，程序从该标签之后的第一条语句开始执行，直到到达了 switch 的结尾或者遇到一条 break 语句为止。

如果 switch 语句的表达式和所有 case 都没有匹配上，将直接跳转到 switch 结构之后的第一条语句。

case 关键字和它对应的值一起被称为 **case 标签（case label）**。case 标签必须是整型常量表达式。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/second-week-6.png)

任何两个 case 标签的值不能相同，否则就会引发错误。另外，default 也是一种特殊的 case 标签。

### switch 内部的控制流

理解程序在 case 标签之间的执行流程非常重要。如果某个 case 标签匹配成功，将从该标签开始往后顺序执行所有 case 分支，除非程序显式的中断了这一过程，否则直到 switch 的结尾处才会停下。要想避免执行后续的 case 分支代码，我们必须显式的告诉编译器终止执行过程。

大多数情况下，在下一个 case 标签之前应该有一条 break 语句。

然而，也有一些时候默认的 switch 行为才是程序真正需要的。每个 case 标签只能对应一个值，但是有时候我们希望两个或者更多个值共享同一组操作。此时，我们就故意省略 break 语句，使得程序能够连续执行若干个 case 标签。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/second-week-7.png)

C++程序的形式比较自由，所以 case 标签之后不一定非得换行。把几个 case 标签写在一行里，强调这些 case 代表的是某个范围内的值：

```c++
switch (ch) {
    case 'a': case 'e': case 'i': case 'o': case 'u':
        ++count;
        break;
}
```

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/second-week-8.png)

### 漏写 break 容易引发缺陷

有一种常见的错觉是程序只执行匹配成功的那个 case 分支的语句。例如，下面程序的统计结果是错误的：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/second-week-9.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/second-week-10.png)

### default 标签

如果没有任何一个 case 标签可以匹配上 switch 表达式的值，程序将执行紧跟在**default 标签**（default label）后面的语句。

例如，可以增加一个计数值来统计非元音字母的数量，只要在 default 分支内不断递增变量就可以了：

```c++
switch (ch) {
    case 'a': case 'e': case 'i': case 'o': case 'u':
        ++count;
        break;
    default:
        ++other;
        break;
}
```

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/second-week-11.png)

### switch 内部的变量定义

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/second-week-12.png)

# 迭代语句

迭代语句通常称为循环语句，它重复执行操作直到满足某个条件。while 和 for 语句在执行循环体之前检查条件，do while 语句先执行循环体，然后再检查条件。

## while 语句

只要条件为**真**，**while 语句**（while statement）就重复执行循环体，它的语法形式是：

```c++
while (condition)
    statement
```

在 while 结构中，只要 condition 的求值结果为真就一直执行 statement （常常是一个块）。condition 不能为空，如果 condition 第一次求值就是**false**，则 statement 一次都不执行。

while 的条件部分可以是一个表达式或者是一个带初始化的变量声明。通常来说，应该由条件本身或者是循环体设法改变表达式的值，否则循环可能无法终止。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/second-week-13.png)

### 使用 while 循环

当不确定到底要迭代多少次时，使用 while 循环比较合适，比如读取输入的内容就是如此。还有一种情况也应该使用 while 循环，这就是我们想在循环结束后访问循环控制变量。例如：

```c++
vector <int> v;
int i;
// 重复读入数据，直至到达文件末尾或者遇到其他输入问题
while (cin >> i)
    v.push_back(i);
// 寻找第一个负值元素
auto beg = v.begin();
while (beg != v.end() && *beg >= 0)
    ++beg;
if (beg == v.end())
    // 此时我们知道 v 中的所有元素都大于等于0
```

第一个循环从标准输入中读取数据，我们一开始不清楚循环要执行多少次，当 cin 读取到无效数据，遇到其他一些输入错误或是到达文件末尾时循环条件失效。

第二个循环重复执行直到遇到一个负值为止，循环终止后，beg 等于 v.end()，或者指向 v 中一个小于 0 的元素。可以在 while 循环外继续使用 beg 的状态以进行其他处理。

## 传统的 for 语句

**for 语句**的语法形式是：

```c++
for (init-statement; condition; expression)
    statement
```

**关键字 for 及括号里的部分称作 for 语句头。**

init-statement 必须是以下三种形式中的一种：

- 声明语句
- 表达式语句
- 空语句

因为这些语句都以分号作为结束，所以 for 语句的语法形式也可以是这样：

```c++
for (initializer; condition; expression)
    statement
```

一般情况下，init-statement 负责初始化一个值，这个值将随着循环的进行而改变。condition 作为循环控制的条件，只要 condition 为真，就执行一次 statement。如果 condition 第一次的求值结果就是 false，则 statement 一次也不会执行。expression 负责修改 init-statement 初始化的变量，这个变量正好就是 condition 检查的对象，修改发生在每次循环迭代之后。statement 可以是一条单独的语句也可以是一条复合语句。

### 传统 for 循环的执行流程

```c++
// 重复处理 s 中的字符直至我们处理完全部字符或者遇到了一个表示空白的字符
for (decltype(s.size()) index = 0; index != s.size() && !isspace(s[index]); ++index)
    s[index] = toupper(s[index]);  // 将当前字符改写成大写形式
```

求值的顺序如下所示：

1. 循环开始时，首先执行一次 init-statement。此例子中，定义 index 并初始化为 0 。
2. 接下来判断 condition。如果 index 不等于 s.size() 而且在 s[index] 位置的字符不是空白，则执行 for 循环体的内容。否则，循环终止。如果第一次迭代时条件就为假，for 循环体一次也不会执行。
3. 如果条件为真，执行循环体。此例中，for 循环体将 s[index] 位置的字符改写成大写形式。
4. 最后执行 expression。此例中，将 index 的值加 1 。

这 4 步说明了 for 循环第一次迭代的过程。

其中第 1 步只在循环开始时执行一次，第 2 3 4 步重复执行直到条件为假时终止，也就是在 s 中遇到一个空白字符或者 index 等于 s.size() 时终止。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/second-week-14.png)

### for 语句头中的多重定义

和其他的声明一样，init-statement 也可以定义多个对象。但是 init-statement 只能有一条声明语句，因此，所有变量的基础类型必须相同。

举个例子，我们用下面的循环把 vector 的元素拷贝一份添加到原来的元素后面：

```c++
// 记录下 v 的大小，当到达原来的最后一个元素后结束循环
for (decltype(v.size()) i = 0, sz = v.size(); i != sz; ++i)
    v.push_back(v[i]);
```

在这个循环中，我们在 init-statement 里同时定义了索引 i 和循环控制变量 sz。

### 省略 for 语句头的某些部分

for 语句头能省略掉 init-statement，condition 和 expression 中的任何一个（或者全部）。

如果不需要初始化，则我们可以使用一条空语句作为 init-statement。例如，对于在 vector 对象中寻找第一个负数的程序，完全可以用 for 循环改写：

```c++
auto beg = v.begin();
for ( /*空语句*/ ; beg != v.end() && *beg >= 0; ++beg)
    ;  // 什么都不做
```

注意：**分号必须保留以表明我们省略掉了 init-statement。**

说得更准确一点，分号表示的是一个空的 init-statement。在这个循环中，因为所有要做的工作都在 for 语句头的条件和表达式部分完成了，所以 for 循环体也是空的。其中，条件部分决定何时停止查找，表达式部分递增迭代器。

省略 condition 的效果等价于在条件部分写了一个 true。因为条件的值永远是 true，所以在循环体内必须有语句负责退出循环，否则循环就会无休止地执行下去：

```c++
for (int i = 0; /*条件为空*/ ; ++i) {
    // 对 i 进行处理，循环内部的代码必须负责终止迭代过程！
}
```

我们还可以省略掉 for 语句头中的 expression，但是在这样的循环中就要求条件部分或者循环体必须改变迭代变量的值。

举个例子，之前有一个将整数读入 vector 的 while 循环，我们使用 for 语句改写：

```c++
vector <int> v;
for (int i; cin >> i; /*表达式为空*/ )
    v.push_back(i);
```

因为条件部分能改变 i 的值，所以这个循环不需要表达式部分。其中，条件部分不断检查输入流的内容，只要读取完所有的输入或者遇到一个输入错误就终止循环。

## do while 语句（do while statement）

do while 语句和 while 语句十分相似，唯一的区别就是，do while 语句先执行循环体后检查条件。不管条件的值如何，我们都至少执行一次循环。do while 语句的语法形式如下所示：

```c++
do
    statement
while (condition);
```

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/second-week-15.png)

在 do 语句中，求 condition 的值之前首先执行一次 statement，condition 不能为空。

如果 condition 的值为假，循环终止，否则，重复循环过程。condition 使用的变量必须定义在循环体之外。

我们可以使用 do while 循环（不断地）执行加法运算：

```c++
// 不断提示用户输入一对数，然后求其和
string rsp;  // 作为循环的条件，不能定义在 do 内部
do {
    cout << "please enter two values: ";
    int val1 = 0, val2 = 0;
    cin >> val1 >> val2;
    cout << "The sum of " << val1 << " and " << val2 << " = " << val1 + val2 << "\n\n" << "More? Enter yes or no: ";
    cin >> rsp;
} while (!rsp.empty() && rsp[0] != 'n');
```

循环首先提示用户输入两个数字，然后输出和并询问是否继续。条件部分检查用户的回答，如果用户没有回答，或者用户的回答以字母 n 开始，循环都将终止。否则循环继续执行。

因为对于 do while 来说先执行语句或者块，后判断条件，所以不允许在条件部分定义变量，如果允许，则变量的使用出现在定义之前，这显然是不合常理的！

# 跳转语句

跳转语句中断当前的执行过程。C++语言提供了 4 种跳转语句：break，continue，goto 和 return。此笔记暂时记录前三种跳转语句。

## break 语句（break statement）

**break 语句**负责终止离它最近的 while，do while，for 或 switch 语句，并从这些语句之后的第一条语句开始继续执行。

break 语句只能出现在迭代语句或者 switch 语句内部（包括嵌套在此类循环里的语句或块的内部）。break 语句的作用范围仅限于最近的循环或者 switch。

## continue 语句（continue statement）

**continue 语句**终止最近的循环中的当前迭代并立即开始下一次迭代。continue 语句只能出现在 for，while 和 do while 循环的内部，或者嵌套在此类循环里的语句或块的内部。

- 和 break 语句类似的是：出现在嵌套循环中的 continue 语句也仅作用于离它最近的循环。
- 和 break 语句不同的是：只有当 switch 语句嵌套在迭代语句内部时，才能在 switch 里使用 continue。

continue 语句中断当前的迭代，但是仍然继续执行循环。

- 对于 while 或者 do while 语句来说，继续判断条件的值。
- 对于传统的 for 循环来说，继续执行 for 语句头的 expression。
- 对于范围 for 语句来说，则是用序列中的下一个元素初始化循环控制变量。

## goto 语句（goto statement）

**goto 语句**的作用是从 goto 语句无条件跳转到同一函数内的另一条语句。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/second-week-16.png)

goto 语句的语法形式是：

```c++
goto label;
```

其中，label 是用于标记和识别一条语句的标示符。**带标签语句**（labeled statement）是一种特殊的语句，在它之前有一个标示符以及一个冒号：

```c++
end: return;  // 带标签语句，可以作为 goto 目标
```

标签标示符独立于变量或其他标示符的名字，因此，标签标示符可以和程序中其他实体的标示符使用同一个名字而不会相互干扰。goto 语句和控制权转向的那条带标签的语句必须位于同一个函数之内。

和 switch 语句类似，goto 语句也不能将程序的控制权从变量的作用域之外转移到作用域之内：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/second-week-17.png)

向后跳过一个已经执行的定义是合法的。跳回到变量定义之前意味着系统将销毁该变量，然后重新创建它：

```c++
// 向后跳过一个带初始化的变量定义是合法的
begin:
    int sz = get_size();
    if (sz <= 0) {
        goto begin;
    }
```

在上面的代码中，goto 语句执行后将销毁 sz。因为跳回到 begin 的动作跨过了 sz 的定义语句，所以 sz 将重新定义并初始化。

# 参考链接

[来自官方手册](https://zh.cppreference.com/w/首页)

C++ Primer中文译本（由于文件过大，需自行下载或[联系我](https://liutiantian233.github.io/about/)）
