
# Gradio Docling + LangChain + RAG Implementation

This project demonstrates how to implement **Retrieval-Augmented Generation (RAG)** using **Gradio**, **LangChain**, **Docling**, **Milvus**, and **HuggingFace**. The system supports multiple file types, including **PDF, Images, HTML, and PPTX**, for document conversion, chunking, and question answering.

---

## Features
1. **File Formats Supported**:
   - **PDF**: Text extracted using the `PyPdfiumDocumentBackend`.
   - **Images**: OCR can be implemented if actual text extraction is desired.
   - **HTML**: Direct parsing of HTML content.
   - **PPTX**: PowerPoint files processed for extracting slide content.
   - **Other formats under testing**:
     - `.txt`, `.md`, `.asciidoc`
   - **Not supported**: `.docx` (Word), `.xlsx` (Excel).

2. **Chunking**:
   - Utilizes LangChain's `RecursiveCharacterTextSplitter` for splitting documents into manageable chunks.
   - Configurable `chunk_size` and `chunk_overlap` for optimal performance.

3. **RAG Workflow**:
   - Extracts text from uploaded files using `Docling`.
   - Splits documents into chunks for embedding and retrieval.
   - Uses **Milvus** as a vector store for embedding-based retrieval.
   - Employs HuggingFace LLMs (e.g., Mistral-7B-Instruct) for answering user queries based on the retrieved context.

4. **Gradio Interface**:
   - **Upload & Split**: Allows users to upload files and split them into chunks.
   - **RAG Q&A**: Enables users to ask questions based on the uploaded content.

---

## Requirements
Install the following dependencies to run the project:
```bash
pip install docling docling-core python-dotenv langchain-text-splitters langchain-huggingface langchain-milvus gradio
```

---

## Architecture
1. **Document Conversion**:
   - The `DocumentConverter` from Docling automatically detects file formats and converts them into a unified text representation.
   - Extracted text is exported in Markdown format for consistency.

2. **Embedding and Retrieval**:
   - Documents are embedded using the `sentence-transformers/all-MiniLM-L6-v2` model.
   - Embeddings are stored in a temporary **Milvus** vector database for fast retrieval.

3. **RAG Chain**:
   - Retrieved context is formatted into a prompt using LangChain's `PromptTemplate`.
   - HuggingFace's endpoint is used to query LLMs like `Mistral-7B-Instruct`.

---

## Usage
### 1. Run the Application
Run the following command to launch the Gradio app:
```bash
python gradio_docling_RAG_langchain.py
```

### 2. Upload and Split Documents
- Navigate to the **Upload & Split** tab.
- Upload supported file types (PDF, Images, HTML, PPTX).
- Click "Split Documents" to chunk the uploaded files.

### 3. Ask Questions
- Go to the **RAG Q&A** tab.
- Input a question related to the uploaded documents.
- Click "Ask" to get an answer based on the document content.

---

## File Handling
### Supported Formats
| File Type | Handling Mechanism              | Notes                                |
|-----------|---------------------------------|--------------------------------------|
| PDF       | PyPdfiumDocumentBackend        | Extracts text from PDF files.        |
| Images    | OCR-based (if implemented)     | Extracts text from images (requires OCR). |
| HTML      | Direct Parsing                 | Extracts text from HTML files.       |
| PPTX      | Slide Content Parsing          | Extracts text from PowerPoint slides.|

### Unsupported Formats
- `.docx` (Word documents): Currently not supported.
- `.xlsx` (Excel files): Parsing not implemented.

---

## Example Workflow
1. **Upload a PDF file**.
2. **Split into chunks**:
   - A PDF with 10 pages is chunked into 1000-character segments with a 200-character overlap.
3. **Ask a question**:
   - Query: "What is the content of the first page?"
   - The system retrieves relevant chunks and generates an answer using the LLM.

---

## Future Enhancements
- Add support for `.txt` and `.md` file formats.
- Expand compatibility with `.docx` and `.xlsx`.
- Integrate advanced OCR libraries for better image processing.
- Implement additional chunking strategies.

---

## Developed By
**Partha Pratim Ray**  
GitHub: [ParthaPRay](https://github.com/ParthaPRay)

# Output

![image](https://github.com/user-attachments/assets/26e83a20-2b0e-490f-a6c9-d35013aa203c)

![image](https://github.com/user-attachments/assets/0270b7d6-8a77-4544-bed6-b56772e426ef)

