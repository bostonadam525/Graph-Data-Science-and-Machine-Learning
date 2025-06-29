# Graph Machine Learning
* This repo is dedicated to machine learning with Graphs.
* An excellent resource is the open source course CS224W from Stanford which can be found on YouTube.
* These are my notes from that open source course as well as some other resources. 


# Types of Graphs and Networks 

1. Networks (aka Natural Graphs)
    1. Social networks
    2. Communication and transactions
    3. Biomedicine —> relationships between genes/proteins
    4. Brain connections —> neurons and their hidden connections


2. Graphs (as a representation)
    1. Information/knowledge organized and linked
    2. Software can be a graph
    3. Similarity networks —> similar data points are connected (eg. Patient networks, social networks)
    4. Relational structures 
        1. Molecules
        2. Scene graphs
        3. 3D shapes
        4. Particle-based physics 


* **Note: The distinction between networks & graphs is often blurred…!!!!!**

* **The Big Question:**
  * **How do we take advantage of relational structures to make more accurate predictions?**
    - **Domains that are complex will have a rich relational structure and can thus be represented as a relational graph.**
    - **Modeling rich relationships  == better predictions!!!!!**


## Modern Deep Learning/Machine Learning 
* Mostly designed for and pretty much biased for simple linear sequences & grids
* For example: images, text


## Networks are more complex to process - Why????
1. Changing size and complex structures (e.g. no spatial locality like a grid in deep learning)
2. No fixed node order or reference point
3. Very dynamic with multimodal features

* Oh and by the way, **Networks are != images and text**!!!!! 


## Feature Engineering
* Traditional machine learning is all about Feature Engineering to get the best predictions.
* **Graph ML is the opposite**.
  * There is no “feature engineering”.
  * With data represented as a Graph, you have **“Representation Learning”** that automatically learns the features of a graph or network that can be applied to an algorithm  and a downstream prediction task. 


## Wait, what is Representation Learning?
* Maps nodes to d-dimensional embeddings.
* Similar nodes in a network are embedded closer together.



## Graph Machine Learning -- high-level overview
* With Graphs, you can get a high-level to very granular representation of your data:
    * Graph-level (entire graph/network)
    * Node level
    * Community/subgraph level (collection of similar nodes)
    * Edge-level (similar relationships)

---
# Applications of Graph ML

## Node level tasks
1. **Node classification**
    1. predict property of a node
    2. Example: categorize online users/items
2. **Link prediction**
    1. Predict whether there are missing links or edges between 2 or more nodes.
    2. Example: Completing a knowledge graph
    3. Example: Entity resolution 
3. **Graph classification**
    1. Categorize graphs —> predict properties of drug molecules
4. **Clustering**
    1. Do nodes in a graph form a community?
    2. Example: Social network “social circle” detection
5. **Graph Generation** —> discover and predict new drugs
6. **Graph Evolution** —> physical simulation 


### Real-World Examples of Node level tasks
1. Protein Folding
    1. Predict protein 3D structure based on amino acid sequence.
    2. Graph representation:
        1. Nodes: amino acids of protein sequence 
        2. Edges: amino acids that are similar to each other (residues)



## Edge Level Examples
1. **Recommendation Systems**
    1. This is the **most common example of a bipartite graph**.
    2. User-Item interactions (e.g. movies, music, merchandise)
    3. **Nodes: Users + Items**
    4. **Edges: User-Item interactions** 
    5. Goal: Recommend user preferences given node-edge relationships/interactions with items 
    6. Prediction Task: Nodes should be closer together that are more similar based on their edge interactions. 
2. **Drug Side Effects in healthcare**
    1. Patients take many drugs to treat complex or co-existing conditions.
    2. Task: given a pair of drugs —> predict adverse side effects 
    3. Goal: Biomedical Graph Link Prediction
        1. Nodes: Drugs & Proteins
        2. Edges: Interactions
            1. Protein-Protein interactions 
        3. Query: How likely will Simvastatin & Cipro when taken together lead to muscle breakdown?
    4. New drug side-effects can be discovered



## Subgraph-Level Machine Learning Tasks
    1. **Traffic Prediction in Google Maps** -- this is an example that we use just about everyday!
        1. Nodes: Road segments 
        2. Edges: Connectivity between road segments
        3. GNN predicts travel time given data



## Graph Level Machine Learning Tasks
1. Drug Discovery
    1. Nodes: Atoms
    2. Edges: Chemical Bonds
    3. Which molecules should be prioritized?
    4. GNN classification can predict optimal combinations.
2. Graph Generation
    1. Generate new molecular structures or pathways that have not been seen before
    2. Optimize existing drug molecules

---
# Choice of Graph Representation 

