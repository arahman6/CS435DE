# Lab 12 – NP-Complete

## Q1 – Transitivity of Polynomial-Time Reductions

### Problem

Suppose Prob1, Prob2, and Prob3 are decision problems.

- Prob1 is polynomial-time reducible to Prob2.
- Prob2 is polynomial-time reducible to Prob3.

**Explain why Prob1 must be polynomial-time reducible to Prob3.**

### Answer

This follows from the **transitivity property** of polynomial-time reductions.

Let:
- Prob1 ≤p Prob2 (i.e., there exists a polynomial-time reduction from Prob1 to Prob2)
- Prob2 ≤p Prob3 (i.e., there exists a polynomial-time reduction from Prob2 to Prob3)

### Chain of Reductions

If we can transform:

1. Any instance of **Prob1** to an instance of **Prob2** in **polynomial time**, and  
2. Then transform that instance of **Prob2** to an instance of **Prob3** in **polynomial time**,  

Then we can compose these two reductions to get a **polynomial-time reduction** from **Prob1 to Prob3**.

### Why Is It Still Polynomial?

- Suppose the first reduction takes time O(p(n))  
- The second reduction takes time O(q(n))  
- Then the combined reduction takes time O(p(n) + q(p(n)))  
- Since both p and q are polynomials, the composition is also a polynomial.

### Conclusion

Therefore, **Prob1 is polynomial-time reducible to Prob3**.  
This property is essential in proving NP-completeness and supports the **closure of polynomial-time reductions under composition**.

---

## Q2 – Polynomial Reduction from Hamiltonian Cycle to TSP

### Problem

Illustrate the proof that the **Hamiltonian Cycle (HC)** problem is polynomial-time reducible to the **Traveling Salesman Problem (TSP)** using the provided graph (a square: A—B—D—C—A).

---

### Answer

#### Step 1: Input Graph for Hamiltonian Cycle

We are given a graph G with vertices:

```
Vertices: {A, B, C, D}
Edges: {AB, BC, CD, DA}
```

This graph **does** contain a Hamiltonian cycle:
```
A → B → D → C → A
```

### Step 2: Reduction to TSP

We construct a **complete weighted graph** `G' = (V, E')`:

- For each pair of vertices:
  - If there is an edge in the original HC graph, set cost = 1
  - If not, set cost = 2 (or any number > 1)

So, adjacency matrix (weights):

|     | A | B | C | D |
|-----|---|---|---|---|
| A   | - | 1 | 2 | 1 |
| B   | 1 | - | 2 | 1 |
| C   | 2 | 2 | - | 1 |
| D   | 1 | 1 | 1 | - |



### Step 3: Solve TSP with Cost Constraint

- Objective: Find a tour of cost exactly **4** (using only edges with weight 1)
- TSP solution with total cost = 4 corresponds exactly to a **Hamiltonian cycle** in the original graph

#### So:
- If a Hamiltonian cycle exists, there is a TSP tour of cost = number of vertices (4 in this case)
- If no HC exists, any TSP tour will cost more than 4


### Converse

- A solution to the TSP instance with cost ≤ n (number of vertices) implies a Hamiltonian cycle exists
- Thus, solving TSP solves the Hamiltonian Cycle problem


### Conclusion

We have shown a **polynomial-time reduction** from HamiltonianCycle to TSP:

- Construct a complete graph
- Assign weights: 1 to existing edges, higher cost to others
- A Hamiltonian cycle corresponds to a minimum-cost TSP solution

This proves **HC ≤p TSP**

---

## Q3 – Proving TSP is NP-Complete

### Problem

Show that the **Traveling Salesman Problem (TSP)** is **NP-complete**.

(Hint: Use the relationship between TSP and the Hamiltonian Cycle (HC) problem. Assume HC is NP-complete.)

### Answer

To prove that TSP is NP-complete, we must show two things:

### 1. TSP ∈ NP

