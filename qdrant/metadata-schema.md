# Metadata Schema

Each document chunk stored in the vector database should include metadata.

## Required Fields

- file_id
- file_name
- file_url
- mime_type
- chunk_index
- chunk_text
- last_modified
- source

## Optional Fields

- department
- document_type
- access_level
- author
- version

## Example

```json
{
  "file_id": "google-drive-file-id",
  "file_name": "Employee Handbook.pdf",
  "file_url": "https://drive.google.com/...",
  "mime_type": "application/pdf",
  "chunk_index": 1,
  "chunk_text": "Employees are eligible for annual leave...",
  "last_modified": "2026-06-11T10:00:00Z",
  "source": "google_drive",
  "department": "HR",
  "document_type": "policy"
}