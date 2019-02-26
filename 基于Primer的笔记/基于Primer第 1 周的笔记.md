# 写在前面

这是基于C++ Primer的第一周笔记，主要内容为C++的基本语句和逻辑运算，数据类型与基础表达式。详细请见C++ Primer的1.1节至1.3节，2.1节至2.2节，4.1节至4.5节和4.11.1节。

# 第一个`Hello World`

都说程序员写毛笔字都是提笔就是Hello World，那么C++的第一个程序介绍也从这里开始吧！

C++的基本构造是从函数（function）开始，其中必有一个main函数，所以C++的基本模版如下：

```c++
int main()
{
    return 0;
}
```

其中的main必定属于int类型，所以需要int进行调用和命名。return为最基本的返回项，可有可无，特定情况下仅仅为保留结果和显示。

**重点：每一句结尾都得有一个 ; 这可能会经常被遗忘！**

关于C++的编译和运行，详情可见[C++的Macbook最佳环境](https://liutiantian233.github.io/tech/2019/mac-cpp-environment.html)

# C++的输入和输出

C++与Python不同的是没有内置最基本的 I/O 语句，采用的是STL库（standard library）来进行 I/O 输入和输出。其中最基本的**标准输入**和**标准输出**分别为**cin**和**cout**。当然标准库里还有两个基本语句**cerr**和**clog**分别为错误和警告。

## 一个标准程序

```c++
#include <iostream>

int main()
{
    std::cout << "Hello World" << std::endl;
}
```

第一行就是调用C++的基础STL标准库，俗称头文件。

## 输出数据

在main函数中的：

`std::cout << "Hello World" << std::endl;`

`<<`叫做**输出运算符**，`endl`叫做**操纵符**，作用分别为输出和短暂缓冲数据。

## 读取数据

这里读取数据采用的是`cin`语句，通常为：

`std::cin >> v1;`

`>>`叫做**输入运算符**，作用显而易见，作为输入数据。

# C++中注释的方法

还记得2018年程序员界最火🔥的两大新闻吗，除了删库跑路，另一个就是同事不写注释，程序员暴走这条了。所以来说，任何程序都应该使用注释来使程序更加易读和易懂。

## C++注释的种类

C++有两种注释，分别为单行和多行注释。单行注释为双斜线开始（//）至此行结束，多行注释为（/\*）开始，（\*/）结束。

值得注意的是，多行注释无法嵌套注释，即：

```c++
/*
 * 嵌套 /* 注释 */
 * 是不可行的
 */
```

# 数据类型

C++中的数据类型包括**算数类型**（arithmetic type）和**空类型**（void），其中空类型不做任何具体的值。

## 算数类型

而算数类型又分为**整型**（包括字符和布尔）和**浮点型**。它们的数据尺寸如下：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/first-week-2.png)

## 类型转换（convert）

顾名思义，这是一种强行将一种类型转换成另一种类型的转换。对于这种转换，在C++中也是允许合法的。比如：

```c++
bool b = 42;     // b 为 true
int i = b;       // i 为 1
i = 3.14;        // i 为 3
double pi = i;   // pi 为 3.0
```

## 字面值常量（literal）

每一个字面值常量都对应了一个数据类型，它们的形式和值决定了它们的数据类型。

### 整型和浮点型字面值

整型字面值可以写成十进制，八进制，十六进制等，0开头的整数为八进制，0x或者0X开头的为十六进制。我们可以用以下任意一种方法代表20：

```c++
20     // 十进制
024    // 八进制
0x14   // 十六进制
```

浮点型字面值一般表现为一个小数或者科学记数法表示的指数，其中指数使用E或者e。

### 字符和字符串表示的字面值

单引号为字符字面值，双引号为字符串字面值。

```c++
'a'        // 字符字面值
"Hello"    // 字符串字面值
```

### 转义序列

一些情况下需要用到转义序列打印**不可打印**的符号，比如：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/first-week-3.png)

### 布尔字面值

true 和 flase 是布尔类型的字面值。

# 变量（variable）

变量在C++中是一种存储类型，可参与运算。

## 变量的定义

首先是**类型说明符（type specifier）**，之后是一个或多个变量，逗号分隔，分号结束。

### 初始值

当对象获得了一个特定的值，我们称之为对象被**初始化**（initialized）了。

**重点：C++中初始化和赋值是两个完全不同的操作！**

### 列表初始化（list initialization）

