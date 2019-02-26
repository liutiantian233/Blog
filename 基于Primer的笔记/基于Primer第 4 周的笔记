# 命名空间的 using 声明

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-1.jpg)

这是基于C++ Primer的第四周笔记，主要内容为C++的字符和字符串的标准模版库。包括命名空间的声明，标准库类型的字符串，处理字符串对象中的字符和额外的字符串操作。详细请见C++ Primer的3.1节至3.2节和9.5节。

目前为止，我们用到的库函数基本上都属于命名空间的 std，而程序也显式地将这一点标示了出来。例如，std::cin 表示从标准输入中读取内容。此处使用作用域操作符（::）的含义是：编译器应从操作符左侧名字所示的作用域中寻找右侧那个名字。因此，std::cin 的意思就是要使用命名空间 std 中的名字 cin。

上面的方法显得比较繁琐，然而幸运的是，通过更简单的途径也能使用到命名空间中的成员。也就是使用 **using 声明（using declaration）**。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-2.png)

## 每个名字都需要独立的 using 声明

按照规定，每个 using 声明引入命名空间中的一个成员。例如，可以把要用到的标准库中的名字都以 using 声明的形式表示出来，重写的程序如下：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-3.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-4.png)

## 头文件不应包含 using 声明

位于头文件的代码一般来说不应该使用 using 声明。这是因为头文件的内容会拷贝到所有引用它的文件中去，如果头文件里有某个 using 声明，那么每个使用了该头文件的文件就都会有这个声明。对于某些程序来说，由于不经意间包含了一些名字，反而可能产生始料未及的名字冲突。

# 标准库类型 string

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-5.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-6.png)

# 定义和初始化 string 对象

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-7.png)

可以通过默认的方式初始化一个 string 对象，这样就会得到一个空的 string，也就是说，该 string 对象中没有任何字符。如果提供了一个字符串字面值，则该字面值中除了最后那个空字符外其他所有的字符都被拷贝到新创建的 string 对象中去。如果提供的是一个数字和一个字符，则 string 对象的内容是给定字符连续重复若干次后得到的序列。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-8.png)

## 直接初始化和拷贝初始化

C++语言有几种不同的初始化方式，通过 string 我们可以清晰地看到在这些初始化方式之间到底有什么区别和联系。如果使用等号（=）初始化一个变量，实际上执行的是**拷贝初始化（copy initialization）**，编译器把等号右侧的初始值拷贝到新创建的对象中去。与之相反，如果不使用等号，则执行的是**直接初始化（direct initialization）**。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-9.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-10.png)

# string 对象上的操作

一个类除了要规定初始化其对象的方式外，还要定义对象上所能执行的操作。其中，类既能定义通过函数名调用的操作，也能定义 **<< +** 等各种运算符在该类对象上的新含义。下表列举了 string 的大多数操作。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-11.png)

## 读写 string 对象

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-12.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-13.png)

## 读取未知数量的 string 对象

下面编写一个程序用于读取数量未知的 string 对象：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-14.png)

## 使用 getline 读取一整行

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-15.png)

和输入运算符一样，getline 也会返回它的流参数。因此既然输入运算符能作为判断条件，我们也能用 getline 的结果作为条件。例如，可以通过改写之前的程序让它一次输出一整行，而不再是每行输出一个词了：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-16.png)

## string 的 empty 和 size 操作

顾名思义，**empty** 函数根据 string 对象是否为空返回一个对应的布尔值。empty 是 string 的一个成员函数。调用该函数的方法很简单，只要使用点操作符指明是哪个对象执行了 empty 函数就可以了。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-17.png)

## string::size_type 类型

对于 size 函数来说，返回一个 int 或者返回一个 unsigned 似乎都是合情合理的。但其实 size 函数返回的是一个 string::size_type 类型的值，下面就对这种新的类型稍作解释。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-18.png)

尽管我们不太清楚 string::size_type 类型的细节，但是有一点是肯定的：它是一个无符号类型的值，而且能足够存放下任何 string 对象的大小。所有用于存放 string 类的 size 函数返回值的变量，都应该是 string::size_type 类型的。

过去，string::size_type 这种类型有点神秘，不太容易理解和使用。在 C++11 新标准中，允许编译器通过 auto 或者 decltype 来推断变量的类型：

```c++
auto len = line.size();  // len 的类型是 string::size_type
```

由于 size 函数返回的是一个无符号整型数，因此切记，如果在表达式中混用了带符号数和无符号数将可能产生意想不到的结果。例如，假设 n 是一个具有负值的 int，则表达式 s.size() < n 的判断结果几乎肯定是 true。这是因为负值 n 会自动地转换成一个比较大的无符号值。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-19.png)

## 比较 string 对象

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-20.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-21.png)

## 为 string 对象赋值

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-22.png)

## 两个 string 对象相加

两个 string 对象相加得到一个新的 string 对象，其内容是把左侧的运算对象与右侧的运算对象串接而成。也就是说，对 string 对象使用加法运算符（+）的结果是一个新的 string 对象，它所包含的字符由两部分组成：前半部分是加号左侧 string 对象所包含的字符，后半部分是加号右侧 string 对象所包含的字符。另外，复合赋值运算符（+=）负责把右侧 string 对象的内容追加到左侧 string 对象的后面：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-23.png)

## 字面值和 string 对象相加

