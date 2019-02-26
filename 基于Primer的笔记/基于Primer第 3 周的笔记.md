# 写在前面

这是基于C++ Primer的第三周笔记，主要内容为C++的函数和更多的程序类型。包括函数基础，参数传递，返回类型，复合类型，处理类型，引用和指针。详细请见C++ Primer的6.1节至6.3节，2.3节至2.5节。

# 函数

函数是一个命名的代码块，通过调用函数执行相应代码。函数可以有 0 个或多个参数，而且（通常）会产生一个结果。可以重载函数，也就是说，同一个名字可以对应几个不同的函数。

# 函数基础

一个典型的**函数**（function）定义包括以下部分：**返回类型（return type）**，函数名字，由 0 个或多个**形参**（parameter）组成的列表以及函数体。其中，形参以逗号隔开，形参的列表对于一对圆括号之内。函数执行的操作在语句块中说明，该语句块称为**函数体（function body）**。

我们通过**调用运算符**（call operator）来执行函数。调用运算符的形式是一对圆括号，它作用于一个表达式，该表达式是函数或者指向函数的指针：圆括号之内是一个用逗号隔开的**实参**（argument）列表，用实参初始化函数的形参。调用表达式的类型就是函数的返回类型。

## 编写函数

编写一个求数的阶乘的程序。n 的阶乘是从 1 到 n 所有数字的乘积。

程序如下：

```c++
int fact(int val) {
    int ret = 1;          // 局部变量，用于保存计算结果
    while (val > 1)
        ret *= val --;    // 把 ret 和 val 的乘积赋给 ret, 然后 val 减一
    return ret;           // 返回结果
}
```

函数的名字是 fact，作用于一个整型参数，返回一个整型值。在 while 循环内部，在每次迭代时用后置递减运算符将 val 的值减一。return 语句负责结束 fact 并返回 ret 的值。

## 调用函数

要调用 fact 函数，必须提供一个整数值，调用得到的结果也是一个整数：

```c++
int main() {
    int j = fact(5);
    cout << "5! is " << j << endl;
    return 0;
}
```

函数的调用完成两项工作：一是用实参初始化函数对应的形参，二是将控制权转移给被调用函数。此时，**主调函数**（calling function）的执行被暂时中断，**被调函数**（called function）开始执行。

## 形参和实参

实参是形参的初始值。尽管实参于形参存在对应关系，但是并没有规定实参的求值顺序。编译器能以任何可行的顺序对实参求值。

实参的类型必须与对应的形参类型匹配。函数有几个形参，就必须提供相同数量的实参。因为函数的调用规定实参数量应与形参数量一致，所以形参一定会被初始化。

## 函数的形参列表

函数的形参列表可以为空，但是不能省略。想定义一个不带形参的函数，最常用的办法是书写一个空的形参列表。也可以使用关键字 void 表示函数没有形参：

```c++
void f1() {}        // 隐式的定义空形参列表
void f2(void) {}    // 显式的定义空形参列表
```

任意两个形参都不能同名，而且函数最外层作用域中的局部变量也不能使用与函数形参一样的名字。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-3.png)

## 函数返回类型

大多数类型都能用作函数的返回类型。一种特殊的返回类型是 void，它表示函数不返回任何值。函数的返回类型不能是数组类型或函数类型，但可以是指向数组或函数的指针。

# 局部对象

在C++语言中，名字有作用域，对象有**生命周期（lifetime）**。

- 名字的作用域是程序文本的一部分，名字在其中可见。
- 对象的生命周期是程序执行过程中该对象存在的一段时间。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-4.png)

## 自动对象

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-5.png)

## 局部静态对象

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-6.png)

如果局部静态变量没有显式的初始值，它将执行值初始化，内置类型的局部静态变量初始化为 0 。

# 函数声明

和其他名字一样，函数的名字也必须在使用之前声明。类似于变量，函数只能定义一次，但可以声明多次。

函数的声明和函数的定义非常类似，唯一的区别是函数声明无须函数体，用一个分号代替即可。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-7.png)

## 在头文件中进行函数声明

我们建议变量在头文件中声明，在源文件中定义。与之类似，函数也应该在头文件中声明而在源文件中定义。

看起来把函数的声明直接放在使用该函数的源文件中是合法的，也比较容易被人接受；但是这么做可能会很繁琐而且容易出错。相反，如果把函数声明放在头文件中，就能确保同一函数的所有声明保持一致。而且一旦我们想改变函数的接口，只需改变一条声明即可。

定义函数的源文件应该把含有函数声明的头文件包含进来，编译器负责验证函数的定义和声明是否匹配。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-8.png)

# 分离式编译

