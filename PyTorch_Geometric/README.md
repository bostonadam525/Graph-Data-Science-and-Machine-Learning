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

## Computation Graph
- Defined: The neighbour of a node defines its computational graph.
- Example from pyg: We have an input graph and the computational graph is defined by the node and its connections (neighbors):

<img width="494" height="191" alt="image" src="https://github.com/user-attachments/assets/4817806a-6760-4690-a2d3-240b4d4610ee" />

- [source](https://www.youtube.com/watch?v=JtDgmmQ60x8)
