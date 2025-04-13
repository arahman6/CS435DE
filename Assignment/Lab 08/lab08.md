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


