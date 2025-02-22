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
