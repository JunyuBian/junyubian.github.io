---
title: Sorting Algorithms - Quick Sort
date: 2020-04-23 13:42:56
categories: 
- Notes
tags:
- Algorithm
- C++
- en
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

# Quick Sort

## How to do it...

Divide and conquer.

In each division, seperate the data into two parts. 

All elements in the first part should be all less than the elements in the second part.

Loop until the array is sorted.

<!--more-->

## How to code it...

```c++
int partition(int array[], int left, int right) {
  int pivot;
  if (left < right) {
    int low = left;
    int high = right;
    int key = array[left];
    
    while (low < high) {
      while (array[high] >= ket && low < high) {
				high--;
      }
      array[low] = array[high];
      while (array[low] <= array[high] && low < high) {
        low++;
      }
      array[high] = array[low];
    }
    pivot = low;
    array[pivot] = key;
  }
  return pivot;
} 
```

```c++
void QuickSort(int array[], int left, int right) {
	if (left < right) {
    int pivot = partition(array, left, right);
    QuickSort(array, left, pivot - 1);
    QuickSort(array, pivot + 1, right);
  }
}
```

## How to improve it...

```c++
void QuickSortRandom(int array[], int left, int right) {
	if (left < right) {
    srand(unsigned(time(NULL)));
    int Tem = rand()%(right - left + 1) + left;
    swap(array[left], array[Tem]);
    int pivot = partition(array, left, right);
    QuickSortRandom(array, left, pivot - 1);
    QuickSortRandom(array, pivot + 1, right);
  }
}
```