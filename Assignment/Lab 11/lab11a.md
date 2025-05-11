# Lab 11A – Dynamic Programming

## Q1 – 0/1 Knapsack with Item Tracking

### Problem Statement

Modify the classical dynamic programming solution of the 0/1 Knapsack problem to not only compute the maximum value, but also to **track the items** selected using a `Keep[i][w]` array.

---

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


