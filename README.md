# RAG System with Qdrant and Ollama
A Retrieval-Augmented Generation (RAG) system built with LlamaIndex that allows you to query PDF documents using natural language. The system uses Qdrant as a vector database, Ollama for language generation, and HuggingFace embeddings for document processing.

## Features

- **PDF Document Processing**: Automatically loads and chunks PDF documents
- **Vector Search**: Uses BGE embeddings and Qdrant for semantic search
- **Cross-encoder Reranking**: Improves retrieval quality with sentence transformers
- **Local LLM**: Powered by Ollama (Llama 3.1:8b)
- **Interactive Queries**: Jupyter notebook interface for easy experimentation

## Setup

1. **Clone the Repository**:
   ```bash
   pip install -r requirements.txt
     ```

2. Configure environment: Copy .env.example to .env and fill in your configuration:

   ```bash
   cp .env.example .env
   ```
   ```env
   QDRANT_URL = "your-qdrant-instance-url"
   QDRANT_API = "your-qdrant-api-key"
   OLLAMA_URL = "your-ollama-instance-url"

3. Add your documents: Place your PDF files in the docs/ directory

4. Run the system: Open and execute the cells in index.ipynb

## Usage

After running the setup cells, you can query your documents using the answer() function:

```python
response = answer("What is the main topic of the document?")
print(response)
```

## Architecture
- Document Loading: Uses SimpleDirectoryReader to load PDFs from the docs folder
- Text Splitting: SentenceSplitter creates 150-token chunks with 40-token overlap
- Embeddings: BGE-large-en model with fallback to bge-base-en-v1.5
- Vector Store: Qdrant with cosine similarity
- Retrieval: Top-30 similarity search followed by cross-encoder reranking (top-12)
- Generation: Ollama Llama 3.1:8b with custom prompt template

## Configuration
Key parameters you can adjust:

- `chunk_size`: Size of text chunks (default: 150)
- `chunk_overlap`: Overlap between chunks (default: 40)
- `similarity_top_k`: Number of candidates to retrieve (default: 30)
- `reranker_top_n`: Final number of chunks to use (default: 12)

## Requirements

- Python 3.11+
- Qdrant instance (local or cloud)
- Ollama with Llama 3.1:8b model or any other
- GPU recommended for embeddings
