# Lab 4

## Problem 1. Stability of Sorting Algorithms

A sorting algorithm is considered **stable** if it preserves the relative order of equal elements in the sorted output. Below is an analysis of the stability of Insertion Sort, Bubble Sort, and Selection Sort.

### Insertion Sort
- **Stable:** Yes.
- **Explanation:** Insertion Sort maintains stability because it only moves elements when necessary. When an element is inserted into its correct position, it does not swap equal elements, thus maintaining their original order.

### Bubble Sort
- **Stable:** Yes.
- **Explanation:** Bubble Sort only swaps adjacent elements if they are in the wrong order. If two elements are equal, they remain in their original relative order, making Bubble Sort a stable sorting algorithm.

### Selection Sort
- **Stable:** No.
- **Explanation:** Selection Sort finds the smallest element in the remaining array and swaps it with the current position. This swap can change the relative order of equal elements, making Selection Sort an unstable sorting algorithm.

---

## Problem 2. Performing Merge Sort on the Array `[7, 6, 5, 4, 3, 2, 1]`

### Step 1: Splitting the Array
Merge Sort follows a **divide and conquer** approach, breaking the array into smaller subarrays until each contains only one element.

1. Split `[7, 6, 5, 4, 3, 2, 1]` into:
   - Left half: `[7, 6, 5, 4]`
   - Right half: `[3, 2, 1]`
2. Further splitting:
   - `[7, 6]` -> `[7]` and `[6]`
   - `[5, 4]` -> `[5]` and `[4]`
   - `[3, 2, 1]` -> `[3]` and `[2, 1]`
   - `[2, 1]` -> `[2]` and `[1]`

### Step 2: Merging the Subarrays
After breaking down the array, the merging process begins by sorting and combining the subarrays step by step.

1. Merge `[7]` and `[6]` -> `[6, 7]`
2. Merge `[5]` and `[4]` -> `[4, 5]`
3. Merge `[6, 7]` and `[4, 5]` -> `[4, 5, 6, 7]`
4. Merge `[2]` and `[1]` -> `[1, 2]`
5. Merge `[1, 2]` and `[3]` -> `[1, 2, 3]`
6. Merge `[4, 5, 6, 7]` and `[1, 2, 3]` -> `[1, 2, 3, 4, 5, 6, 7]`

### Final Sorted Array:
`[1, 2, 3, 4, 5, 6, 7]`


### Time Complexity Analysis
Merge Sort operates in $$O(n log n)$$ time complexity since it repeatedly splits the array into halves and merges them back together in sorted order.

### Stability of Merge Sort
Merge Sort is a **stable sorting algorithm** because when merging subarrays, equal elements retain their original relative order.

# Problem 3

## **A. Pseudo-code for MergeSortPlus**
MergeSortPlus is a hybrid sorting algorithm that improves Merge Sort by using Insertion Sort for smaller subarrays (size ≤ 20). This optimizes performance because Insertion Sort is efficient for small datasets.

### **Pseudo-code**
1. **Function MergeSortPlus(A, left, right):**
   - If `right - left ≤ 20`:  
     - Use **InsertionSort(A, left, right)** to sort the subarray.
   - Else:  
     - Find the middle index `mid = (left + right) / 2`
     - Recursively call `MergeSortPlus(A, left, mid)`
     - Recursively call `MergeSortPlus(A, mid+1, right)`
     - Merge the sorted subarrays using the standard Merge procedure.

2. **Function InsertionSort(A, left, right):**
   - Iterate over `i` from `left + 1` to `right`
   - Set `key = A[i]`
   - Move elements larger than `key` one position to the right
   - Insert `key` in the correct position

3. **Function Merge(A, left, mid, right):**
   - Merge the two sorted halves into a single sorted array

---

