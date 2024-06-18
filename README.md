# RAG-LLAMA3
Retrieval Augemented Generation (RAG) with Ollama Llama3 model and Qdrant Vector Database


## Deploy
### 1. Install Ollama and run Llama3:8b model

Ref : https://medium.com/@shadabshaukat/run-llama3-on-your-m1-pro-macbook-08388b4b98e1

```
ollama run llama3:8b
```

> Pull the mxbai-embed-large embedding model from ollama **


```
ollama pull mxbai-embed-large
```


### 2. Install Python 3.12 

```
brew install Python3
```

### 3. Run Qdrant Vector database as a Local Docker Container

```
colima start

docker pull qdrant/qdrant

docker run -p 6333:6333 -p 6334:6334 \
    -v $(pwd)/qdrant_storage:/qdrant/storage:z \
    qdrant/qdrant
```
    
### 4. Clone Repo

```
git clone https://github.com/shadabshaukat/RAG-LLAMA3.git && cd RAG-LLAMA3/
```

> In this sample, PDFs stored in directory 'data' will be converted into vectors and written to Qdrant vector store and the similarity search be done using those PDFs as context

### 5. Deploy a Python Virtual environment

```
python3 -m venv .venv

source .venv/bin/activate

pip install -r requirements.txt
```

### 6. Run RAG as Python Script

```
python3 main.py
```

### 7. Exit Python Virtual Environment

```
deactivate
```

## Sample Run

```
% python3 main.py

Loading files: 100%|████████████████████████████████████| 1/1 [00:02<00:00,  2.64s/file]
INFO:__main__:initializing the vector store related objects
INFO:httpx:HTTP Request: GET http://localhost:6333/collections/oci_goldengate/exists "HTTP/1.1 200 OK"
INFO:__main__:initializing the OllamaEmbedding
INFO:__main__:initializing the global settings
INFO:__main__:enumerating docs
INFO:__main__:enumerating text_chunks
INFO:__main__:enumerating nodes
INFO:__main__:initializing the storage context
INFO:__main__:indexing the nodes in VectorStoreIndex
INFO:httpx:HTTP Request: GET http://localhost:6333/collections/oci_goldengate/exists "HTTP/1.1 200 OK"
INFO:httpx:HTTP Request: GET http://localhost:6333/collections/oci_goldengate "HTTP/1.1 200 OK"
INFO:httpx:HTTP Request: PUT http://localhost:6333/collections/oci_goldengate/points?wait=true "HTTP/1.1 200 OK"
INFO:httpx:HTTP Request: PUT http://localhost:6333/collections/oci_goldengate/points?wait=true "HTTP/1.1 200 OK"
INFO:httpx:HTTP Request: PUT http://localhost:6333/collections/oci_goldengate/points?wait=true "HTTP/1.1 200 OK"
INFO:httpx:HTTP Request: PUT http://localhost:6333/collections/oci_goldengate/points?wait=true "HTTP/1.1 200 OK"
INFO:httpx:HTTP Request: PUT http://localhost:6333/collections/oci_goldengate/points?wait=true "HTTP/1.1 200 OK"
INFO:httpx:HTTP Request: PUT http://localhost:6333/collections/oci_goldengate/points?wait=true "HTTP/1.1 200 OK"
INFO:httpx:HTTP Request: PUT http://localhost:6333/collections/oci_goldengate/points?wait=true "HTTP/1.1 200 OK"
INFO:httpx:HTTP Request: PUT http://localhost:6333/collections/oci_goldengate/points?wait=true "HTTP/1.1 200 OK"
INFO:httpx:HTTP Request: PUT http://localhost:6333/collections/oci_goldengate/points?wait=true "HTTP/1.1 200 OK"
INFO:__main__:initializing the VectorIndexRetriever with top_k as 5
INFO:__main__:creating the RetrieverQueryEngine instance
INFO:__main__:creating the HyDEQueryTransform instance
INFO:__main__:retrieving the response to the query
INFO:httpx:HTTP Request: POST http://localhost:11434/api/chat "HTTP/1.1 200 OK"
INFO:httpx:HTTP Request: POST http://localhost:6333/collections/oci_goldengate/points/search "HTTP/1.1 200 OK"
INFO:httpx:HTTP Request: POST http://localhost:11434/api/chat "HTTP/1.1 200 OK"

Here's a sample parameter file for an extract in OCI GoldenGate that captures DDL operations on Oracle Database:

-- Capture DDL operations for listed schema tables
ddl include mapped

-- Add step-by-step history of DDL operations captured to the report file. Very useful when troubleshooting.
ddloptions report

-- Write capture stats per table to the report file daily.
report at 00:01

-- Rollover the report file weekly. Useful when PR runs without being stopped/started for long periods of time to keep the report files from becoming too large.
reportrollover at 00:01 on Sunday

-- Report total operations captured, and operations per second every 10 minutes.
reportcount every 10 minutes, rate

-- Table map list for apply
MAP SRC_OCIGGLL.*, TARGET SRCMIRROR_OCIGGLL.*;

This parameter file captures DDL operations for the listed schema tables in the `SRC_OCIGGLL` schema and maps them to the `SRCMIRROR_OCIGGLL` target. It also includes options for reporting, such as step-by-step history of DDL operations captured, daily capture stats per table, weekly report file rollover, and total operations captured with rate every 10 minutes.
```
