---
name: devexpress-documentation
description: Search and retrieve official DevExpress documentation. Use for WPF, Blazor, XtraReports, eXpressAppFramework, MAUI, WindowsForms, XPO, Dashboard, OfficeFileAPI, and all DevExpress technologies. Get accurate, current information from docs.devexpress.com—API references, tutorials, code samples, and best practices.
compatibility: Requires DevExpress MCP Server (https://api.devexpress.com/mcp/docs)
---

Search DevExpress official documentation and return accurate, detailed results.

## Usage

`/devexpress-documentation [technology] [question]`

- **technology** (optional): specific DevExpress technology (e.g. `WPF`, `Blazor`, `XtraReports`, `eXpressAppFramework`)
- **question**: what you want to know or find in the documentation

If no technology is specified, search across all relevant technologies based on the question.

## Instructions

Given the following query: $ARGUMENTS

1. Parse the arguments to extract:
   - The DevExpress technology (if specified)
   - The actual question or search topic

2. Call `devexpress_docs_search` with:
   - `technologies`: an array of relevant technologies (infer from context if not specified)
   - `question`: the extracted question

   Available technologies: `Angular`, `AspNet`, `AspNetBootstrap`, `AspNetCore`, `AspNetMvc`, `Blazor`, `CoreLibraries`, `Dashboard`, `DevExtremeAspNetMvc`, `eXpressAppFramework`, `jQuery`, `MAUI`, `OfficeFileAPI`, `React`, `ReportServer`, `VCL`, `Vue`, `WindowsForms`, `WPF`, `XPO`, `XtraReports`

3. Analyze the search results and select the most relevant article URL(s).

4. Call `devexpress_docs_get_content` on the most relevant URL to retrieve the full documentation content.

5. Present the results clearly:
   - Start with a concise direct answer
   - Include relevant code samples from the documentation
   - Provide the source URL(s) for reference
   - Highlight any important notes or warnings from the docs

Always prefer official documentation content over general knowledge. If multiple technologies are relevant, search them all.

## Version-specific documentation

By default, this plugin queries the latest DevExpress documentation. To pin searches to a specific product version (e.g. 24.2), users can add a versioned MCP server:

**Claude Code** (`~/.claude/.mcp.json`):

```json
{
  "mcpServers": {
    "dxdocs24_2": {
      "url": "https://api.devexpress.com/mcp/docs?v=24.2",
      "type": "http"
    }
  }
}
```

**GitHub Copilot CLI** (`~/.copilot/mcp.json`):

```json
{
  "mcpServers": {
    "dxdocs24_2": {
      "url": "https://api.devexpress.com/mcp/docs?v=24.2",
      "type": "http"
    }
  }
}
```

If the user requests documentation for a specific version and a versioned MCP server is available (e.g. `dxdocs24_2`), prefer using that server's tools. Otherwise, use the default `dxdocs` server.
