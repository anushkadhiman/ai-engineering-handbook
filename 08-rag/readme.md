# Retrieval-Augmented Generation (RAG)

A collection of notes and concepts around building **RAG systems** —  
covering retrieval, embeddings, chunking, evaluation, and system design.

---

### What This Section Covers

**Retrieval**

- Sparse vs Dense retrieval
- Hybrid search (keyword + semantic)
- Approximate Nearest Neighbor (ANN) search
- Distance metrics (cosine, L2, etc.)

**Chunking**

- Character-based splitting
- Recursive chunking
- Token-based chunking
- Chunk size vs overlap trade-offs

**Embeddings**

- What embeddings are
- Choosing embedding models
- Dense vs sparse embeddings
- Fine-tuning embeddings

**Vector Databases**

- What is a vector DB
- Indexing and storage
- HNSW and other ANN algorithms
- Query-time retrieval

**Retrieval Optimization**

- Improving recall vs precision
- Hybrid retrieval strategies
- Query rewriting
- Multi-query retrieval

**Re-ranking**

- Why re-ranking is needed
- Bi-encoders vs cross-encoders
- Trade-offs (latency vs quality)

**Evaluation**

- Retrieval metrics (MRR, Recall, Precision)
- End-to-end RAG evaluation
- Common failure cases

**Advanced RAG Concepts**

- GraphRAG
- Multi-step retrieval
- Synthetic dataset generation
- Latency optimization

**Common RAG Architectures**

- Standard RAG
- Fusion RAG
- Corrective RAG
- Agentic RAG
- Modular RAG
- Multimodal RAG

Each architecture is suited for different use cases.

**Where RAG is Used**

- Question answering systems
- Document chat (PDFs, reports, etc.)
- Enterprise knowledge assistants
- Search and recommendation systems
- AI copilots

**Key Challenges**

- Poor retrieval quality
- Wrong chunking strategy
- Irrelevant context injection
- High latency
- Hallucination despite retrieval
