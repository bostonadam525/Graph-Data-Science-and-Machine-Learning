# Hybrid Graphs
- There are various approaches to this in the modern semantic stack.


---
# Hybrid Context Graph (aka "Vector Knowledge Graph" or Neuro-Symbolic Context Graph)
- CONCEPT: It bridges the classical Semantic Web (symbolic, deterministic logic) and modern Vector Search / NLP (probabilistic, unstructured textual embeddings).

```
HYBRID SYSTEM
                     ┌───────────────────────────┐
                     │   Hybrid Context Graph    │
                     └─────────────┬─────────────┘
                                   │
         ┌─────────────────────────┴─────────────────────────┐
         ▼                                                   ▼
┌─────────────────────────┐                         ┌─────────────────────────┐
│     Semantic Web        │                         │  Unstructured / Vector  │
│    (Symbolic Layer)     │                         │   (Probabilistic Layer) │
├─────────────────────────┤                         ├─────────────────────────┤
│ • Cross-walked          │                         │ • Extracted clinical    │
│   ontologies            │    Cross-Linked Via     │   notes/documents       │
│   (SNOMED-CT, RxNorm,   │ <─────────────────────> │ • Dense vector          │
│   UMLS, ICD-10)         │   Entity Linking &      │   embeddings &          │
│ • RDF/OWL triples       │   Document Provenance   │   chunk similarity      │
│ • Strict graph schema   │                         │ • Cosine similarity     │
└─────────────────────────┘                         └─────────────────────────┘

```
## Why it's not just the "Semantic Web"
- The traditional Semantic Web relies on explicit, deterministic logic (RDF, OWL, SPARQL) where every node and edge must be formally defined.
- However, it struggles with raw unstructured clinical notes or fuzzy document similarities because open text doesn't natively fit into clean subject-predicate-object triples without losing context. [source](https://graphwise.ai/fundamentals/what-is-a-semantic-layer/#:~:text=It%20creates%20virtualized%20views%2C%20calculated%20metrics%2C%20and,and%20using%20ontologies%20to%20define%20data%20meaning.)


## Why it's a "Hybrid Context Graph"
- By anchoring unstructured text or vector embeddings directly to cross-walked ontologies (like SNOMED-CT mapped via UMLS CUIs), you can create a system that delivers:

