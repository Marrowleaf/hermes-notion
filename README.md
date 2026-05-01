# Notion

> Notion API via curl — create, read, update pages, databases (data sources), blocks, and search with full JSON control.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://github.com/Marrowleaf/hermes-notion)

## Features

- Search pages and databases by keyword
- Create, read, and update pages with rich property types
- Query databases with filters and sorts
- Create new databases with custom schemas
- Add content blocks to pages (text, lists, embeds)
- Full property type support: title, rich text, select, multi-select, date, checkbox, number, URL, email, relations
- Batch record creation (up to 10 per request via Airtable-style patterns)
- Uses latest API version (2025-09-03) with data sources endpoints

## Installation

```bash
hermes skills install productivity/notion
```

Or manually clone into `~/.hermes/skills/productivity/notion/`.

## Usage

```bash
# Search for a page
curl -s -X POST "https://api.notion.com/v1/search" -H "Authorization: Bearer $NOTION_API_KEY" -H "Notion-Version: 2025-09-03" -H "Content-Type: application/json" -d '{"query": "page title"}'

# Create a page in a database
curl -s -X POST "https://api.notion.com/v1/pages" -H "Authorization: Bearer $NOTION_API_KEY" -H "Notion-Version: 2025-09-03" -H "Content-Type: application/json" -d '{"parent":{"database_id":"xxx"},"properties":{"Name":{"title":[{"text":{"content":"New Item"}}]}}}'

# Query a database with filter
curl -s -X POST "https://api.notion.com/v1/data_sources/{id}/query" -H "Authorization: Bearer $NOTION_API_KEY" -H "Notion-Version: 2025-09-03" -H "Content-Type: application/json" -d '{"filter":{"property":"Status","select":{"equals":"Active"}}}'
```

## Configuration

- `NOTION_API_KEY`: Required — create an integration at https://notion.so/my-integrations (key starts with `ntn_` or `secret_`)
- Store in `~/.hermes/.env` as `NOTION_API_KEY=ntn_your_key_here`
- **Important:** Share target pages/databases with your integration in Notion (click "..." → "Connect to" → your integration name)

## Requirements

- curl
- Notion integration with API key
- Target pages/databases must be shared with the integration

## License

MIT