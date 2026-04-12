# LangChain

LangChain is an open-source development framework designed to simplify creating applications using Large Language Models (LLMs) like GPT-4. It connects LLMs to external data sources, APIs, and computation tools to build complex, context-aware, and agentic workflows in Python or JavaScript. Developed by Harrison Chase in October 2022, LangChain has become a dominant tool for building AI-driven applications like chatbots, document analyzers, and autonomous agents.

**So, what are the key features and components?**

- **Components/Modules:** Modular abstractions for working with LLMs, including prompts, models, and indexes.
- **Chains:** Sequences of actions that link LLMs with other tools (e.g., prompt + model + parser).
- **Retrieval (RAG):** Tools for connecting LLMs to private data, such as databases, PDFs, and websites.
- **Agents:** Systems that use LLMs to determine which actions to take, allowing for autonomous decision-making.
- **LangGraph & LangSmith:** Extensions for building stateful, multi-actor agents and monitoring/evaluating applications.

---

## What are MultiQueryRetriever and MultiVectorRetriever?

Both retrievers are advanced LangChain techniques designed to overcome the limitations of standard vector search, but they focus on different parts of the process: one optimizes the query, while the other optimizes the documents.

1. **MultiQueryRetriever (Query Optimization)**
   This retriever solves the problem where a user's question might not perfectly match the way information is written in your database.
   - **How it works:** It uses an LLM to automatically rephrase your original question into 3–5 different versions from multiple perspectives.

   - **The Process:**
     - The LLM generates alternative queries (e.g., How to fix a car? becomes Car repair steps, Automotive troubleshooting, etc.).
     - The system performs a vector search for every variation.
     - It deduplicates and merges all unique documents found across all searches.

   - **Best For:** Improving recall when users provide vague or poorly phrased questions.

2. **MultiVectorRetriever (Document Optimization)**
   This retriever decouples the data used for searching from the data sent to the LLM for answering.
   - **How it works:** It stores multiple vectors for a single parent document. Instead of searching the full text, it might search shorter child chunks or summaries while returning the original, larger document for context.

   - **Popular Methods:**
     - **Summaries:** You embed a concise summary of a long document. If a query matches the summary, the retriever fetches the full document.
     - **Hypothetical Questions:** You generate questions the document could answer and embed those. If the user asks a similar question, the document is retrieved.
     - **Smaller Chunks (Parent-Child):** You embed tiny snippets for high precision but return the large parent section so the LLM has enough context.

   - **Best For:** Complex data like tables, images (via descriptions), or very long documents where the meat of the info is buried.

---

## What are Self-querying and TimeWeightedVectorStoreRetriever?

These two retrievers are specialized tools for handling metadata filtering and time-sensitive information, respectively.

**1. Self-Querying Retriever**
The Self-Querying Retriever addresses the semantic search limitation where a model might find relevant text but ignore specific constraints (like from 2023 or rating > 4).

- How it works: It uses an LLM to self-query by translating a natural language question into a structured query. It splits the user's input into two parts:
- A Search Term: Used for semantic vector search.
- A Metadata Filter: Used to filter the database (e.g., filtering by genre or year).
- Example: If you ask, What are movies about space released after 2010?, the LLM creates a filter { year: { $gt: 2010 } } and searches the vector store only for space movies within that subset.
  Best For: Datasets with rich metadata (products, movie databases, structured logs) where users often ask for specific subsets.

**2. Time-Weighted Vector Store Retriever**
The Time-Weighted Retriever is designed for applications where freshness matters as much as relevance.

- How it works: It calculates a combined score for each document based on two factors:
  - Semantic Similarity: How well the document matches the query.
  - Recency: How long ago the document was last accessed or created.
- The Decay Formula: It uses a decay rate (often exponential). Information that hasn't been accessed in a long time fades away, while frequently or recently accessed info stays top of mind.
- Best For: Memory for AI agents, customer support bots, or news feeds where old information might be outdated or irrelevant to current events.

