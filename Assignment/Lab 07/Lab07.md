# Lab 6 

## Problem 01:
Show that any comparison-based algorithm to sort 4 elements requires at least 5 comparisons in the worst case.

### Solution:

For comparison-based sorting algorithms, the lower bound of the number of comparisons is determined by the decision tree model. 

- The total number of possible permutations of 4 distinct elements is `4! = 24`.
- Each leaf node in the decision tree represents one of these permutations.
- A binary decision tree with depth `d` has at most `2^d` leaves.
- Therefore, we must have:  
  `2^d ≥ 24`

Now, solve for `d`:  
- `2^4 = 16 < 24`
- `2^5 = 32 ≥ 24`

### Conclusion:
- Minimum number of comparisons required in the worst case is **5**.
- Therefore, **any comparison-based sorting algorithm must perform at least 5 comparisons in the worst case** to sort 4 distinct elements.



## Problem 2: Radix Sort using Radix = 9

**Given:**\
S = {125, 27, 729, 1, 27, 8, 64, 343, 216}\
**Radix:** 9

### Step 1: Sort by Least Significant Digit (Units place)

Extract unit digit:

$$
\begin{align}
125& -> 5 \\
27& -> 7 \\
729& -> 9 \\
1& -> 1 \\
27& -> 7 \\
8& -> 8 \\
64& -> 4 \\
343& -> 3 \\
216& -> 6
\end{align}
$$


After sorting based on unit digit:\
**[1, 343, 64, 125, 216, 27, 27, 8, 729]**


### Step 2: Sort by Middle Digit (Tens place)

Extract tens digit:

$$
\begin{align}
1& -> 0 \\
343& -> 4 \\
64& -> 6 \\
125& -> 2 \\
216& -> 1 \\
27& -> 2 \\
27& -> 2 \\
8& -> 0 \\
729& -> 2 \\
\end{align}
$$



After sorting based on tens digit:\
**[1, 8, 216, 125, 27, 27, 729, 343, 64]**


### Step 3: Sort by Most Significant Digit (Hundreds place)

Extract hundreds digit:

$$
\begin{align}
1& -> 0 \\
8& -> 0 \\
216& -> 2 \\
125& -> 1 \\
27& -> 0 \\
27& -> 0 \\
729& -> 7 \\
343& -> 3 \\
64& -> 0
\end{align}
$$

After sorting based on hundreds digit:\
**[1, 8, 27, 27, 64, 125, 216, 343, 729]**

### Final Sorted List:

**{1, 8, 27, 27, 64, 125, 216, 343, 729}**





## Problem 3 (Radix Sort using radix 9)

**Given List:**\
S = {80, 27, 72, 1, 27, 8, 64, 34, 16}\
**Radix:** 9


### Step 1: Sort by Least Significant Digit (Units place)

Extract unit digits:

$$
\begin{align}
80& -> 0 \\
27& -> 7 \\
72& -> 2 \\
1& -> 1 \\
27& -> 7 \\
8& -> 8 \\
64& -> 4 \\
34& -> 4 \\
16& -> 6
\end{align}
$$

**After sorting by unit digit:**\
[80, 1, 72, 64, 34, 16, 27, 27, 8]


### Step 2: Sort by Most Significant Digit (Tens place)

Extract tens digits:

$$
\begin{align}
80& -> 8 \\
1& ->  0 \\
72& ->  7 \\
64& ->  6 \\
34& -> 3 \\
16& -> 1 \\
27& -> 2 \\
27& -> 2 \\
8& -> 0
\end{align}
$$

**After sorting by tens digit:**\
[1, 8, 16, 27, 27, 34, 64, 72, 80]


Final Sorted Output:

**[1, 8, 16, 27, 27, 34, 64, 72, 80]**
