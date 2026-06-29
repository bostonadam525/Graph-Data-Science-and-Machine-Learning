# Agents


---
## What is an AI Agent
1. Entity that perceives its environment through inputs
2. Reasons and plans using an LLM as a cognitive engine
3. Using tools and ingegrations takes actions
4. Augumented with persistent memory to --> store, retrieve, and apply knowledge across interactions.

- This is best depicted as:
```
Perception | Action | Reasoning | Memory


              AGENT

```
### Stateless Agents
- What they can do:
  - Perceive inputs
  - Reason over inputs
  - Produce outputs
- NO MEMORY!!!!
  - They are not able to retain or recall information beyond single interactions.

- **Disadvantages of Stateless Agents**
  - Cannot perform Long-Horizon Tasks (e.g. run for several minutes, hours, days)
  - No context awareness across sessions
  - No learning or adaptation abilities
  - High operational costs --> "context stuffing" --> sending the same prompt through the context window everytime == more tokens == more $$$ and computational cost
 
### Memory Augmented Agents
- Same DAG as Stateless Agents: Perceive inputs, Reason over inputs, Produce inputs all using the LLM as the cognitive guide.
- However, the key difference is the outputs are **persistently stored and retrieved as memory**
  - Memory --> augments reasoning, perception, and action capabilities with **persistent memory** enabling:
      1) Context awareness
      2) Long-horizon tasks
      3) Adaptive behaviors
   
- **Advantages of Memory-Augmented Agents**
  1. Supports long-horizon tasks
  2. Sustained Context Awareness across sessions
  3. Improved efficiency & reduced operational cost
  4. Greater reliability in multi-step workflows
 
#### Types of Memory
1. Naive-memory augmented agent
   - Going from stateless to an agent that remembers can be achieved with a naive implementation of a memory augmented agent with recollections of previous interaction between the user(s) and the assistant(s).
   - Key benefit --> reliability in continuation of interaction with historical context

2. Conversational Memory
   - ideally, conversational memory is a time-ordered log of prior user-agent chat turns, stores as: timestamp, user_message, assistant message
   - Why do we need to go beyond conversational memory?
     - **Conversation windows are finite; user relationships are not.**
     - Not all valuable information surfaces in a single conversation --> moving beyond a single interaction or prompt, etc.
     - Agents need structured, queryable knowledge -- not just chat logs.


---
## Classes of Agentic Memory
1. Short Term
   - Semantic Cache --> caching previous prompts and responses
   - Working Memory --> LLM context window, and any session based interaction (this is similar to a "scratch pad" where the LLM can list its reasoning with each step over time)

2. Long Term
   - Procedural --> Workflow, Toolbox
   - Semantic --> Entity memory, Knowledge base (e.g. data, domain specific knowledge), Persona
   - Episodic --> Summaries, Conversational
  
---
# What is Agent Memory?
- Refers to the system of architectural components, control mechanisms, tools, and software harness that enables an AI agent to persistently store, organize, retrieve, and reuse information across time, interactions, and execution contexts, ensuring temporal and contextual continuity, even across fragmented interactions.
- These usually consist of:
  1. Embedding model
  2. Database(s)
  3. LLM
 
## **A dirct parallel is a RAG pipeline.**
- Diagram below is from deeplearning.ai
- The concept is that you leverage a memory manager and different forms of agentic memory to  query the data ingestion source for the memory types.

<img width="1059" height="567" alt="image" src="https://github.com/user-attachments/assets/fb8d027a-2085-4cae-9122-8c3554fd3970" />

## Where is Memory located in an Agentic System?
1. LLM
2. Embedding model
3. Data ingestion (e.g. databases)

- The **Agentic memory core** is the data ingestion core (Database). 
  - This is the primary data infrastructure component of an agent system.
  - This is responsible for managing the complete lifecycle of agent memory.
  - Database layer handles persistent storage, efficient retrieval, and memory operations that enable agents to: learn from interactions and maintain consistent performance across sessions.
- A database is the **Agentic Memory core**

## Deterministic vs Agent-Triggered
- Memory operations are based on 2 main things:

1. Deterministic agentic actions
   - Memory reads/writes that run automatically on a fixed schedule or predefined condition, independent of the agent's judgement. 

2. Agent Triggered
   - Memory reads/writes that the agent decides to invoke based on its own real-time assessment of needs.
  
## What are Memory Units? 
- A memory unit is the smallest atomic piece of information represented with a minimal set of attributes so it can be captured, retrieved, and updated by a memory-augmented agent.

## What is Context Engineering?
- This involves optimally selecting and shaping information placed into an LLM context window so it can perform a task reliably -- while explicitly accounting for context window limits and model constraints.
- What this means for agentic workflows? We may have multiple data sources (e.g. API, database, MCP, tool calls) -- but rather than stuffing it all within the same context window --> we optimally select the context
- The goal is to maximize the signal to noise ratio of each token in the context window.

