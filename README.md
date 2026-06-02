# RAG Chatbot using LangGraph, LangChain, FAISS, and Groq

## Overview

This project demonstrates a simple Retrieval-Augmented Generation (RAG) chatbot built using:

* LangGraph for agent workflow orchestration
* LangChain for document processing and tool integration
* FAISS as the vector database
* Hugging Face Embeddings (BAAI/bge-small-en-v1.5)
* Groq LLM (Llama 3.3 70B Versatile)

The chatbot retrieves relevant information from a local text document and answers user questions using the retrieved context.

---

## Architecture

```text
User Query
     │
     ▼
 LangGraph Agent
     │
     ▼
 Tool Calling Decision
     │
     ▼
  RAG Tool
     │
     ▼
 FAISS Vector Store
     │
     ▼
 Retrieved Context
     │
     ▼
 Groq LLM
     │
     ▼
 Final Response
```

---

## Features

* Document ingestion from local text files
* Recursive text chunking
* Hugging Face embeddings
* FAISS vector database
* LangGraph agent workflow
* Tool-calling support
* Context-aware question answering
* Groq Llama 3.3 integration

---

## Tech Stack

| Component     | Technology              |
| ------------- | ----------------------- |
| LLM           | Llama 3.3 70B Versatile |
| Provider      | Groq                    |
| Framework     | LangChain               |
| Orchestration | LangGraph               |
| Embeddings    | BAAI/bge-small-en-v1.5  |
| Vector Store  | FAISS                   |
| Language      | Python                  |

---

## Project Structure

```text
project/
│
├── data.txt
├── main.py
├── .env
├── requirements.txt
└── README.md
```

---

## Installation

### Clone Repository

```bash
git clone <your-repository-url>
cd <repository-name>
```

### Create Virtual Environment

```bash
python -m venv .venv
```

### Activate Environment

Windows:

```bash
.venv\Scripts\activate
```

Linux/Mac:

```bash
source .venv/bin/activate
```

### Install Dependencies

```bash
pip install langchain
pip install langchain-community
pip install langchain-classic
pip install langgraph
pip install langchain-huggingface
pip install sentence-transformers
pip install faiss-cpu
pip install python-dotenv
pip install groq
```

---

## Environment Variables

Create a `.env` file:

```env
GROQ_API_KEY=your_groq_api_key
```

---

## Workflow

### 1. Load Documents

```python
loader = TextLoader("data.txt")
docs = loader.load()
```

### 2. Split Documents

```python
splitter = RecursiveCharacterTextSplitter(
    chunk_size=500,
    chunk_overlap=200
)
```

### 3. Generate Embeddings

```python
embeddings = HuggingFaceEmbeddings(
    model_name="BAAI/bge-small-en-v1.5"
)
```

### 4. Create FAISS Vector Store

```python
vectorStore = FAISS.from_documents(
    chunks,
    embeddings
)
```

### 5. Create Retriever

```python
retriever = vectorStore.as_retriever(
    search_type="similarity",
    search_kwargs={"k":4}
)
```

### 6. Build LangGraph Agent

The graph consists of:

* Chat Node
* Tool Node
* Conditional Tool Routing
* Response Generation

---

## Example Query

```python
initial_state = {
    "messages": [
        HumanMessage(
            content="Say Types of AI only from the uploaded doc"
        )
    ]
}
```

### Example Output

```text
1. Narrow AI (Weak AI)
2. General AI (Strong AI)
3. Super AI
```

---

## How RAG Works

1. User asks a question.
2. Query is sent to the retriever.
3. FAISS searches similar document chunks.
4. Relevant context is returned.
5. Context is supplied to the LLM.
6. LLM generates an answer grounded in retrieved data.

---

## Future Improvements

### Retrieval Improvements

* Hybrid Search (BM25 + Vector Search)
* Reranking using Cross Encoders
* Metadata Filtering
* Multi-query Retrieval
* Parent-Child Retrieval

### Document Support

* PDF Support
* DOCX Support
* Web Page Ingestion
* YouTube Transcript Processing
* CSV and Excel Support

### Agent Enhancements

* Multiple Tools
* Web Search Tool
* Calculator Tool
* Database Query Tool
* Memory Support

### Vector Database Enhancements

* ChromaDB
* Pinecone
* Weaviate
* Milvus
* Qdrant

### User Interface

* Streamlit Chat Interface
* Gradio Interface
* React Frontend
* Authentication System
* Chat History

### Production Features

* Docker Deployment
* FastAPI Backend
* Monitoring with LangSmith
* Caching
* Evaluation Pipeline

### Advanced RAG

* Agentic RAG
* Corrective RAG (CRAG)
* Graph RAG
* Self-RAG
* Adaptive RAG

---

## Learning Outcomes

This project helps understand:

* Retrieval-Augmented Generation (RAG)
* Vector Databases
* Embeddings
* LangChain Tools
* LangGraph Workflows
* Tool Calling
* FAISS Similarity Search
* LLM Integration with Groq

---

## License

This project is open-source and available under the MIT License.
