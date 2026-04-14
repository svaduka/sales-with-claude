# Retrieval-Augmented Generation (RAG)

## Overview
RAG is the core technology for LOT A (Enterprise AI/RAG Control Plane). Current capability gap is HIGH - GenAI experience exists but no RAG architecture background mentioned.

**Why Learn:** LOT A is foundational for all LOTs B; without RAG expertise, cannot architect the Control Plane that all use cases depend on.

---

## Topics

### Topic 1: RAG Fundamentals & Architecture
**Why Learn:** Must understand how RAG works to design enterprise Control Plane

**Learning Objectives:**
- Understand RAG vs. fine-tuning vs. prompt engineering
- Learn RAG components: document ingestion, chunking, embedding, vector DB, retrieval, generation
- Master RAG evaluation metrics (faithfulness, answer relevance, context relevance)
- Understand when to use RAG vs. other approaches

**Resources:**
- **Course:** "Building RAG Applications" (LangChain Academy)
- **Paper:** "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks" (Lewis et al.)
- **Tutorial:** LangChain RAG tutorials
- **Video:** "RAG from Scratch" series (Greg Kamradt)

**Practice/Labs:**
- Build simple RAG system with LangChain + OpenAI + Pinecone
- Ingest 100 insurance policy documents
- Query system with underwriting questions
- Measure retrieval accuracy

**Time Estimate:** 32 hours (1 week)

**Priority:** **CRITICAL**

---

### Topic 2: Vector Databases & Embeddings
**Why Learn:** Must select vector DB for enterprise RAG Control Plane; core infrastructure decision

**Learning Objectives:**
- Compare vector DBs: Pinecone, Weaviate, Milvus, Qdrant, Chroma, pgvector
- Understand embedding models: OpenAI, Cohere, Sentence Transformers, multilingual models
- Learn vector similarity search (cosine, euclidean, dot product)
- Master indexing strategies (HNSW, IVF, etc.)

**Resources:**
- **Documentation:** Pinecone, Weaviate, Qdrant docs
- **Course:** "Vector Databases" (Weaviate Academy)
- **Benchmark:** VectorDB Bench comparison
- **Library:** sentence-transformers for embeddings

**Practice/Labs:**
- Set up trial accounts: Pinecone, Weaviate, Qdrant
- Ingest same 1,000 documents into each
- Compare query performance (latency, accuracy)
- Test multilingual embeddings for Greek and English
- Benchmark cost per query/storage

**Time Estimate:** 24 hours

**Priority:** **CRITICAL**

---

### Topic 3: RAG for Multi-Lingual Content (Greek + English)
**Why Learn:** Insurance documents are mix of Greek and English; RAG must handle both seamlessly

**Learning Objectives:**
- Learn multilingual embedding models (mE5, multilingual-e5, paraphrase-multilingual)
- Understand cross-lingual retrieval challenges
- Master language detection and routing
- Learn translation strategies (translate query, translate docs, or bilingual embeddings)

**Resources:**
- **Model:** multilingual-e5 embeddings (Hugging Face)
- **Paper:** "Multilingual Retrieval-Augmented Generation"
- **Library:** langdetect for language detection
- **Tool:** DeepL API for high-quality Greek-English translation

**Practice/Labs:**
- Build RAG system with Greek and English documents
- Test query in Greek, retrieve Greek + English docs
- Compare retrieval accuracy with monolingual vs. multilingual embeddings
- Implement language-aware retrieval weighting

**Time Estimate:** 20 hours

**Priority:** **HIGH**

---

### Topic 4: Document Chunking Strategies
**Why Learn:** Chunking strategy affects retrieval quality and context window utilization; critical design decision

**Learning Objectives:**
- Learn chunking approaches: fixed-size, semantic, recursive, document-structure-aware
- Understand chunk size trade-offs (256, 512, 1024 tokens)
- Master overlap strategies to avoid context loss
- Learn metadata preservation during chunking