## **B. Java Code for MergeSortPlus**
```java
public class MergeSortPlus {
    
    public static void mergeSortPlus(int[] arr, int left, int right) {
        if (right - left <= 20) {
            insertionSort(arr, left, right);
            return;
        }

        int mid = left + (right - left) / 2;
        mergeSortPlus(arr, left, mid);
        mergeSortPlus(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }

    private static void insertionSort(int[] arr, int left, int right) {
        for (int i = left + 1; i <= right; i++) {
            int key = arr[i];
            int j = i - 1;
            while (j >= left && arr[j] > key) {
                arr[j + 1] = arr[j];
                j--;
            }
            arr[j + 1] = key;
        }
    }

    private static void merge(int[] arr, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;
        
        int[] leftArr = new int[n1];
        int[] rightArr = new int[n2];

        for (int i = 0; i < n1; i++)
            leftArr[i] = arr[left + i];
        for (int j = 0; j < n2; j++)
            rightArr[j] = arr[mid + 1 + j];

        int i = 0, j = 0, k = left;
        
        while (i < n1 && j < n2) {
            if (leftArr[i] <= rightArr[j]) {
                arr[k] = leftArr[i];
                i++;
            } else {
                arr[k] = rightArr[j];
                j++;
            }
            k++;
        }

        while (i < n1) {
            arr[k] = leftArr[i];
            i++;
            k++;
        }

        while (j < n2) {
            arr[k] = rightArr[j];
            j++;
            k++;
        }
    }
}
```


## **C. Running Time Comparison of MergeSort and MergeSortPlus**

```java
import java.util.Arrays;
import java.util.Random;

class Main {
    static int[] theArray;

    public static void merge(int[] arr, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;

        int[] leftArr = new int[n1];
        int[] rightArr = new int[n2];

        for (int i = 0; i < n1; i++)
            leftArr[i] = arr[left + i];
        for (int j = 0; j < n2; j++)
            rightArr[j] = arr[mid + 1 + j];

        int i = 0, j = 0, k = left;

        while (i < n1 && j < n2) {
            if (leftArr[i] <= rightArr[j]) {
                arr[k] = leftArr[i];
                i++;
            } else {
                arr[k] = rightArr[j];
                j++;
            }
            k++;
        }

        while (i < n1) {
            arr[k] = leftArr[i];
            i++;
            k++;
        }

        while (j < n2) {
            arr[k] = rightArr[j];
            j++;
            k++;
        }
    }

    public static void mergeSort(int[] arr, int left, int right) {
        if (left >= right)
            return;

        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }

    public static void mergeSortPlus(int[] arr, int left, int right) {
        if (right - left <= 20) {
            insertionSort(arr, left, right);
            return;
        }

        int mid = left + (right - left) / 2;
        mergeSortPlus(arr, left, mid);
        mergeSortPlus(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }

    private static void insertionSort(int[] arr, int left, int right) {
        for (int i = left + 1; i <= right; i++) {
            int key = arr[i];
            int j = i - 1;
            while (j >= left && arr[j] > key) {
                arr[j + 1] = arr[j];
                j--;
            }
            arr[j + 1] = key;
        }
    }

    public static void main(String[] args) {
        int n = 10000; // Size of test array
        int numRuns = 10000;
        long totalMergeSortTime = 0;
        long totalMergeSortPlusTime = 0;
        boolean allIdentical = true;

        for (int run = 0; run < numRuns; run++) {
            int[] originalArray = new Random().ints(n, 0, 10000).toArray();
            int[] array1 = Arrays.copyOf(originalArray, originalArray.length);
            int[] array2 = Arrays.copyOf(originalArray, originalArray.length);

            long startTime = System.nanoTime();
            mergeSortPlus(array1, 0, array1.length - 1);
            long endTime = System.nanoTime();
            totalMergeSortPlusTime += (endTime - startTime);

            startTime = System.nanoTime();
            mergeSort(array2, 0, array2.length - 1);
            endTime = System.nanoTime();
            totalMergeSortTime += (endTime - startTime);

            if (!Arrays.equals(array1, array2)) {
                allIdentical = false;
            }
        }

        double avgMergeSortPlusTime = totalMergeSortPlusTime / (double) numRuns;
        double avgMergeSortTime = totalMergeSortTime / (double) numRuns;

        System.out.println("Average MergeSortPlus Execution Time over " + numRuns + " runs: " + avgMergeSortPlusTime + " ns");
        System.out.println("Average MergeSort Execution Time over " + numRuns + " runs: " + avgMergeSortTime + " ns");
        System.out.println("Were all sorted arrays identical across all runs? " + (allIdentical ? "Yes" : "No"));
    }
}


// Output for 10000 sample size with 10000 simulation
Average MergeSortPlus Execution Time over 10000 runs: 883965.9926 ns
Average MergeSort Execution Time over 10000 runs: 1127342.644 ns
Were all sorted arrays identical across all runs? Yes

=== Code Execution Successful ===


```

