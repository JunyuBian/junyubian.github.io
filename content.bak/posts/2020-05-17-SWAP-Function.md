---
title: SWAP Function
date: 2020-05-17 19:28:00
<<<<<<< HEAD
categories: 
- Notes
tags:
- Algorithm
- C++
- en
=======
categories:
- Notes
- En
tags:
- Algorithm
- C++
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
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

<!--more-->

# Addition and Subtraction

```C++
int a = 1;
int b = 2;
a = a+b;
b = a-b;
a = a-b;
```

<<<<<<< HEAD
# Multiplication and Division 
=======
# Multiplication and Division
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59

```C++
int a = 1;
int b = 2;
a = a*b;
b = a/b;
a = a/b;
```

# XOR

```C++
<<<<<<< HEAD
int a = 1; 
=======
int a = 1;
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
int b = 2;
a = a^b;
b = b^a; // b = b^(a^b) = b^a^b = b^b^a = 0^a = a
a = a^b; // a = (a^b)^a = a^b^a = a^a^b = 0^b = b
```
<<<<<<< HEAD



=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
