---
title: KMP Algorithm
date: 2020-04-17 00:31:29
categories: 
- Notes
tags:
- Algorithm
- C++
- 算法
- Tom Show
- en
---

# Background...

Once upon a time, Tom asked his father to find `abab` inside `abcaabababaa`.

Tom's dad did this in a traditional way (brute force). He compared each character of the first string with each character of the second string. When he find one character not matching, for example, the third character in the second string in this case, he start again from the second character of the second string. It went on and on and on...

# Moving on...

Unfortunately, Tom had a bad temper about waiting. He wanted to make some change. Tom noticed that, if the n-th character in the first string happened to be not match, even if he start again, he will make a compare with that character again in the future. Therefore, Tom decided not to start from the begining each time a not match is found.

He talked to his dad, "when we have a not match for the n-th character, if we consider the characters before, we do have a big match, and if so, we actually can use the head of `abab` to try to match the tail of `abab`, the longest mathing substring will be the place for us to start again." 

For example, for `abab`, there will be 3 possible heads: `a`, `ab`, `aba`. And there will be 3 possible tails: `b`, `ab`, `bab`. The **longest matching** is `ab`, so each time there's a not mathing, we don't need to start from begin, instead we can start from the 3-rd character to make a comparison.

# Coding work...

Taking the above thought into real code, c++, for example:

We first need a function to generate all the **longest matching** for each substring of the string we are trying to search.

```c++
int * FindLongestMatching(string first){
  int * tableOfFirst = new int[first.length()];
  tableOfFirst[0] = -1;
  int i = 0;
  int j = -1;
  while (i < p.length() - 1) {
    if (j == -1 || first[i] == first[j]) {
      i++；
      j++；
      tableOfFirst[i] = j;
    }
    else {
      j = tableOfFirst[j];
    }
  }
  return tableOfFirst;
}
```

With this function, we can make a linear time matching:

```c++
int KMP (string first, string second) {
  int i = 0;
  int j = 0;
  int * tableOfFirst = FindLongestMatching(first);
  while (i < second.length() && j < first.length()) {
    if (j == -1 || second[i] == first[j]) {
      i++;
      j++;
    }
    else {
      j = tableOfFirst[j];
    }
  }
  if (j == first.length()){
    return i-j;
  }
  return -1;
}
```

Tom is happy now.