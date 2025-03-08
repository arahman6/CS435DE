
## Problem 1: Amortized Cost Analysis
### **1. Aggregate Analysis**
We calculate the **total cost** of all operations and divide by **n**.

#### **Step 1: Compute Total Cost**
The cost function is:

$$
C(i) =
\begin{cases}
i, & \text{if } i \text{ is a power of 2} \\
1, & \text{otherwise}
\end{cases}
$$

For **n** operations, we sum up the cost:

$$T(n) = \sum_{i=1}^{n} C(i)$$

#### **Step 2: Break Down Cost Contribution**
1. The number of times $$i$$ is a power of 2 is $$log_2(n)$$ (powers of $$2$$ up to $$n: \(1, 2, 4, 8, \dots\)$$).
2. The sum of powers of 2 is:

   $$\sum_{k=0}^{\log_2{n}} 2^k = 2^{\log_2{n} + 1} - 1 = 2n - 1 \approx O(n)$$

3. The cost of the remaining operations is $$(n - log₂(n))$$ since there are $$n - log_2(n)$$ operations where cost is $$1$$.

Thus, the **total cost** is:

$$
\begin{align}
T(n) = & (n - \log_2 n) + (2n - 1)\\
T(n) = & 3n - \log_2 n - 1
\end{align}
$$


#### **Step 3: Compute Amortized Cost**
$$
\begin{align}
\text{Amortized cost per operation} &= \frac{T(n)}{n} \\
&= \frac{3n - \log_2 n - 1}{n}\\
&= 3 - \frac{\log_2 n}{n} - \frac{1}{n}
\end{align}
$$


For large $$n$$, $$\(\log_2 n / n\) and \(1/n\)$$ approach $$0$$, so:

$$
\text{Amortized cost} = O(3) = O(1)
$$

Thus, using **aggregate analysis**, the amortized cost per operation is $$O(1)$$.


### **2. Amortized Analysis (Accounting Method)**

We assign an **amortized charge** for every operation and use the **stored credit** to balance the actual cost.

#### **Step 1: Assign Credits**
- Assign **3 credits** per operation.
- When an operation costs **1**, store **2 extra credits**.
- When an operation costs **i** (power of 2), **use the extra stored credits** to pay for it.

#### **Step 2: Justification**
- Most operations only cost **1** (storing 2 extra credits).
- The occasional high-cost operations (**powers of 2**) are **paid** using the stored credits.
- Since every operation only **uses or stores** a constant number of credits, the **amortized cost remains constant**.

Thus, using **amortized analysis**, the amortized cost per operation is also **O(1)**.

