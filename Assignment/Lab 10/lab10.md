# Lab 10

### Q2. Counts the number of collisions

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

### Q3. Red-Black tree having n nodes

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
