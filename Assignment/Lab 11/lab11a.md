# Lab 11A – Dynamic Programming

## Q1 – 0/1 Knapsack with Item Tracking

### Problem Statement

Modify the classical dynamic programming solution of the 0/1 Knapsack problem to not only compute the maximum value, but also to **track the items** selected using a `Keep[i][w]` array.

### Updated Knapsack Algorithm with Item Tracking

#### Inputs:
- `n`: number of items
- `W`: total capacity
- `v[]`: values of items (1-based index)
- `w[]`: weights of items (1-based index)



### Pseudo-code

```plaintext
function KnapsackWithTracking(n, W, v, w):
    let V[0..n][0..W] be a table of zeros
    let Keep[0..n][0..W] be a table of false values

    for i from 1 to n:
        for j from 0 to W:
            if w[i] <= j:
                if V[i-1][j] < v[i] + V[i-1][j - w[i]]:
                    V[i][j] = v[i] + V[i-1][j - w[i]]
                    Keep[i][j] = true
                else:
                    V[i][j] = V[i-1][j]
                    Keep[i][j] = false
            else:
                V[i][j] = V[i-1][j]
                Keep[i][j] = false

    // Trace back to find items selected
    j = W
    for i from n down to 1:
        if Keep[i][j] == true:
            print "Item", i, "selected (value:", v[i], ", weight:", w[i], ")"
            j = j - w[i]

    return V[n][W] // the maximum value
```



### Explanation

- `V[i][j]` stores the maximum value using first `i` items and capacity `j`.
- `Keep[i][j]` stores whether item `i` was used to get that value.
- After building the tables, trace back using `Keep[i][j]` to list the items included in the optimal solution.



### Sample Output (for small input)

```
Item 3 selected (value: 60, weight: 10)
Item 1 selected (value: 100, weight: 20)
Max value = 160
```

---

## Q2 – Time Complexity of Dynamic Programming Solution

### Question

Determine the running time complexity of your pseudo code. Has the Dynamic Programming approach of solving the Knapsack problem changed the exponential time complexity of the original brute-force solution?



### Answer

#### Time Complexity of the DP Algorithm:

The dynamic programming approach uses a table `V[n+1][W+1]` where:

- `n` = number of items
- `W` = total capacity of the knapsack

The algorithm fills this table using **nested loops** over `n` and `W`.  
Thus, the **time complexity** is:

```plaintext
O(n * W)
```

This is because for every item (`n`), we iterate through all weight capacities (`W`).

#### Space Complexity:

The space used is also:

```plaintext
O(n * W)
```

due to the storage in both `V` and `Keep` tables.



### Comparison with Brute Force

The brute-force recursive solution checks **all possible subsets** of items, which leads to an **exponential time complexity** of:

```plaintext
O(2^n)
```

This happens because each item has two choices (include or exclude), and there are `n` items.



### Conclusion

Yes, the dynamic programming approach **dramatically improves** performance:

- **Brute Force**: `O(2^n)` (Exponential)
- **Dynamic Programming**: `O(n * W)` (Pseudo-polynomial)

This reduction makes the problem **tractable for moderate values of `n` and `W`**, especially when `W` is not too large.


