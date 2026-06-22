# PyTorch Geometric
- These are my personal notes from deep dives into the PyG tutorials and related subjects. 
- Source: https://pytorch-geometric.readthedocs.io/en/stable/get_started/colabs.html


---
# Graph types
1. Undirected
2. Directed
3. Node labeled
4. Edge labeled

# Graph Representation 
- A Graph can be represented as an Adjancency Matrix.
- Why can't we input a matrix into a neural network?

## Problems with matrix --> NN
1. Different sizes
2. Not invariant to node ordering
   - G = G prime graph if graph is identical
   - however, the matrices are NOT the same....thus can't use for deep learning.
  
---
# Definitions
- G = (V,E)
- What this means --> number of nodes is equal to num of features. 