1. **Symbolic Precision (Ontology Layer):** Formal hierarchies, strict relationships (e.g., DrugA $\$rightarrow treats $\$rightarrow ConditionB), crosswalks, and logical inferencing. [source](https://atlan.com/know/context-graph-vs-ontology/#:~:text=Richer%20than%20taxonomy%20but%20still%20limited.%20%2D,schema%3B%20the%20knowledge%20graph%20is%20the%20database.)

2. **Probabilistic Context (Document Layer):** Unstructured EHR notes, clinical trial PDFs, or doctor's dictations linked via dense vector embeddings (e.g., BioBERT, SapBERT) to preserve natural language nuances.


## How This Architecture Works in Practice
1. The Cross-Walked Ontology Layer (The Ground Truth)
- You import standard biomedical ontologies in RDF format and use unified crosswalks (like UMLS or RxNorm mappings):
  - SNOMED-CT: `snomed:233604007` ("Pneumonia")
  - ICD-10: `icd10:J18.9` ("Pneumonia, unspecified")
  - `RxNorm: rxnorm:161` ("Acetaminophen")

- These ontologies provide the exact, deduplicated nodes that prevent LLMs from confusing similar terms.


2. Entity Extraction & Grounding (The Bridge)
- When an unstructured clinical note arrives: "Patient presents with acute inflammation of the lungs and was prescribed Tylenol."
- An Entity Linking (Named Entity Recognition + Disambiguation) model extracts the mentions and maps them directly to the ontology nodes:
  - "inflammation of the lungs" $\rightarrow$ maps to SNOMED-CT `233604007` (Pneumonia).
  - "Tylenol" $\rightarrow$ maps to RxNorm `161` (Acetaminophen) via crosswalk.
 
3. Document Similarity & Chunk Annotation (The Context Layer)
- Instead of discarding the original document, you chunk the note and store it as a document node inside the RDF graph:
  - Vector Side: The chunk is converted into a vector embedding and stored in an index.
  - RDF/Graph Side: The chunk node is linked to the ontological entities using predicates like `prov:wasDerivedFrom` or `schema:mentions`.

```
# Example RDF Representation of the Hybrid Graph

@prefix ex: <http://example.org/health/> .
@prefix snomed: <http://snomed.info/id/> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix schema: <http://schema.org/> .

# Unstructured Document Chunk Node
ex:ClinicalNote_1042_Chunk1 
    a schema:DigitalDocument ;
    schema:text "Patient presents with acute inflammation of the lungs..." ;
    ex:hasVectorEmbedding "[-0.012, 0.431, 0.089, ...]" ;  # Vector context
    schema:mentions snomed:233604007 ;                   # Linked to SNOMED
    prov:wasAttributedTo ex:Doctor_42 .

# SNOMED Ontology Node (Cross-walked)
snomed:233604007 
    a ex:MedicalCondition ;
    rdfs:label "Pneumonia" ;
    ex:sameAsICD10 <http://hl7.org/fhir/sid/icd-10/J18.9> . # Crosswalk

```
### Key Advantages of this Hybrid Approach

| Feature | Standard RAG / Vector DB | Pure Semantic Web / Knowledge Graph | Hybrid Context Graph (Your Model) |
| :--- | :--- | :--- | :--- |
| **Data Format** | Unstructured text chunks + vectors | RDF triples / OWL ontologies | Chunks + Vectors linked to RDF triples |
| **Clinical Accuracy** | High risk of hallucination / context drift | High accuracy, but misses nuance in free text | High accuracy + full textual nuance |
| **Cross-Ontology Search** | Poor (relies on keyword matching) | Excellent (via explicit OWL/UMLS mappings) | Excellent (traverses crosswalks across text) |
| **Agent Utility** | Good for text generation, bad for reasoning | Good for logic queries, bad for fuzzy text | Optimal for Agentic AI (GraphRAG + Reasoning) |


---
# Graph Machine Learning with Hybrid Graphs 
- The hybrid context graph architecture is designed to be trained on by Graph Neural Networks (GNNs), processed via standard graph traversal algorithms, and served as a high-precision tool for LLM agents.
- By structuring a graph this way—combining symbolic cross-walks (e.g., SNOMED-CT/RxNorm) with textual embeddings and document chunks—you can unlock a powerful set of capabilities.

## 1. **Training GNNs (GraphSAGE & RotatE) on this Graph**
  - Because a graph such as above has multiple node types (Documents, Patients, Conditions, Drugs) and edge types (mentions, treats, sameAs), it is treated as a Heterogeneous Knowledge Graph. [source](https://pytorch-geometric.readthedocs.io/en/2.5.0/tutorial/heterogeneous.html#:~:text=Standard%20Message%20Passing%20GNNs%20(MP%2DGNNs)%20can%20not,update%20functions%20individually%20for%20each%20edge%20type.)

```
[Document Chunk Node] ──(mentions)──> [SNOMED: Pneumonia] ──(sameAs)──> [ICD-10: J18.9]
          │                                  ▲
   (derivedFrom)                         (treats)
          ▼                                  │
   [EHR Record Node] ─────────────────> [RxNorm: Antibiotic]
```


### Training with GraphSAGE (Inductive Learning)
- How it works: GraphSAGE generates embeddings by aggregating features from a node’s local neighborhood. [source](https://snap.stanford.edu/graphsage/#:~:text=After%20training%2C%20GraphSAGE%20can%20be%20used%20to,easily%20integrated%20into%20other%20machine%20learning%20pipelines.)
- Use Case: can use node attribute features like Dense Vector Embeddings (from document chunks) combined with Ontological Types.
- What it predicts: It can perform Inductive Link Prediction or Node Classification on unseen documents. For example, if a new clinical note arrives, GraphSAGE can predict which SNOMED codes or disease risks should automatically be linked to it based on neighborhood topology—without needing to retrain. [source](https://snap.stanford.edu/graphsage/#:~:text=In%20contrast%2C%20GraphSAGE%20is%20an%20inductive%20framework,attribute%20schema%20as%20the%20training%20data.%20Code.)

### Training with RotatE (Knowledge Graph Embeddings)
- How it works: RotatE projects relations as rotations in a complex vector space ($A + R \approx B$) to capture relation patterns (symmetry, inversion, composition).
- Use Case: RotatE is used for Knowledge Graph Completion.
- What it predicts: Given an input triple like (`RxNorm:DrugA`, `treats`, `?`) or (`Document_101`, `mentions`, `?`), RotatE calculates the distance in complex vector space to predict missing medical relationships or missing document annotations that were omitted in the raw text.

--- 
## 2. Graph Algorithms & Traversals for Predictions
- Once a GNN or KG Embeddings are trained, you can combine them with classical graph algorithms to query and make predictions given a specific input node:
  - a. Shortest Path & Pathfinding (Dijkstra / $A^*$):
    - Example Query: "What is the clinical mechanism connecting this specific unstructured doctor's note to a high-risk side effect?"
    - Execution: Traverses from the Document Chunk Node $\rightarrow$ Extracted SNOMED Entity $\rightarrow$ Ontological Hierarchy $\rightarrow$ RxNorm Drug $\rightarrow$ Adverse Reaction Node.
  
  - b. Personalized PageRank (PPR) & Random Walks:
    - Example Query: Given an input patient record, which historical clinical documents or ontology concepts are most structurally relevant?
    - Execution: Performs random walks starting at the patient's linked entities to measure graph closeness, filtering out noise in large medical databases.
  
  - c. Community Detection (Louvain / Leiden):Groups document chunks, patient notes, and medical concepts into high-level thematic "sub-topics" or patient phenotypes automatically.


## 3. Using the Graph as an Agent-Tool for an LLM (GNN-RAG & Agentic Workflows)
- In an agentic pipeline, this setup moves far beyond basic vector search (Naive RAG).
- The LLM does not need to read the whole database; it uses the Graph + GNN as an execution environment tool.

### Pattern A: The GNN as an LLM Search Filter (GNN-RAG)
- The user asks the agent a question: "Find historical trials or notes mentioning complications related to Pneumonia treatments."
- GNN Retrieval: The GNN (or RotatE/GraphSAGE model) takes the target `SNOMED:Pneumonia` entity node, scores the relevance of all $k$-hop neighbor document nodes, and extracts the top 5 most relevant path subgraphs.
- LLM Context Injection: The GNN hands only those targeted subgraphs and text chunks to the LLM. The LLM generates an accurate answer grounded by the graph topology.

### Pattern B: The LLM as a Graph Query Agent (SPARQL Tool Calling)
- The LLM acts as an agent with access to a custom tool function (execute_graph_query).
- LLM Translation: The agent converts natural language into a Cypher or SPARQL query using the SNOMED/RxNorm crosswalks:
```
SELECT ?documentText ?drugName WHERE {
  ?doc ex:mentions snomed:233604007 ;
       schema:text ?documentText .
  snomed:233604007 ex:treatedBy ?drug .
  ?drug rdfs:label ?drugName .
}
```
- Execution & Guardrails: A SHACL shape validates the query parameters, the database executes the query, and the exact result is returned to the agent without hallucination.

## Summary
- This hybrid structure gives the best of both worlds:
  - 1) Use GNNs (GraphSAGE/RotatE) for link prediction, entity matching, and node classification.
    2) Use Graph Algorithms (PageRank, $A^*$) for pathfinding, context retrieval, and sub-graph ranking.
    3) Use LLMs / Agent Tools for natural language understanding, query generation, and final response synthesis.  
