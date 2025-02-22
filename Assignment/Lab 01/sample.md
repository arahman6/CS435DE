# Problem 4

**Problem Statement**  
You are given a solution `T` to a SubsetSum problem with set `S = {s_0, s_1, ..., s_{n-1}}` and a non-negative integer `k`. The set `T` is a subset of `S` whose elements sum to `k`, and `s_{n-1}` is part of `T`. Determine whether `T' = T - {s_{n-1}}` is necessarily a solution to the SubsetSum problem with inputs `S' = {s_0, s_1, ..., s_{n-2}}` and `k' = k - s_{n-1}`.

---

## Solution

### 1. **Sum Calculation**  
Since `T` is a valid solution, the sum of its elements is `k`. Removing `s_{n-1}` from `T` gives a new subset `T'`. The sum of `T'` is:
