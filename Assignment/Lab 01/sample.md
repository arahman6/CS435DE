**The Cauchy-Schwarz Inequality**\
$$\left( \sum_{k=1}^n a_k b_k \right)^2 \leq \left( \sum_{k=1}^n a_k^2 \right) \left( \sum_{k=1}^n b_k^2 \right)$$




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
$$
\sum_{t \in T} t = k.
$$  
After removing \( s_{n-1} \), the new subset \( T' = T - \{s_{n-1}\} \) has sum:  
$$
\sum_{t \in T'} t = \sum_{t \in T} t - s_{n-1} = k - s_{n-1} = k'.
$$  
This satisfies the new target \( k' \).

---

### 2. Subset Verification  
- \( T \subseteq S \), and \( s_{n-1} \) is explicitly removed.  
- \( T' \subseteq S' = S - \{s_{n-1}\} \).  

---

### 3. Edge Cases  
- **Case 1**: If \( T = \{s_{n-1}\} \):  
  - \( T' = \emptyset \), the empty set.  
  - The sum of \( \emptyset \) is \( 0 \), which matches \( k' = k - s_{n-1} = 0 \) (since \( k = s_{n-1} \)).  

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
Yes, \( T - \{s_{n-1}\} \) is always a valid solution to the SubsetSum problem with inputs \( S' \) and \( k' \).  

**Final Answer**:  
$$
\boxed{Yes}
$$
