
## Problem 1: Amortized Cost Analysis
### **1. Aggregate Analysis**
We calculate the **total cost** of all operations and divide by **n**.

#### **Step 1: Compute Total Cost**
The cost function is:

$$
C(i) =
\begin{cases}
i, & \text{if } i \text{ is a power of 2} \\
1, & \text{otherwise}
\end{cases}
$$

For **n** operations, we sum up the cost:

$$T(n) = \sum_{i=1}^{n} C(i)$$

#### **Step 2: Break Down Cost Contribution**
1. The number of times $$i$$ is a power of 2 is $$log_2(n)$$ (powers of $$2$$ up to $$n: \(1, 2, 4, 8, \dots\)$$).
2. The sum of powers of 2 is:

   $$\sum_{k=0}^{\log_2{n}} 2^k = 2^{\log_2{n} + 1} - 1 = 2n - 1 \approx O(n)$$

3. The cost of the remaining operations is $$(n - log₂(n))$$ since there are $$n - log_2(n)$$ operations where cost is $$1$$.

Thus, the **total cost** is:

$$
\begin{align}
T(n) = & (n - \log_2 n) + (2n - 1)\\
T(n) = & 3n - \log_2 n - 1
\end{align}
$$


#### **Step 3: Compute Amortized Cost**
$$
\begin{align}
\text{Amortized cost per operation} &= \frac{T(n)}{n} \\
&= \frac{3n - \log_2 n - 1}{n}\\
&= 3 - \frac{\log_2 n}{n} - \frac{1}{n}
\end{align}
$$


For large $$n$$, $$\(\log_2 n / n\) and \(1/n\)$$ approach $$0$$, so:

$$
\text{Amortized cost} = O(3) = O(1)
$$

Thus, using **aggregate analysis**, the amortized cost per operation is $$O(1)$$.


### **2. Amortized Analysis (Accounting Method)**

We assign an **amortized charge** for every operation and use the **stored credit** to balance the actual cost.

#### **Step 1: Assign Credits**
- Assign **3 credits** per operation.
- When an operation costs **1**, store **2 extra credits**.
- When an operation costs **i** (power of 2), **use the extra stored credits** to pay for it.

#### **Step 2: Justification**
- Most operations only cost **1** (storing 2 extra credits).
- The occasional high-cost operations (**powers of 2**) are **paid** using the stored credits.
- Since every operation only **uses or stores** a constant number of credits, the **amortized cost remains constant**.

Thus, using **amortized analysis**, the amortized cost per operation is also **O(1)**.



## Problem 2:  Improving Bubble Sort for Best Case $$O(n)$$ Time Complexity

### **Optimized Bubble Sort Algorithm**
A simple way to **optimize Bubble Sort** is by adding a **boolean flag** to check if any swaps were performed during a pass. If no swaps occur in a full pass, the array is already sorted, and we can terminate early.

#### **Optimized Java Code (BubbleSort1.java)**
```java
public class BubbleSort1 {
    public static void bubbleSort(int[] arr) {
        int n = arr.length;
        boolean swapped;

        for (int i = 0; i < n - 1; i++) {
            swapped = false; // Reset swap flag for each pass

            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    // Swap elements
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    swapped = true; // Set swap flag to true
                }
            }

            // If no swaps occurred, the array is already sorted
            if (!swapped) break;
        }
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5}; // Already sorted input
        bubbleSort(arr);
        
        // Print sorted array
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }
}
```


#### **Why This Works (Best Case $$O(n)$$ Proof)**

1. **Original Bubble Sort Complexity**  
   - Without the `swapped` flag, Bubble Sort **always runs in $$O(n^2)$$**, even if the array is already sorted.

2. **Early Termination Using `swapped` Flag**  
   - If no swaps occur in a full pass, we **break out of the loop**, reducing the time complexity.

3. **Best Case Scenario (Already Sorted Input)**  
   - In the best case, no swaps occur, so the algorithm **only performs one pass** ($$O(n)$$ time complexity).

4. **Final Complexity Analysis**
   - **Best case (already sorted):** $$O(n)$$
   - **Worst case (reversed order):** $$O(n^2)$$
  


## Problem 3: Optimizing Bubble Sort by Reducing Unnecessary Comparisons

### **Problem Statement**
In Bubble Sort, after each pass through the array, the **largest element is placed in its final sorted position**. By leveraging this observation, we can **reduce the number of comparisons in each subsequent pass**. This optimization effectively cuts the running time of Bubble Sort **in half**.

#### **Optimized Approach**
1. **Standard Bubble Sort Review**  
   - In a traditional **Bubble Sort**, each pass compares adjacent elements and moves the largest element to its final position.
   - However, after `i` passes, the **last i elements are already sorted** and do not need further comparisons.

2. **Optimization: Reduce Comparisons in Each Pass**  
   - Instead of always iterating over the entire array, we **reduce the iteration range** after each pass.
   - On the **$i-th$ pass**, only compare up to `n - i - 1` elements, since the last `i` elements are sorted.

```java
public class BubbleSort2 {
    public static void bubbleSort(int[] arr) {
        int n = arr.length;
        boolean swapped;

        for (int i = 0; i < n - 1; i++) {
            swapped = false;
            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    swapped = true;
                }
            }
            if (!swapped) break;
        }
    }

    public static void printArray(int[] arr) {
        for (int num : arr) {
            System.out.print(num + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        int[] arr = {64, 34, 25, 12, 22, 11, 90};
        System.out.println("Original array:");
        printArray(arr);

        bubbleSort(arr);

        System.out.println("Sorted array:");
        printArray(arr);
    }
}

```




#### **Why This Optimization Works**
- The **original Bubble Sort** performs **n-1 passes**, each with **n-1 comparisons** in the worst case, leading to **$$O(n^2)$$ complexity**.
- The **optimized Bubble Sort** reduces unnecessary comparisons:
  - **First pass:** `n-1` comparisons  
  - **Second pass:** `n-2` comparisons  
  - **…**  
  - **Last pass:** `1` comparison  
  - This results in an **average of $$n/2$$ passes**, cutting the number of comparisons in half.

- **Final Complexity Analysis**:
  - **Worst Case:** **$$O(n^2)$$**
  - **Best Case (already sorted, with early termination):** **$$O(n)$$**
  - **Improved Efficiency:** The total number of comparisons is reduced by a **factor of $$2$$**, making the algorithm **twice as fast** compared to the unoptimized version.

#### **Conclusion**
By limiting the number of comparisons in each pass, we significantly reduce the overall computation while preserving the correctness of Bubble Sort. This modified version achieves **better performance while maintaining the same worst-case complexity**.


Thus, this optimized **Bubble Sort** runs in $$O(n)$$ in the best case while maintaining $$O(n^2)$$ **in the worst case**.



