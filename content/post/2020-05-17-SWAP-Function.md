---
layout: post
title: SWAP Function
subtitle: SWAP Function
description: In this blog, we will look into several ways of implementing swap in different ways.
excerpt: In this blog, we will look into several ways of implementing swap in different ways.
date: 2020-05-17
author: Junyu
tags:
    - algorithm
    - notes
    - c++
URL: "/2020/05/17/SWAP-Function/"
categories: [ Tech ]
---

In this blog, we will look into several ways of implementing swap in different ways.

# Intermedia Variable

```c++
int a = 1;
int b = 2;
int tem = a;
a = b;
b = temp;
```

# Addition and Subtraction

```C++
int a = 1;
int b = 2;
a = a+b;
b = a-b;
a = a-b;
```

# Multiplication and Division 

```C++
int a = 1;
int b = 2;
a = a*b;
b = a/b;
a = a/b;
```

# XOR

```C++
int a = 1; 
int b = 2;
a = a^b;
b = b^a; // b = b^(a^b) = b^a^b = b^b^a = 0^a = a
a = a^b; // a = (a^b)^a = a^b^a = a^a^b = 0^b = b
```



