# Lab 11 – Graph Theory

## Q1 – Answer questions about the graph G = (V, E)

Refer to the graph provided in the assignment image.

### a. Let U = {A, B}. Draw G[U].

- **Vertices:** A, B  
- **Edges:** Edge between A and B exists in the original graph.  
- **G[U] includes:**  
  - Nodes: A, B  
  - Edge: A — B

### b. Let W = {A, C, G, F}. Draw G[W].

- **Vertices:** A, C, G, F  
- **Edges among them:**  
  - A — C (No direct edge)
  - A — F (Yes)
  - C — F (Yes)
  - F — G (Yes)

- **G[W] includes:**  
  - Nodes: A, C, G, F  
  - Edges: A — F, C — F, F — G


### c. Let Y = {A, B, D, E}. Draw G[Y].

- **Vertices:** A, B, D, E  
- **Edges among them:**  
  - A — B (Yes)
  - B — D (No)
  - D — E (Yes)

- **G[Y] includes:**  
  - Nodes: A, B, D, E  
  - Edges: A — B, D — E


### d. Consider subgraph H of G (includes A, B, F and edges A — B, A — F)

#### Question:  
Is there a subset X of vertex set V so that H = G[X]?  

#### Answer:
**No**, H is **not** an induced subgraph of G, i.e., **H ≠ G[X]** for any X.

- If we choose X = {A, B, F}, then we should include **all edges among A, B, F** from G.
- In G, there is also an edge **B — F**, which is **missing in H**.
- Therefore, H is not an induced subgraph because not all edges between nodes in X are included.


### Conclusion:
Only subgraphs that include **all edges** between vertices in the subset qualify as **induced subgraphs**.


---

## Q2 – Unique Minimum Spanning Tree & Cuts

### Problem Statement

Show that a graph has a **unique minimum spanning tree (MST)** if, for every cut of the graph, there is a **unique light edge** crossing the cut.  
Also, show that the **converse is not true** by providing a counterexample.


### Proof – If every cut has a unique light edge, then the MST is unique

Let’s assume:

- In every cut of the graph, the **lightest edge** (minimum weight crossing the cut) is **unique**.
- By the **cut property** in MST theory, **every unique light edge** must be included in any MST.

#### Implication:

- Since every cut has a unique light edge, and every MST must include this edge (by cut property),
- Therefore, **all MSTs must include the same edges**.
- Hence, the **MST is unique**.


### Converse is not true – Counterexample

A graph may have a **unique MST**, even if **some cuts have multiple light edges**.

#### Example:

Consider a triangle graph:

```
    A
   / \
  1   1
 /     \
B-------C
   weight = 2
```

- Edges: AB(1), AC(1), BC(2)
- MST: Choose AB and AC (total weight = 2)
- Cut between {A} and {B, C} has **two lightest edges** of weight 1 (AB and AC)

There are **multiple light edges** crossing the cut, yet the MST is still **unique**.


### Conclusion

- **Forward statement is true**: Unique light edge across every cut ⇒ Unique MST.
- **Converse is false**: Unique MST does **not** imply unique light edge for every cut.

---


## Q4 – Maximum Spanning Tree and Greedy Algorithms

### Problem

Consider the problem of computing a **maximum spanning tree** (MaxST), which is a spanning tree that **maximizes** the sum of edge costs.

Do **Prim’s** and **Kruskal’s** algorithms work for this problem (assuming we choose the crossing edge with **maximum cost**)?


### Answer

Yes, both **Prim’s** and **Kruskal’s** algorithms work for finding the **maximum spanning tree**, provided we make the following adjustment:

- Instead of selecting the **minimum-weight edge** (as in MST),
- We select the **maximum-weight edge** at each step.


#### Kruskal’s Algorithm:

- Sort all edges in **decreasing** order of weight.
- At each step, add the **maximum-weight edge** that does **not form a cycle**.
- Stop when we have `n - 1` edges.

This yields a **maximum spanning tree**.


#### Prim’s Algorithm:

- Start from an arbitrary node.
- At each step, add the **maximum-weight edge** that connects a node in the tree to one **not** in the tree.
- Repeat until all nodes are connected.

This also yields a **maximum spanning tree**.


Both algorithms are based on the **greedy approach** using the **cut property**. The same principles apply:

- Instead of choosing the **lightest** edge across a cut, we choose the **heaviest**.
- The algorithms are structurally the same — only the **edge selection criteria** is reversed.


### Conclusion

- **Yes**, both **Prim’s** and **Kruskal’s** algorithms work for the **maximum spanning tree** problem.
- Just reverse the edge selection order (prefer heavier edges).


