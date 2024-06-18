# RAG-LLAMA3
Retrieval Augemented Generation (RAG) with Ollama Llama3 model and Qdrant Vector Database


## Deploy
### 1. Install Ollama and run llama3:8b model

Ref : https://medium.com/@shadabshaukat/run-llama3-on-your-m1-pro-macbook-08388b4b98e1

ollama run llama3:8b

Pull the 'mxbai-embed-large' embedding model from ollama

ollama pull mxbai-embed-large


### 2. Install Python 3.12 


### 3. Install Qdrant Vector database in Docker

colima start

docker pull qdrant/qdrant

docker run -p 6333:6333 -p 6334:6334 \
    -v $(pwd)/qdrant_storage:/qdrant/storage:z \
    qdrant/qdrant
    
### 4. Clone Repo

git clone https://github.com/shadabshaukat/RAG-LLAMA3.git && cd RAG-LLAMA3/

In this sample, PDFs will be stored in directory '/Users/shadab/Downloads/data' 

### 5. Deploy a Python Virtual environment

python3 -m venv .venv

source .venv/bin/activate

pip install -r requirements.txt

### 6. Run RAG as Python Script

python3 main.py

### 7. Exit Python Virtual Environment

deactivate

