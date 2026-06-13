# Employee Knowledge Base RAG Chatbot

## Project Title

Employee Knowledge Base RAG Chatbot using n8n, Google Drive, Gemini, and Qdrant

---

## Short Summary

This project is an AI-powered Retrieval-Augmented Generation (RAG) chatbot built entirely in n8n. It automatically monitors a Google Drive folder, indexes company documents into a Qdrant vector database using Gemini embeddings, and allows employees to ask natural-language questions through a chat interface.

The system maintains an up-to-date knowledge base by automatically processing newly uploaded documents and re-indexing modified files. Employees can then retrieve accurate answers grounded in company documentation rather than relying solely on the LLM's general knowledge.

---

## Project Goal

Build a production-style employee knowledge assistant from scratch using:

* n8n
* Google Drive
* Google Gemini
* Qdrant Vector Database
* AI Agent
* Vector Store Retrieval
* Chat Memory
* Error Handling Workflows

---

## Architecture Diagram

```
                    Google Drive
                           │
        ┌──────────────────┴──────────────────┐
        │                                     │
 New Document Workflow            Updated Document Workflow
        │                                     │
        └───────────────┬─────────────────────┘
                        │
                 Document Processing
                        │
                Gemini Embeddings
                        │
                     Qdrant
                Vector Database
                        │
                        ▼
               Employee Chatbot
                        │
                  AI Agent
                        │
            Vector Store Retrieval
                        │
                    Response
```

---

## Tools Used

| Tool          | Purpose                  |
| ------------- | ------------------------ |
| n8n           | Workflow orchestration   |
| Google Drive  | Document storage         |
| Google Gemini | LLM and embeddings       |
| Qdrant        | Vector database          |
| AI Agent      | Conversational interface |
| Chat Memory   | Session memory           |
| Google OAuth  | Authentication           |

---

## Workflows

The system consists of four workflows working together.

### 01 - Auto Document Indexing

Purpose:

Automatically detects and processes newly added files in a Google Drive folder.

Responsibilities:

* Monitor designated Drive folder
* Download new documents
* Extract content
* Generate embeddings
* Store vectors in Qdrant

---

### 01B - Updated Document Reindexing

Purpose:

Ensures the vector database stays synchronized when documents change.

Responsibilities:

* Detect document updates
* Remove outdated vectors
* Generate fresh embeddings
* Reinsert updated content into Qdrant

---

### 02 - Employee KB Chatbot

Purpose:

Provides a conversational interface for employees.

Responsibilities:

* Receive user questions
* Retrieve relevant chunks from Qdrant
* Send context to Gemini
* Generate grounded responses
* Maintain conversation memory

---

### 99 - Error Handler

Purpose:

Centralized workflow for handling failures.

Responsibilities:

* Capture workflow errors
* Log issues
* Send notifications
* Improve monitoring and troubleshooting

---

## How the Four Workflows Work Together

1. Employees upload documents to Google Drive.
2. Auto Document Indexing processes newly added files.
3. Updated Document Reindexing refreshes changed files.
4. Processed content is stored in Qdrant.
5. Employees ask questions through the chatbot.
6. Relevant information is retrieved from Qdrant.
7. Gemini generates answers using retrieved context.
8. Error Handler captures and reports failures across the system.

---



## Local Setup

### Prerequisites

* Docker Desktop
* n8n
* Qdrant
* Google Account
* Gemini API Key

---


```

---


---

## How to Import Workflows into n8n

1. Open n8n.
2. Click Import Workflow.
3. Select the workflow JSON file.
4. Repeat for all four workflows.
5. Configure credentials.
6. Activate workflows.

Recommended import order:

```
99 - Error Handler
01 - Auto Document Indexing
01B - Updated Document Reindexing
02 - Employee KB Chatbot
```

---

## Qdrant Setup

Create a collection:

```
employee_knowledge_base
```

Suggested configuration:

* Distance Metric: Cosine
* Vector Size: Match Gemini embedding dimensions

Configure Qdrant credentials inside n8n and connect all vector store nodes to the collection.

---

## Gemini Setup

1. Create a Gemini API key.
2. Add Gemini credentials in n8n.
3. Connect Gemini Chat Model node.
4. Connect Gemini Embeddings node.
5. Test both connections before activating workflows.

Required uses:

* Embedding generation
* AI Agent responses

---

## Known Limitations

* Supports only configured document formats.
* Retrieval quality depends on chunking strategy.
* Requires internet access for Gemini API.
* No role-based access control.
* Limited monitoring and analytics.
* Large document collections may require optimization.

---

## Future Improvements

* User authentication and permissions
* Department-specific knowledge bases
* Multi-language support
* Source citation in responses
* Slack and Microsoft Teams integration
* Email notifications
* Dashboard for monitoring indexing status
* Automated backup and recovery
* Hybrid search (keyword + vector search)
* Human feedback collection for answer quality

---


```
