# 📚 Paper Summarizer RAG System

> **Automated document analysis tool using Python and Google Gemini**

This project is a **Retrieval-Augmented Generation (RAG)** system designed to analyze complex academic papers and research PDFs. It uses **Google's Gemini Flash** model to generate accurate, context-aware summaries and answer specific technical queries while minimizing hallucinations.

## 🚀 Features

* **📄 PDF Ingestion**: Upload any research paper or PDF document directly via the UI.
* **🧠 Intelligent Chunking**: Automatically splits documents into manageable 800-character chunks with overlap to preserve context.
* **🔍 Vector Search**: Uses **FAISS (Facebook AI Similarity Search)** and `all-MiniLM-L6-v2` embeddings for high-speed, relevant information retrieval.
* **🤖 Context-Aware Answers**: Integrates **Google Gemini 1.5 Flash** to answer user queries *only* based on the provided text, effectively reducing AI hallucinations.
* **⚡ Interactive UI**: Built with **Streamlit** for a responsive and easy-to-use web interface.

## 🛠️ Tech Stack

* **Language:** Python 3.11+
* **LLM:** Google Gemini (`gemini-flash-latest`)
* **Vector Database:** FAISS (CPU)
* **Embedding Model:** SentenceTransformers (`all-MiniLM-L6-v2`)
* **Framework:** Streamlit
* **PDF Processing:** PyPDF

## ⚙️ Architecture

The system follows a standard RAG pipeline:
1.  **Ingestion**: The PDF is read and text is extracted using `pypdf`.
2.  **Indexing**: Text is split into chunks and converted into vector embeddings. These are stored in a FAISS index.
3.  **Retrieval**: When a user asks a question, the system searches for the top 4 most similar chunks in the document.
4.  **Generation**: The retrieved chunks are sent to Google Gemini with a strict prompt: *"Based ONLY on the following context... answer the user's question."*

## 📦 Installation

1.  **Clone the repository**
    ```bash
    git clone [https://github.com/arpanmukherjee38/rag.git](https://github.com/arpanmukherjee38/rag.git)
    cd rag
    ```

2.  **Install dependencies**
    ```bash
    pip install -r requirements.txt
    ```

3.  **Set up API Keys**
    You need a Google AI Studio API key. Set it as an environment variable:
    
    *On Mac/Linux:*
    ```bash
    export GOOGLE_API_KEY="your_actual_api_key_here"
    ```
    *On Windows (PowerShell):*
    ```powershell
    $env:GOOGLE_API_KEY="your_actual_api_key_here"
    ```

## 🏃‍♂️ Usage

1.  **Run the Streamlit App**
    ```bash
    streamlit run app.py
    ```
2.  **Upload a PDF**: Use the sidebar to upload a research paper.
3.  **Click "Process Paper"**: Wait for the embedding and indexing to finish.
4.  **Ask Questions**: Enter queries like *"What is the main conclusion?"* or *"Explain the methodology."*

## 📂 File Structure

* `app.py`: Main Streamlit application containing the UI and RAG logic.
* `build_index.py`: Standalone script for offline indexing of PDFs.
* `summarize.py`: CLI version of the tool using Ollama (optional).
* `requirements.txt`: List of Python dependencies.

## 🛡️ Hallucination Handling
To ensure accuracy, the prompt engineering includes strict constraints:
> "Based ONLY on the following context from an academic paper, answer the user's question. If the context doesn't contain the answer, say you cannot answer."

This prevents the model from relying on pre-trained knowledge that might be irrelevant to the specific paper being analyzed.

---
*Created by [Arpan Mukherjee](https://github.com/arpanmukherjee38)*
