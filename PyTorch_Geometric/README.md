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

- [source](https://www.youtube.com/watch?v=JtDgmmQ60x8)

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

### How does inductive learning prevent overfitting on GNNs?
- Inductive learning prevents GNNs from overfitting by teaching the model to learn generalizable functions of node features and local neighborhood structures, rather than memorizing fixed node positions or global graph layouts.
- This helps GNNs avoid overfitting in production through a few key mechanisms:
  - **Topology Independence:** Instead of creating a look-up table of specific node representations, inductive GNNs (like GraphSAGE) train on a parameterized function. The model evaluates how local subgraphs connect, allowing it to extrapolate to entirely unseen nodes, edges, or graphs.
  - **Feature-Based Mapping:** The model learns to transform node embeddings based on intrinsic attributes (e.g., user profiles, transaction amounts) mixed with their immediate neighbors' attributes, ensuring it can handle new entities that share similar behavioral patterns.
  - **Neighborhood Sampling:** By aggregating fixed-size samples of neighborhoods during training, the GNN forces robustness against topological variance and prevents the model from relying on the exact global structure of the training data.
---
# Graph Attention Networks (GAT)
- A Graph Attention Network (GAT) is a specialized neural network designed to process graph-structured data (like social networks or molecules). Unlike standard graph methods that treat all neighbor nodes equally, GAT uses self-attention to learn which connections are the most important, allowing nodes to weigh their neighbors' influence dynamically.
- Given a graph as we see below:
  - how much features of node "c" are important to node "i"?
  - Can we learn such importance in an automated manner? (without rule based or strict labeling). YES with GAT!

<img width="502" height="269" alt="image" src="https://github.com/user-attachments/assets/74c08780-8e65-485b-8519-c81075b016df" />

## How GATs work
- **Attention Coefficients:** For every connection (edge) between nodes, GAT calculates an importance score. This score tells the network how much "attention" a target node should pay to a specific neighbor.
- **Weighted Aggregation:** When a node updates its own data representation, it combines the features of its neighbors using these learned attention weights.
- **Multi-Head Attention:** Similar to models like Transformers, GATs use multiple parallel "attention heads" to capture different types of relationships simultaneously, making the network's predictions more robust.

## Why use GAT? 
- **Flexibility:** It does not require knowing the entire graph structure in advance, making it highly effective for both inductive and transductive tasks (evaluating graphs that were unseen during training).
- **Interpretability:** By looking at the attention weights, you can easily see which nodes the network focused on to make its predictions.
- **Efficiency:** The operations are local and parallelizable across neighborhoods, meaning the network scales efficiently without requiring costly matrix operations.

## Graph Attention Layer
- INPUT: a set of node features
- OUTPUT: a new set of node features

1. Apply parameterized linear transformation to every node
2. Apply self attention mechanism --> specify node j's features to node i
3. Normalization (softmax for e (i,j))
4. Attention mechanism -- `a` --> is a single layer feed forward neural network
5. Use it.....
6. Multi-head attention --> concatenation, average (on the final prediction layer of the network)
   - original paper on GAT suggests concatenation on inner layers, average on final layers --> gives more stable results.
  
## Pros of GATs
1. Computationally Efficient
   - self-attention layers can be parallelized across edges.
   - output features can be parallelized across nodes.

2. Allows to assign **different importances to nodes** of the same neighborhood.
3. Applied in a **shared manner** to all edges in the graph --> NOT required to have the **entire graph** beforehand
4. Works on BOTH:
   - a) Transductive learning -- accesses the entire graph, can use features of nodes in train and test set
   - b) Inductive learning --- multiple graphs, learn from a set of graphs, then test network in other unseen graphs.

5. Message passing implementation
