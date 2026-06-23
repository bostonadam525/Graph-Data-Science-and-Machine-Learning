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
- Defined: **The neighbour of a node defines its computational graph.**
- Example from pyg: We have an input graph and the computational graph is defined by the node and its connections (neighbors):

<img width="494" height="191" alt="image" src="https://github.com/user-attachments/assets/4817806a-6760-4690-a2d3-240b4d4610ee" />

- (source)[https://www.youtube.com/watch?v=JtDgmmQ60x8]

## Graph Neural Networks
- Above is how we get to a neural network.
- Every node has its own computation graph.
- There is redundancy for each node in the network....

<img width="666" height="191" alt="image" src="https://github.com/user-attachments/assets/32be00e3-338d-4078-9862-d45e42954983" />
- source (same as above)

- So, to then take this to a graph neural network we get this -- each nodes computational graph is a layer in the neural net:


<img width="502" height="269" alt="image" src="https://github.com/user-attachments/assets/6e2ab982-9b6f-4503-a6b2-78ff556bc181" />
- source (same as above)

### How much to unroll?
- Essentially this is "hopping" from node to node.
- The question of how many layers to unroll depends on the problem you are solving.
- If this is a social network it could be multiple layers.

## Math of GNNs
- each computational layer shares the same weights
- Good review page: [The Math Behind Graph Neural Networks](https://medium.com/@cristianleo120/the-math-behind-graph-neural-networks-3427c16570d0)
- Important paper: [Inductive Representation Learning on Large Graphs](https://arxiv.org/pdf/1706.02216)

---
## Inductive Learning on Graphs -- Brief
- Basically, before GraphSAGE, the most common way of getting node embeddings: those feature vectors that represent a node and its place in the graph, were almost all transductive -- which means they need to see the entire graph during training.
- Real quick review:

1. **Transductive Learning:** model has access to entire graph during training which is all nodes and edges. The ML task is to infer the labels or properties of the unlabeled nodes within this single, fixed graph. A transductive model learns embeddings ONLY for specific nodes it was trained on. If a new node is added to the graph later on, the model CANNOT generate an embedding for it without being completely retrained. Sound like a familiar ML problem?

2. **Inductive Learning:** model is trained on a set of graphs or a subgraph and is then expected to make predictions on new, previously unseen nodes or even entirely new graphs. Thus, an inductive model learns a general function that generates embeddings by mapping a node's local neighborhood structure and features to a vector representation. This function can be applied to any node, old or new. [source](https://apxml.com/courses/introduction-to-graph-neural-networks/chapter-3-foundational-gnn-architectures/inductive-learning-graphsage)