---

## LangChain Memory

In LangChain, Memory is the system component that enables LLMs to remember previous interactions. Since standard language models are stateless—meaning they treat every request as an isolated event—memory is what allows for natural, multi-turn conversations where the AI recalls your name or previous context.

**How it Works**
Every memory system performs two primary actions during a conversation:

- **Reading:** Before generating a response, the chain reads from memory to supplement the user's current input with past context.
- **Writing:** After generating a response, the chain writes the new interaction back into memory for future use.

---

### Core Types of Memory

**1. Buffer-Based Memory**

- **ConversationBufferMemory:** The simplest type. It stores the entire raw history of a conversation.
  - Pros: Perfectly accurate recall of every word.
  - Cons: Rapidly consumes tokens and will eventually hit the model's context limit.

- **ConversationBufferWindowMemory:** Maintains a sliding window of the last K interactions.
  - Best For: Keeping prompts lean and avoiding token overflow.

- **ConversationTokenBufferMemory:** Similar to the window memory, but flushes history based on a max token count instead of a set number of messages.
  - Best For: Precise cost and performance management.

**2. Summarization & Knowledge Memory**

- **ConversationSummaryMemory:** Uses an LLM to create a running summary of the chat as it progresses.
  - Best For: Extremely long conversations where keeping full text is impossible.

- **ConversationEntityMemory:** Extracts and stores specific facts about entities (people, places, objects) mentioned in the conversation.

- **ConversationKGMemory:** Builds a Knowledge Graph (triplets like User, lives in, Berlin) to track relationships between entities.

- **VectorStoreRetrieverMemory:** Stores history as embeddings in a Vector Database (like Pinecone or Chroma) and retrieves only the most semantically relevant parts of the past when needed.

**3. Modern & Persistent Memory**

- **LCEL (Adding Memory):** Modern LangChain uses the RunnableWithMessageHistory class. It wraps your chain and automatically manages history by mapping it to a MessagesPlaceholder in your prompt.

- **Memory Using SQLite:** For production apps that need to remember users after a restart, you can swap the default InMemoryChatMessageHistory for SQLChatMessageHistory. This persists all messages in a local SQLite database or other SQL-compatible stores.

---

### Text Splitters

Once you've loaded documents, they are often too large for an LLM's context window. Text Splitters break them into manageable chunks while trying to keep semantically related content together.

**1. Character-Based Splitters**

