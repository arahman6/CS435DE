# Lab 9 Heap








# Q4: Maximum Number of Nodes of Height $$h$$ in an $$n$$ -element Heap

## Problem
Show that in an $$n$$-element heap, there are at most:

$$
[n / 2^{(h+1)}]
$$

nodes of height $$h$$.

## Understanding the Heap Structure

- A heap is a complete binary tree.
- In a complete binary tree of $$n$$ nodes:
  - The height of the tree is $$⌊log₂ n⌋$$.
  - Leaves are at the lowest level (height 0).
  - Nodes at height $$h$$ are at $$log_{2} n - h$$ levels from the root.

## Key Observations

- The total number of nodes at height $$h$$ lies in the upper part of the tree.
- For a node to have height $$h$$, it must have $$h$$ levels below it — that is, $$h$$ edges down to the deepest leaf.
- In a binary heap, the number of nodes at a given height decreases exponentially as height increases.

## Proof

Let’s calculate the number of nodes at height $$h$$.

- The number of nodes at height $$h$$ is at most:

  Total number of nodes in levels $$0$$ to $$(log_{2} n − h − 1)$$


But we can use a tighter bound using the structure of the heap:

1. In a binary heap, at least half of the nodes are leaves (nodes at height 0). That’s ⌊n/2⌋.
2. At most, there are:
3. $$n / 2^{(h+1)}$$

   nodes of height $$h$$ (since we halve the number of potential parents with each increase in height).

So we get:

\# of nodes at height $$h ≤[n / 2^{(h+1)}]$$


## Conclusion

Thus, in an n-element heap, **the number of nodes of height $$h$$ is at most**:

$$
[n / 2^{(h+1)}]
$$

This result follows from the structure of the complete binary tree underlying the heap.