C++有几种不同的初始化方式，如下，初始化变量 a 为 0：

```c++
int a = 0;
int a = {0};
int a{0};
int a(0);
```

使用中括号初始化在C++11中全面应用。其中的特点是，如果初始化存在丢失数据的风险时，编译器会报错。

### 默认初始化（default initilized）

默认值由变量类型决定！

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/first-week-4.png)

## 变量声明和定义的关系

C++允许**分离式编译**（separate compilation）机制，该机制运行原理为：将程序分隔为若干文件，每个文件可以被独立编译。

而为了支持分离式编译，C++将声明和定义区分开，**声明**（declaration）让程序所知，一个文件如果想使用别处定义的名字，必须包含对那个名字的声明，而**定义**（definition）负责创建与名字关联的实体。

如果想声明变量而不去定义，则添加关键词`extern`！

**注意：变量能且只能被定义一次，却可以被多次声明！**

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/first-week-5.png)

## 标识符（identifier）

由字母数字和下划线组成，必须以字母和下划线开头，对大小写敏感。

如下表，C++本身使用的名字不可作为标识符。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/first-week-6.png)

### 一般性规则

以下规则提高可读性：

- 体现实际含义
- 一般用小写字母
- 自定义的类名称一般大写字母开头
- 由多个单词组成需区分单词

## 名字的作用域（scope）

不论在程序的什么位置，使用到的每一个名字都会指向一个实体。然而，同一个名字如果出现在程序不同的位置也可能是指向不同的实体。**作用域**一般都是以花括号分隔。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/first-week-7.png)

### 嵌套的作用域

作用域可以被彼此包含，**内层作用域（inner scope）**和**外层作用域（outer scope）**。作用域中一旦声明了某个名字，它所嵌套着的所有作用域中都能访问该名字。同时，允许在**内层作用域**中重新定义**外层作用域**已有的名字。

# 表达式

表达式由一个或多个**运算对象**（operand）组成，对表达式求值将得到一个**结果**（result）。字面值和变量是最简单的**表达式**（expression）。把一个**运算符**（operator）和一个或多个运算对象组合就是复杂的表达式。

## 基本概念

C++定义了**一元运算符**（unary operator）和**二元运算符**（binary operator）。

### 组合运算符和运算对象

即运算对象的**求值顺序**（order of evaluation）包括**优先级**（precedence）和**结合律**（associativity）。

### 运算对象转换

详见**算数转换**

### 重载运算符

即自定义运算符。

### 左值和右值

这是一个继承C语言中的概念，但是在C++中就不是那么容易理解的：

- **左值表达式**的求值结果是一个对象或者是一个函数，然而以常量对象为代表的某些左值实际上不能作为赋值语句的左值运算对象。
- 虽然某些表达式的求值结果是对象，但它们是右值，非左值。

做一个简单的归纳：**当一个对象被用作右值的时候，用的是对象的值（内容）；当对象被用作左值的时候，用的是对象的身份（在内存中的位置）。**

**重点！！！**

## 优先级和结合律

即**复合表达式（compound expression）**，**括号无视优先级和结合律**。

## 求值顺序

优先级规定了运算对象的组合方式，但没有说明运算对象按照什么顺序求值。大多数情况下，不会明确指定求值的顺序。

其中有四种运算符规定了求值顺序，它们分别是**逻辑与**，**逻辑或**，**条件运算符**和**逗号运算符**。

### 求值顺序和优先级结合律

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/first-week-10.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/first-week-11.png)

## 算数运算符

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/first-week-8.png)

上表按照优先级排序，以上所有都满足左结合律，意味着当优先级相同时，从左向右顺序进行组合。**算数运算符的运算对象和求值结果都是右值。**

## 逻辑和关系运算符

**逻辑和关系运算符的运算对象和求值结果都是右值。**

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/first-week-9.png)

## 赋值运算符

**赋值运算满足右结合律！赋值运算优先级较低！切勿混淆相等运算符和赋值运算符！**

## 递增和递减运算符

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/first-week-12.png)

# 算数转换（arithmetic conversion）

## 整数提升

负责把小整数类型提升至较大的整数类型。

## 理解算数转换

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/first-week-13.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/first-week-14.png)

# 参考链接

[来自官方手册](https://zh.cppreference.com/w/首页)

C++ Primer中文译本（由于文件过大，需自行下载或[联系我](https://liutiantian233.github.io/about/)）
