# Math Problem 1: Increasing and Nondecreasing Functions

## Analysis
We analyze whether the given functions are increasing or eventually nondecreasing.

1. **Function:** $$f(x) = -x^2$$
   - **Derivative:** $$f'(x) = -2x$$
   - Since $$f'(x)$$ is negative for $$x > 0$$ and positive for $$x < 0$$, the function is **not increasing**. It is a downward-facing parabola, meaning it is **not eventually nondecreasing** either.

2. **Function:** $$f(x) = x^2 + 2x + 1$$
   - **Derivative:** $$f'(x) = 2x + 2$$
   - For $$x < -1$$, $$f'(x) < 0$$ (decreasing), and for $$x > -1$$, $$f'(x) > 0$$ (increasing).
   - Since it increases for $$x > -1$$, it is **eventually nondecreasing** but not always increasing.

3. **Function:** $$f(x) = x^3 + x$$
   - **Derivative:** $$f'(x) = 3x^2 + 1$$
   - Since $$3x^2 + 1 > 0$$ for all $$x$$, the function is **always increasing**.

## Conclusion
- $$f(x) = -x^2$$: **Neither increasing nor eventually nondecreasing**.
- $$f(x) = x^2 + 2x + 1$$: **Eventually nondecreasing**.
- $$f(x) = x^3 + x$$: **Always increasing**.

---

# Math Problem 2: Asymptotic Growth Comparison

We compare $$f(x)$$ and $$g(x)$$ using Big-O notation.

1. **$$f(x) = 2x^2, g(x) = x^2 + 1$$**
   - $$2x^2 = O(x^2)$$, and $$x^2 + 1 = O(x^2)$$.
   - Both grow at the same rate: **$$f(x) \sim g(x)$$**.

2. **$$f(x) = x^2, g(x) = x^3$$**
   - $$x^2 = O(x^3)$$ but $$x^3 \neq O(x^2)$$.
   - $$f(x)$$ grows **slower** than $$g(x)$$: **$$f(x)$$ grows no faster than $$g(x)$$**.

3. **$$f(x) = 4x + 1, g(x) = x^2 - 1$$**
   - $$4x + 1 = O(x)$$ and $$x^2 - 1 = O(x^2)$$.
   - $$f(x)$$ grows **slower** than $$g(x)$$: **$$f(x)$$ grows no faster than $$g(x)$$**.

## Conclusion
- **(1) $$f(x) \sim g(x)$$ (same asymptotic growth).**
- **(2) $$f(x)$$ grows no faster than $$g(x)$$.**
- **(3) $$f(x)$$ grows no faster than $$g(x)$$.**




# Problem 1: GCD Algorithm

## Solution
To compute the greatest common divisor (GCD) of two integers $m$ and $$n$$, we can use the **Euclidean Algorithm**, which efficiently finds the GCD by repeatedly applying the modulus operation.

### Java Implementation
```java
public class GCD {
    public static int gcd(int m, int n) {
        while (n != 0) {
            int temp = n;
            n = m % n;
            m = temp;
        }
        return m;
    }

    public static void main(String[] args) {
        System.out.println(gcd(48, 18)); // Output: 6
    }
}
```
`Output: 6`

# Problem 2: SubsetSum Problem

## Problem Statement
You are given a set $$S = \{s_0, s_1, \dots, s_{n-1}\}$$ of positive integers and a non-negative integer $$k$$. Your algorithm should determine whether there exists a subset $$T \subseteq S$$ such that:
$$
\sum_{t \in T} t = k
$$
If such a subset exists, return `true`; otherwise, return `false`.

## Brute Force Solution
A brute force approach generates all possible subsets of $S$ and checks if any subset sums to $k$.

### Java Implementation
```java
import java.util.ArrayList;
import java.util.List;

public class SubsetSum {
    public static boolean subsetsum(int[] S, int k, List<Integer> subset, int index) {
        if (k == 0) return true;
        if (index == S.length || k < 0) return false;

        // Include S[index] in the subset
        subset.add(S[index]);
        if (subsetsum(S, k - S[index], subset, index + 1)) return true;
        subset.remove(subset.size() - 1);

        // Exclude S[index] and move to the next element
        return subsetsum(S, k, subset, index + 1);
    }

    public static void main(String[] args) {
        int[] S = {3, 5, 6, 2};
        int k = 10;
        List<Integer> subset = new ArrayList<>();
        System.out.println(subsetsum(S, k, subset, 0) ? subset : "No solution");
    }
}

```



# Problem 3: Greedy Strategy for SubsetSum

## Problem Statement
Consider solving the SubsetSum problem using a **greedy strategy**:
1. Sort the set $S$.
2. Initialize an empty subset $T$.
3. Iterate through the sorted elements, adding an element to $T$ if the sum does not exceed $k$.

## Example Execution
**Given:** $S = \{3, 5, 6, 2\}$ and $k = 10$.
1. After sorting: $S = \{2, 3, 5, 6\}$.
2. Start with $T = \{\}$.
3. Add $2$ to $T$: $T = \{2\}$.
4. Add $3$: $T = \{2, 3\}$.
5. Add $5$: $T = \{2, 3, 5\}$ (sum is $10$).
6. Skip $6$ since $2+3+5+6 > 10$.

Final subset: $T = \{2, 3, 5\}$

## Does This Always Work?
- **No.** The greedy strategy may fail in some cases.
- **Counterexample:** $S = \{1, 2, 4, 8\}, k = 7$.
  - The greedy algorithm picks $\{4, 2, 1\}$, which sums to $7$.
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

## Conclusion
The greedy algorithm works in some cases but does **not always** guarantee a correct solution.

# Problem 4: SubsetSum Problem with Modified Inputs

## Problem Statement
You are given a solution $T$ to a SubsetSum problem with a set $S = \{s_0, s_1, \ldots, s_{n-1}\}$ and $k$ some non-negative integer. (Recall that $T$ is a solution if it is a subset of $S$ the sum of whose elements is equal to $k$.) Suppose that $s_{n-1}$ belongs to $T$. Is it necessarily true that the set $T - \{s_{n-1}\}$ is a solution to the SubsetSum problem with inputs $S'$, $k'$ where $S' = \{s_0, s_1, \ldots, s_{n-2}\}$ and $k' = k - s_{n-1}$? Explain. *Hint*: The sum of an empty set of integers is (by convention) equal to 0.

## Analysis
Yes, it is necessarily true that the set $T - \{s_{n-1}\}$ is a solution to the SubsetSum problem with inputs $S'$ and $k'$.

### Explanation
#### Given:
- $T$ is a solution to the SubsetSum problem with set $S$ and sum $k$.
- $s_{n-1}$ belongs to $T$.

This means:
$$
\sum_{t \in T} t = k
$$
Since $s_{n-1} \in T$, we can write:
$$
\sum_{t \in T - \{s_{n-1}\}} t + s_{n-1} = k
$$
Let $T' = T - \{s_{n-1}\}$. Then:
$$
\sum_{t \in T'} t = k - s_{n-1}
$$
Let $k' = k - s_{n-1}$ and $S' = \{s_0, s_1, \ldots, s_{n-2}\}$.

Since $T' \subseteq S'$ and the sum of the elements in $T'$ is $k'$, $T'$ is a solution to the SubsetSum problem with inputs $S'$ and $k'$.

### Conclusion
Therefore, if $s_{n-1}$ belongs to $T$, then $T - \{s_{n-1}\}$ is necessarily a solution to the SubsetSum problem with inputs $S'$ and $k'$.