**Resources:**
- **Article:** "Chunking Strategies for RAG" (LlamaIndex blog)
- **Library:** LangChain text splitters
- **Tool:** LlamaIndex chunking utilities
- **Experiment:** Chunking strategy comparison

**Practice/Labs:**
- Chunk 68-page technical document 4 different ways
- Compare retrieval quality across strategies
- Test with multi-page insurance contracts
- Optimize chunk size for Greek text (different from English)

**Time Estimate:** 16 hours

**Priority:** **HIGH**

---

### Topic 5: RAG Retrieval Optimization & Re-ranking
**Why Learn:** Must achieve high retrieval accuracy for enterprise use; poor retrieval = poor answers

**Learning Objectives:**
- Learn retrieval strategies: dense, sparse, hybrid
- Master re-ranking with cross-encoders
- Understand query expansion and hypothetical document embeddings
- Learn MMR (maximal marginal relevance) for diversity

**Resources:**
- **Model:** Cross-encoder re-rankers (ms-marco models)
- **Library:** Cohere re-rank API
- **Pattern:** Hybrid search (vector + keyword)
- **Tutorial:** "Advanced RAG Retrieval Techniques"

**Practice/Labs:**
- Implement hybrid search (vector + BM25)
- Add cross-encoder re-ranking step
- Compare retrieval accuracy with/without re-ranking
- Test on ambiguous insurance queries

**Time Estimate:** 20 hours

**Priority:** **HIGH**

---

### Topic 6: RAG with Citations & Source Tracking
**Why Learn:** EU AI Act requires explainability; must track which documents informed each answer

**Learning Objectives:**
- Learn source attribution in RAG responses
- Master metadata tracking through pipeline
- Understand citation formatting
- Learn audit trail design for compliance

**Resources:**
- **Pattern:** LangChain retrieval with source documents
- **Feature:** LlamaIndex citation nodes
- **Design:** Audit trail database schema
- **Compliance:** EU AI Act explainability requirements

**Practice/Labs:**
- Build RAG system that returns answer + source documents
- Add citation links in generated text
- Store retrieval decisions in audit log
- Create citation report for compliance review

**Time Estimate:** 12 hours

**Priority:** **HIGH**

---

### Topic 7: RAG Evaluation & Monitoring
**Why Learn:** Must demonstrate RAG quality in proposal; need metrics for success criteria

**Learning Objectives:**
- Learn RAG evaluation frameworks: RAGAS, LlamaIndex evaluation
- Understand metrics: context relevance, faithfulness, answer relevance, correctness
- Master human evaluation design
- Learn monitoring and alerting for production RAG

**Resources:**
- **Framework:** RAGAS (RAG Assessment)
- **Tool:** LangSmith for RAG tracing
- **Library:** Phoenix for RAG observability
- **Methodology:** Human evaluation rubrics

**Practice/Labs:**
- Evaluate RAG system with RAGAS metrics
- Create ground truth Q&A dataset (50 insurance questions)
- Measure precision@k and recall@k
- Build monitoring dashboard with alerting

**Time Estimate:** 20 hours

**Priority:** **MEDIUM**

---

### Topic 8: Enterprise RAG Architecture & Governance
**Why Learn:** LOT A Control Plane must support multi-vendor ecosystem with governance

**Learning Objectives:**
- Design enterprise RAG architecture: ingestion, indexing, query, monitoring layers
- Learn RAG governance: access controls, usage limits, cost controls
- Master multi-tenancy patterns (if needed)
- Understand API design for RAG service

**Resources:**
- **Reference:** Enterprise RAG architecture patterns
- **Design:** API gateway for RAG services
- **Tool:** Kong/Apigee for API management
- **Pattern:** RBAC for document-level access control

**Practice/Labs:**
- Design enterprise RAG architecture diagram
- Build RESTful API for RAG queries
- Implement user authentication and authorization
- Add usage metering and cost tracking

