---
layout: post
title: Diff Array
subtitle: Diff Array
description: In this blog, we will talk about one trick can be used to solve problems to do with frequent addition and subtraction to a subsection of an array
excerpt: In this blog, we will talk about one trick can be used to solve problems to do with frequent addition and subtraction to a subsection of an array
date: 2020-11-08
author: Junyu
tags:
    - algorithm
    - notes
    - c++
URL: "/2020/11/08/Diff-Array/"
categories: [ Tech ]
---

- [Functionality](#functionality)
- [Trick](#trick)
  - [Recovering original array](#recovering-original-array)
  - [Opearting a diff array](#opearting-a-diff-array)

In this blog, we will talk about one trick can be used to solve problems to do with frequent addition and subtraction to a subsection of an array  - [Diff Array](https://labuladong.gitbook.io/algo/suan-fa-si-wei-xi-lie/3.3-yi-xiang-bu-dao-xi-lie/cha-fen-ji-qiao).

# Functionality

Todo with frequent addition and subtraction to a subsection of an array.

e.g. Given array `arr`, add 1 for elements between  `arr[0]` and `arr[3]` inclusively, then, substract 3 for elements between  `arr[2]` and `arr[5]` inclusively, what will be the final `arr`.

# Trick

##Constracting a diff array

Diff array is an array recording the difference between two adjacent elements in `arr`, i.e. `diffArr[i] = arr[i] - arr[i-1]`.

```cpp
vector<int> diffArr(arr.size());
diffArr[0] = arr[0];
for (int i = 0; i < arr.size(); i++) {
  diffArr[i] = arr[i] - arr[i-1];
}
```

## Recovering original array

To recover `arr` from `diffArr`, we are going to add elements in `diffArr` with previous elements (one element before) in `arr`.

```cpp
vecotr<int> result(diffArr.size());
result[0] = diffArr[0];
for (int i = 1; i < diffArr.size(); i++) {
  result[i] = result[i-1]+diff[i];
}
```

## Opearting a diff array

With method mentioned in previous section, to add or substract `amount` for elements between `arr[a]` and `arr[b]` inclusively, we just need `diffArr[a] += amount` and `diffArr[b+1] -= amount`. 

Remember to check `b+1` if it excesses the boundary of array, 
