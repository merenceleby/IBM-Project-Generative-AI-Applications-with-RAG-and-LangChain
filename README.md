# IBM-Project-Generative-AI-Applications-with-RAG-and-LangChain

A production-style **Retrieval-Augmented Generation (RAG)** application that turns any uploaded PDF into a **queryable knowledge base** using **LangChain**, **IBM watsonx**, **ChromaDB**, and a **Gradio** UI.

This project was built as the capstone of the *Generative AI Applications with RAG and LangChain* course and demonstrates end-to-end skills in **LLM orchestration**, **vector search**, and **practical GenAI application design**.



## 🚀 What This Project Does

- Lets a user **upload a PDF document**.
- Splits the document into **semantic chunks**.
- Creates dense **vector embeddings** using an IBM watsonx embedding model.
- Stores vectors in an in-memory **Chroma** vector database.
- Uses **LangChain’s RetrievalQA** chain with an IBM **Granite 3.2 8B Instruct** model to:
  - Retrieve the most relevant chunks.
  - Generate grounded, context-aware answers to user questions.
- Exposes everything through a clean **Gradio web interface**.

In short:  
> “Ask questions about your own documents, powered by RAG, with all orchestration done in code.”




## 🏗️ Architecture Overview

**High-level RAG pipeline:**

1. **Upload PDF** via Gradio.
2. **Load document** with `PyPDFLoader`.
3. **Chunk text** using `RecursiveCharacterTextSplitter`  
   - `chunk_size=1000`, `chunk_overlap=20`
4. **Embed chunks** with IBM watsonx embedding model.
5. **Store vectors** in **Chroma** (`Chroma.from_documents(...)`).
6. **Convert DB to retriever** (`vectordb.as_retriever()`).
7. **Build RetrievalQA chain** with:
   - `llm = WatsonxLLM(...)` using Granite
   - `retriever = vectordb.as_retriever()`
8. **Answer user query** grounded on retrieved chunks.

You can find all of this implemented in a single, readable script (`app.py`).



## 🧰 Tech Stack

- **Language & Frameworks**
  - Python
  - LangChain
  - Gradio

- **LLM & Embeddings (IBM watsonx)**
  - `ibm/granite-3-2-8b-instruct` (generation model)
  - `ibm/slate-125m-english-rtrvr-v2` (retriever/embedding model)
  - `ibm-watsonx-ai` SDK
  - `langchain-ibm` integration layer

- **Vector Store & Document Handling**
  - **ChromaDB** as vector store
  - `PyPDFLoader` (LangChain community)
  - `RecursiveCharacterTextSplitter`


### Note: 
This code is tested inside the IBM watsonx Lab environment.  
If you run it locally, make sure to configure your watsonx credentials (API key, project_id, and model access).  
Without valid credentials, the LLM and embedding models will not initialize.

## 📸 Screenshot:
<img width="1585" height="535" alt="QA Bot screenshot" src="https://github.com/user-attachments/assets/cfc52599-c67c-438a-9855-bb0a6587567b" />


