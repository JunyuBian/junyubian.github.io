---
layout: post
title: EMPLACE_BACK in C++
subtitle: EMPLACE_BACK in C++
description: There are different type of containers in C++ STL. To add a new element into the back of a container, we normally use `push_back()`. In this blog, we will look into a new way of performing push back - `emplace_back()`.
excerpt: There are different type of containers in C++ STL. To add a new element into the back of a container, we normally use `push_back()`. In this blog, we will look into a new way of performing push back - `emplace_back()`.
date: 2020-05-16
author: Junyu
tags:
    - algorithm
    - notes
    - c++
URL: "/2020/05/16/emplace_back-in-C++/"
categories: [ Tech ]
---

There are different type of containers in C++ STL. To add a new element into the back of a container, we normally use `push_back()`. In this blog, we will look into a new way of performing push back - `emplace_back()`.

# Background Knowledge

Rvalue References: with aim of increasing the efficiency of C++, rvalues are included. It doesn't  need to copy the value, the rvalue reference is bound to the value itself.

To claim an Rvalue:

```C++
T && T_reference = t;
```

# For emplace_back( )...

How is `emplace_back()` defined:

```C++
template <typename T>
	void emplace_back (T && t);
```

An example for `emplace_back()` from [this blog](https://blog.csdn.net/xiaolewennofollow/article/details/52559364): 

```C++
#include <vector>  
#include <string>  
#include <iostream>  
 
struct President  
{  
    std::string name;  
    std::string country;  
    int year;  
 
    President(std::string p_name, std::string p_country, int p_year)  
        : name(std::move(p_name)), country(std::move(p_country)), year(p_year)  
    {  
        std::cout << "I am being constructed.\n";  
    }
    President(const President& other)
        : name(std::move(other.name)), country(std::move(other.country)), year(other.year)
    {
        std::cout << "I am being copy constructed.\n";
    }
    President(President&& other)  
        : name(std::move(other.name)), country(std::move(other.country)), year(other.year)  
    {  
        std::cout << "I am being moved.\n";  
    }  
    President& operator=(const President& other);  
};  
 
int main()  
{  
    std::vector<President> elections;  
    std::cout << "emplace_back:\n";  
    elections.emplace_back("Nelson Mandela", "South Africa", 1994); //没有类的创建  
 
    std::vector<President> reElections;  
    std::cout << "\npush_back:\n";  
    reElections.push_back(President("Franklin Delano Roosevelt", "the USA", 1936));  
 
    std::cout << "\nContents:\n";  
    for (President const& president: elections) {  
       std::cout << president.name << " was elected president of "  
            << president.country << " in " << president.year << ".\n";  
    }  
    for (President const& president: reElections) {  
        std::cout << president.name << " was re-elected president of "  
            << president.country << " in " << president.year << ".\n";  
    }
 
}
```

The output from the above code would be:

```
emplace_back:
I am being constructed.
 
push_back:
I am being constructed.
I am being moved.
 
Contents:
Nelson Mandela was elected president of South Africa in 1994.
```

### [移动构造函数](https://blog.csdn.net/carbon06/article/details/81222759?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-7.channel_param&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-7.channel_param)

---

对于拷贝构造函数、赋值构造函数必须实现指针变量的深拷贝，可能会造成高耗时。移动构造函数不会进行变量成员的深拷贝，而是交换所有权，避免拷贝时的性能损耗。

声明为：

```c++
className(className &&)
```

### emplace_back()

---

C++11新特性，声明为

```c++
template<class ... Args>
void emplace_back(Arg&& ... args);
```

接收一个右值引用，调用其移动构造函数，将对象移动到容器中。

对比push_back：调用对象拷贝构造函数，容器中存储拷贝后的副本。

### std::move

---

用于将左值转化为右值引用类型。

