---
name: "notion"
displayName: "Notion"
description: "Interact with Notion workspace - create, read, update pages and databases. Manage project documentation, meeting notes, and knowledge bases directly from Kiro."
keywords: ["notion", "workspace", "pages", "databases", "documentation", "wiki"]
author: "PIEM Space"
---

# Notion

## Overview

This power enables seamless integration with Notion workspaces through the official Notion MCP server. Create, read, update, and manage Notion pages and databases directly from Kiro without switching contexts.

**Key Capabilities:**
- Create and update Notion pages with rich content
- Query and manage Notion databases
- Search across your workspace
- Sync project documentation between codebase and Notion

**Use Cases:**
- Document project decisions and architecture
- Create meeting notes and sprint planning
- Manage task databases and project trackers
- Build knowledge bases and wikis

## Onboarding

### Prerequisites

- Notion account with workspace access

### Setup

1. **Connect to Notion MCP:**
   - The power uses Notion's official MCP endpoint: `https://mcp.notion.com/mcp`
   - Authentication is handled through Notion's OAuth flow

2. **Grant Workspace Access:**
   - When first connecting, authorize Kiro to access your Notion workspace
   - Select which pages/databases to share with the integration

### Configuration

The MCP server connects via remote URL - no local installation required.

**Environment:** No additional environment variables needed (OAuth-based authentication).

## Common Workflows

### Workflow 1: Create Project Documentation Page

**Goal:** Create a new documentation page in Notion for a project

**Steps:**
1. Use `notion-create-pages` to create a new page
2. Specify parent page/database and title
3. Add content blocks (headings, paragraphs, code blocks)

**Example:**
```
Create a new page titled "Architecture Overview" under the Engineering wiki with:
- Overview section
- System diagram placeholder
- Technology stack table
```

### Workflow 2: Search and Query

**Goal:** Find content across your Notion workspace

**Steps:**
1. Use `notion-search` for semantic search
2. Use `notion-fetch` to get full page details

**Example:**
```
"Search Notion for 'sprint planning'"
"Get details of page 'Project Roadmap'"
```

### Workflow 3: Update Page Content

**Goal:** Update existing page with new information

**Steps:**
1. Use `notion-fetch` to retrieve current content
2. Use `notion-update-page` to modify properties or content

**Example:**
```
Update the "Sprint 2 Planning" page:
- Change status property to "Completed"
- Add retrospective notes section at the end
```

### Workflow 4: Create Meeting Notes

**Goal:** Quickly create structured meeting notes

**Steps:**
1. Create page with meeting template structure
2. Add attendees, date, agenda sections
3. Include action items section

**Example:**
```
Create meeting notes for "Team Sync - Dec 19":
- Attendees: Alice, Bob, Charlie
- Agenda items from talking points
- Action items section
```

### Workflow 5: Manage Databases

**Goal:** Create and update Notion databases

**Steps:**
1. Use `notion-create-database` to create new database
2. Use `notion-update-database` to modify schema

**Example:**
```
"Create a Tasks database with Status, Priority, and Due Date properties"
"Add a new 'Assignee' property to the Tasks database"
```

## Troubleshooting

### Connection Issues

**Problem:** MCP server won't connect
**Solution:**
1. Verify Notion account is logged in
2. Re-authorize the integration if needed
3. Check if workspace permissions are granted

### Permission Errors

**Problem:** "Access denied" when accessing pages
**Cause:** Integration doesn't have access to the page
**Solution:**
1. Open the page in Notion
2. Click "Share" → "Invite"
3. Add the integration to the page

### Rate Limiting

**Problem:** Too many requests error
**Cause:** Notion API rate limits exceeded
**Solution:**
1. Wait a few seconds between operations
2. Batch operations when possible
3. Use pagination for large queries

## Best Practices

- Use database templates for consistent page structures
- Link related pages to build connected knowledge graphs
- Use properties for filtering and organizing content
- Keep page hierarchy shallow (max 3-4 levels deep)
- Use inline databases for task lists within pages

## Configuration

**No placeholders needed** - the mcp.json configuration works as-is with Notion's official MCP endpoint.

---

**MCP Server Type:** Remote (HTTP/SSE)
**Endpoint:** `https://mcp.notion.com/mcp`
**Authentication:** OAuth (handled by Notion)
**Documentation:** https://developers.notion.com/
