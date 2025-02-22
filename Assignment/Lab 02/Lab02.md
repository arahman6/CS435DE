# Lab 2: Asymptotic Analysis

## Problem Statement
Determine the **asymptotic running time** of the following procedure:
```java
int[] arrays(int n) {  
    int[] arr = new int[n];  

    for(int i = 0; i < n; ++i) {  
        arr[i] = 1;  
    }  

    for(int i = 0; i < n; ++i) {  
        for(int j = i; j < n; ++j) {  
            arr[i] += arr[j] + i + j;  
        }  
    }  

    return arr;  
}  
```

## **Analysis**
1. The first loop runs $$O(n)$$ times.  
2. The nested loop executes $$O(n^2)$$ operations:  
   - The outer loop runs $$n$$ times.  
   - The inner loop runs from `j = i` to `j = n-1`, executing `(n - i)` times.  
   - The total number of operations is:  
     $$\sum_{i=0}^{n-1} (n - i) = \frac{n(n+1)}{2} = O(n^2)$$  

## **Final Answer**
The overall complexity is $$O(n^2)$$.  




# Lab 2: Merging Two Sorted Arrays

## Problem Statement
Given two sorted arrays of integers, the goal is to design an algorithm that merges them into a single sorted array containing all elements from both input arrays.

### **Example**
#### **Input:**
Array 1: **[1, 4, 5, 8, 17]**  
Array 2: **[2, 4, 8, 11, 13, 21, 23, 25]**  

#### **Output:**
Merged Sorted Array: **[1, 2, 4, 4, 5, 8, 8, 11, 13, 17, 21, 23, 25]**

---

## **A. Pseudocode for Merge Algorithm**
We use a two-pointer approach to efficiently merge the sorted arrays.

**Algorithm `Merge(arr1, arr2)`**
1. Initialize an empty result array `merged[]`.
2. Set two pointers:  
   - `i = 0` (points to the start of `arr1`)  
   - `j = 0` (points to the start of `arr2`)
3. While both pointers are within bounds:
   - If `arr1[i] <= arr2[j]`, append `arr1[i]` to `merged[]` and increment `i`.
   - Else, append `arr2[j]` to `merged[]` and increment `j`.
4. Append any remaining elements of `arr1[]` or `arr2[]` to `merged[]`.
5. Return the merged sorted array.

---

## **B. Asymptotic Running Time**
- Since each element is processed **exactly once**, the time complexity is: $$O(n + m)$$
  where `n` and `m` are the lengths of `arr1` and `arr2`, respectively.

---

## **C. Java Implementation**

```java
int[] merge(int[] arr1, int[] arr2) {  
    int n = arr1.length, m = arr2.length;  
    int[] merged = new int[n + m];  
    int i = 0, j = 0, k = 0;  

    while (i < n && j < m) {  
        if (arr1[i] <= arr2[j]) {  
            merged[k++] = arr1[i++];  
        } else {  
            merged[k++] = arr2[j++];  
        }  
    }  

    while (i < n) {  
        merged[k++] = arr1[i++];  
    }  
    while (j < m) {  
        merged[k++] = arr2[j++];  
    }  

    return merged;  
}  
```

## **Final Answer**
- **Algorithm:** Two-pointer approach.
- **Time Complexity:** $$O(n + m)$$