- **CharacterTextSplitter:** The most basic method. It splits based on a fixed character count and a specific separator (like \n\n).
- **RecursiveCharacterTextSplitter:** The gold standard for general text. It tries to split by the most natural characters first (paragraphs \n\n, then sentences \n, then words ) to keep related ideas in the same chunk.
- **MarkdownHeaderTextSplitter:** Intelligent splitting based on Markdown headers (#, ##, ###). It preserves the document's structure by adding the header path to the metadata of each chunk.
- **HTMLHeaderTextSplitter:** Similar to Markdown, but targets HTML tags (h1, h2, etc.) to slice web pages logically.

**2. Token & NLP Methods**

- **TokenTextSplitter:** Splits based on LLM tokens (using tiktoken) rather than characters. This is vital for ensuring your chunks fit perfectly within model limits without going over.
- **Text Splitting Methods in NLP:** These involve using libraries like NLTK or Spacy to split specifically at sentence boundaries or logical grammatical breaks rather than arbitrary character counts.
- **SemanticChunker:** A high-intelligence splitter that uses embeddings to find break points. It splits text where it detects a significant change in meaning or topic.

**3. Specialized Format Splitters**

- **Split Code:** RecursiveCharacterTextSplitter.from_language allows you to split code (Python, JS, C++, etc.) using separators specific to that language (like class or function definitions).
- **RecursiveJsonSplitter:** Designed for deeply nested JSON. it traverses the structure and splits it while maintaining the path to each value so the LLM understands the context of the data.

---

### Embeddings

In the LangChain ecosystem, Embeddings turn text into mathematical vectors, allowing computers to measure how similar two pieces of information are.

**1. Cloud-Based (High Precision)**

- **OpenAI Embeddings:** The industry standard (text-embedding-3-small/large). It offers high performance and low latency but requires an API key and incurs costs per token via the OpenAI Platform.
- **Upstage:** Excellent for high-performance retrieval, particularly with complex layouts and multi-lingual support, accessible via the Upstage Console.

**2. Local & Open Source (Privacy/Cost-Free)**

- **HuggingFace Embeddings:** Runs any open-source model (like all-MiniLM-L6-v2) locally on your hardware using the sentence-transformers library.
- **Ollama Embeddings:** Allows you to run models like mxbai-embed-large or nomic-embed-text locally with a simple setup via Ollama's official site.
- **LlamaCpp / GPT4ALL:** Optimized for running embeddings on standard consumer CPUs without needing a powerful GPU.

**3. Optimization & Advanced Types**

- **CacheBackedEmbeddings:** Prevents re-computing vectors for the same text by storing results in a cache (like Redis or a local file). This saves significant time and money during document ingestion.
- **Multimodal Embeddings:** These models (like CLIP) embed both images and text into the same vector space, enabling you to search for images using text descriptions (e.g., Find a picture of a cat in a hat).

---

### Vector Stores

In LangChain, Vector Stores are the databases that store and search your high-dimensional embeddings. They turn searching for keywords into searching for meaning.

**1. Local & Developer-Friendly (In-Memory/Local)**

- **Chroma:** The most popular open-source choice for LangChain. It’s ChromaDB is easy to set up and runs entirely on your local machine—perfect for prototyping.
- **FAISS (Facebook AI Similarity Search):** A high-performance library from Meta optimized for dense vector sets. Use FAISS when you need blazing-fast local search without the overhead of a full database.

**2. Cloud-Native & Managed (Scale-Ready)**

- **Pinecone:** A fully managed, Pinecone cloud-native vector database. It handles massive scale with zero infrastructure management, offering high-speed retrieval and live index updates.
- **Weaviate:** An open-source vector database that allows you to store both vectors and objects. Weaviate is known for its modularity and GraphQL support.
- **Qdrant:** Highly efficient and written in Rust. Qdrant provides a powerful API for filtering results based on specific metadata.

**3. Enterprise & Multi-Model**

- **Elasticsearch:** If you already use Elastic for search, their Vector Search integration allows you to combine traditional keyword search with vector similarity.
- **MongoDB Atlas:** Use Atlas Vector Search to keep your application data and vectors in the same database, simplifying your stack.
- **PGVector:** A specialized extension for PostgreSQL. PGVector lets you perform vector similarity searches directly within your existing SQL environment.
- **Neo4j:** A Graph Database that integrates vector search. Neo4j is the go-to for GraphRAG, where you need to navigate complex relationships alongside semantic search.

---

### Retriever

Retrievers are the logic layer that sits on top of your Vector Store to fetch the most relevant documents for an LLM. While a basic search just finds similar text, these advanced retrievers solve specific problems like accuracy, relevance, and lost-in-the-middle effects.

**1. Accuracy & Logic Boosters**

- **MultiQueryRetriever:** Uses an LLM to generate multiple variations of a user's question from different perspectives. This overcomes the limitations of a single search query by catching more relevant documents.
- **Self-querying:** The retriever uses an LLM to parse a natural language query into metadata filters and a search string. For example, Show me movies from 1994 becomes a filter year=1994 + a vector search for movies.
- **Contextual Compression:** Instead of passing full documents, this Compressor extracts only the relevant snippets from retrieved documents, reducing noise and saving tokens.

**2. Structuring & Hierarchy**

- **Parent Document Retriever:** Strikes a balance by splitting documents into small child chunks for precise searching, but returning the larger parent document to the LLM to provide better context.
- **MultiVectorRetriever:** Allows you to store multiple vectors per document. You can store a summary, specific keywords, or even different versions of the text to improve retrieval hits.

**3. Hybrid & Ranking Strategies**

- **Ensemble Retriever:** Combines multiple retrievers (like a BM25 keyword search and a Vector search).
  Convex Combination (CC): A specific way to weight the scores from different retrievers (e.g., 70% Vector + 30% Keyword) to get the best of both worlds.
- **Long Context Reorder:** LLMs often struggle with information in the middle of a long prompt. This Reorderer places the most relevant documents at the beginning and end of the prompt to maximize recall.

**4. Specialized Retrievers**

- **TimeWeightedVectorStoreRetriever:** Prioritizes recent information over old data. It uses a decay score so that newer documents are ranked higher, even if they are slightly less similar than older ones.

---

### Rerankers

Rerankers act as a high-precision second pass in RAG pipelines. While initial retrievers (bi-encoders) are fast at finding a broad set of candidates, rerankers (cross-encoders) use deep attention to joint-process query-document pairs and reorder them by actual relevance.

**1. Cross-Encoder Reranker**
Standard embedding models (bi-encoders) encode queries and documents separately, which can miss subtle context. A Cross-Encoder processes the query and each document together as a single input string.

- **How it Works:** It uses full self-attention across all tokens in both the query and the document to output a definitive relevance score.
- **Best For:** Maximum accuracy where you need to detect negations or complex logical constraints that simple vector similarity might miss.

- **Implementation:** In LangChain, this is typically done using the HuggingFaceCrossEncoder wrapped in a CrossEncoderReranker.

**2. JinaReranker**
Jina AI provides powerful, API-based reranking models specifically optimized for multilingual tasks and long-context processing (up to 1024 tokens).

- **Key Features:** Highly competitive on benchmarks for text-to-SQL, function calling, and code retrieval.

- **Usage:** You can integrate it as a Document Transformer or a compressor in a ContextualCompressionRetriever.

- **Benefit:** Ideal for global applications needing reliable, high-performance reranking via a simple API call.

**3. FlashRank Reranker**
FlashRank is an ultra-lite and blazing-fast Python library for reranking results locally without a GPU.

- **Efficiency:** Uses tiny (as small as 4MB) but highly optimized cross-encoder models, making it suitable for edge devices or latency-sensitive production environments.

- **LangChain Integration:** Supported via the FlashrankRerank class. It is often used as a Document Compressor to narrow down a large set of initial results to a concise top-N for the LLM.

---

### LangChain Expression Language (LCEL)

LangChain Expression Language (LCEL) is a declarative way to compose chains. It transforms standard Python functions and components into Runnables, which automatically support features like streaming, async execution, and parallelization.

**The Building Blocks of LCEL**

- **RunnablePassthrough:** Used to pass inputs through a chain unchanged or to add extra keys to a dictionary. It’s essential for piping data into the next step.
- **RunnableLambda:** A wrapper that converts any custom Python function into a Runnable, allowing you to use your own logic within a pipe (|).
- **RunnableParallel:** Executes multiple Runnables in parallel, merging their outputs into a dictionary. This is the key to speeding up chains that perform multiple searches or lookups.
- **Binding:** Use .bind() to pass constant arguments (like stop sequences or functions) to a model without changing the input schema of the chain.
- **Generator:** LCEL supports streaming via Python generators. When a Runnable yields data, the chain can stream results token-by-token to the user.

**Flow Control & Reliability**

- **Routing:** Allows you to conditionally branch your chain logic. Based on the input, the chain can route the query to different prompts or models (e.g., a Math chain vs. a History chain).
- **Fallbacks:** If a specific component fails (e.g., OpenAI API is down), Fallbacks allow the chain to automatically switch to a backup model like Anthropic or Ollama.
- **RunnableRetry:** Automatically retries a step if it encounters a transient error (like a network timeout), ensuring your pipeline is resilient.
- **WithListeners:** Attaches hooks to your chain to perform side effects (like logging or tracking latency) when a step starts or finishes.

**State & Runtime Configuration**

- **RunnableWithMessageHistory:** The modern way to handle memory. It wraps a chain and dynamically injects message history based on a session_id.
- **Configure-Runtime-Chain-Components:** Use .with_config() or .configurable_fields() to swap models or parameters (like temperature) at the moment you call the chain.
- **Inspect Runnables:** Use .get_graph() or .print_graph() to visualize the logic flow and debug the internal structure of complex LCEL chains.

**Defining Runnables Simply**

- **@chain Decorator:** You can create a Runnable by simply adding the @chain decorator to a function. This turns a standard Python function into an LCEL-compatible object that supports .invoke(), .stream(), and .batch().

---

### Chains

In LangChain, Chains are the logical glue that connects an LLM with other components like prompts, tools, and memory. While legacy off-the-shelf chains exist, the modern standard is to build custom sequences using LCEL.

**1. Summarization**
LangChain provides specialized patterns for condensing long documents that exceed a model's context window:

- **Stuff:** Stuffs all text into one prompt. Simple and cheap, but limited by token limits.
- **Map-Reduce:** Summarizes individual chunks (Map) and then summarizes those summaries (Reduce). Great for massive documents.
- **Refine:** Iteratively updates a summary as it reads through the document. High quality, but slower as it is sequential.
- **Implementation:** These can be invoked via load_summarize_chain.

**2. SQL & Structured Data**
These chains allow LLMs to interact with databases and return data in specific formats:

- **SQL Chain:** Converts natural language into SQL queries, executes them, and translates the result back into English. The SQLDatabaseChain is the core tool here.
- **Structured Output Chain:** Ensures the LLM returns data in a valid format (like JSON or a Pydantic model) rather than conversational text. This is critical for building APIs or feeding data into other software.
- **StructuredDataChat:** Specifically designed for chatting with CSVs, Excel, or SQL tables, providing a conversational interface for data analysis.

---

### Agents

In LangChain, Agents use an LLM as a reasoning engine to determine which Tools to call and in what order to solve a task. Unlike a fixed chain, an agent can iterate until it finds the answer.

**1. Tools & Binding**

- **Tools:** Functions or APIs (e.g., Google Search, a calculator, or a database lookup) that the LLM can trigger.
- **Bind Tools:** The process of telling an LLM which tools are available. Using .bind_tools(), you attach the tool's schema to the model so it knows the how and when to call them.

**2. Agent Architectures**

- **Tool Calling Agent:** The modern standard. It relies on the model's native capability (like OpenAI's Function Calling) to output structured tool requests.
- **ReAct (Tool Calling Agent with More LLM Models):** For models that don't natively support tool calling, the Reason + Act pattern uses specific prompting to force the model to think and then act in a loop.
- **Agentic RAG:** Unlike standard RAG, an Agentic RAG system can decide if it needs to search, how to rewrite a bad query, or whether to look in a different vector store entirely.

