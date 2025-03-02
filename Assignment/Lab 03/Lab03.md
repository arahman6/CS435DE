# Fibonacci Growth and Recursive Complexity

## **Proof by Induction: $$\( F_n > (4/3)^n \)$$ for $$\( n > 4 \)$$**

### **Step 1: Base Case**
We verify the given inequality for \( n = 5 \) and \( n = 6 \) using the provided table:

- $$\( F_5 = 5 \)$$, $$\( (4/3)^5 \approx 4.21 \)$$ → **$$\( 5 > 4.21 \)$$ ✅**
- $$\( F_6 = 8 \)$$, $$\( (4/3)^6 \approx 5.62 \)$$ → **$$\( 8 > 5.62 \)$$ ✅**

Thus, the inequality holds for the base cases $$\( n = 5 \)$$ and $$\( n = 6 \)$$.

---

### **Step 2: Inductive Hypothesis**
Assume that the inequality holds for some $$\( n = k \)$$ and $$\( n = k-1 \)$$:

$$\[F_k > \left(\frac{4}{3}\right)^k, \quad F_{k-1} > \left(\frac{4}{3}\right)^{k-1}\]$$

---

### **Step 3: Inductive Step**
Using the Fibonacci recurrence relation:

$$\[F_{k+1} = F_k + F_{k-1}\]$$

By the inductive hypothesis:

$$\[F_{k+1} > \left(\frac{4}{3}\right)^k + \left(\frac{4}{3}\right)^{k-1}\]$$

Factor out $$\( (4/3)^{k-1} \)$$:

$$\[F_{k+1} > \left(\frac{4}{3}\right)^{k-1} \left( \left(\frac{4}{3}\right) + 1 \right)\]$$

Since $$\( (4/3) + 1 = 7/3 \)$$, we get:

$$\[F_{k+1} > \left(\frac{4}{3}\right)^{k-1} \times \frac{7}{3}\]$$

Since $$\( \frac{7}{3} > \frac{4}{3} \)$$, it follows that:

$$\[F_{k+1} > \left(\frac{4}{3}\right)^{k+1}\]$$

Thus, by induction, the inequality holds for all $$\( n > 4 \)$$.

---

## **Asymptotic Running Time of Recursive Fibonacci Algorithm**
The standard recursive Fibonacci algorithm follows:

$$\[T(n) = T(n-1) + T(n-2) + O(1)\]$$

From our proof, we established that:

$$\[F_n > \left(\frac{4}{3}\right)^n\]$$

This lower bound suggests that the recursion tree grows **exponentially**, meaning the recursive algorithm runs in **exponential time**:

$$\[O(2^n)\]$$

---

## **Is Recursive Fibonacci Fast or Slow?**
- **Slow** ❌: The exponential runtime makes it impractical for large $$\( n \)$$.
- **Inefficient**: Redundant computations significantly increase the number of recursive calls.
- **Better Alternative**: The **dynamic programming** approach reduces time complexity to **$$\( O(n) \)$$**, and **matrix exponentiation** further improves it to **$$\( O(\log n) \)$$**.

Thus, the naive recursive Fibonacci algorithm is **highly inefficient** for large inputs.
