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
