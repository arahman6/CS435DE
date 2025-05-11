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


### ✅ Conclusion:
Only subgraphs that include **all edges** between vertices in the subset qualify as **induced subgraphs**.