To compare the performance of **MergeSort** and **MergeSortPlus**, I run tests measuring their execution times on the same dataset. The steps involved in testing are as follows:

1.  **Generate a random array of integers** of size **n = 10000**.
2.  **Make a copy of the array** to ensure both algorithms sort the same input.
3.  **Measure the execution time** of **MergeSortPlus**.
4.  **Measure the execution time** of **MergeSort**.
5.  **Compare the execution times and verify correctness** run **10000 simulation** for checking if both sorted outputs are identical.

### Conclusion from the Experiment

#### Performance Comparison:

-   **MergeSortPlus Average Execution Time:** **883,965.99 ns**
-   **MergeSort Average Execution Time:** **1,127,342.64 ns**
-   **Difference:** MergeSortPlus is approximately **21.6% faster** than standard MergeSort.

#### Key Observations:

1.  **MergeSortPlus is Faster:**

    -   This is expected because **InsertionSort is efficient for small subarrays** (size ≤ 20).
    -   When the recursion reaches small subarrays, switching to **InsertionSort reduces overhead** compared to recursive calls in MergeSort.
2.  **MergeSortPlus Outperforms in Practical Cases:**

    -   **InsertionSort has O(n²) worst-case time**, but it is efficient **for small inputs**.
    -   **MergeSort has O(n log n) complexity**, but its recursive overhead is **not negligible** for small subarrays.
3.  **Correctness is Maintained:**

    -   The results confirm that **MergeSort and MergeSortPlus produce identical sorted arrays**, ensuring **MergeSortPlus is a valid optimization**.

#### Final Verdict:

**MergeSortPlus is a better alternative to standard MergeSort** in real-world scenarios where **recursive calls can be optimized for small subarrays**. This confirms that **hybrid sorting approaches can be practical in performance-critical applications**.


## Problem 4
### **Binary Trees**

#### **(a) Four Different Binary Trees of Height 3**

A binary tree of height 3 means the longest path from the root to a leaf contains 3 edges (4 levels). Below are four different binary trees with varying numbers of nodes:

**1. Full Binary Tree (Balanced, Maximum Nodes)**
- Each node has two children except for the leaves.
- Number of nodes: **15**  

```markdown
          1
       /     \
      2       3
    /   \    /   \
    4    5   6     7
  / \   / \ / \   / \ 
  8 9 10 11 12 13 14 15
```


**2. Skewed Left Tree**
- Each node has only a left child.
- Number of nodes: **4**  

```markdown
        1
       /
      2
     /
    3
   /
  4
```


**3. Skewed Right Tree**
- Each node has only a right child.
- Number of nodes: **4**  

```markdown
  1
   \
    2
     \
      3
       \
        4
```


 **4. Partially Filled Tree**
- Some nodes have one child, others have two.
- Number of nodes: **7**  

```markdown
        1
       / \
      2   3
     /     \
    4       5
   /         \
  6           7
```

Each of these trees satisfies the height condition while having a unique number of nodes.

---

#### **(b) Verifying the Statement**

**Statement:** Every binary tree of height 3 has at most $2^3 = 8$ leaves.

- A **full binary tree** (where every node has 0 or 2 children) has the maximum number of leaves at height 3, which is:

$$2^3 = 8$$

- If a tree is **not full**, the number of leaves is **less than 8**.
- From the examples drawn, it is confirmed that no binary tree of height 3 can have more than 8 leaves.

**Conclusion:**  
The statement is **true** because in the worst-case scenario, the maximum number of leaves in a binary tree of height 3 is **8**.

---

#### **(c) Generalization for Any Height $n$**

For a binary tree of height $n$:

- The **maximum number of leaves** in a full binary tree follows the formula:

$$
2^n
$$

- This occurs when all levels are completely filled.
- If the tree is not full, the number of leaves is **less than** $2^n$.

Thus, the maximum number of leaves in a binary tree of height $n$ is $2^n$.