## Memory Engineering
- Disciplined focus on designing, building, and maintaining memory systems for AI agents.
- It encompasses the storage, retrieval, classification, and lifecycle management of agent memory.
- This is MEMORY LIFECYCLE MANAGEMENT.

## What is the memory lifecyle? 
- There are many steps.....

1. Raw data sources
2. Aggregation + ingestion (collection information from multiple sources --> RAW DATA)
3. Representation + metadata enrichment (vector embeddings, metadata --> timestamps, intent, semantics, information)
4. Storage (e.g. databases --> short term, medium term, long term)
5. Organization of information (Modeling, indexing, relationships --> specify temporal, semantic, and relational indexing)
6. Retrieval (actionable memory --> e.g. text search, vector similarity, graph traversal)
7. Retrieved memory and context is sent to the LLM for inference, processing, and reasoning.

- The key: **Continuous Learning Lifecycle** --> memory feeds LLM reasoning and outcomes become new memory components.

<img width="852" height="889" alt="image" src="https://github.com/user-attachments/assets/e8e3d1b4-589c-4053-a28e-da0d6689e349" />


---
# Memory Engineering - Components
- This is the intersection of different engineering disciplines coming together. 
1. Database engineering
   - persistent storage
   - typed schemas
   - ACID transactions
   - multi-store architecture
2. Agent Engineering
   - memory lifecycle
   - write-back loops
   - memory extraction
   - autonomous consolidation
   - context-aware routing
3. Machine Learning Engineering
   - embedding models
   - fine tuning (e.g. SLMs)
   - model versioning
   - reranking pipelines
   - continual learning
  
4. Information Retrieval
   - hybrid search
   - vector indexes (HNSW, IVF)
   - relevance ranking
   - context assembly
   - query optimization

<img width="849" height="847" alt="image" src="https://github.com/user-attachments/assets/94abb166-e4fa-4192-a352-198294b95842" />

---
# Memory Aware Agent




---
# References
1. Agent Memory: Building Memory-Aware Agents: https://www.deeplearning.ai/courses/agent-memory-building-memory-aware-agents
2. A-MEM: Agentic Memory for LLM Agents: https://arxiv.org/abs/2502.12110


