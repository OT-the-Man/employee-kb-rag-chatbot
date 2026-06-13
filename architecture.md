# Architecture

## System Overview

The Employee Knowledge Base RAG Chatbot is an AI-powered knowledge management system built with n8n, Google Drive, Google Gemini, and Qdrant. The solution enables employees to ask natural-language questions about company information and receive context-aware answers generated from internal documents.

The system uses a Retrieval-Augmented Generation (RAG) architecture to ensure responses are grounded in company knowledge rather than relying solely on the language model's pre-trained knowledge. Documents stored in Google Drive are automatically processed, split into chunks, converted into vector embeddings using Gemini, and stored in Qdrant for semantic search.

When employees submit questions through the chatbot, relevant document chunks are retrieved from Qdrant and supplied to the AI Agent as context. Gemini then generates accurate responses based on the retrieved information. The system also supports automatic document reindexing to ensure that changes made to company documents are reflected in future responses.

## Architecture Diagram

```
                           Google Drive
                                │
                                ▼
              ┌─────────────────────────────────┐
              │ 01 - Auto Document Indexing     │
              │ Detect New Documents            │
              └─────────────────────────────────┘
                                │
                                ▼
                     Document Processing
                                │
                                ▼
                     Gemini Embeddings
                                │
                                ▼
                         Qdrant Cloud
                       Vector Database
                                ▲
                                │
              ┌─────────────────────────────────┐
              │ 01B - Updated Document          │
              │ Reindexing Workflow             │
              └─────────────────────────────────┘
                                │
                                ▼
                      Refresh Stored Vectors

────────────────────────────────────────────────────

                           Employee
                                │
                                ▼
              ┌─────────────────────────────────┐
              │ 02 - Employee KB Chatbot        │
              └─────────────────────────────────┘
                                │
                                ▼
                           AI Agent
                                │
                                ▼
                    Retrieve Context from
                         Qdrant Cloud
                                │
                                ▼
                      Gemini Chat Model
                                │
                                ▼
                          AI Response

────────────────────────────────────────────────────

                     99 - Error Handler
                                │
                                ▼
               Captures Workflow Failures
               Logs Errors and Sends Alerts
```

## Workflow Architecture

The solution consists of four interconnected workflows that work together to maintain and serve the knowledge base.

### 01 - Auto Document Indexing

This workflow automatically detects newly added documents in Google Drive. The files are downloaded, processed, chunked into smaller sections, embedded using Gemini, and stored in Qdrant. This ensures new company knowledge becomes searchable without manual intervention.

### 01B - Updated Document Reindexing

This workflow monitors existing documents for changes. When a document is modified, the previous vectors are replaced with newly generated embeddings to keep the vector database synchronized with the latest version of the document.

### 02 - Employee KB Chatbot

This workflow serves as the user-facing chatbot. Employee questions are processed by an AI Agent, which retrieves relevant context from Qdrant before generating responses with Gemini. This retrieval step helps reduce hallucinations and improve answer accuracy.

### 99 - Error Handler

This workflow provides centralized error management across the system. Workflow failures, processing issues, and integration errors are captured, logged, and can be routed to notification systems for monitoring and troubleshooting.

## Core Services

| Service       | Purpose                                      |
| ------------- | -------------------------------------------- |
| n8n           | Workflow orchestration and automation        |
| Google Drive  | Storage for company documents                |
| Google Gemini | Embeddings generation and conversational AI  |
| Qdrant Cloud  | Vector database for semantic search          |
| AI Agent      | Retrieval-Augmented Generation orchestration |
| Chat Memory   | Maintains conversational context             |
| Error Handler | Centralized workflow monitoring and recovery |

```
```