随着程序越来越复杂，我们希望把程序的各个部分分别存储在不同文件中。为了允许编写程序时按照逻辑关系将其划分开来，C++语言支持所谓的**分离式编译（separate compilation）**。分离式编译允许我们把程序分割到几个文件中去，每个文件独立编译。

## 编译和链接多个源文件

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-9.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-10.png)

# 参数传递

如前所述，每次调用函数时都会重新创建它的形参，并用传入的实参对形参进行初始化。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-11.png)

和其他变量一样，形参的类型决定了形参和实参交互的方式。如果形参是引用类型，它将绑定到对应的实参上；否则，将实参的值拷贝后赋给形参。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-12.png)

## 传值参数

当初始化一个非引用类型的变量时，初始值被拷贝给变量。此时，对变量的改动不会影响初始值：

```c++
int n = 0;   // int 类型的初始变量
int i = n;   // i 是 n 的值的副本
i = 42;      // i 的值改变，n 的值不变
```

传值参数的机理完全一样，函数对形参做的所有操作都不会影响实参。

### 指针形参

指针的行为和其他非引用类型一样。当执行指针拷贝操作时，拷贝的是指针的值。拷贝之后，两个指针是不同的指针。因为指针使我们可以间接地访问它所指的对象，所以通过指针可以修改它所指对象的值：

```c++
int n = 0, i = 42;
int *p = &n, *q = &i;  // p 指向 n; q 指向 i
*p = 42;               // n 的值改变; p 不变
p = q                  // p 现在指向了 i; 但是 i 和 n 的值都不变
```

指针形参的行为与之类似：

```c++
// 该函数接受一个指针, 然后将指针所指的值置为 0
void reset(int *ip) {
    *ip = 0;  // 改变指针 ip 所指对象的值
    ip = 0;   // 只改变了 ip 的局部拷贝, 实参未被改变
}
```

调用 reset 函数之后，实参所指的对象被置为 0，但是实参本身并没有改变：

```c++
int i = 42;
reset(&i);          // 改变 i 的值而非 i 的地址
cout << i << endl;  // 输出 0
```

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-13.png)

## 传引用参数

回忆过去所学的知识，我们知道对于引用的操作实际上是作用在引用所引的对象上：

```c++
int n = 0, i = 42;
int &r = n;  // r 绑定了 n（即 r 是 n 的另外一个名字）
r = 42;      // 现在 n 的值是 42
r = i;       // 现在 n 的值和 i 相同
i = r;       // i 的值和 n 相同
```

引用形参的行为与之类似。通过使用引用形参，允许函数改变一个或多个实参的值。

举个例子，改写上一节的 reset 程序，使其接受的参数是引用类型而非指针：

```c++
// 该函数接受一个 int 对象的引用, 然后将对象的值置为 0
void reset(int &i) {  // i 是传给 reset 函数的对象的另一个名字
    i = 0;            // 改变了 i 所引对象的值
}
```

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-14.png)

### 使用引用避免拷贝

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-15.png)

举个例子，准备编写一个函数比较两个 string 对象的长度。因为 string 对象可能会非常长，所以应该尽量避免直接拷贝它们，这时使用引用形参是比较明智的选择。又因为比较长度无须改变 string 对象的内容，所以把形参定义成对常量的引用：

```c++
// 比较两个 string 对象的长度
bool isShorter(const string &s1, const string &s2) {
    return s1.size() < s2.size();
}
```

当函数无须修改引用形参的值时最好使用常量引用。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-16.png)

### 使用引用形参返回额外信息

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-17.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-18.png)

```c++
// 返回 s 中 c 第一次出现的位置索引
// 引用形参 occurs 负责统计 c 出现的总次数
string::size_type find_char(const string &s, char c, string::size_type &occurs) {
    auto ret = s.size();  // 第一次出现的位置（如果有的话）
    occurs = 0;           // 设置表示出现次数的形参的值
    for (decltype(ret) i = 0; i != s.size(); ++i) {
        if (s[i] == c) {
            if (ret == s.size())
                ret = i;  // 记录 c 第一次出现的位置
            ++occurs;     // 将出现的次数加一
        }
    }
    return ret;           // 出现次数通过 occurs 隐式地返回
}
```

当我们调用 find_char 函数时，必须传入三个实参：作为查找范围的一个 string 对象，要找的字符以及一个用于保存字符出现次数的 size_type 对象。假设 s 是一个 string 对象，ctr 是一个 size_type 对象，则我们通过如下形式调用 find_char 函数：

```c++
auto index = find_char(s, 'o', ctr);
```

调用完成后，如果 string 对象中确实存在 o，那么 ctr 的值就是 o 出现的次数，index 指向 o 第一次出现的位置；否则如果 string 对象中没有 o，index 等于 s.size() 而 ctr 等于 0 。

## const 形参和实参

