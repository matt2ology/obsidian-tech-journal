---
aliases:
note-created-on: 2024-11-27 (Wednesday) 12:25AM
note-type: Housekeeping
UID: 20241127T0025
tags:
related-notes:
  - "[[Obsidian Recommended Tags for a Zettelkasten Workflow]]"
---

# JSON Types

```json
{
  "types": {
    "UID": "date",
    "title": "text",
    "note-type": "text",
    "processed": "checkbox",
    "note-created-on": "text",
    "source": "text",
    "author": "text",
    "published-date": "text",
    "description": "text",
    "tags": "multitext"
  }
}
```

## **1. Identification and Metadata**

These fields help uniquely identify the note and define its type and origin:

- **UID:** Unique identifier for the note, often linked to creation or context.
- **title:** The note's primary title or name for quick identification.
- **note-type:** Specifies the type (e.g., reference, literature, permanent).
- **note-created-on** and **processed** provide timestamps and workflow status for chronological tracking and prioritization.

## **2. Source Information**

These fields clarify the origins and authorship of the content:

- **source:** Original source of the content (e.g., book, article, website).
- **author:** The creator(s) of the original content.
- **published-date:** Date the original source was published (if applicable).

## **3. Content Description**

These fields provide additional context and thematic categorization:

- **description**: A brief summary of the note's purpose or content.
- **tags**: Categories, topics, or thematic tags for searching and filtering.
