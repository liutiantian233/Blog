# 写在前面

这是基于C++ Primer的第五周笔记，主要内容为C++的函数模版和输出输入的基本标准库。包括函数重载，特殊用途的语言特性，函数模版，IO 类和文件的输入输出。详细请见C++ Primer的6.4节至6.5节，8.1节至8.2节和16.1.1节。

# 函数重载

如果同一作用域内的几个函数名字相同但形参列表不同，我们称之为**重载（overloaded）函数**。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-2.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-3.png)

## 定义重载函数

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-4.png)

## 判断两个形参的类型是否相异

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-5.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-6.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-7.png)

## 重载和 const 形参

顶层 const 不影响传入函数的对象。一个拥有顶层 const 的形参无法和另一个没有顶层 const 的形参区分开来：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-8.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-9.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-10.png)

## const_cast 和重载

const_cast 在重载函数的情景中最有用。举个例子：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-11.png)

## 调用重载的函数

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-12.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-13.png)

# 重载与作用域

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-14.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-15.png)

# 特殊用途语言特征

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-16.png)

# 默认实参

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-17.png)

## 使用默认实参调用函数

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-18.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-19.png)

## 默认实参声明

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-20.png)

## 默认实参初始值

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-21.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-22.png)

# 内联函数和 constexpr 函数

之前我们编写了一个小函数，它的功能是比较两个 string 形参的长度并返回长度较小的 string 的引用。把这种规模较小的操作定义成函数有很多好处，主要包括：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-23.png)

## 内联函数可避免函数调用对开销

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-24.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-25.png)

## constexpr 函数

**constexpr 函数**（constexpr function）是指能用于常量表达式的函数。定义 constexpr 函数的方法与其他函数类似，不过要遵循几项约定：函数的返回类型及所有形参的类型都得是字面值类型，而且函数体中必须有且只有一条 return 语句：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-26.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-27.png)

## 把内联函数和 constexpr 函数放在头文件内

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-28.png)

# 调试帮助

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-29.png)

## assert 预处理宏

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-30.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-31.png)

## NDEBUG 预处理变量

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-32.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-33.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-34.png)

# 定义模版

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-35.png)

# 函数模版

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-36.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-37.png)

## 实例化函数模版

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-38.png)

## 模版类型参数

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-39.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-40.png)

## 非类型模版参数

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-41.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-42.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-43.png)

## inline 和 constexpr 的函数模版

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-44.png)

## 编写类型无关的代码

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-45.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-46.png)

## 模版编译

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-47.png)

## 大多数编译错误在实例化期间报告

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-48.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-49.png)

# IO 库

我们的程序已经使用了很多 IO 库设施了。我们已经介绍了大部分 IO 库设施：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-50.png)

# IO 类

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-51.png)

## IO 类型间的关系

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-52.png)

标准库使我们能忽略这些不同类型的流之间的差异，这是通过**继承机制**（inheritance）实现的。利用模版，我们可以使用具有继承关系的类，而不必了解继承机制如何工作的细节。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-53.png)

# IO 对象无拷贝或赋值

我们不能拷贝或对 IO 对象赋值：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-54.png)

由于不能拷贝 IO 对象，因此我们也不能将形参或返回类型设置为流类型。进行 IO 操作的函数通常以引用方式传递和返回流。读写一个 IO 对象会改变其状态，因此传递和返回的引用不能是 const 的。

# 条件状态

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-55.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-56.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-57.png)

## 查询流的状态

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-58.png)

IO 库定义了一个与机器无关的 `iostate` 类型，它提供了表达流状态的完整功能。这个类型应作为一个位集合来使用。IO 库定义了 4 个 `iostate` 类型的 constexpr 值，表示特定的位模式。这些值用来表示特定类型的 IO 条件，可以与位运算符一起使用来一次性检测或设置多个标志位。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-59.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-60.png)

## 管理条件状态

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-61.png)

# 管理输出缓冲

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-62.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-63.png)

## 刷新输出缓冲区

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-64.png)

## unitbuf 操纵符

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-65.png)

## 关联输入和输出流

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-66.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-67.png)

# 文件输入输出

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-68.png)

# 使用文件流对象

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-69.png)

## 用 fstream 代替 iostream&

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-70.png)

## 成员函数 open 和 close

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-71.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-72.png)

## 自动构造和析构

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-73.png)

# 文件模式

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-74.png)

## 以 out 模式打开文件会丢弃已有数据

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-75.png)

## 每次调用 open 时都会确定文件模式

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fifth-week-76.png)

# 参考链接

[来自官方手册](https://zh.cppreference.com/w/首页)

C++ Primer中文译本（由于文件过大，需自行下载或[联系我](https://liutiantian233.github.io/about/)）
