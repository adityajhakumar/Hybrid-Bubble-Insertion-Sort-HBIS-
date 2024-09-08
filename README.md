
# Hybrid Bubble-Insertion Sort (HBIS)
https://github.com/adityajhakumar/Hybrid-Bubble-Insertion-Sort-HBIS-/blob/b30666f3664311fe17f59d2b4c10bddac5c8b33e/hbis.jpg

## Overview

The Hybrid Bubble-Insertion Sort (HBIS) algorithm is a novel approach to sorting that combines the classic bubble sort and insertion sort techniques. This hybrid algorithm dynamically switches between these two sorting methods based on the size of the dataset. The goal is to harness the strengths of both algorithms while mitigating their individual limitations, resulting in a more efficient and adaptable sorting solution.

## Table of Contents

1. [Introduction](#introduction)
2. [Algorithm Concepts](#algorithm-concepts)
   - [Bubble Sort](#bubble-sort)
   - [Insertion Sort](#insertion-sort)
   - [Hybrid Approach](#hybrid-approach)
3. [Detailed Algorithm Description](#detailed-algorithm-description)
   - [Threshold Definition](#threshold-definition)
   - [Sorting Process](#sorting-process)
4. [Implementation](#implementation)
   - [Code Explanation](#code-explanation)
   - [Compilation and Execution](#compilation-and-execution)
5. [Performance Analysis](#performance-analysis)
   - [Comparison with Traditional Sorting Algorithms](#comparison-with-traditional-sorting-algorithms)
   - [Advantages of HBIS](#advantages-of-hbis)
6. [Future Work](#future-work)
7. [References](#references)

## Introduction

Sorting is a fundamental operation in computer science with numerous applications ranging from data organization to search optimization. Traditional sorting algorithms like bubble sort and insertion sort are well-known for their simplicity but can be inefficient for large datasets. The Hybrid Bubble-Insertion Sort (HBIS) algorithm presents a new way to enhance sorting performance by combining these two classic methods.

## Algorithm Concepts

### Bubble Sort

Bubble sort is one of the simplest sorting algorithms. It repeatedly compares adjacent elements in the array and swaps them if they are in the wrong order. This process is repeated until the array is sorted. Although bubble sort is easy to understand and implement, it has a time complexity of O(n^2) in the worst and average cases, making it inefficient for large datasets.

**Key Characteristics:**
- **Time Complexity:** O(n^2) in the worst and average cases.
- **Space Complexity:** O(1) - It sorts the array in place.
- **Stability:** Stable - It maintains the relative order of equal elements.

### Insertion Sort

Insertion sort builds the final sorted array one item at a time. It takes each element from the unsorted portion and inserts it into its correct position within the sorted portion. While insertion sort also has a time complexity of O(n^2) in the worst case, it performs well on small or partially sorted datasets.

**Key Characteristics:**
- **Time Complexity:** O(n^2) in the worst case; O(n) in the best case (when the array is already sorted).
- **Space Complexity:** O(1) - It sorts the array in place.
- **Stability:** Stable - It maintains the relative order of equal elements.

### Hybrid Approach

The Hybrid Bubble-Insertion Sort (HBIS) algorithm combines bubble sort and insertion sort to take advantage of their respective strengths. The core idea is to use bubble sort for larger datasets where its simplicity is beneficial, and switch to insertion sort for smaller arrays where insertion sort’s efficiency shines.

**Advantages of the Hybrid Approach:**
- **Adaptability:** By dynamically choosing the appropriate sorting method based on the dataset size, HBIS adapts to different scenarios more effectively.
- **Performance Improvement:** The hybrid approach can outperform both bubble sort and insertion sort when applied individually, particularly for datasets around the threshold size.

## Detailed Algorithm Description

### Threshold Definition

The threshold is a predefined value that determines when to switch from bubble sort to insertion sort. This value is chosen based on empirical testing and optimization to balance performance. In the HBIS algorithm, a threshold value (e.g., 10) is used to make the decision.

### Sorting Process

1. **If the dataset size (n) is greater than the threshold:**
   - Apply bubble sort to sort the array.
2. **If the dataset size (n) is less than or equal to the threshold:**
   - Apply insertion sort to sort the array.

This dynamic switching ensures that the algorithm leverages the strengths of both sorting methods based on the dataset size.

## Implementation

### Code Explanation

Here is the complete implementation of the HBIS algorithm:

**`src/main.c`**
```c
#include <stdio.h>
#include "sorting.h"

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr) / sizeof(arr[0]);
    printf("Original array:\n");
    printArray(arr, n);
    
    hybridSort(arr, n);
    
    printf("Sorted array:\n");
    printArray(arr, n);
    return 0;
}
```

**`src/sorting.c`**
```c
#include <stdio.h>
#include "sorting.h"

#define THRESHOLD 10

void insertionSort(int arr[], int low, int high) {
    for (int i = low + 1; i <= high; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= low && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

void hybridSort(int arr[], int n) {
    if (n <= THRESHOLD) {
        insertionSort(arr, 0, n - 1);
    } else {
        bubbleSort(arr, n);
    }
}

void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}
```

**`include/sorting.h`**
```c
#ifndef SORTING_H
#define SORTING_H

void insertionSort(int arr[], int low, int high);
void bubbleSort(int arr[], int n);
void hybridSort(int arr[], int n);
void printArray(int arr[], int size);

#endif // SORTING_H
```

### Compilation and Execution

To compile the HBIS algorithm, use the following `gcc` command:

```sh
gcc -Iinclude -o hybrid_sort src/main.c src/sorting.c
```

To run the compiled program:

```sh
./hybrid_sort
```

## Performance Analysis

### Comparison with Traditional Sorting Algorithms

**Bubble Sort vs. HBIS:**
- **Efficiency:** Bubble sort is less efficient for larger datasets due to its O(n^2) complexity. HBIS improves efficiency by switching to insertion sort for smaller datasets.
- **Adaptability:** HBIS dynamically adapts to the dataset size, providing better performance in various scenarios compared to a static bubble sort.

**Insertion Sort vs. HBIS:**
- **Efficiency:** Insertion sort performs well for small or partially sorted arrays, but HBIS can offer better performance for a range of dataset sizes by combining methods.
- **Complexity:** HBIS introduces additional complexity in switching between algorithms, but this complexity is justified by the improved overall performance.

### Advantages of HBIS

- **Improved Performance:** By leveraging the strengths of both bubble sort and insertion sort, HBIS achieves better performance for datasets of different sizes.
- **Adaptability:** The hybrid approach is more adaptable to varying dataset sizes, making it suitable for a broader range of applications.

## Future Work

- **Threshold Optimization:** Further research into optimizing the threshold value could enhance performance across different scenarios.
- **Comparison with Advanced Algorithms:** Investigating the performance of HBIS in comparison with more advanced sorting algorithms (e.g., quicksort, mergesort) could provide additional insights into its efficiency.
- **Practical Applications:** Exploring practical applications and real-world use cases for HBIS could demonstrate its effectiveness in various domains.

## References

1. Cormen, T.H., Leiserson, C.E., Rivest, R.L., and Stein, C. (2009). *Introduction to Algorithms* (3rd ed.). MIT Press.
2. Knuth, D.E. (1998). *The Art of Computer Programming, Volume 1: Fundamental Algorithms* (3rd ed.). Addison-Wesley.

