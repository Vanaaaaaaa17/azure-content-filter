# Usage Guide

[← Back to README](../README.md)


This document provides detailed instructions on how to use the Azure Content Filter service.

## 1. HTTP Trigger (`filter_comment`)

The HTTP trigger allows you to filter text on-demand by sending a POST request.

### Endpoint
`POST /api/filter_comment`

### Request Format
**Headers:**
- `Content-Type`: `application/json`

**Body:**
```json
{
  "comment": "String to be filtered"
}
```

### Response Format
**Success (200 OK):**
```json
{
  "original": "Original string",
  "filtered": "Filtered string with bad words masked (****)",
  "is_safe": boolean,
  "id": "MongoDB Document ID"
}
```

**Note:** The results are now stored in your configured MongoDB instance in the `reviews` collection.

**Error (400 Bad Request):**
- If the body is invalid JSON.
- If the `comment` field is missing.

### Example (cURL)
```bash
curl -X POST http://localhost:7071/api/filter_comment \
     -H "Content-Type: application/json" \
     -d '{"comment": "This is a really bad example."}'
```

---


