# Document Q&A System with Llama3

A Streamlit-based application that enables users to ask questions about PDF documents using AI-powered document retrieval and question answering.

## Features

- **PDF Document Processing**: Automatically loads and processes PDF files from a specified directory
- **AI-Powered Q&A**: Uses Llama3-8b model via Groq API for intelligent question answering
- **Vector Search**: Implements FAISS vector database for fast document similarity search
- **Source Transparency**: Shows relevant document chunks used to generate answers
- **Session Persistence**: Caches vector embeddings to avoid reprocessing documents

## Technology Stack

- **Frontend**: Streamlit
- **Language Model**: Llama3-8b-8192 (via Groq API)
- **Embeddings**: OpenAI Embeddings
- **Vector Database**: FAISS
- **Document Processing**: LangChain with PyPDF loader
- **PDF Processing**: PyPDF2

## Prerequisites

- Python 3.7+
- OpenAI API key
- Groq API key

## Installation

1. Clone the repository
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Create a `.env` file in the project root with your API keys:
   ```
   OPENAI_API_KEY=your_openai_api_key_here
   GROQ_API_KEY=your_groq_api_key_here
   ```

4. Create a `science_direct` folder in the project directory and place your PDF files there

## Usage

1. Run the Streamlit application:
   ```bash
   streamlit run app.py
   ```

2. Click "Documents Embedding" to process and embed your PDF documents (one-time setup)

3. Enter your question in the text input field

4. View the AI-generated answer based on your documents

5. Expand "Document Similarity Search" to see the relevant document chunks that were used

## How It Works

1. **Document Loading**: Loads PDF files from the `science_direct` directory
2. **Text Splitting**: Breaks documents into 1000-character chunks with 200-character overlap
3. **Vector Embedding**: Converts text chunks to vector embeddings using OpenAI's embedding model
4. **Storage**: Stores embeddings in FAISS vector database for fast retrieval
5. **Query Processing**: When a question is asked, finds the most relevant document chunks
6. **Answer Generation**: Uses Llama3 to generate contextual answers based on retrieved chunks

## Configuration

- **Chunk Size**: 1000 characters
- **Chunk Overlap**: 200 characters  
- **Document Limit**: First 20 documents from the directory
- **Model**: Llama3-8b-8192

## Project Structure

```
├── app.py              # Main Streamlit application
├── requirements.txt    # Python dependencies
├── .env               # API keys (create this file)
└── science_direct/    # Directory for PDF documents (create this folder)
```

## Performance

The application displays response time for each query to help monitor performance. Vector embeddings are cached in the session state to avoid reprocessing documents on subsequent queries.

## Limitations

- Only processes PDF files
- Limited to first 20 documents in the directory
- Requires internet connection for API calls
- Answers are constrained to the provided document context only