当形参是 const 时，必须要注意关于顶层 const 的讨论。顶层 const 作用于对象本身：

```c++
const int ci = 42;  // 不能改变 ci, const 是顶层的
int i = ci;         // 正确: 当拷贝 ci 时, 忽略了它的顶层 const
int *const p = &i;  // const 是顶层的, 不能给 p 赋值
*p = 0;             // 正确: 通过 p 改变对象的内容是允许的, 现在 i 变成了 0
```

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-19.png)

```c++
void fcn(const int i) { /* fcn 能够读取 i, 但是不能向 i 写值 */ }
```

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-20.png)

```c++
void fcn(const int i) { /* fcn 能够读取 i, 但是不能向 i 写值 */ }
void fcn(int i) {}      // 错误: 重复定义了 fcn(int)
```

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-21.png)

### 指针或引用形参与 const

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-22.png)

```c++
int i = 42;
const int *cp = &i;  // 正确
const int &r = i;    // 正确
const int &r2 = 42;  // 正确
int *p = cp;         // 错误
int &r3 = r;         // 错误
int &r4 = 42;        // 错误
```

将同样的初始化规则应用到参数传递上可得如下形式：

```c++
int i = 0;
const int ci = i;
string::size_type ctr = 0;
reset(&i);        // 调用形参类型是 int* 的 reset 函数
reset(&ci);       // 错误
reset(i);         // 调用形参类型是 int& 的 reset 函数
reset(ci);        // 错误
reset(42);        // 错误
reset(ctr);       // 错误
// 正确
find_char("Hello World!", 'o', ctr);
```

### 尽量使用常量引用

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-23.png)

## 数组形参

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-24.png)

## main: 处理命令行选项

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-25.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-26.png)

## 含有可变形参的参数

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-27.png)

# 返回类型和 return 语句

return 语句终止当前正在执行的函数并将控制权返回到调用该函数的地方。

return 语句有两种形式：

```c++
return;
return expression;
```

## 无返回值函数

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-28.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-29.png)

## 有返回值函数

return 语句的第二种形式提供了函数的结果。只要函数的返回类型不是 void，则该函数内的每条 return 语句必须返回一个值。return 语句返回值的类型必须与函数的返回类型相同，或者能隐式地转换成函数的返回类型。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-30.png)

### 值是如何被返回的

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-31.png)

### 不要返回局部对象的引用或指针

函数完成后，它所占用的存储空间也随之被释放掉。因此，函数终止意味着局部变量的引用将指向不再有效的内存区域。

返回局部对象的指针也是错误的。一旦函数完成，局部对象被释放，指针将指向一个不存在的对象。

### 调用运算符

调用运算符也有优先级和结合律。调用运算符的优先级与点运算符和箭头运算符相同，并且也符合左结合律。

### 引用返回左值

函数的返回类型决定函数调用是否是左值。调用一个返回引用的函数得到左值，其他返回类型得到右值。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-32.png)

### 列表初始化返回值

C++11 新标准规定，函数可以返回花括号包围的值的列表。类似于其他返回结果，此处的列表也用来对表示函数返回的临时量进行初始化。如果列表为空，临时量执行值初始化；否则，返回的值由函数的返回类型决定。

### 主函数 main 的返回值

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-33.png)

### 递归

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-34.png)

## 返回数组指针

因为数组不能被拷贝，所以函数不能返回数组。不过，函数可以返回数组的指针或引用。

# 复合类型

**复合类型**（compound type）是指基于其他类型定义的类型。C++语言有几种复合类型，这里将介绍两种：引用和指针。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-35.png)

# 引用

**引用**（reference）为对象起了另外一个名字，引用类型引用（refers to）另外一种类型。通过将声明符写成 **&d** 的形式来定义引用类型，其中 **d** 是声明的变量名：

```c++
int ival = 1024;
int &refval = ival;  // refval 指向 ival（是 ival 的另一个名字）
int &refval2;        // 报错: 引用必须被初始化
```

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-36.png)

## 引用即别名

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-37.png)

```c++
refval = 2;        // 把 2 赋给 refval 指向的对象, 此处即是赋给了 ival
int ii = refval;   // 与 ii = ival 执行结果一样
```

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-38.png)

```c++
// 正确: refval3 绑定到了那个与 refval 绑定的对象上, 这里就是绑定到 ival 上
int &refval3 = refval;
// 利用与 refval 绑定的对象的值初始值变量 i
int i = refval;
```

因为引用本身不是一个对象，所以不能定义引用的引用。

## 引用的定义

允许在一条语句中定义多个引用，其中每个引用标识符都必须以符号 **&** 开头：

