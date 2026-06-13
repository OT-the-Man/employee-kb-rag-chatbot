# Architecture

## System Overview

This project is an Employee Knowledge Base RAG chatbot built in n8n.

The system has two main workflows:

1. Document Indexing Workflow
2. Employee Chatbot Workflow

## Document Indexing Workflow

Google Drive detects new or updated company documents.

The workflow downloads the file, extracts the text, splits it into chunks, generates embeddings, and stores the chunks in Qdrant.

## Employee Chatbot Workflow

An employee asks a question through the n8n chat interface.

The chatbot searches Qdrant for relevant document chunks, sends the retrieved context to Gemini, and returns an answer based only on the knowledge base.

## Services

- n8n for workflow automation
- Google Drive for document storage
- Google Gemini for embeddings and chat responses
- Qdrant Cloud for vector storage