**3. Specialized Agents & Workflows**

- **CSV/Excel Analysis Agent:** Uses a Python REPL tool to write and execute code dynamically to analyze data and create charts.
- **File Management Toolkit:** An agent equipped with tools to read, write, and organize files on your local disk.
- **Multi-Modal Report Agent:** A complex graph that coordinates Web Searching (Tavily), RAG (Internal docs), and Image Generation (DALL-E) to compile a full document.
- **TwoAgentDebateWithTools:** A Multi-Agent setup where two agents with different personas or tools argue a point to reach a more nuanced conclusion.

**4. Advanced Control (LangGraph)**

- **Iteration-human-in-the-loop:** Critical for production. The agent pauses before a high-stakes tool call (like sending an email or deleting a file) to wait for human approval.
- **Stateful Iteration:** Using LangGraph, agents can maintain state over dozens of steps, allowing them to loop back and retry if a tool returns an error.

---

### Evaluation

To ensure your RAG pipeline actually works, you need more than just vibes—you need Evaluation. This transition from demo to production involves measuring accuracy, hallucinations, and retrieval quality.

**1. Synthetic Data & Frameworks**

- **Generate Synthetic Test Dataset (with RAGAS):** Manually writing QA pairs is slow. Ragas uses an LLM to digest your documents and automatically generate diverse Question-Context-Answer ground-truth datasets.
- **Evaluation using RAGAS:** The gold standard for RAG. It provides metrics like Faithfulness (is the answer derived from the context?) and Answer Relevance.
- **HF-Upload:** Once you've generated or evaluated a dataset, you can push it to the Hugging Face Hub for versioning and community sharing.