```c++
int i1 = 1024, i2 = 2048;  // i1 和 i2 都是 int
int &r = i1, r2 = i2;      // r 是一个引用, 与 i1 绑定到一起, r2 是 int
int i3 = 1024, &ri = i3;  // i3 是 int, ri 是一个引用, 与 i3 绑定到一起
int &r3 = i3, &r4 = i2;   // r3 和 r4 都是引用
```

所有引用的类型都要和与之绑定的对象严格匹配。而且，引用只能绑定在对象上，而不能与字面值或者某个表达式的计算结果绑定在一起。

```c++
int &refval4 = 10;    // 错误: 引用类型的初始值必须是一个对象
double dval = 3.14;
int &refval5 = dval;  // 错误: 此处引用类型的初始值必须是 int 型对象
```

# 指针

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-39.png)

```c++
int *ip1, *ip2;      // ip1 和 ip2 都是指向 int 型对象的指针
double dp, *dp2;     // dp2 是指向 double 型对象的指针, dp 是 double 型对象
```

## 获取对象的地址

指针存放某个对象的地址，要想获取该地址，需要使用**取地址符（操作符 & ）**：

```c++
int ival = 42;
int *p = &ival;     // p 存放变量 ival 的地址, 或者说 p 是指向变量 ival 的指针
```

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-40.png)

所有指针的类型都要和它所指向的对象严格匹配：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-41.png)

## 指针值

指针的值（即地址）应属下列 4 种状态之一：

1. 指向一个对象。
2. 指向紧邻对象所占空间的下一个位置。
3. 空指针，意味着指针没有指向任何对象。
4. 无效指针，也就是上述情况之外的其他值。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-42.png)

## 利用指针访问对象

如果指针指向了一个对象，则允许使用**解引用符**（操作符 * ）来访问该对象：

```c++
int ival = 42;
int *p = &ival;
cout << *p;
```

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-43.png)

## 空指针

**空指针**（null pointer）不指向任何对象，在试图使用一个指针之前代码可以首先检查它是否为空。以下列出几个生成空指针的方法：

```c++
int *p1 = nullptr;
int *p2 = 0;
int *p3 = NULL;
```

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-44.png)

## 赋值和指针

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-45.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-46.png)

## 其他指针操作

只要指针拥有一个合法值，就能将它用在条件表达式中。和采用算术值作为条件遵循的规则类似，如果指针的值是 0，条件取 false：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-47.png)

## viod* 指针

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-48.png)

概括来说，以 **void*** 的视角来看内存空间也就仅仅是内存空间，没办法访问内存空间中所存的对象。

# 理解复合类型的声明

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-49.png)

## 定义多个变量

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-50.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-51.png)

## 指向指针的指针

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-52.png)

## 指向指针的引用

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-53.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-54.png)

# const 限定符

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-55.png)

## 初始化和 const

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-56.png)

## 默认情况下，const 对象仅在文件内有效

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-57.png)

# const 的引用

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-58.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-59.png)

## 对 const 的引用可能引用一个并非 const 的对象

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-60.png)

# 指针和 const

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-61.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-62.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-63.png)

## const 指针

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-64.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-65.png)

# 顶层 const

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-66.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-67.png)

# constexpr 和常量表达式

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-68.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-69.png)

## constexpr 变量

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-70.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-71.png)

## 字面值类型

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-72.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-73.png)

## 指针和 constexpr

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-74.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-75.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-76.png)

# 处理类型

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-77.png)

# 类型别名

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-78.png)

其中，关键字 typedef 作为声明语句中的基本数据类型的一部分出现。含有 typedef 的声明语句定义的不再是变量而是类型别名。和以前的声明语句一样，这里的声明符也可以包含类型修饰，从而也能由基本数据类型构造出复合类型来。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-79.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-80.png)

## 指针，常量和类型别名

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-81.png)

# auto 类型说明符

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-82-1.png)

此处编译器将根据 val1 和 val2 相加的结果来推断 item 的类型。如果 val1 和 val2 这两个变量的类型是 double，则 item 的类型就是 double，以此类推。

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-82-2.png)

## 复合类型，常量和 auto

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-83.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-84.png)

其次，auto 一般会忽略掉顶层 const，同时底层 const 则会保留下来，比如当初始值是一个指向常量的指针时：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-85.png)

# decltype 类型指示符

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-86.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-87.png)

## decltype 和引用

如果 decltype 使用的表达式不是一个变量，则 decltype 返回表达式结果对应的类型。有些表达式将向 decltype 返回一个引用类型。一般来说当这种情况发生时，意味着该表达式的结果对象能作为一条赋值语句的左值：

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201901/third-week-88.png)

# 参考链接

[来自官方手册](https://zh.cppreference.com/w/首页)

C++ Primer中文译本（由于文件过大，需自行下载或[联系我](https://liutiantian233.github.io/about/)）
