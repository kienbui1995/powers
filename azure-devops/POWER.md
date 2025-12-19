---
name: "azure-devops"
displayName: "Azure DevOps"
description: "Interact with Azure DevOps directly from Kiro. Manage projects, work items, wikis, and search across your organization."
keywords: ["azure-devops", "ado", "work-items", "wiki", "devops"]
author: "PIEM Space"
---

# Azure DevOps

## Overview

Azure DevOps MCP Server brings Azure DevOps context to your AI agents. Query projects, manage work items, search content, and interact with wikis directly from Kiro without switching to the Azure DevOps web interface.

This power includes the following domains:
- **core** - Project and team information
- **work** - Iterations, areas, and work management
- **work-items** - Tasks, bugs, user stories, and queries
- **search** - Search across code, work items, and wiki
- **wiki** - Create, read, and update wiki pages

## Onboarding

### Prerequisites

- Node.js 20+
- Azure DevOps organization with appropriate permissions
- Microsoft account linked to your Azure DevOps organization

### Installation

This power uses the official `@azure-devops/mcp` package from Microsoft.

### Authentication

The first time you execute an Azure DevOps tool, a browser window will open prompting you to login with your Microsoft account. Ensure you use credentials matching your Azure DevOps organization.

## Common Workflows

### Workflow 1: List Projects and Teams

**Goal:** Discover available projects and teams in your organization

**Steps:**
1. Use `core_list_projects` to see all projects
2. Use `core_list_project_teams` to list teams in a specific project
3. Use `work_list_iterations` to see sprint iterations

**Example:**
```
"List my ADO projects"
"List teams for project 'MyProject'"
"List iterations for project 'MyProject'"
```

### Workflow 2: Manage Work Items

**Goal:** Create, update, and query work items

**Steps:**
1. Use `wit_my_work_items` to see your assigned items
2. Use `wit_create_work_item` to create new items
3. Use `wit_update_work_item` to modify existing items

**Example:**
```
"List my work items for project 'MyProject'"
"List work items in current iteration for 'MyProject' project and 'MyProject Team'"
"Create a new task in project 'MyProject' with title 'Implement login feature'"
"Update work item 12345 to set status to 'In Progress'"
```

### Workflow 3: Search Content

**Goal:** Find code, work items, or wiki content

**Steps:**
1. Use `search_code` to search repositories
2. Use `search_workitem` to find work items
3. Use `search_wiki` to search wiki pages

**Example:**
```
"Search for 'authentication' in project 'MyProject'"
"Find work items containing 'bug fix'"
```

### Workflow 4: Wiki Management

**Goal:** Create and update wiki documentation

**Steps:**
1. Use `wiki_list_wikis` to see available wikis
2. Use `wiki_get_page_content` to read pages
3. Use `wiki_create_or_update_page` to modify content

**Example:**
```
"List all wikis in the 'MyProject' project"
"Get the content of wiki page '/Getting Started'"
"Create a wiki page '/Architecture/Overview' with content about system design"
"Update the wiki page '/API/Authentication' with new documentation"
```

## Troubleshooting

### Error: Authentication Failed

**Cause:** Microsoft account not linked to Azure DevOps organization
**Solution:**
1. Verify your Microsoft account has access to the organization
2. Clear browser cache and try again
3. Check organization permissions in Azure DevOps

### Error: Project Not Found

**Cause:** Incorrect project name or no access
**Solution:**
1. Use exact project name (case-sensitive)
2. Verify you have access to the project
3. Run "List my ADO projects" to see available projects

### Error: MCP Server Won't Start

**Cause:** Node.js not installed or wrong version
**Solution:**
1. Verify Node.js 20+: `node --version`
2. Install/update Node.js if needed
3. Restart Kiro

## Best Practices

- Always use exact project names (case-sensitive)
- Start with "List my ADO projects" to discover available projects
- Use iterations and teams for more specific work item queries
- Keep wiki page paths organized with clear hierarchy

## MCP Config Placeholders

Before using this power, replace the following placeholder in `mcp.json`:

- **`YOUR_ADO_ORG_NAME`**: Your Azure DevOps organization name
  - **How to get it:** Look at your Azure DevOps URL: `https://dev.azure.com/{org-name}` - the `{org-name}` part is your organization name

**After replacing, your mcp.json should look like:**
```json
{
  "mcpServers": {
    "azure-devops": {
      "command": "npx",
      "args": ["-y", "@azure-devops/mcp", "contoso", "-d", "core", "work", "work-items", "search", "wiki"]
    }
  }
}
```

---

**Package:** `@azure-devops/mcp`
**MCP Server:** azure-devops
**Source:** https://github.com/microsoft/azure-devops-mcp