1. Objects: nodes, vertices —> N
2. Interactions: links, edges —> E 
3. System: network, graph —> G(N,E)


## How to build a graph
1. What are the nodes?
2. What are the edges?
3. Choice of network representation of a given domain/problem  determines the success of your predictions. 


## Directed vs. Undirected Graphs

1. **Undirected**
    1. Links: undirected (symmetrical, reciprocal)
    2. Examples: 
        1. Collaborations
        2. Social network friends
2. **Directed**
    1. Links: directed (arcs)
    2. Examples:
        1. Phone calls
        2. Twitter followers
    3. Connectivity of Directed Graphs
        1. Strongly connected
            1. Path from each node to every other node and vice versa (e.g. A-B, B-A)
        2. Weakly connected 
            1. Connected if we ignore edge directions
    4. Strongly Connected Components (SCCs)
        1. Not every node is part of a nontrivial strongly connected component.
            1. In-component: nodes that can reach SCC
            2. Out-component: nodes that can be reached from SCC
3. **Undirected Node degrees, k**
    1. Number of edges adjacent to node
    2. Avg node degree = sum of all nodes in network —> 2*E/N
        1. 2 times the number of edges divided by number of Nodes
4. **Directed Node degrees**
    1. In-degree
    2. Out-degree
    3. Total degree of a node is the sum of in + out degrees
5. **Bipartite Graphs**
    1. Nodes can be divided into 2 disjointed sets U and V
    2. Every link connects node U to one in V
    3. U and V are independent sets
    4. Examples:
        1. Authors to papers they authored
        2. Actors to movies they appeared in 
        3. Users to movies they rated
        4. Recipes to ingredients they contain
6. **Folded Networks**
        1. Author collaboration networks
        2. Movie co-rating networks



# Representing Graphs
1. **Adjacency Matrix**
    1. Graph is represented as a matrix.
    2. 1 == if link from node to node
    3. 0 == if no links/connections
    4. Symmetry
        1. Undirected graphs are symmetric 
        2. Directed graphs are NOT symmetric 
    5. Node Degrees
        1. Summation across row and/or columns
    6. Adjacency Matrices are Sparse
        1. Most real-world networks are sparse matrices
      