即使一种类型并非所需，我们也可以使用它，不过前提是该种类型可以自动转换成所需的类型。因为标准库允许把字符字面值和字符串字面值转换成 string 对象，所以在需要 string 对象的地方就可以使用这两种字面值来代替。利用这一点将之前的程序改写为如下形式：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-24.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-25.png)

s4 和 s5 初始化时只用到了一个加法运算符，因此很容易判断是否合法。s6 的初始化形式之前没有出现过，但其实它的工作机理和连续输入连续输出是一样的，可以用如下的形式分组：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-26.png)

# 处理 string 对象中的字符

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-27.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-28.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-29.png)

## 处理每个字符（使用基于范围的 for 语句）

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-30.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-31.png)

for 循环把变量 c 和 str 联系了起来，其中我们定义循环控制变量的方式与定义任意一个普通变量是一样的。此例子，通过使用 auto 关键字让编译器来决定变量 c 的类型，这里 c 的类型是 char。每次迭代，str 的下一个字符被拷贝给 c，因此该循环可以读作“对于字符串 str 中的每个字符 c，执行某某操作。”此例中的“某某操作”即输出一个字符，然后换行。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-32.png)

```c++
string s("Hello World!!!");
// punct_cnt 的类型和 s.size() 的返回类型一样
decltype (s.size()) punct_cnt = 0;
// 统计 s 中标点符号的数量
for (auto c : s)        // 对于 s 中的每个字符
    if (ispunct(c))     // 如果该字符是标点符号
        ++punct_cnt;    // 将标点符号的计数值加一
cout << punct_cnt << " punctuation characters in " << s << endl;
```

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-33.png)

这里我们使用 decltype 关键字声明计数变量 punct_cnt，它的类型是 s.size() 函数返回值的类型，也就是 string::size_type。使用范围 for 语句处理 string 对象中的每个字符并检查其是否是标点符号。如果是，使用递增运算符给计数变量加一。最后，待范围 for 语句结束后输出统计结果。

## 使用范围 for 语句改变字符串中的字符

如果想要改变 string 对象中字符的值，必须把循环变量定义成引用类型。记住，所谓引用只是给定对象的一个别名，因此当使用引用作为循环控制变量时，这个变量实际上被依次绑定到了序列的每个元素上。使用这个引用，我们就能改变它绑定的字符。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-34.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-35.png)

## 只处理一部分字符

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-36.png)

要想访问 string 对象中的单个字符有两种方式：一种是使用下标，另外一种是使用迭代器。

**下标运算符 [ ] **接收的输入参数是 string::size_type 类型的值，这个参数表示要访问的字符的位置，返回值是该位置上字符的引用。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-37.png)

下标的值称作“下标”或**“索引”**，任何表达式只要它的值是一个整型值就能作为索引。不过，如果某个索引是带符号类型的值将自动转换成由 string::size_type 表达的无符号类型。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-38.png)

只要字符串不是常量，就能为下标运算符返回的字符赋新值。例如，下面的程序将字符串的首字符改成了大写形式：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-39.png)

## 使用下标执行迭代

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-40.png)

## 使用下标执行随机访问

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-41.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-42.png)

上述程序的执行过程是这样的：首先初始化变量 hexdigits 令其存放从 0 到 F 的十六进制数字，注意我们把 hexdigits 声明成了常量，这是因为在后面的程序中不打算再改变它的值。在循环内部使用输入值 n 作为 hexdigits 的下标，hexdigits [n] 的值就是 hexdigits 内位置 n 处的字符。例如，如果 n 是 15，则结果是 F，如果 n 是 12，则结果是 C，以此类推。把得到的十六进制数字添加到 result 内，最后一并输出。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-43.png)

# 额外的 string 操作

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-44.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-45.png)

# 构造 string 的其他方法

除了已经介绍过的构造函数，以及与其他顺序容器相同的构造函数外，string 类型还支持另外三个构造函数，如下表所示。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-46.png)

当从一个 string 拷贝字符时，我们可以提供一个可选的开始位置和一个计数值。开始位置必须小于或者等于给定的 string 的大小。如果位置大于 size，则构造函数抛出一个 out_of_range 异常。如果我们传递了一个计数值，则从给定位置开始拷贝这么多个字符。不管我们要求拷贝多少个字符，标准库最多拷贝到 string 结尾，不会更多。

## substr 操作

substr 操作返回一个 string，它是原始 string 的一部分或者全部的拷贝。可以传递给 substr 一个可选的开始位置和计数值：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-47.png)

如果开始位置超过了 string 的大小，则 substr 函数抛出一个 out_of_range 异常。如果开始位置加上计数值大于 string 的大小，则 substr 会调整计数值，只会拷贝到 string 的末尾。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-48.png)

# 改变 string 的其他方法

string 类型支持顺序容器的赋值运算符以及 assign insert 和 erase 操作。除此之外，它还定义了额外的 insert 和 erase 版本。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-49.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-50.png)

## append 和 replace 函数

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-51.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-52.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-53.png)

## 改变 string 的多种重载函数

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-54.png)

# string 搜索操作

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-55.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-56.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-57.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-58.png)

## 指定在哪里开始搜索

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-59.png)

## 逆向搜索

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-60.png)

# compare 函数

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-61.png)

# 数值转换

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-62.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-63.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/fourth-week-64.png)

# 参考链接

[来自官方手册](https://zh.cppreference.com/w/首页)

C++ Primer中文译本（由于文件过大，需自行下载或[联系我](https://liutiantian233.github.io/about/)）
