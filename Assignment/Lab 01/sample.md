**The Cauchy-Schwarz Inequality**\
$$\left( \sum_{k=1}^n a_k b_k \right)^2 \leq \left( \sum_{k=1}^n a_k^2 \right) \left( \sum_{k=1}^n b_k^2 \right)$$



# Problem 3: Greedy Strategy for SubsetSum

## Problem Statement
Consider solving the SubsetSum problem using a **greedy strategy**:
1. Sort the set $$S$$.
2. Initialize an empty subset $$T$$.
3. Iterate through the sorted elements, adding an element to $$T$$ if the sum does not exceed $$k$$.

## Example Execution
**Given:** $$S = \{3, 5, 6, 2\}$$ and $$k = 10$$.
- After sorting: $$S = \{2, 3, 5, 6\}$$.
- Start with $$T = \{\}$$.
- Add $$2$$ to $$T$$: $$T = \{2\}$$.
- Add $$3$$: $$T = \{2, 3\}$$.
- Add $$5$$: $$T = \{2, 3, 5\}$$ (sum is $$10$$).
- Skip $$6$$ since $$2+3+5+6 > 10$$.

Final subset: $$T = \{2, 3, 5\}$$ ✅

## Does This Always Work?
- **No.** The greedy strategy may fail in some cases.
- **Counterexample:** $$S = \{1, 2, 4, 8\}$$, $$k = 7$$.
  - The greedy algorithm picks $$\{4, 2, 1\}$$, which sums to $$7$$ ✅.
  - However, in some cases, it may miss an optimal subset.

## Java Implementation

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class GreedySubsetSum {
    public static List<Integer> greedySubsetSum(int[] S, int k) {
        Arrays.sort(S); // Sort the set in ascending order
        List<Integer> subset = new ArrayList<>();
        int sum = 0;

        for (int num : S) {
            if (sum + num <= k) {
                subset.add(num);
                sum += num;
            }
        }

        return sum == k ? subset : new ArrayList<>(); // Return subset if valid, else empty list
    }

    public static void main(String[] args) {
        int[] S = {3, 5, 6, 2};
        int k = 10;
        List<Integer> result = greedySubsetSum(S, k);
        System.out.println(!result.isEmpty() ? result : "No solution");
    }
}
```



# Problem 4

**Problem Statement**  
You are given a solution \( T \) to a SubsetSum problem with set \( S = \{s_0, s_1, \ldots, s_{n-1}\} \) and a non-negative integer \( k \).  
- \( T \subseteq S \) and the sum of elements in \( T \) equals \( k \).  
- \( s_{n-1} \in T \).  

**Question**: Is \( T' = T - \{s_{n-1}\} \) necessarily a solution to the SubsetSum problem with inputs:  
- \( S' = \{s_0, s_1, \ldots, s_{n-2}\} \),  
- \( k' = k - s_{n-1} \)?  

---

## Solution

### 1. Sum Calculation  
Since \( T \) is a valid solution:  
$$\sum_{t \in T} t = k$$  
After removing \( s_{n-1} \), the new subset \( T' = T - \{s_{n-1}\} \) has sum:  
$$\sum_{t \in T'} t = \sum_{t \in T} t - s_{n-1} = k - s_{n-1} = k'$$  
This satisfies the new target \( k' \).

---

### 2. Subset Verification  
- \( T \subseteq S \), and \( s_{n-1} \) is explicitly removed.  
- \( T' \subseteq S' = S - \{s_{n-1}\} \).  

---

### 3. Edge Cases  
- **Case 1**: If \( T = \{s_{n-1}\} \):  
  - \( T' = \varnothing \), the empty set.  
  - The sum of \( \varnothing \) is \( 0 \), which matches \( k' = k - s_{n-1} = 0 \) (since \( k = s_{n-1} \)).  

- **Case 2**: If \( s_{n-1} \) is negative:  
  - \( k' = k - s_{n-1} \) could be negative.  
  - SubsetSum allows solutions for any integer \( k' \), so \( T' \) remains valid.  

---

### 4. General Case  
For any \( s_{n-1} \in T \):  
- \( T' \subseteq S' \).  
- \( \sum_{t \in T'} t = k' \).  

---

## Conclusion  
Yes, \( T - \{s_{n-1}\} \) is always a valid solution.  

**Final Answer**:  
$$\boxed{Yes}$$