**2. Evaluator Types**

- **LLM-as-Judge:** Using a superior model (like GPT-4o) to grade a smaller model's output based on a rubric.
- **Embedding-based (embedding_distance):** Measures how semantically close a predicted answer is to the reference answer using vector math.
- **Groundedness Evaluation:** A specific check to ensure the LLM only used the provided context and didn't hallucinate external info.
- **Heuristic Evaluation:** Fast, code-based checks (e.g., Does the output contain JSON?, Is it longer than 100 words?).
- **Pairwise Evaluation:** Presenting two different model responses to a Judge LLM and asking: Which one is better for this specific prompt?

**3. LangSmith: The Evaluation Hub**
LangSmith is the primary platform for managing the LLM lifecycle:

- **LangSmith-Dataset:** A centralized place to store your Golden Sets for testing.
- **Custom LLM Evaluation:** Writing your own logic in LangSmith to grade runs based on business-specific KPIs.
- **Repeat & Online Evaluation:**
  - **Repeat:** Running the same test 5+ times to account for LLM variance.
  - **Online:** Evaluating real-world user traces in real-time to catch regressions.
- **Compare Experiments:** A side-by-side UI to see if a new prompt or a new Reranker actually improved your scores.

**4. Alternatives & Monitoring**

- **LangFuse:** A popular open-source alternative to LangSmith for Online Evaluation and tracing, often preferred for self-hosting requirements.

