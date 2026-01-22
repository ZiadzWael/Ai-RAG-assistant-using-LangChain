
# RAG Assistant with LangChain & IBM Watsonx

A **Retrieval-Augmented Generation (RAG) Assistant** that integrates **LangChain**, **IBM Watsonx**, and vector databases for efficient document-based question answering.

## Features

- **Retrieval-Augmented Generation**: Answer questions based on uploaded PDFs.
- **Mistral Mixtral 8x7B LLM**: IBM Watsonx's open-source language model.
- **Vector Embeddings**: IBM Slate embeddings for semantic understanding.
- **Chroma Vector Store**: Efficient in-memory vector storage.
- **Gradio UI**: Easy-to-use web interface for document uploads and queries.

## Architecture

```
PDF Upload → Document Loading → Text Splitting → Embeddings Generation
                                                         ↓
                                                  Vector Store (Chroma)
                                                         ↓
User Query → Retrieval → Context Building → LLM Processing → Response
```

## Prerequisites

- Python 3.9+
- IBM Watsonx API Key & Project ID
- pip or conda

## How To Run

1. **Clone the Repo**  
   ```bash
   git clone https://github.com/YourUsername/Ai-RAG-assistant-using-LangChain.git
   cd Ai-RAG-assistant-using-LangChain
   ```

2. **Set up Virtual Environment**  
   ```bash
   python -m venv venv
   .env\Scripts\Activate.ps1   # Windows
   source venv/bin/activate      # macOS/Linux
   ```

3. **Install Dependencies**  
   ```bash
   cd Backend
   pip install -r requirements.txt
   ```

4. **Configure IBM Watsonx Credentials**  
   Update `Backend/rag_assistant.py` with your IBM Watsonx credentials:
   ```python
   IBM_API_KEY = "your_api_key"
   PROJECT_ID = "your_project_id"
   WATSONX_URL = "https://eu-de.ml.cloud.ibm.com"
   ```

5. **Run the App**  
   ```bash
   python rag_assistant.py
   ```
   Open `http://localhost:7860` in your browser.

## Usage

- **Upload PDF**: Click "Upload PDF File" and select a file.
- **Ask a Question**: Type your question in the textbox.
- **View Answer**: The assistant returns the most relevant answer from the document.

### Example Queries

- "What is the main topic?"
- "Summarize the findings."
- "Explain the methodology."

## Configuration

### LLM Parameters
- **Model**: Mistral Mixtral 8x7B
- **Max Tokens**: 500
- **Temperature**: 0.5

### Vector Store
- **Embeddings**: IBM Slate 30M
- **Storage**: Chroma (on-disk)
- **Chunk Size**: 500 tokens

## Project Structure

```
Backend/
├── rag_assistant.py
├── requirements.txt
└── chroma_db/

Frontend/
└── (Embedded Gradio UI)
```

## Technologies Used

- **LLM**: IBM Watsonx (Mistral Mixtral 8x7B)
- **Embeddings**: IBM Slate 30M
- **Vector Store**: Chroma
- **Document Loader**: LangChain (PyPDFLoader)
- **UI**: Gradio

## Key Components

- **Document Loader**: Extracts text from PDFs.
- **Text Splitter**: Splits documents into smaller chunks.
- **Embeddings**: Converts text into vectors for semantic similarity.
- **Retriever**: Searches the vector store for relevant content.
- **LLM Chain**: Combines context with queries for answers.

## Region Configuration

### EU Region (Frankfurt)
```python
WATSONX_URL = "https://eu-de.ml.cloud.ibm.com"
```

### US Region (South)
```python
WATSONX_URL = "https://us-south.ml.cloud.ibm.com"
```

## Common Issues

- **API Key Issues**: Ensure the API key format is correct.
- **Large PDFs**: Reduce chunk size, or use persistent storage for Chroma.
- **Timeouts**: Check internet connectivity and IBM Watsonx service status.

## Performance Tips

- **Batch Processing**: Use concurrency for multiple documents.
- **Caching**: Cache frequent queries.
- **Indexing**: Use persistent storage for vector data.
- **Tuning**: Adjust model parameters like temperature.

## Security

- **Environment Variables**: Store API keys securely and load them with `os.getenv()`.
- **.env File**: Add to `.gitignore`:
   ```
   IBM_API_KEY=your_api_key
   PROJECT_ID=your_project_id
   ```

## Acknowledgments

- IBM Watsonx AI
- LangChain
- Gradio
- Chroma
- Mistral AI

## Resources

- LangChain Docs: [https://docs.langchain.com](https://docs.langchain.com)
- IBM Watsonx: [https://www.ibm.com/products/watsonx-ai](https://www.ibm.com/products/watsonx-ai)
- Gradio: [https://gradio.app](https://gradio.app)
- Chroma: [https://docs.trychroma.com](https://docs.trychroma.com)
- Mistral AI: [https://mistral.ai](https://mistral.ai)

## Future Enhancements

- Support for more document formats (DOCX, TXT)
- Batch processing improvements
- Advanced query handling
- Integration with other vector databases