![image](https://github.com/user-attachments/assets/831936bf-cf08-4b7c-8e49-2b3c25500b43)

Source: [Stanford CS224W: Machine Learning with Graphs | 2021 | Lecture 1.3 - Choice of Graph Representation​](https://www.youtube.com/watch?v=P-m1Qv6-8cI&list=PLoROMvodv4rPLKxIpqhjhPgdQy7imNkDn&index=3)

2. **Edge list**
    1. List of edges is another representation of graphs but not ideal.
    2. This represents all possible connections between nodes and edges.
  
![image](https://github.com/user-attachments/assets/4e688566-e1b7-480f-833b-b210dc93f57e)
Source: Same as above

3. **Adjacency list**
    1. Easier to work with if networks are:
        1. Large
        2. Sparse
    2. Allows quick retrieval of all neighbors of a given node
        1. Example: 
            1. 1:
            2. 2: 3, 4
            3. 3: 2, 4
            4. 4:5
            5. 5:1, 2
4. Node and Edge Attributes, possible options:
    1. Weight (e.g. frequency of communication)
    2. Ranking (e.g. best friend, second best friend, etc.)
    3. Type (e.g. friend, relative, co-worker)
    4. Sign (e.g. friend vs. foe, trust vs. distrust)
    5. Properties depend on structure of rest of graph
        1. e.g. number of common friends


* This is a great reference for visualizing graphs via the mathematical representations above: [visualalgo.net](https://visualgo.net/en/graphds)

![image](https://github.com/user-attachments/assets/9dbda41d-0c8e-440e-b350-e8a7321b05aa)


## Other types of graphs
1. Unweighted (undirected)
2. Weighted (undirected)
    1. Instead of 0 or 1, we can use higher values with specific weights.
3. Self-edges (self-loops, undirected)
    1. Entries on diagonal of adjacency matrix
4. Multigraph (undirected)
    1. Same links but different meaning 
5. Connected (undirected) graph
    1. Any 2 vertices can be joined by a path. 
    2. Disconnected graph is made up by 2 or more connected parts
    3. A graph is connected if there exists a (finite) path between each pair of nodes.
    4. A graph is disconnected if there does not exist a path connecting every pair of nodes

![image](https://github.com/user-attachments/assets/6db6f997-26c6-4593-818c-8d3eb584f455)

* [Source](https://olizardo.github.io/networks-textbook/lesson-graphs-connectivity.html)

---
# Traditional Methods for ML in Graphs

## Different levels of tasks for ML in Graphs
1. Node-level predictions (vertices)
2. Link-level predictions (edges)
3. Graph-level predictions (entire graph or sub-graphs or communities)



## Traditional Machine Learning Pipelines
* These clasically invovle:

1. Train ML model: 
    * Random Forest
    * SVM
    * Neural network

2. Apply Model
    * Given node-link-graph, obtain features + make predictions 



## Feature-Design for Graphs on Undirected Graphs
* **The goal here is: How do we make predictions for a set of objects?**

### Design choices:
1. Features
    1. d-dimensional vectors
2. Objects
    1. Nodes
    2. Edges
    3. Set of nodes
    4. Entire graphs
3. Objective function
    1. What task are we trying to solve


### Mathematical Function
* The goal is to learn a function:

```
- Given: G ‎ =  (V, E)
- Learn function: f : V -> R (e.g. for given node V)
```


## Node-level Tasks
* Semi-supervised case (Node Classification)
* Given a few nodes that are labeled how can we predict the nodes that are not labeled? 
* We need Machine learning features!


### Goal: Describe the structure and position of a Node in the network:

#### 1. **Node degree (structure of network around node)**
		* **Degree k of node v is number of edges (neighboring nodes) the node has.**
		* **All neighboring nodes are treated equally which is a downside because they are unique!!!**
		* This only tells us how many nodes are connected based on their similar features/links/edges but **not their weighted or ranked level of importance to the entire network!!**
		* As example: we could have 4 nodes of patients with heart disease which are similar because of this feature. However, related to other nodes and edges, how important or impactful is each node to the entire group?

  ![image](https://github.com/user-attachments/assets/6bc92235-831c-4da1-b042-67de46c7bd9f)

  Source: Stanford CS224W: Machine Learning for Graphs https://cs224w.stanford.edu


#### 2. **Node centrality** 
		* Node degree counts neighboring nodes without capturing each nodes importance in the network.
		* Centrality c takes node importance in the entire graph into account
		* how we model importance:
			1. **Eigenvector centrality**

   ![image](https://github.com/user-attachments/assets/9562325f-53ca-4ff1-9fa8-4e26ee64b9f6)
   Source: Stanford CS224W: Machine Learning for Graphs https://cs224w.stanford.edu

			2. **Betweenness centrality** — node lies on many shortest paths between other nodes (e.g. a “transit hub” connector for other nodes)

   ![image](https://github.com/user-attachments/assets/65dfc103-2611-4515-bfba-b689d0bc2886)
   [Source](https://www.youtube.com/watch?v=3IS7UhNMQ3U&list=PLoROMvodv4rPLKxIpqhjhPgdQy7imNkDn&index=4)
   

			3. **Closeness centrality** — node is important if it has small shortest path lengths to all other nodes

   ![image](https://github.com/user-attachments/assets/76809f61-5da8-4ce9-bfe7-0c38941418a8)
   [Source](https://www.youtube.com/watch?v=3IS7UhNMQ3U&list=PLoROMvodv4rPLKxIpqhjhPgdQy7imNkDn&index=4)

			* ….more…

#### 3. **Clustering coefficient**
		* measures how connected v’s neighboring nodes are
		* # edges of neighbor nodes / kv2
		* Metric is between 0 and 1


  ![image](https://github.com/user-attachments/assets/30e98ecc-e7c1-4b9e-a3f1-8d8fef2f6760)
  [Source](https://www.youtube.com/watch?v=3IS7UhNMQ3U&list=PLoROMvodv4rPLKxIpqhjhPgdQy7imNkDn&index=4)

  
#### 4. **Graphlets**
		* Clustering coefficient counts **num of triangles** in ego-network of node
		* We can generalize this by counting # of pre-specified subgraphs or graphlets
		* We can quantify the number of possible graph lets 
		* 2-node, 3-node, 4-node, 5-node graphlets 
    * Source: same as above

![image](https://github.com/user-attachments/assets/1cc343d0-ecf9-45b6-afd3-ed3fa036e4b4)


![image](https://github.com/user-attachments/assets/6491ac7e-f838-4276-9e59-6d61ac27624f)



### Graphlet Degree Vector (GDV)
* Graphlet degree vector counts the number of graphlets that a node touches at a particular orbit position.
* If we only consider graphlets of 2 to 5 nodes we get a total of **73 orbit positions.**
* Therefore, GDV will be a vector of 73 coordinates.
  * It is a signature of a given node that describes the topology of node's neighborhood. Captures its interconnectivities out to a distance of 4 hops. You can compare GDV of two nodes and get a highly constraining measure of local topological similarity between them. Maybe you can use it as your node feature vector??
  * [Source](https://wandb.ai/syllogismos/machine-learning-with-graphs/reports/3-Motifs-and-Structural-Roles-in-Networks--VmlldzozNzU1NTg)

### Automorphism Orbits
* For a node `uuu of graph G`, the automorphism orbit of `uuu` is `Orb(u)={v∈V(G);v=f(u)` for some `f=Aut(G)}Orb(u) = \lbrace v \in V(G)`; v = f(u) \text{ for some } f = Aut(G)\rbraceOrb(u)={v∈V(G);v=f(u) for some f=Aut(G)}

![image](https://github.com/user-attachments/assets/d5b7800d-877e-46c7-a62a-779663a78720)


* The Aut denotes an automorphism group of G, i.e., an isomorphism from G to itself. This is a bit confusing, you can look at the image below to see how a,b,c,da, b, c, da,b,c,d are orbit positions for the node vvv in graph GGG. You assume vvv in those positions and count the number of instances that graphlet touches node vvv
* The node vvv can assume any of the positions a,b,da, b, da,b,d in the graphlets. But not ccc Hence in the graphlet degree vector you put in 0 for orbit position ccc

![image](https://github.com/user-attachments/assets/9018780e-2fb3-4681-8b9b-db5fb9e51875)


### Graphlet Node Features
* If we only consider graphlets 2 to 5 nodes we will have:

1. Vector of 73 coordinates is a signature of a node that describes the topology of a node’s neighborhood 
2. Distance of 4 hops captures interconnectivity — a chain of 4 edges has 5 nodes
3. Graphlet degree vector provides measure of node’s local network topology
    1. By comparing vectors of 2 nodes this provides a more detailed measure of local topological similarity than node degrees or clustering coefficients
  
---
# Structural Roles in networks
* Roles are functions of nodes in a Network.
* Roles are measured by structural behaviors.
* **Note roles are different from groups/communities!!!!**
  * Roles are based on the **similarity of ties between subsets of nodes**.
  * Nodes with the **same role have similar structural properties**, however they don’t need to be in direct or even indirect interaction with each other.
* A **Group/community** is formed based on **adjacency, proximity or reachability of nodes in the same community** and are well-connected to each other.


## Structural equivalence
* In the diagram below, nodes u and v are structurally equivalent if they have the **same relationships to each other.**
* **Structurally equivalent nodes are likely to be similar in different ways.**
* A an example, node u and v are structurally equivalent in the figure below because they connect other nodes **in the same way.**
* [Source](https://snap-stanford.github.io/cs224w-notes/preliminaries/motifs-and-structral-roles_lecture)

![image](https://github.com/user-attachments/assets/b51d0e6a-325e-497a-bfbf-eaf803a8ed82)


## Discovering Structural Roles in Networks
* These are a few problems where determining structural roles in a network are useful
* [Source](https://wandb.ai/syllogismos/machine-learning-with-graphs/reports/3-Motifs-and-Structural-Roles-in-Networks--VmlldzozNzU1NTg)

![image](https://github.com/user-attachments/assets/5324ad30-a3e7-43e1-aa6b-daa80da52be0)

* Another summary of role discovery from Rossi et al. 2016:

![image](https://github.com/user-attachments/assets/2a69188a-112f-4292-b611-64bb2b7e2baf)


## RoIX
* Roles allow us to identify different properties of nodes in network. Here we will introduce an automatic structural roles discovery method called RolX. It’s an unsupervised learning approach without prior knowledge.
* [More about RoIX here](https://snap-stanford.github.io/cs224w-notes/preliminaries/motifs-and-structral-roles_lecture)



---
# References
1. [Stanford CS224W: ML with Graphs | 2021](https://www.youtube.com/watch?v=4dVwlE9jYxY&list=PLoROMvodv4rPLKxIpqhjhPgdQy7imNkDn&index=5)
2. [Network comparison using directed graphlets](https://arxiv.org/abs/1511.01964)
3. [Encoding edge type information in graphlets](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0273609)
4. [Traditional ML for Graphs](https://medium.com/@taunkdhaval08/traditional-ml-for-graphs-ca7bdbef7544)
5. [Motifs and Structural Roles in Networks](https://wandb.ai/syllogismos/machine-learning-with-graphs/reports/3-Motifs-and-Structural-Roles-in-Networks--VmlldzozNzU1NTg)
6. [Biological network comparison using graphlet degree distribution](https://academic.oup.com/bioinformatics/article/23/2/e177/202080?login=false)
7. [Stanford SNAP - Motifs and Structral Rules in Network](https://snap-stanford.github.io/cs224w-notes/preliminaries/motifs-and-structral-roles_lecture)
8. [Stanford CS224W Class Notes](https://snap-stanford.github.io/cs224w-notes/)
9. [Rossi et al. Role Discovery in Networks, 2016](https://arxiv.org/pdf/1405.7134)