---

### LangGraph

LangGraph is the evolutionary next step for LangChain, moving away from linear chains toward circular, stateful graphs. While chains are great for simple A to B flows, LangGraph is designed for agents that need to loop, self-correct, and maintain a memory of their reasoning process.

**1. Core Features (The Brain of the Graph)**

- **State Management:** LangGraph maintains a shared State object (often a TypedDict or Pydantic model). Every node in the graph can read from and write to this state.
- **Cycles & Loops:** Unlike standard chains, LangGraph allows for edges that loop back to previous steps. This is essential for agents that need to try again if a tool call fails.
- **Checkpoints (Persistence):** LangGraph can automatically save the state after every step. This enables -
  - **Human-in-the-loop interactions** (pausing the agent for approval) and **Time Travel** (reverting to a previous state to debug).
  - **Nodes & Edges:**
    - **Nodes:** Python functions or Runnables that perform work (e.g., Call LLM, Search Web).
    - **Edges:** The logic that determines which node to visit next, often using Conditional Edges based on the LLM's output.

**2. Structures (How you build it)**

- **StateGraph:** The primary class used to define the flow. You add nodes, define the entry point, and map the edges.
- **MessageGraph:** A specialized structure where the state is simply a list of messages. It’s the fastest way to build a chat agent.
- **Compiled Graph:** Once defined, you compile the graph into a Runnable that supports .invoke(), .stream(), and .astream_events().
- **Subgraphs:** For complex enterprise apps, you can embed a graph inside another graph, allowing for modular team development.

**3. Use Cases**

