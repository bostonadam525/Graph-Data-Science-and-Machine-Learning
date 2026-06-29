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
