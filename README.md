# RAG Assistant with LangChain & IBM Watsonx

A production-ready Retrieval-Augmented Generation (RAG) assistant that combines the power of LangChain, IBM Watsonx LLMs, and modern vector databases to enable intelligent document-based question answering.

## Features

- **Advanced RAG Pipeline**: Seamlessly retrieve and generate answers from uploaded PDF documents
- **Mistral Mixtral 8x7B LLM**: Leverages IBM Watsonx's powerful open-source language model
- **Vector Embeddings**: IBM Slate embeddings for semantic document understanding
- **Chroma Vector Store**: Efficient in-memory vector storage and retrieval
- **Interactive UI**: Gradio-based web interface for easy document uploads and queries
- **Multi-Region Support**: EU (Frankfurt) and US (South) region endpoints
- **Streaming Responses**: Real-time token streaming for better user experience
- **Source Attribution**: Transparent document references for all generated answers

## Architecture

```
PDF Upload → Document Loading → Text Splitting → Embeddings Generation
                                                         ↓
                                                  Vector Store (Chroma)
                                                         ↓
User Query → Retrieval → Context Building → LLM Processing → Response
```

## Prerequisites

- Python 3.9 or higher
- IBM Watsonx API Key
- IBM Watsonx Project ID
- pip or conda package manager

## How To Run

### 1. Clone the Repository
```bash
git clone <your-repo-url>
cd "Ai RAG assistant using LangChain"
```

### 2. Create Virtual Environment
```bash
python -m venv venv

# Windows
.\venv\Scripts\Activate.ps1

# macOS/Linux
source venv/bin/activate
```

### 3. Install Dependencies
```bash
cd Backend
pip install -r requirements.txt
```

### 4. Configure Credentials
Update `Backend/rag_assistant.py` with your IBM Watsonx credentials:

```python
IBM_API_KEY = "your_ibm_api_key"
PROJECT_ID = "your_project_id"
WATSONX_URL = "https://eu-de.ml.cloud.ibm.com"  # or us-south
```

Alternatively, set environment variables:
```bash
$env:IBM_API_KEY = "your_api_key"
$env:PROJECT_ID = "your_project_id"
```

### 5. Run the Application
```bash
python rag_assistant.py
```

The web interface will launch at `http://localhost:7860`

## Usage

1. **Upload Document**: Click "Upload PDF File" and select a PDF file
2. **Ask Questions**: Type your question in the query field
3. **Get Answers**: The assistant retrieves relevant context and generates an answer
4. **View Sources**: See which document sections were used for the answer

### Example Queries
- "What is the main topic of this document?"
- "Summarize the key findings."
- "Explain the methodology used."
- "List all important dates mentioned."

## Configuration

### Model Parameters
The LLM is configured with the following parameters:
- **Model**: Mistral Mixtral 8x7B Instruct
- **Max Tokens**: 500
- **Temperature**: 0.5
- **Top P**: 0.95
- **Decoding Method**: Greedy

Modify these in the `get_llm()` function for different behaviors.

### Vector Store Settings
- **Embeddings**: IBM Slate 30M English
- **Storage**: Chromadb (persistent on disk)
- **Chunk Size**: 500 characters
- **Chunk Overlap**: 100 characters
- **Retrieval**: Top 3 most relevant documents

## Project Structure

```
Backend/
├── rag_assistant.py          # Main application
├── requirements.txt           # Python dependencies
└── chroma_db/                # Vector store storage

Frontend/
└── (Gradio UI - embedded in rag_assistant.py)
```

## Technologies Used

| Component | Technology |
|-----------|-----------|
| LLM Framework | LangChain 0.1+ |
| Language Model | Mistral Mixtral 8x7B (IBM Watsonx) |
| Embeddings | IBM Slate 30M English RTL |
| Vector Store | Chromadb |
| Document Loader | LangChain PyPDFLoader |
| Web Interface | Gradio |
| API Client | IBM Watsonx AI SDK |

## Key Components

### Document Loader
Extracts text from PDF files with automatic page splitting and metadata preservation. Uses PyPDFLoader for reliable PDF processing.

### Text Splitter
Splits documents into manageable chunks using RecursiveCharacterTextSplitter to optimize retrieval performance while maintaining semantic coherence.

### Embeddings
Converts text chunks into high-dimensional vectors using IBM Slate 30M embeddings for efficient semantic similarity matching.

### Retriever
Performs similarity search on the vector store to identify the most relevant document chunks for a given query.

### LLM Chain
Combines retrieved context with user queries using ChatPromptTemplate and create_retrieval_chain for accurate, context-aware response generation.

## Region Configuration

### EU Region (Frankfurt)
```python
WATSONX_URL = "https://eu-de.ml.cloud.ibm.com"
```

### API Key Issues
- Verify API key format starts with `cpd-apikey-`
- Ensure Project ID matches your Watsonx workspace
- Confirm that region URL matches your API key's region
- Check that API key has not expired

### Memory Issues with Large PDFs
- Reduce chunk_size in text_splitter() function
- Implement batch processing for multiple documents
- Use persistent Chroma storage instead of in-memory
- Increase available system memory

### Connection Timeouts
- Verify stable internet connectivity
- Check IBM Watsonx service status
- Adjust timeout settings in Credentials configuration
- Review firewall and proxy settings

## Performance Optimization

- **Batch Processing**: Process multiple documents concurrently to improve throughput
- **Query Caching**: Implement caching for frequently asked questions
- **Index Optimization**: Use persistent vector store for repeated usage to avoid re-embedding
- **Model Tuning**: Adjust temperature and token limits based on your specific use case
- **Chunk Optimization**: Fine-tune chunk size and overlap for your document type

## Security Best Practices

IMPORTANT: Never commit API keys to version control

### Use Environment Variables
Create a `.env` file (add to `.gitignore`):
```
IBM_API_KEY=your_api_key_here
PROJECT_ID=your_project_id_here
```

### Load from Environment
```python
IBM_API_KEY = os.getenv("IBM_API_KEY")
PROJECT_ID = os.getenv("PROJECT_ID")
```


## Acknowledgments

- IBM Watsonx AI for providing powerful LLM and embedding models
- LangChain for the flexible and comprehensive RAG framework
- Mistral AI for developing the Mixtral model
- Chroma for efficient vector storage capabilities
- Gradio for the intuitive web interface framework

## Useful Resources

- LangChain Documentation: https://docs.langchain.com
- IBM Watsonx AI: https://www.ibm.com/products/watsonx-ai
- Gradio Documentation: https://gradio.app
- Chroma Documentation: https://docs.trychroma.com
- Mistral AI: https://mistral.ai

## Roadmap

Future enhancements:
- Support for multiple document formats (DOCX, TXT, CSV)
- Batch document processing
- Advanced query refinement and re-ranking
- Integration with additional vector databases
- Fine-tuning capabilities for custom models
- API endpoint for programmatic access
- Multi-language support