- **Self-Correction (RAG):** If the retrieved documents aren't relevant, the agent can loop back and rewrite the search query instead of giving a bad answer.
- **Multi-Agent Teams:** Assigning different nodes to different experts (e.g., one node for Researcher, one for Writer, and one for Editor) who pass the state between them.
- **Long-Running Tasks:** Because of Persistence, you can build agents that work on a task for days, surviving server restarts or waiting for user feedback via a Human-in-the-loop break.

---

### Core Features of Langgraph

**1. Foundations & Basic Construction**

- **Python Syntax:** LangGraph relies heavily on Type Annotations and Annotated Types (like Annotated[list, add_messages]). The add_messages function is a reducer that tells the graph to append new messages to the history rather than overwriting it.
- **Building an Agent:** You define a state (the schema), add a node for the LLM, and a node for the Tools. You connect them with a Conditional Edge that checks if the LLM wants to call a tool or finish.
- **ToolNode:** LangGraph provides a pre-built ToolNode that automatically executes tool calls and returns the results to the state, saving you from writing boilerplate code.

**2. Control & Human Interaction**

- **Human-in-the-loop:** You can interrupt the graph before a specific node (like a tool that sends an invoice). The graph saves its state, waits for a user to approve/edit, and then resumes.
- **Manual State Update:** While a graph is paused, you can use .update_state() to manually change the history or variables, effectively steering the agent.
- **Asking Humans for Help:** You can create a state key (e.g., user_input_needed) that triggers a branch to a human-input node when the LLM gets stuck.

**3. Advanced Architectures**

- **Parallel Execution:** By creating multiple edges from a single node, you can run nodes in parallel. LangGraph handles the fan-out and fan-in logic automatically.
- **Subgraphs:** You can nest graphs. A Writer subgraph can have its own internal loops for drafting and editing, while appearing as a single node to the Main manager graph.
- **DeleteMessages:** To keep the context window clean, you can use the RemoveMessage tool to explicitly delete old or irrelevant messages from the state.

**4. Persistence & Streaming**

- **Memory (Checkpointers):** By passing a checkpointer (like SqliteSaver) during compilation, your agent gains persistent memory. Even if the server restarts, the conversation thread survives.
- **Streaming Modes:** LangGraph supports multiple streaming modes:
  - **values:** Streams the full state after each step.
  - **updates:** Streams only what changed in the state.
  - **debug:** Streams the internal logic of every transition.
- **Long-Term Memory:** This involves a separate storage layer where the agent can write notes about a user (preferences, past topics) that persist across completely different conversation threads.

---

### Structures of Langgraph

In LangGraph, Structures allow you to move from a Naive RAG (one-way flow) to Agentic RAG, where the system evaluates its own work and corrects errors in real-time.

**1. Evolution of RAG Structures**

- **Naive RAG:** A simple linear path: Retrieve → Augment → Generate. It fails if the retrieved documents are poor or irrelevant.
- **Groundedness Check:** A Self-RAG node that evaluates the LLM's response against the retrieved documents. If the answer isn't grounded in the text, the graph loops back to try again.
- **Query Rewrite:** If the initial retrieval finds nothing, the Query Rewrite node uses an LLM to rephrase the user's question into a more search-friendly version before retrying the vector search.
- **Web Search Module:** An escalation path. If the vector database doesn't have the answer, a conditional edge routes the query to a Web Search Tool (like Tavily) to find fresh information.

**2. Advanced Agentic Patterns**

- **Agentic RAG:** An autonomous agent that decides which tool to use (Vector DB vs. Web Search) and how many documents it needs to satisfy the query.
- **Adaptive RAG:** A sophisticated architecture that first classifies the query complexity. It chooses the fastest path for easy questions and a deep, multi-step Agentic path for complex ones.

**3. Multi-Agent Structures**
When a task is too big for one LLM, you split it into a Multi-Agent graph:

