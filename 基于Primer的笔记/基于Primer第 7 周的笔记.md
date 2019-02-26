# 写在前面

这是基于C++ Primer的第七周笔记，主要内容为C++的String流，try语句块，异常处理，容器库概览和迭代器。包括throw表达式，抛出异常，捕获异常，异常类层次，容器类型成员，容器定义和初始化，插入迭代器和反向迭代器等。详细请见C++ Primer的8.3节，5.6节，18.1节，9.2节和10.4节。

# String 流

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-2.png)

## 使用 istringstream

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-3.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-4.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-5.png)

## 使用 ostringstrean

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-6.png)

# try 语句块和异常处理

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-7.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-8.png)

## throw 表达式

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-9.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-10.png)

## try 语句块

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-11.png)

### 编写处理代码

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-12.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-13.png)

### 函数在寻找处理代码的过程中退出

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-14.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-15.png)

## 标准异常

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-16.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-17.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-18.png)

# 异常处理

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-19.png)

## 抛出异常

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-20.png)

### 栈展开

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-21.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-22.png)

### 栈展开过程中对象被自动销毁

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-23.png)

### 析构函数与异常

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-24.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-25.png)

### 异常对象

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-26.png)

## 捕获异常

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-27.png)

### 查找匹配的处理代码

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-28.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-29.png)

### 重新抛出

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-30.png)

### 捕获所有异常的处理代码

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-31.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-32.png)

## 函数 try 语句块与构造函数

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-33.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-34.png)

## noexcept 异常说明

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-35.png)

### 违反异常说明

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-36.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-37.png)

### 异常说明的实参

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-38.png)

### noexcept 运算符

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-39.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-40.png)

### 异常说明与指针，虚函数和拷贝控制

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-41.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-42.png)

# 容器库概览

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-43.png)

## 对容器可以保存的元素类型的限制

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-44.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-45.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-46.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-47.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-48.png)

# 迭代器

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-49.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-50.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-51.png)

## 迭代器范围

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-52.png)

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-53.png)

## 使用左闭合范围蕴含的编程假定

![](https://raw.githubusercontent.com/liutiantian233/Blog/master/201902/seventh-week-54.png)

# 容器类型成员



# 参考链接

[来自官方手册](https://zh.cppreference.com/w/首页)

C++ Primer中文译本（由于文件过大，需自行下载或[联系我](https://liutiantian233.github.io/about/)）