**Time Estimate:** 24 hours

**Priority:** **HIGH**

---

### Topic 9: RAG Performance & Scalability
**Why Learn:** Must handle queries from 200+ users, 11K+ queries/day (from RFP context)

**Learning Objectives:**
- Learn RAG performance bottlenecks: embedding generation, vector search, LLM inference
- Master caching strategies (query cache, embedding cache)
- Understand load balancing and rate limiting
- Learn cost optimization techniques

**Resources:**
- **Pattern:** Semantic caching for RAG
- **Tool:** Redis for query caching
- **Strategy:** Embedding cache to reduce costs
- **Monitoring:** Latency and throughput metrics

**Practice/Labs:**
- Benchmark RAG query latency end-to-end
- Implement semantic query caching
- Load test with 100 concurrent queries
- Optimize for cost (reduce LLM calls)

**Time Estimate:** 20 hours

**Priority:** **MEDIUM**

---

### Topic 10: RAG Security & Compliance
**Why Learn:** GDPR, EU AI Act, DORA compliance required; RAG must be secure and auditable

**Learning Objectives:**
- Learn data privacy in RAG (PII handling, data residency)
- Master access control at document/chunk level
- Understand prompt injection attacks and defenses
- Learn compliance documentation for RAG systems

**Resources:**
- **Guide:** GDPR compliance for RAG systems
- **Pattern:** Row-level security in vector DBs
- **Defense:** Prompt injection mitigation techniques
- **Framework:** EU AI Act compliance checklist

**Practice/Labs:**
- Implement document-level access control in RAG
- Test prompt injection attacks and defenses
- Build PII redaction layer before embedding
- Create compliance documentation template

**Time Estimate:** 16 hours

**Priority:** **MEDIUM**

---

## Learning Path Sequence

**Week 1:** Topics 1 & 2 (RAG Fundamentals + Vector DBs)
**Week 2:** Topics 3 & 4 (Multilingual + Chunking)
**Week 3:** Topics 5 & 6 (Retrieval Optimization + Citations)
**Week 4:** Topics 7 & 8 (Evaluation + Enterprise Architecture)
**Week 5:** Topics 9 & 10 (Performance + Security)

**Total Time Estimate:** 204 hours (~5 weeks full-time or 10 weeks part-time)

---

## Key Tools & Frameworks to Master

| Tool/Framework | Purpose | Priority |
|----------------|---------|----------|
| **LangChain** | RAG orchestration, chains, agents | CRITICAL |
| **LlamaIndex** | Data ingestion, indexing, querying | CRITICAL |
| **Pinecone / Weaviate / Qdrant** | Vector database (choose 1-2) | CRITICAL |
| **OpenAI / Anthropic APIs** | LLM for generation | CRITICAL |
| **Sentence Transformers** | Open-source embeddings | HIGH |
| **Cohere** | Re-ranking and embeddings | MEDIUM |
| **RAGAS** | RAG evaluation framework | HIGH |
| **LangSmith** | RAG tracing and debugging | MEDIUM |

---

## Success Criteria

- ✅ Can explain RAG architecture and design enterprise Control Plane
- ✅ Can compare 3+ vector databases with pros/cons for enterprise use
- ✅ Can build working RAG system with Greek + English documents
- ✅ Can demonstrate RAG with citations and source tracking
- ✅ Can evaluate RAG quality with quantitative metrics (RAGAS)
- ✅ Can design RAG governance model for multi-vendor ecosystem
- ✅ Can answer technical questions about RAG scalability and compliance
- ✅ Can estimate RAG infrastructure costs for proposal

---

## Integration with IDP

RAG and IDP work together:
1. **IDP** extracts structured data and text from documents
2. **RAG** indexes the extracted content for retrieval and Q&A
3. **Control Plane (LOT A)** orchestrates both IDP and RAG for all use cases

Learn both in parallel for maximum effectiveness.