---
# Agentic Memory & Graph ontologies
- To understand why agentic memory is inherently reliant on **graph ontologies**, we must examine the architectural shift from treating AI as a solitary text-predictor to treating it as a dynamic, persistent software system (Rasmussen et al., 2025).
    - When memory is decoupled from the model and moved into a dedicated infrastructure layer, standard databases (flat text or pure vector stores) often fall short. They lack the ability to model complex, evolving relationships over time.
    - This is where **graph ontologies** provide the structural framework required to govern the entire memory lifecycle.
    
    ## 1. Why Monolithic Prompts Are Brittle
    
    Legacy AI systems often rely on multi-page monolithic prompts which are not only regressing system design back to circa 2022 (initial release of ChatGPT), but overfitting a model. A "monolithic prompt" attempts to pack task logic, control flow, historical context, and output generation into a single, massive context window (arXiv:2605.15425). This paradigm is highly fragile for several reasons:
    
    - **Diluted Signal-to-Noise Ratio:** Stuffing raw data, tool outputs, and historical logs into one prompt violates the core rule of **Context Engineering**: *maximizing the semantic signal per token*. The model becomes overwhelmed by noise, leading to attention drift or "lost-in-the-middle" phenomena.
    - **All-or-Nothing Execution Failures:** If a single step in a monolithic prompt fails or generates an invalid output, the entire pipeline collapses, requiring an expensive, full-context rerun (arXiv:2605.15425).
    - **Context Explosion & Memory Drift:** Monolithic prompts cannot scale. As an agent interacts over long horizons, text accumulation causes uncontrolled contextual growth, which introduces contradictory or stale information and degrades the model’s reasoning (SuperOpt, n.d.).
    - **Lack of Traceability:** In a massive block of unstructured prompt text, it is nearly impossible to track state changes, trace provenance, or enforce deterministic data updates.
    
    ## 2. Why Agentic Memory Relies on Graph Ontologies
    
    Graph ontologies solve the brittleness of monolithic prompts by transforming raw data into an explicit network of structured **Memory Units** (nodes) and their semantic, temporal, or causal relationships (edges) (Rasmussen et al., 2025).
    
    Here is how the core components of an agentic system align with graph architecture:
    
    ### A. The Database Layer as the Memory Core
    
    The user notes state that the *Agentic Memory Core is the Database Layer*, responsible for managing the complete lifecycle. A graph database running a formal ontology acts as this core infrastructure because it handles:
    
    - **Persistent & Relational Storage:** Instead of dumping text into a flat file, it map interactions into typed schemas (e.g., an episode node connected to an entity node via an `INTERACTED_WITH` edge) (Rasmussen et al., 2025).
    - **Continuous Learning Loops:** As outcomes occur, they are written back into the graph, evolving the network over time without rewriting historical data (Rasmussen et al., 2025).
    
    ### B. Structuring Atomic "Memory Units"
    
    A memory unit is the smallest atomic piece of information. In a graph ontology, a memory unit maps precisely to a **node or a hyper-edge with metadata attributes** (e.g., timestamps, intent, semantics) (Rasmussen et al., 2025). Because these units are structured with minimal, strict attributes, the agent can update a single node (e.g., changing a user preference) without disturbing the rest of the memory ecosystem.
    
    ### C. Precision Context Engineering (Maximizing Signal-to-Noise)
    
    Instead of stuffing multiple raw data sources into a context window, graph ontologies allow an agent to use **Graph Traversal** alongside vector search.
    
    > Rather than fetching a massive chunk of text via broad similarity search, the agent can retrieve a specific entity node and precisely traverse its adjacent edges to pull *only* contextually relevant facts (e.g., "Find the user's favorite tool, its schema, and their last 3 execution errors"). This guarantees a maximized signal-to-noise ratio for every token spent.
    > 
    
    ### D. Governing Deterministic vs. Agent-Triggered Operations
    
    Graph ontologies provide a clean substrate for both execution styles:
    
    - **Deterministic Actions:** Predefined database triggers or code scripts can run automatically to clean up, archive, or index graph connections (e.g., a scheduled script that prunes edges older than 30 days or consolidates tightly clustered entities into a single "community node") (Rasmussen et al., 2025).
    - **Agent-Triggered Actions:** When an LLM actively decides it needs information, it doesn't just guess keywords; it can dynamically formulate precise graph queries (like Cypher or SPARQL) based on its real-time assessment to pull exact subgraphs into its context window (CEUR-WS, 2026).
    
    ## 3. The Memory Engineering Intersection
    
    Managing this continuous lifecycle requires a disciplined synthesis of four distinct fields, unified by the graph schema:
    
    ```markdown
                      +-----------------------------------+
                      |        GRAPH ONTOLOGY             |
                      |  (The Unifying Semantic Layer)    |
                      +-----------------+-----------------+
                                        |
           +----------------------------+----------------------------+
           |                            |                            |
    +------v--------------+    +--------v------------+    +----------v----------+
    |DATABASE ENGINEERING |    | AGENT ENGINEERING   |    | MACHINE LEARNING /  |
    | - Typed schemas     |    | - Memory extraction |    | INFORMATION RETR.   |
    | - ACID transactions |    | - Autonomous loops  |    | - Vector embeddings |
    | - Graph traversal   |    | - Context routing   |    | - Hybrid search     |
    +---------------------+    +---------------------+    +---------------------+
    ```
    
    - **Database Engineering:** Enforces the typed graph schema, manages ACID transactions during multi-node memory writes, and optimizes traversal indexing.
    - **Agent Engineering:** Extracts memory units from interaction traces, routes data to the correct subgraphs, and handles the autonomous write-back loops when an agent learns a new rule.
    - **Machine Learning & Information Retrieval:** Combines structural graph queries with dense vector search (hybrid search), embedding graph nodes into a shared vector space so the agent can find related context using both semantic similarity and explicit relational connections (Rasmussen et al., 2025).
    
    ### Summary
    
    - Monolithic prompts fail because they treat memory as a giant, unstructured scratchpad (among other reasons).
    - Agentic memory relies on **graph ontologies** because they provide a stable, scalable database core. By breaking data down into atomic memory units and linking them explicitly, the system allows agents to dynamically traverse, cleanly engineer context windows, and execute deterministic lifecycle management safely outside the LLM context window.
    - Thus, having a solid graph ontology foundation forms the foundation for future development of a more modern state of the art infrastructure using agentic memory.
    
    ### References
    
    - CEUR-WS. (2026). Personal Agents and Conversational Memory. *CEUR Workshop Proceedings*, 4210, paper 1.
    - arXiv. (2026). Runtime-Structured Task Decomposition for Agentic Coding Systems. *arXiv preprint*, arXiv:2605.15425.
    - Rasmussen, P., Paliychuk, P., Beauvais, T., Ryan, J., & Chalef, D. (2025). Zep: A Temporal Knowledge Graph Architecture for Agent Memory. *arXiv preprint*, arXiv:2501.13956.
        - *Cited by: 265*
    - SuperOpt. (n.d.). *SuperOpt: Agentic Environment Optimization for Autonomous AI Agents*. Superagentic AI.
