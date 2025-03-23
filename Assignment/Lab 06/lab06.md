

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

### **Problem 2 Solution**

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

---

#### **Part (b): At Least Half Are Good Pivots?**  
- Total elements: $\( n = 9 \)$.  
- Good pivots: **5**.  
- Threshold for "half": $\( \frac{n}{2} = 4.5 \)$.  
- **Conclusion**: $\( 5 > 4.5 \)$, so $\(\boxed{\text{True}}\)$.  

-   **Valid Good Pivots**: 5,4,3,2,35,4,3,2,3 **(5 elements)**.

-   This matches the original answer.
