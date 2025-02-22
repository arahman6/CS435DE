# Problem 01: Asymptotic Analysis

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




# Problem 02: Merging Two Sorted Arrays

## Problem Statement
Given two sorted arrays of integers, the goal is to design an algorithm that merges them into a single sorted array containing all elements from both input arrays.

### **Example**
#### **Input:**
Array 1: $$\[1, 4, 5, 8, 17\]$$  
Array 2: $$\[2, 4, 8, 11, 13, 21, 23, 25\]$$

#### **Output:**
Merged Sorted Array: $$\[1, 2, 4, 4, 5, 8, 8, 11, 13, 17, 21, 23, 25\]$$

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




# Problem 03: Big-O and Little-o Analysis

## Problem Statement
Use the definitions of **Big-O** $$O(f(n))$$ and **Little-o** $$o(f(n))$$ to determine whether each of the following statements is true or false, and provide a proof.

---

### **A. $$1 + 4n^2$$ is $$O(n^2)$$**  
**True** 
By definition, a function $$f(n)$$ is in **$$O(g(n))$$** if there exist positive constants $$c$$ and $$n_0$$ such that:

$$f(n) \leq c \cdot g(n) \quad \text{for all } n \geq n_0$$

Here, $$f(n) = 1 + 4n^2$$ and $$g(n) = n^2$$.  
For large $$n$$, the $$4n^2$$ term dominates, and we can choose $$c = 5$$ and $$n_0 = 1$$, such that:

$$1 + 4n^2 \leq 5n^2$$

Thus, **$$1 + 4n^2$$ is $$O(n^2)$$**.

---

### **B. $$n^2 - 2n$$ is _not_ $$O(n)$$**  
**True** 
For $$O(n)$$, we would need:

$$n^2 - 2n \leq c \cdot n$$

for some constant $$c$$ and sufficiently large $$n$$.  
Dividing both sides by $$n$$:

$$n - 2 \leq c$$

This is **false** for arbitrarily large $$n$$ since the left-hand side grows indefinitely, while $$c$$ is a constant.  
Thus, **$$n^2 - 2n$$ is _not_ $$O(n)$$**.

---

### **C. $$\log(n)$$ is $$o(n)$$**  
**True** 
Little-o $$o(f(n))$$ means:

$$\lim_{n \to \infty} \frac{\log(n)}{n} = 0$$

Since:

$$\frac{\log(n)}{n} \to 0 \quad \text{as } n \to \infty$$

this satisfies the condition for $$ o(n) $$.  
Thus, **$$\log(n)$$ is $$o(n)$$**.

---

### **D. $$n$$ is _not_ $$o(n)$$**  
**True** 
For $$n$$ to be in $$o(n)$$, we require:

$$\lim_{n \to \infty} \frac{n}{n} = 0$$

However:

$$\frac{n}{n} = 1$$

which does **not** tend to zero.  
Thus, **$$n$$ is _not_ $$o(n)$$**.

---

## **Final Answers**
| Statement | True/False |
|-----------|-----------|
| $$1 + 4n^2$$ is $$O(n^2)$$ | True |
| $$n^2 - 2n$$ is _not_ $$O(n)$$ | True |
| $$\log(n)$$ is $$o(n)$$ | True |
| $$n$$ is _not_ $$o(n)$$ | True |




# Problem 04: Power Set Algorithm

## **Problem Statement**
Given a set $$X$$, the **power set** $$P(X)$$ is the set of all subsets of $$X$$. The goal is to compute the power set of a given set using a brute-force approach.

---

## **Algorithm: PowerSet(X)**
### **Input:**  
A list $$X$$ of elements.  

### **Output:**  
A list $$P$$ consisting of all subsets of $$X$$, where elements of $$P$$ are sets.  

### **Steps:**
1. Initialize an empty list $$P$$ to store subsets.
2. Create an empty set $$S$$ and add it to $$P$$.
3. While $$X$$ is not empty:
   - Remove the first element $$f$$ from $$X$$.
   - For each subset $$x$$ in $$P$$:
     - Create a new subset $$T = x \cup \{f\}$$.
     - Add $$T$$ to $$P$$.
4. Return $$P$$.

---

## **Java Implementation**
```java
import java.util.*;  

public class PowerSet {  

    public static List<Set<Integer>> powerSet(List<Integer> X) {  
        List<Set<Integer>> P = new ArrayList<>();  
        P.add(new HashSet<>()); // Add empty set  

        for (int f : X) {  
            List<Set<Integer>> newSubsets = new ArrayList<>();  
            for (Set<Integer> subset : P) {  
                Set<Integer> T = new HashSet<>(subset);  
                T.add(f);  
                newSubsets.add(T);  
            }  
            P.addAll(newSubsets);  
        }  
        return P;  
    }  

    public static void main(String[] args) {  
        List<Integer> X = Arrays.asList(1, 2, 3);  
        List<Set<Integer>> powerSet = powerSet(X);  
        System.out.println(powerSet);  
    }  
}  

```

## **Time Complexity Analysis**
- The number of subsets of a set of size $$n$$ is $$2^n$$.
- Each element in $$X$$ generates new subsets by iterating over $$P$$.
- The overall time complexity is **$$O(2^n)$$**.

---

## **Final Answer**
- **Algorithm:** Iterative subset generation.
- **Time Complexity:** $$O(2^n)$$.
