### **Q1A**

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

### Q1B: Expected Collisions in a Hash Table

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


---


### Q2

For a red-black tree with all nodes black, the tree must be a **perfect binary tree** (all paths from root to leaves have the same length). The number of nodes in a perfect binary tree is 
$$2^h-1$$
, where hh is the height. This restricts valid node counts to 
$$n=1,3,7$$
for 
$$h=1,2,3$$
. Other values of 
$$n$$
are not possible.

| Num nodes nn | Does there exist a red-black tree with nn nodes, all of which are black? |
| --- | --- |
| 1 | Yes |
| 2 | No |
| 3 | Yes |
| 4 | No |
| 5 | No |
| 6 | No |
| 7 | Yes |

---

### Q3

Here's the Markdown table filled out for Q3:

| Num nodes n | Does there exist a red-black tree with n nodes that has exactly one red node? |
|-------------|---------------------------------------------------------------------------------|
| 1           | No                                                                              |
| 2           | Yes                                                                             |
| 3           | No                                                                              |
| 4           | Yes                                                                             |
| 5           | Yes                                                                             |
| 6           | No                                                                              |
| 7           | No                                                                              |

#### Reasoning:

-   A red-black tree must maintain balance, and **a red node must always have black children**.

-   The simplest configuration with one red node requires **at least two black nodes** to be children of that red node.

-   Only certain tree sizes permit such configurations, while preserving the black-height and red-black properties.


---

### **Q4. Red-Black Tree Insertion Steps**

**1. Insert 21 (Initially Empty Tree):**  
- 21 becomes the root (must be **black**).

```
21 (B)
```

**2. Insert 32:**  
- 32 is inserted as the right child of 21 (colored **red**).  
- No violations (parent is black).
- 
```
21 (B)
  \
   32 (R)
```

**3. Insert 64:**  
- 64 is inserted as the right child of 32 (colored **red**).  
- **Violation**: Red node (32) has a red child (64).  
- **Fix**:  
  - Left rotation at grandparent (21).  
  - Recolor: 32 becomes **black**, 21 and 64 become **red**.  
```
   32 (B)
  /   \
21 (R) 64 (R)
```

**4. Insert 75:**  
- 75 is inserted as the right child of 64 (colored **red**).  
- **Violation**: Red node (64) has a red child (75).  
- **Fix**:  
  - Parent (64) and uncle (21) are both red.  
  - Recolor parent and uncle to **black**, grandparent (32) stays **black** (root).  
```
   32 (B)
  /   \
21 (B) 64 (B)
          \
           75 (R)
```

**5. Insert 15:**  
- 15 is inserted as the left child of 21 (colored **red**).  
- No violations (parent 21 is **black**).  
```
   32 (B)
  /   \
21 (B) 64 (B)
/        \
15 (R) 75 (R)

```

**Final Red-Black Tree:**  
All red-black tree properties are satisfied after all insertions. 






