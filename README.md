# 📚 Local PDF RAG Assistant

A Python-based **Retrieval-Augmented Generation (RAG)** application that lets users ask questions about PDF documents and receive AI-generated answers grounded in relevant document content.

The application uses **Streamlit** for the user interface, **ChromaDB** for vector storage and similarity search, **Sentence Transformers** for text embeddings, and **Ollama with Qwen3 4B** for local answer generation.

## ✨ Features

- 📄 **PDF Upload:** Upload a PDF document through a simple web interface.
- ✂️ **Text Chunking:** Divide extracted document text into smaller chunks for retrieval.
- 🧠 **Semantic Embeddings:** Convert document chunks and questions into numerical vector representations.
- 🔎 **Vector Search:** Retrieve relevant document sections using ChromaDB.
- 🤖 **Local AI Generation:** Generate answers using Qwen3 4B through Ollama.
- 📖 **Source Inspection:** View retrieved text chunks to understand which document content was used.
- 🔒 **Local Processing:** Run the application on your computer without sending prompts to a hosted LLM API.

> **Note:** Local processing depends on your machine and software configuration. The embedding model may download from an external model repository on its first run.

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| Streamlit | Interactive web interface |
| PyMuPDF | PDF text extraction |
| Sentence Transformers | Generate text embeddings |
| ChromaDB | Vector storage and similarity search |
| Ollama | Run the local language model |
| Qwen3 4B | Generate natural-language answers |
| Requests | Communicate with the Ollama API |
| uv | Python dependency and environment management |

## ⚙️ Prerequisites

Before running the project, install:

- Python 3.11 or later
- [Ollama](https://ollama.com/)
- [uv](https://docs.astral.sh/uv/getting-started/installation/)

Make sure your system has sufficient RAM and disk space to run the language model and embedding model.

## 🚀 Installation and Setup

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd RAG
```

Replace `<YOUR_GITHUB_REPOSITORY_URL>` with your actual GitHub repository URL.

### 2. Install project dependencies

If the repository contains `pyproject.toml` and `uv.lock`, run:

```bash
uv sync
```

This creates or updates the project environment and installs the declared dependencies.

### 3. Download the Ollama model

```bash
ollama pull qwen3:4b
```

Verify that it is installed:

```bash
ollama list
```

### 4. Start Ollama

On Windows, Ollama may already be running in the background. Otherwise, start the Ollama application or run:

```bash
ollama serve
```

Keep the Ollama service running while using the application.

### 5. Run the application

From the project directory, execute:

```bash
uv run streamlit run app.py
```

Open the local URL displayed in your terminal, usually:

```text
http://localhost:8501
```

## 💬 How to Use

1. Open the application in your browser.
2. Upload a text-based PDF document.
3. Click **Index PDF** to extract, chunk, embed, and store the document content.
4. Enter a question related to the document.
5. Click **Get Answer**.
6. Read the generated response and expand **View retrieved sources** to inspect the retrieved text.

For best results, begin with questions whose answers are clearly present in the uploaded document.

## 🧩 How RAG Works

The application follows this workflow:

1. **Document ingestion:** Extract text from the PDF.
2. **Chunking:** Split the text into smaller, overlapping sections.
3. **Embedding:** Convert each chunk into a vector representation.
4. **Indexing:** Store vectors and their associated text in ChromaDB.
5. **Retrieval:** Convert a user question into an embedding and retrieve similar chunks.
6. **Generation:** Send the question and retrieved context to Qwen3 through Ollama.
7. **Response:** Display the generated answer and retrieved source text.

RAG provides relevant external context to a language model at query time. It does not require retraining the model on the uploaded document.

## 📁 Project Structure

```text
RAG/
├── app.py
├── pyproject.toml
├── uv.lock
└── chroma_db/       # Generated local vector database
```

The `chroma_db/` directory is created when the application stores indexed documents. It may be regenerated locally and should not be committed unless you intentionally want to distribute the index.

## ⚠️ Current Limitations

- The current implementation indexes one PDF at a time and replaces the existing document collection when a new PDF is indexed.
- Scanned PDFs without an extractable text layer require OCR.
- Answer quality depends on the document text, chunking strategy, embedding model, and retrieval relevance.
- The application displays retrieved text chunks, but does not yet provide precise page-number citations.
- The model and embedding downloads may require an internet connection the first time they are used.
- Performance depends on the computer's available memory and processing power.

## 🔮 Future Improvements

- Support multiple PDFs in a single knowledge base.
- Add page-level source citations.
- Improve retrieval with hybrid search and reranking.
- Add conversation history and document management.
- Evaluate retrieval accuracy and answer faithfulness.
- Add OCR support for scanned documents.
- Deploy a web version with secure document handling and user authentication.

## 🎯 Learning Outcomes

This project demonstrates practical use of:

- Retrieval-Augmented Generation (RAG)
- Large Language Models (LLMs)
- Text embeddings and semantic search
- Vector databases
- PDF processing
- Local AI inference
- Python application development

## 👨‍💻 Author

**Darshil Jaiswal**

Computer Science Engineering — Artificial Intelligence and Machine Learning

GitHub: [darshiljaiswal2-afk](https://github.com/darshiljaiswal2-afk)

---

If you find this project useful, consider giving the repository a ⭐ on GitHub.