A problem is in NP if a solution can be **verified in polynomial time**.

- Given a TSP tour (sequence of cities), we can:
  - Check that it visits every city exactly once
  - Compute the total tour cost
  - Compare it to the cost bound `k`
- All of this can be done in **polynomial time**

So, **TSP ∈ NP**

### 2. TSP is NP-Hard (via reduction from Hamiltonian Cycle)

We reduce the **Hamiltonian Cycle (HC)** problem to **TSP** in polynomial time:

#### Given:
An instance of HC on graph `G = (V, E)`

#### Construct TSP instance:
- Create a complete graph `G' = (V, E')` where:
  - Cost = 1 if edge ∈ E
  - Cost = 2 if edge ∉ E
- Set bound `k = |V|` (number of vertices)

#### Logic:
- If HC exists in G ⇒ a TSP tour in G' of cost exactly `|V|`
- If no HC exists ⇒ any TSP tour costs > `|V|`
- Therefore, solving this TSP instance solves HC

This is a polynomial-time reduction: **HC ≤p TSP**

### Conclusion

- TSP ∈ NP
- HC ≤p TSP (TSP is NP-hard)

Thus, **TSP is NP-complete**

---

# Lab 12 – NP-Complete

## Q4 – O(n) Algorithm to Find Prefix with Sum = 10

### Problem

Design an **O(n)** algorithm that, given an array of integers of size `n`,  
**outputs the first numbers** in the array (from left to right) whose **sum is exactly 10**,  
or indicates that **no such prefix exists**.


### Algorithm Idea

- Traverse the array from left to right
- Maintain a running sum
- As soon as the sum reaches 10, return the prefix
- If sum exceeds 10 or the end is reached, return failure


### Pseudocode

```python
function find_prefix_sum_10(arr):
    sum = 0
    prefix = []

    for num in arr:
        sum += num
        prefix.append(num)

        if sum == 10:
            return prefix
        elif sum > 10:
            break

    return "No such prefix found"
```

### Time Complexity

- The loop runs at most `n` times
- All operations inside the loop are constant time

**Time Complexity = O(n)**

### Example

```python
Input: [2, 3, 5, 1, 4]
Output: [2, 3, 5]   # sum = 10

Input: [1, 2, 3]
Output: "No such prefix found"
```

### Conclusion

This is an efficient **linear-time** solution that checks only the prefix sum and avoids unnecessary computation.

---


## Q5 – Dynamic Programming Solution to Subset Sum

### Problem

Use **Dynamic Programming** to solve the **Subset Sum** problem:

- Set `S = {3, 2, 1, 5}`
- Target sum `k = 4`

### Step-by-Step DP Table Construction

Let `dp[i][j]` = True if a subset of the first `i` elements can sum to `j`.

- `i` = 0 to 4 (number of elements)
- `j` = 0 to 4 (target sum)

#### Initialize:
- `dp[0][0] = True` (empty subset sums to 0)
- `dp[0][1...k] = False` (no subset of 0 elements sums to >0)


### Table Building (S = [3, 2, 1, 5])

```plaintext
    j →   0     1     2     3     4
i ↓
0       T     F     F     F     F
1 (3)   T     F     F     T     F
2 (2)   T     F     T     T     F
3 (1)   T     T     T     T     T
4 (5)   T     T     T     T     T   ← same as row 3, 5 > 4 (no update)
```

### Explanation

- At `dp[3][4] = True`: we can make 4 using subset {3, 1}
- The table confirms that a **subset sum of 4 is possible**


### Final Result

There **exists a subset** of `{3, 2, 1, 5}` that sums to `4`  
Example subset: `{3, 1}` or `{2, 1, 1}` (depending on implementation)


### Conclusion

We have solved SubsetSum using **Dynamic Programming in O(n*k)** time,  
with a table showing which sums can be made with the first `i` elements of the set.

---
