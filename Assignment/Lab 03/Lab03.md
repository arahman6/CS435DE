# Problem 1: Solution

### **1. Base Case: $$\( n \geq 5 \)$$**  
We verify for $$\( F(5) \)$$:

$$
\begin{align*} 
F(5) &= F(4) + F(3)\\
     &= (F(3) + F(2)) + (F(2) + F(1))\\
     &= ((F(2) + F(1)) + (F(1) + F(0))) + ((F(1) + F(0)) + 1)\\
     &= ((1 + 1) + (1 + 0)) + ((1 + 0) + 1)\\
     &= 1 + 0 + 4 = 5
\end{align*}
$$

From the given data,

$$
\left(\frac{4}{3}\right)^5 \approx 4.21
$$

Since $$\( 5 > 4.21 \)$$, we conclude:

$$
F(5) > \left(\frac{4}{3}\right)^5
$$


### **2. Induction Step**
#### **Inductive Hypothesis:**  
Assume $$\( F(n) > \left(\frac{4}{3}\right)^n \)$$. We need to prove:

$$
F(n+1) > \left(\frac{4}{3}\right)^{n+1}
$$

Using the Fibonacci recurrence:

$$
\begin{align*} 
F(n+1) &= F(n) + F(n-1)\\
       &> \left(\frac{4}{3}\right)^n + \left(\frac{4}{3}\right)^{n-1}\\
       &= \left(\frac{4}{3}\right)^{n-1} \left(\frac{4}{3} + 1\right)\\
       &= \left(\frac{4}{3}\right)^{n-1} \times \frac{7}{3}\\
       &> 1.75 \times \left(\frac{4}{3}\right)^n
\end{align*}
$$

Since $$\( 1.75 > 1.33 \)$$, we conclude:

$$
F(n+1) > \left(\frac{4}{3}\right)^{n+1}
$$

Thus, by **mathematical induction**, $$\( F_n > (4/3)^n \)$$ for all $$\( n > 4 \)$$.

### **3. Observing Time Complexity**
We observe that the recursive Fibonacci algorithm runs in **exponential time**:

- Each call to $$\( F(n) \)$$ results in **two recursive calls**: $$\( F(n-1) \)$$ and $$\( F(n-2) \)$$.
- This leads to an **exponential number of function calls**.
- Therefore, the recursive Fibonacci algorithm is **very slow for large values of $$\( n \)$$**.

For this reason, **recursive Fibonacci is not efficient** and is typically replaced by **dynamic programming or matrix exponentiation** for faster computation.




# Problem 2: Solution

### **(a) Is $$\( 4^n \)$$ in $$\( O(2^n) \)$$?**
We apply the limit comparison method:

$$
\lim_{n \to \infty} \frac{4^n}{2^n} = \lim_{n \to \infty} \frac{(2^2)^n}{2^n} = \lim_{n \to \infty} 2^{2n - n} = \lim_{n \to \infty} 2^n
$$

Since $$\( 2^n \)$$ grows exponentially, the limit tends to **infinity**. 

Thus, $$\( 4^n \)$$ is **not** in $$\( O(2^n) \)$$, because it grows faster than $$\( 2^n \)$$. 

**Conclusion:** **False**

### **(b) Is $$\( \log n \)$$ in $$\( \Theta(\log_3 n) \)$$?**
We use the limit comparison method:

$$
\lim_{n \to \infty} \frac{\log n}{\log_3 n}
$$

Using the change of base formula:

$$
\log_3 n = \frac{\log n}{\log 3}
$$

Substituting:

$$
\lim_{n \to \infty} \frac{\log n}{\frac{\log n}{\log 3}} = \lim_{n \to \infty} \log 3
$$

Since $$\( \log 3 \)$$ is a constant, the limit is **finite and nonzero**, which satisfies the definition of $$\( \Theta \)$$-notation.

Thus, **$$\( \log n \)$$ is in $$\( \Theta(\log_3 n) \)$$**.

**Conclusion:** **True**


### **(c) Is $$\( (n/2) \log (n/2) \)$$ in $$\( \Theta(n \log n) \)$$?**
We analyze:

$$
\lim_{n \to \infty} \frac{\frac{n}{2} \log \frac{n}{2}}{n \log n}
$$

Breaking it down:

$$
\lim_{n \to \infty} \frac{n}{2} \cdot \frac{\log n - \log 2}{n \log n}
$$

Rearranging:

$$
\lim_{n \to \infty} \frac{n}{2n} \cdot \frac{\log n - \log 2}{\log n}
$$

$$
= \lim_{n \to \infty} \frac{1}{2} \cdot \left( 1 - \frac{\log 2}{\log n} \right)
$$

Since $$\( \log 2 / \log n \to 0 \)$$ as $$\( n \to \infty \)$$, the limit simplifies to:

$$
\frac{1}{2} \times 1 = \frac{1}{2}
$$

Since the result is a nonzero constant, we conclude that:

$$
(n/2) \log (n/2) \in \Theta(n \log n)
$$

**Conclusion:** **True**




