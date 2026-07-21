# Building Blocks of Graphs
* Classical NLP techniques form the backbone of knowledge graphs and graph data science.
* This includes but is not limited to:
  1. Tokenization
  2. Dependency Parsing
  3. Constituency Parsing
  4. NER
  5. Word Sense Disambiguation
 

* This repo contains insights related to this. 
---
# RDF 



---
# SPARQL
- SPARQL --> SPARQL protocol and RDF query language.
- Data Retrieval and QueryingFind patterns:

1. Match specific subject-predicate-object relationships in a graph.
2. Tabular results: Use SELECT queries to get data back in rows and columns.
3. Boolean checks: Use ASK queries to see if a specific data pattern exists.
4. Graph extraction: Use CONSTRUCT or DESCRIBE queries to generate new sub-graphs.

- Data Management and UpdatesAdd and delete: 
1. Insert new triples or remove old ones from a database using update commands.
2. Graph control: Clear, copy, or move entire sets of graphs within a server

- Web and Semantic Integration
1. Federated queries: Search and combine data from multiple different online databases at the same time using the SERVICE keyword.
2. Reasoning: Infer new facts that are not explicitly written in the data by using standard rules and ontologies.
---

# Semantic Web Standards for Agentic Pipelines: Definitions & Core Framework

This document provides a concise glossary of key semantic web standards and outlines a unified structural framework for utilizing them to build an autonomous agentic knowledge graph.

---

## 1. Executive Glossary

*   **RDF (Resource Description Framework):** The foundational graph data model that represents all information as atomic "triples" consisting of a Subject, Predicate, and Object (e.g., `Agent_1` $\rightarrow$ `hasCapability` $\rightarrow$ `WebSearch`).
*   **SPARQL (Protocol and RDF Query Language):** The SQL-equivalent querying and graph-manipulation language designed explicitly for RDF data, allowing agents to read, filter, insert, and delete graph data.
*   **SHACL (Shapes Constraint Language):** A validation standard used to define structural and logical conditions for a graph, acting as a strict compiler/guardrail to ensure data matches expected schemas.
*   **SKOS (Simple Knowledge Organization System):** A standardized model for building controlled vocabularies, taxonomies, and thesauri, enabling hierarchical concept management (e.g., mapping synonyms and broad/narrow topics).
*   **OWL (Web Ontology Language):** A powerful logic language used to define strict domain meanings, entities, relationship characteristics, and constraints, enabling databases to infer new facts via automated reasoning.

---

## 2. Core Architectural Framework

### System Topology

```

```



---
# OWL


---
# SHACL 


---
# SKOS 


--- 
# Ontology Design
