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
