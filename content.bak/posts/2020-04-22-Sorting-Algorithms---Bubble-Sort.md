---
title: Sorting Algorithms - Bubble Sort
date: 2020-04-22 09:23:36
categories:
- Notes
- En
tags:
- Algorithm
- C++
---

In this series of blogs, we will talk about different sorting algorithms.

All the algorithms in the table below will be covered.

| Algorithm                          | Time Complexity (Average Case) | Time Complexity (Worst Case) | Time Complexity (Best Case) | Merg    | Stability  |
| ---------------------------------- | ------------------------------ | ---------------------------- | --------------------------- | ------- | ---------- |
| Bubble Sort                        | O(N^2)                         | O(N^2)                       | O(N^2)                      | O(1)    | Stable     |
| Quick Sort                         | O(NlogN)                       | O(N^2)                       | O(NlogN)                    | O(logN) | Not Stable |
| Quick Sort (with Random Selection) | O(NlogN)                       | O(NlogN)                     | O(NlogN)                    | O(logN) | Not Stable |
| Insertion Sort                     | O(N^2)                         | O(N^2)                       | O(N)                        | O(1)    | Stable     |
| Selection Sort                     | O(N^2)                         | O(N^2)                       | O(N^2)                      | O(1)    | Not Stable |
| Heap Sort                          | O(NlogN)                       | O(NlogN)                     | O(NlogN)                    | O(1)    | Not Stable |
| Merge Sort (with double divides)   | O(NlogN)                       | O(NlogN)                     | O(NlogN)                    | O(N)    | Stable     |
| Merge Sort (with multi divides)    | O(NlogN)                       | O(NlogN)                     | O(NlogN)                    | O(N)    | Stable     |
| Counting Sort                      | O(N+M)                         | O(N+M)                       | O(N+M)                      | O(N+M)  | Stable     |
| Bucket Sort                        | O(N+M)                         | O(N^2)                       | O(N+M)                      | O(N+M)  | Stable     |
| Radix Sort                         | O(N*M)                         | O(N*M)                       | O(N*M)                      | O(N+M)  | Stable     |

# Bubble Sort

## How to do it...

Compare the adjacent elements.

If the first element is greater than the second element, swap them.

Loop until reaching the last pair of elements.

Repeat until all the array is sorted.

<!--more-->

## How to code it...

```c++
void BubbleSort(int array[]) {
  for (int i = 0; i < array.length(); i++) {
  	for (int j = 0; i < array.length() - i; j++) {
			if (array[j] > array[j+1]) {
      	swap(array[j], array[j+1]);
    	}
  	}
	}
}
```

## How to improve it...

We can make a judgement before we do the algorithm.

Check whether the array is already sorted or not.

```c++
void BubbleSortwithCheck(int array[]) {
	for (int i = 0; i < array.length(); i++) {
  	bool sorted = true;
  	for (int j = 0; j < length() - i; j++) {
			if (array[j] > array[j+1]) {
      	swap(array[j], array[j+1]);
      	sorted = false;
    	}
  	}
  	if (sorted) {
			break;
  	}
	}
}
```
