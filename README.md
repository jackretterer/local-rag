# Demo - Local RAG Application Using Unstructured

This repository features a simple notebook which demonstrates how to use [Unstructured](https://unstructured.io/) to ingest and pre-process documents for a local Retrieval-Augmented-Generation (RAG) application

The goal of this repo is not use any cloud services or external APIs and to run everything locally. This demonstrates RAG applications can be built with siloed infrastructure. 

## Caveats

1. This jupyter notebook will try to pre-process ALL files the "files_used" directory.  The "files_used" directory in this repo contains a few PDFs related to the NFL.

2. If you don't use a GPU or some type of accelerator, generating embeddings and LLM generation WILL be slower.

## Setup Steps

1. Install [Python](https://www.python.org/downloads/). Please use version 3.9 or later.

2. Install Docker, Docker-Compose and Docker Desktop and make sure Docker Desktop is running. [Installation instructions are here](https://docs.docker.com/compose/install/)

3. Clone this repository by running the following command

```bash
git clone git@github.com:Unstructured-IO/local-RAG-demo.git
```

4. CD into this repository locally, create a virtual environment, install the requirements

```bash
cd local-RAG-demo #enter local-RAG-demo directory
python3.10 -m venv env #create venv called env
source env/bin/activate #activate environment
pip install -r requirements.txt #install required packages
```

5. Install and Download LLama2 CCP Model. This is slightly different for every OS, but here is a link with [download instructions](https://github.com/ggerganov/llama.cpp#obtaining-and-using-the-facebook-llama-2-model). Below is how to install + download on MAC.

```bash
mkdir model_files #make model files folder to store Llama 2 model files
CMAKE_ARGS="-DLLAMA_METAL=on" FORCE_CMAKE=1 pip install llama-cpp-python #install llama-cpp-python package made for MAC Silicon chips
huggingface-cli download TheBloke/Llama-2-7b-Chat-GGUF --local-dir model_files --local-dir-use-symlinks False --include='*Q4_K*gguf' #download model
```

6. Start Docker Container to Spin up Weaviate VectorDB 

```bash
docker-compose up -d
```


