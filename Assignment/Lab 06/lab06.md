

## Problem 1: Show all steps of QuickSort in sorting the array [1, 6, 2, 4, 3, 5]. Use leftmost values as pivots at each step.

```
                            [1,6,2,4,3,5] → [1,2,3,4,5,6]  
                             /                         \  
                         [1] (sorted)             [6,2,4,3,5] → [2,3,4,5,6]  
                                                   /                     \  
                                         [2,4,3,5] → [2,3,4,5]         [6] (sorted)  
                                           /                \  
                                        [2] (sorted)      [4,3,5] → [3,4,5]  
                                                          /           \  
                                                      [3] (sorted)  [4,5] (sorted)  
```
Final sorted Array [1,2,3,4,5,6]


## Problem 2: 

#### **Part (a): Identifying Good Pivots**  
For the array $\( A = [5, 1, 4, 3, 6, 2, 7, 1, 3] \) (\( n = 9 \))$:  
- A **good pivot** $\( x \)$ satisfies:  
  - Number of elements $\( <x < \frac{3n}{4} = 6.75 \)$,  
  - Number of elements $\( >x < 6.75 \)$.  

**Analysis for Each Element**:  

| Element $\( x \)$ | Count $\( <x \)$ | Count $\( >x \)$ | Good Pivot? |  
|-----------------|----------------|----------------|-------------|  
| 5               | 6              | 2              | Yes        |  
| 1 (first)       | 0              | 7              | No         |  
| 4               | 5              | 3              | Yes        |  
| 3 (first)       | 3              | 4              | Yes        |  
| 6               | 7              | 1              | No         |  
| 2               | 2              | 6              | Yes        |  
| 7               | 8              | 0              | No         |  
| 1 (second)      | 0              | 7              | No         |  
| 3 (second)      | 3              | 4              | Yes        |  

**Good Pivots**: $\(\boxed{[5, 4, 3, 2, 3]}\)$.  


#### **Part (b): At Least Half Are Good Pivots?**  
- Total elements: $\( n = 9 \)$.  
- Good pivots: **5**.  
- Threshold for "half": $\( \frac{n}{2} = 4.5 \)$.  
- **Conclusion**: $\( 5 > 4.5 \)$, so $\(\boxed{\text{True}}\)$.  

-   **Valid Good Pivots**: 5,4,3,2,35,4,3,2,3 **(5 elements)**.

-   This matches the original answer.



### Problem 3: findElementEqualToItsIndex(A, start, end)

**Input:** Sorted array $\( A \)$, starting position `start`, ending position `end`

**Output:** `true` if element $\( A[m] = m \)$ is found, `false` otherwise

#### Pseudocode:
```
mid = (start + end) / 2

if A[mid] == mid:
    return true

if A[mid] < mid and start != end:
    return findElementEqualToItsIndex(A, mid + 1, end)

if A[mid] > mid and start != end:
    return findElementEqualToItsIndex(A, start, mid)

return false
```


#### Count of Operations:
| Operation                                   | Count           |
|---------------------------------------------|-----------------|
| Calculate mid                               | 3               |
| Check A[mid] == mid                         | 3               |
| Return true                                 | 1               |
| Check A[mid] < mid and start != end         | 3               |
| Recursive call on right                     | 3 + T(n/2)      |
| Check A[mid] > mid and start != end         | 3               |
| Recursive call on left                      | 2 + T(n/2)      |
| Return false                                | 1               |



#### Recurrence Relation:
$$
T(n) = 
\begin{cases}
7 & \text{if } n = 1 \\
T\left(\dfrac{n}{2}\right) + 10 & \text{otherwise}
\end{cases}
$$



#### Master Theorem Parameters:
$$
a = 1, \quad b = 2, \quad c = 10, \quad d = 7, \quad k = 0
$$

Checking the condition:

$$
a = b^k \\
1 = 2^0 = 1
$$

Since $\( a = b^k \)$, from the master theorem:

$$
T(n) = \Theta\left(n^k \log n\right) = \Theta(\log n)
$$

**Final Asymptotic Time Complexity:**

$$
T(n) = O(\log n)
$$

Because all $log(n)$ functions are bounded by $O(n)$.



## Problem 4. Pivot-Selection Strategy for QuickSort with Worst-Case $O(n \log{n})$

To guarantee that QuickSort has a worst-case running time of $O(n \log{n})$, we need to select a pivot that ensures balanced partitioning every time. The best strategy for this is the **Median-of-Medians Algorithm**.

### Median-of-Medians Pivot Selection
- **Step 1:** Divide the array into groups of 5 elements (the number 5 is chosen to balance complexity and efficiency).
- **Step 2:** Find the median of each group. This takes $O(n)$ time because there are **$n/5$ groups** and finding the median of each group is constant time.
- **Step 3:** Collect all these medians and recursively find the **median of the medians**.
- **Step 4:** Use this **median-of-medians** as the pivot.

### Why does it guarantee $O(n \log{n})$?
- This pivot selection ensures that the pivot is "good" — meaning that it divides the array into reasonably balanced partitions.
- It prevents worst-case behavior (like always picking the smallest or largest element).
- Each recursive call reduces the problem size by a constant fraction.
- The total running time of QuickSort with this pivot selection is bounded by:

$$
T(n) = T\left(\dfrac{n}{5}\right) + T\left(\dfrac{7n}{10}\right) + O(n)
$$

which solves to $O(n \log n)$.

### Final Conclusion:
Using the **Median-of-Medians** as the pivot selection strategy ensures that QuickSort runs in $O(n \log{n})$ even in the worst case.


## Problem 5: Quick Select Median Finding Steps

**Array:** [1, 12, 8, 7, -2, -3, 6]
**n = 7 (odd), so the median is the element at position ⌊n/2⌋ = 3 (0-based index 3, 4th element in sorted array)**
**Target median is 6 (given)**

#### Step 1:
- **Pivot:** 1 (leftmost)
- Partition around 1:
  - Less than pivot: [-2, -3]
  - Equal to pivot: [1]
  - Greater than pivot: [12, 8, 7, 6]
- **Size of left + equal:** 3 (matches position index 2)

#### Step 2:
- **Median is in the right partition** → [12, 8, 7, 6]

#### Step 3:
- **Pivot:** 12 (leftmost of the new array)
- Partition around 12:
  - Less than pivot: [8, 7, 6]
  - Equal to pivot: [12]
  - Greater than pivot: []
- Since our target index is less than the index of 12, we move to **left partition** [8, 7, 6]

#### Step 4:
- **Pivot:** 8
- Partition around 8:
  - Less than pivot: [7, 6]
  - Equal to pivot: [8]
  - Greater than pivot: []
- Still need the 3rd element → go left again to [7, 6]

#### Step 5:
- **Pivot:** 7
- Partition around 7:
  - Less than pivot: [6]
  - Equal to pivot: [7]
  - Greater than pivot: []
- **Since k is 0 (0-based target in the subarray), the answer is the max of left partition or the pivot**

#### Step 6:
- Reached the base → The median is **6**



### Final Answer:
The median of the array `[1, 12, 8, 7, -2, -3, 6]` is **6**, found through QuickSelect.
