# Lab 09

### Q1A. LIFO Push-Pop

You are allowed exactly 6 pushes (S) of the values `1` to `6` in order and 6 pops (X). You must describe whether certain permutations can be obtained using a stack.

#### (a) Can we produce output `325641`?

We are pushing numbers `1` to `6` in order.\
**S = push**, **X = pop**

The sequence to produce 325641 is: **S S S X X S S X S X X X** 

Here's a breakdown again just to confirm:

| Step | Stack | Operation | Output |
| --- | --- | --- | --- |
| 1 | [1] | S |  |
| 2 | [1, 2] | S |  |
| 3 | [1, 2, 3] | S |  |
| 4 | [1, 2] | X | 3 |
| 5 | [1] | X | 2 |
| 6 | [1, 4] | S |  |
| 7 | [1, 4, 5] | S |  |
| 8 | [1, 4, 5, 6] | S |  |
| 9 | [1, 4, 5] | X | 6 |
| 10 | [1, 4] | X | 5 |
| 11 | [1] | X | 4 |
| 12 | [] | X | 1 |

Final output: **3 2 6 5 4 1**




#### (b) Can we produce output `154623`?

Let's simulate:

-   **Push 1** → stack = [1]

-   **Pop** → outputs `1`

-   **Push 2** → stack = [2]

-   **Push 3** → stack = [2, 3]

-   **Push 4** → stack = [2, 3, 4]

-   **Pop** → outputs `5` Invalid, `5` was never pushed yet!

The output **154623** is **not possible**.

---

### Q1B. Expected Collisions in a Hash Table

**Given:**

- We store `n` keys in a hash table of size $$m = n^2$$.
- A hash function `h` is randomly chosen from a **Universal class H**.
- Let `X` be the **random variable** that counts the number of **collisions**.

**Goal:** Show that the **expected number of collisions** is **< 1/2**.

#### Step 1: Universal Hashing Property

For universal hashing, the probability of collision for any two distinct keys is:

$$\Pr[h(k_i) = h(k_j)] \leq \frac{1}{m}$$


Number of key pairs:

$$\binom{n}{2} = \frac{n(n-1)}{2}$$


#### Step 2: Expected Number of Collisions

Define $$X$$ as the total number of collisions:

$$X = \sum_{1 \leq i < j \leq n} X_{ij}$$

Where:

- $$\( X_{ij} = 1 \) if \( h(k_i) = h(k_j) \)$$
- $$\( X_{ij} = 0 \)$$ otherwise

Then:

$$\mathbb{E}[X] = \sum_{1 \leq i < j \leq n} \mathbb{E}[X_{ij}] \leq \sum_{1 \leq i < j \leq n} \frac{1}{m}$$

$$\mathbb{E}[X] \leq \binom{n}{2} \cdot \frac{1}{m} = \frac{n(n-1)}{2} \cdot \frac{1}{n^2}$$

$$\mathbb{E}[X] = \frac{n(n-1)}{2n^2} = \frac{n-1}{2n}$$


#### Conclusion:

Since:

$$\frac{n-1}{2n} < \frac{1}{2}$$

for all $$\( n \geq 1 \)$$, the **expected number of collisions** is:

$$\boxed{\mathbb{E}[X] < \frac{1}{2}}$$
