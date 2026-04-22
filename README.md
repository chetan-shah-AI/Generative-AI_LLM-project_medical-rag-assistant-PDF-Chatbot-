# 🏥 End-to-End Medical Chatbot (RAG-Based)
<<<<<<< HEAD

---

## What is this project

A **production-grade Generative AI system** that builds a **domain-specific chatbot** using Retrieval-Augmented Generation (RAG).

The system ingests large documents (e.g., a 637-page medical PDF), converts them into embeddings, stores them in a vector database, and uses an LLM to generate **context-aware, grounded responses**.

While this implementation focuses on **healthcare**, the architecture is **fully reusable across industries** such as SaaS, finance, legal, HR, and enterprise knowledge systems.

---

## 0. Problem Statement

Traditional LLM-based systems face critical limitations:

* ❌ No access to private/domain-specific data
* ❌ Hallucinations (especially dangerous in healthcare)
* ❌ Limited context window
* ❌ Lack of explainability

In real-world domains:

* Knowledge is stored in **large documents (PDFs, manuals, policies)**
* Users need **accurate, grounded answers**
* Manual search is **slow and inefficient**

This results in **poor decision-making and low trust in AI systems**.

---

## 1. Project Goals

This system is designed to:

* Build a complete **RAG pipeline**
* Convert documents into a **searchable knowledge base**
* Enable **semantic search using embeddings**
* Integrate **GPT-4o for answer generation**
* Deliver **accurate, context-grounded responses**
* Build a **full-stack chatbot (backend + UI)**
* Deploy using **Docker + AWS + CI/CD**
* Provide a **reusable enterprise AI architecture**

---

## 2. Real Life Business Cases where this project would help and why

This project is not just a medical chatbot — it is a **general-purpose knowledge assistant architecture**.

### Healthcare (Primary Use Case)

* Medical assistants for disease, diagnosis, and treatment queries
* Clinical knowledge retrieval systems
* Research and medical education tools

---

### SaaS / B2B Software

* AI support assistant over documentation and APIs
* Internal developer knowledge assistant
* Customer onboarding chatbot

**Why it matters**
Reduces support load and improves user experience.

---

### Customer Support Systems

* FAQ automation
* Ticket resolution assistant
* Knowledge base search

**Impact**
Faster resolution, reduced cost, better customer satisfaction.

---

### Legal / Compliance

* Contract analysis assistant
* Policy and regulatory search
* Legal documentation Q&A

**Impact**
Saves hours of manual document review.

---

### HR / Internal Tools

* Employee policy chatbot
* Onboarding assistant
* Payroll and benefits queries

**Impact**
Improves internal efficiency and employee experience.

---

### Finance / Banking

* Risk and compliance assistant
* Financial document search
* Investment research support

---

### Insurance

* Claims processing assistant
* Policy understanding chatbot

---

### EdTech / Learning Platforms

* AI tutor over course material
* Book-based Q&A systems

---

### Enterprise Knowledge Systems

* Internal documentation assistant
* SOP and process retrieval

---

### IT / DevOps / Engineering

* Runbook assistant
* Incident response support

---

### Manufacturing / Operations

* Machine manual assistant
* Safety protocol chatbot

---

### Government / Public Sector

* Policy explanation chatbot
* Citizen service assistant

---

## 🔑 Key Insight

This is fundamentally a **"Knowledge Retrieval + AI Reasoning System"**
→ Applicable anywhere large documents exist.

---

## 3. Feature → File Mapping with Evidence from the Code

### PDF Data Loading → `helper.py`

```python id="a1"
DirectoryLoader(data, glob="*.pdf", loader_cls=PyPDFLoader)
```

Loads and extracts content from PDF documents.

---

### Metadata Cleaning → `helper.py`

```python id="a2"
Document(page_content=doc.page_content, metadata={"source": src})
```

Keeps only relevant metadata.

---

### Text Chunking → `helper.py`

```python id="a3"
RecursiveCharacterTextSplitter(chunk_size=500, chunk_overlap=20)
```

Splits large documents into smaller chunks.

---

### Embedding Generation → `helper.py`

```python id="a4"
HuggingFaceEmbeddings("sentence-transformers/all-MiniLM-L6-v2")
```

Converts text into 384-dimensional vectors.

---

### Vector Storage → `store_index.py`

```python id="a5"
PineconeVectorStore.from_documents(...)
```

Stores embeddings in Pinecone.

---

### Retrieval System → `app.py`

```python id="a6"
retriever = docsearch.as_retriever(search_kwargs={"k":3})
```

Fetches top-k relevant chunks.

---

### LLM Integration → `app.py`

```python id="a7"
ChatOpenAI(model="gpt-4o")
```

Generates responses.

---

### RAG Chain → `app.py`

```python id="a8"
create_retrieval_chain(retriever, question_answer_chain)
```

Combines retrieval + generation.

---

### Flask API → `app.py`

Handles user requests and responses.

---

### Frontend UI → `templates/`

Chat interface using HTML/CSS/JS.

---

### Deployment → Docker + GitHub Actions

Automates build and deployment.

---

## 4. Tech Stack

