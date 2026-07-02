# RAG

## Naive RAG or Vanilla RAG - sampleRAG.ipynb

Developed a simple RAG pipeline, and follows 
 - Load the pdf using fitz from pymupdf and store the retrieved text and the source document as a dictionary
    ```py
    documents = {"text": text, "source": filename}
    ```

 - Retrieve chunks of the text with fixed chunk size and overlap chunks in a fixed size and each chunk will be one vector in the embedding matrix
    ```py
    chunk_size = 500
    overlap = 100
    chunk1 = 0-500
    chunk2 = 400-900
    ```

 - Convert the texts of the chunks into embeddings using any text - embedding model (used "all-MiniLM-L6-v2")

 - Create faiss index using IndexFlatIP and add the embeddings to the index along with the metadata and store them in a vector DB or local file .bin and metadata as .pkl

 - Recieve input query from user and generate embeddings for the input query too using the same model used to embedd the document

 - Perform similarity search in the vector DB using the query and fetch top k elements and retieve the chunks using the index from the metadata

 - Build a prompt to let the LLM generate answer only from the retrieved context

 - Call the llama model using groq provider (or any LLM using api/local model) and send the prompt to generate answer for the query
  