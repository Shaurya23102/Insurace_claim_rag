

# 🧠 Insurance Claim RAG System

This project implements a **Retrieval-Augmented Generation (RAG)** system for answering queries related to **Insurance Claims** across three categories — **Vehicle**, **Health**, and **Home Insurance**. The system enhances retrieval efficiency and contextual accuracy through a hybrid approach combining **semantic chunking**, **recursive text splitting**, and **dense + sparse retrieval**.

---

## 🚀 Project Overview

The goal of this project is to create a robust RAG pipeline capable of handling diverse insurance-related queries by efficiently retrieving relevant context from the dataset and generating accurate, context-aware responses using an LLM.

### Categories in Dataset

* **Car Insurance**
* **Health Insurance**
* **Home Insurance**

Each category contains documents and textual data describing policies, claims, and conditions.

---

## ⚙️ Technical Details

### 1. **Semantic Chunking**

* **Method:** Semantic Chunking
* **Threshold Type:** `gradient`
* **Threshold Value:** `90`
* Semantic chunking was used to split documents based on semantic coherence rather than raw token counts.
* **Issue:** Some chunks became very large and could exceed the LLM’s context window so later traditinal splitting meathod recursive text spliiter was applied on semantic chunks.

### 2. **Recursive Text Splitting**

* **Purpose:** Handle oversized chunks resulting from semantic chunking.
* **Chunk Size:** `1500` tokens
* This ensures each text segment fits within the model’s input limit while maintaining contextual integrity.

### 3. **Retrieval Strategy**

A **hybrid retrieval mechanism** was implemented for optimal performance:

* **Dense Retrieval:** Embedding-based search for semantic relevance using hugging face pretrained library `sentence-transformers/all-mpnet-base-v2`
* **Sparse Retrieval:** Keyword-based retrieval BM25 for lexical matching.
* **MMR (Maximal Marginal Relevance):** Used to reduce redundancy and improve result diversity during retrieval.

### 4. **Vector Store**

* **Type:** `ChromaDB`
* Used to efficiently store and query document embeddings for dense retrieval.

---

## 🧩 System Architecture

1. **Data Ingestion:** Load insurance-related documents and categorize them (Car, Health, Home).
2. **Preprocessing:** Apply semantic chunking followed by recursive text splitting.
3. **Embedding Generation:** Convert text chunks into embeddings using a pretrained embedding model.
4. **Indexing:** Store embeddings in **ChromaDB**.
5. **Query Processing:**

   * User query embedded using the same model.
   * Dense and sparse retrieval performed.
   * MMR applied for optimized context selection.
6. **RAG Response:** Retrieved context passed to the LLM to generate the final answer.

---

## 🧠 Key Features

* Semantic chunking with adaptive thresholding.
* Recursive splitting for context-limit safety.
* Hybrid dense + sparse retrieval.
* MMR-based redundancy control.
* Efficient vector storage via **ChromaDB**.
* Structured insurance-specific dataset.

---

## 🛠️ Tech Stack

* **Language:** Python
* **Frameworks/Libraries:** LangChain, ChromaDB, Transformers
* **Models:** `'sentence-transformers/all-mpnet-base-v2'`), LLM ( `GROQ`)
* **Retrieval Algorithms:** Dense, Sparse (BM25), MMR

---




