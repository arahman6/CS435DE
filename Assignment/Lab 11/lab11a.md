# Lab 11A

### **Updated Knapsack Algorithm with Item Tracking**

#### **Inputs:**

-   `n`: number of items

-   `W`: total capacity

-   `v[]`: values of items (1-based index)

-   `w[]`: weights of items (1-based index)



### **Pseudo-code**


```
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

    return V[n][W] // the maximum value`

```

### **Explanation**

-   `V[i][j]` holds the **maximum value** for first `i` items and capacity `j`.

-   `Keep[i][j] = true` means item `i` is included in the optimal solution for capacity `j`.

-   After filling the tables, we **trace back** from `V[n][W]` using `Keep[][]` to print selected items.