* Python
* LangChain
* Flask
* Pinecone
* HuggingFace
* OpenAI GPT-4o
* Docker
* AWS EC2 + ECR
* GitHub Actions

### Why These Choices

* LangChain simplifies RAG orchestration
* Pinecone enables scalable vector search
* GPT-4o provides strong reasoning
* Docker ensures portability
* AWS enables production deployment

---

## 5. System Architecture

```
PDF → Chunking → Embeddings → Pinecone → Retriever → LLM → Response
```

### Layers

1. Raw Data (PDF)
2. Processed Chunks
3. Vector Database
4. RAG Pipeline
5. UI/API Layer
6. CI/CD Piepline

---

## 6. Data Flow / Workflow

1. Load PDF
2. Extract text
3. Clean metadata
4. Chunk text
5. Generate embeddings
6. Store in Pinecone
7. Retrieve relevant chunks
8. Pass to LLM
9. Generate answer

---

## 7. Design Decisions

### RAG vs Fine-tuning

* Faster, cheaper, dynamic data support

### Chunking Strategy

* 500 size, 20 overlap → balance accuracy + performance

### Pinecone

* Managed, scalable

### GPT-4o

* High-quality reasoning

### Flask

* Simplicity for MVP

---

## 8. Error Handling and Logging

* Environment variable validation
* Pinecone index existence checks
* Safe handling of missing data
* Runtime logging in Flask

---

## 9. Challenges & Solutions

### Large Documents

→ Solved using chunking

### Hallucination

→ Solved using RAG

### Retrieval Accuracy

→ Improved via embeddings + top-k

### Deployment Complexity

→ Solved via Docker + CI/CD

---

## 10. Trade-offs

### RAG vs Fine-tuning

* RAG: flexible
* Fine-tuning: expensive

### Pinecone vs FAISS

* Pinecone: scalable
* FAISS: local

### Flask vs FastAPI

* Flask: simple
* FastAPI: performant

---

## 11. Testing

### Current

* Manual validation via queries

### Recommended

* Unit tests for chunking
* Embedding validation
* Retrieval tests
* API tests

---

## 12. Scaling Strategy

### Short Term

* Add more documents
* Improve prompts

### Medium Term

* Modular pipelines
* Add caching

### Long Term

* Distributed systems
* Multi-LLM support
* API productization

---

## 13. Future Improvements

* Conversation memory
* Streaming responses
* Advanced UI (React)
* Multi-document support
* Evaluation metrics (RAGAS)

---

## 🚀 Final Summary

This project demonstrates a **complete production-grade GenAI system**:

* Document ingestion
* Vector search
* LLM reasoning
* Full-stack development
* Cloud deployment

It is not just a chatbot — it is a **reusable enterprise AI architecture** that can power:

* SaaS assistants
* Enterprise search
* Legal tools
* Financial systems
* Knowledge platforms

# How to run?
### STEPS:

Clone the repository

```bash
https://github.com/entbappy/End-to-End-Medical-Chatbot
```

### STEP 01- Create a conda environment after opening the repository

```bash
conda create -n medibot python=3.10 -y
```


```bash
conda activate medibot
```

### STEP 02- install the requirements
```bash
pip install -r requirements.txt
```

### Create a `.env` file in the root directory and add your Pinecone & openai credentials as follows:

```ini
PINECONE_API_KEY = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
OPENAI_API_KEY = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```


```bash
# run the following command to store embeddings to pinecone
python store_index.py
```

```bash
# Finally run the following command
python app.py
```

Now,
```bash
open up localhost:
```



### Techstack Used:

- Python
- LangChain
- Flask
- GPT
- Pinecone



# AWS-CICD-Deployment-with-Github-Actions

## 1. Login to AWS console.

## 2. Create IAM user for deployment

	#with specific access

	1. EC2 access : It is virtual machine

	2. ECR: Elastic Container registry to save your docker image in aws


	#Description: About the deployment

	1. Build docker image of the source code

	2. Push your docker image to ECR

	3. Launch Your EC2 

	4. Pull Your image from ECR in EC2

	5. Lauch your docker image in EC2

	#Policy:

	1. AmazonEC2ContainerRegistryFullAccess

	2. AmazonEC2FullAccess

	
## 3. Create ECR repo to store/save docker image
    - Save the URI: 315865595366.dkr.ecr.us-east-1.amazonaws.com/medicalbot

	
## 4. Create EC2 machine (Ubuntu) 

## 5. Open EC2 and Install docker in EC2 Machine:
	
	
	#optinal

	sudo apt-get update -y

	sudo apt-get upgrade
	
	#required

	curl -fsSL https://get.docker.com -o get-docker.sh

	sudo sh get-docker.sh

	sudo usermod -aG docker ubuntu

	newgrp docker
	
# 6. Configure EC2 as self-hosted runner:
    setting>actions>runner>new self hosted runner> choose os> then run command one by one


# 7. Setup github secrets:

   - AWS_ACCESS_KEY_ID
   - AWS_SECRET_ACCESS_KEY
   - AWS_DEFAULT_REGION
   - ECR_REPO
   - PINECONE_API_KEY
   - OPENAI_API_KEY