- **Structure 1 (Hand-offs):** Agents pass the state to each other like a relay race (e.g., Researcher → Writer → Editor).
- **Structure 2 (Hierarchical/Supervisor):** A Manager node orchestrates sub-agents. It receives the task, delegates it to a specific expert (e.g., SQL Agent or Search Agent), and reviews the result before sending it to the user.

---

### Use-Cases of Langgraph

**1. Advanced RAG & Reasoning**

- **CRAG (Corrective RAG):** Adds a self-correction layer. It evaluates retrieved documents; if they are irrelevant, it triggers a Web Search to find better data, ensuring the model doesn't hallucinate from poor context.
- **Plan-and-Execute:** The agent first creates a multi-step plan to solve a goal, then executes each step one by one. This prevents the forgetting that happens when an agent tries to do too much in one turn.
- **Tree of Thoughts (ToT):** The graph explores multiple reasoning paths in parallel. It evaluates each branch and abandons the ones that don't lead to a solution, mimicking human brainstorming.
- **Reflection:** A Critic node reviews the agent's work and provides feedback. The agent then loops back to improve the response based on that critique.

**2. Multi-Agent Architectures**

- **Multi-Agent Collaboration:** A network where agents talk to each other as peers (e.g., a Coder and a Reviewer) to complete a task.
- **Supervisor / Hierarchical Teams:** A Manager node receives the user request and delegates tasks to specialized sub-agents. For example, a Research Assistant might have a Web Searcher sub-agent and a Technical Writer sub-agent.
- **SQL-Agent:** A specialized graph that can look at a database schema, write a query, check for errors, and re-try if the SQL is invalid.

**3. Specialized Assistants**

- **LangGraph Code Assistant:** A graph designed to write, test, and debug code. If the code fails a unit test, the graph automatically loops back to the Writer node with the error log.
- **Meta Prompt Generator:** An agent that interviews the user to understand their requirements and then generates a high-quality system prompt for other LLMs.
- **Ollama Deep Researcher:** Uses local models (like Deepseek-R1) to perform deep, multi-step research by browsing and synthesizing information without cloud costs.

**4. Deployment & Infrastructure**

- **Deploy on LangGraph Cloud:** This allows you to host your graphs as scalable APIs. It provides built-in support for checkpointing, multi-user persistence, and a visual dashboard for tracing runs.
- **Functional API:** A simplified way to define graphs using standard Python functions, making it easier to integrate LangGraph into existing codebases.

---

### LangGraph Memory

In LangGraph, conversation memory is managed through a stateful graph architecture that separates short-term (thread-scoped) and long-term (cross-thread) memory.

**1. Short-Term Memory (Thread-Scoped)**
This tracks the ongoing conversation within a single session. It is managed by persisting the agent's State using a Checkpointer.

- **MessagesState:** A built-in schema that uses the add_messages annotation to automatically append new messages to the history instead of overwriting them.
- **Checkpointers:** Components like MemorySaver (in-memory) or SqliteSaver/PostgresSaver (persistent) that snapshot the graph state at every step.
- **Thread ID:** A unique identifier used during invocation (config={configurable: {thread_id: ...}}) to load the correct conversation history for a specific user or session.

**2. Context Window Management**
To prevent long histories from exceeding LLM token limits, LangGraph provides three primary strategies:

- **Message Trimming:** Uses trim_messages to keep only the most recent
  messages or tokens.
- **Summarization:** A dedicated summarize node compresses older messages into a concise summary, which is then passed as context for future turns.
- **Removing Messages:** Using RemoveMessage to explicitly delete specific messages from the state to save space.

**3. Long-Term Memory (Cross-Thread)**
This persists user preferences or facts across different conversations using a Store.

- **Namespaces:** Memories are stored under custom namespaces (e.g., [user_id, preferences]) rather than being tied to a single thread ID.
- **Semantic Search:** Advanced setups use vector-based storage (like Mem0 or Redis) to retrieve relevant past facts via similarity search.
