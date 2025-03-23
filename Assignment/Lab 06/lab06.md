

## Problem 1: Show all steps of QuickSort in sorting the array [1, 6, 2, 4, 3, 5]. Use leftmost values as pivots at each step.

```
                            [1,6,2,4,3,5] → [1,2,3,4,5,6]  
                             /                         \  
                         [1] (sorted)             [6,2,4,3,5] → [2,3,4,5,6]  
                                                   /                     \  
                                         [2,4,3,5] → [2,3,4,5]         [6] (sorted)  
                                           /                \  
                                        [2] (sorted)      [4,3,5] → [3,4,5]  
                                                          /           \  
                                                      [3] (sorted)  [4,5] (sorted)  
```
Final sorted Array [1,2,3,4,5,6]
