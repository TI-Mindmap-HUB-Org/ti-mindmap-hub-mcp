<div align="center">

# TI Mindmap HUB — MCP Server

**Threat Intelligence at your fingertips, directly inside your AI assistant.**

[![MCP Protocol](https://img.shields.io/badge/MCP-Compatible-blue?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0IiBmaWxsPSJ3aGl0ZSI+PHBhdGggZD0iTTEyIDJDNi40OCAyIDIgNi40OCAyIDEyczQuNDggMTAgMTAgMTAgMTAtNC40OCAxMC0xMFMxNy41MiAyIDEyIDJ6bTAgMThjLTQuNDIgMC04LTMuNTgtOC04czMuNTgtOCA4LTggOCAzLjU4IDggOC0zLjU4IDgtOCA4eiIvPjwvc3ZnPg==)](https://modelcontextprotocol.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-ti--mindmap--hub.com-orange?style=for-the-badge)](https://ti-mindmap-hub.com)

---

Query threat intelligence reports, CVEs, IOCs, STIX bundles, and weekly briefings — all through natural language, powered by the [Model Context Protocol](https://modelcontextprotocol.io).

[**Get Started**](#-quick-start) · [**Tool Reference**](#-available-tools) · [**Web Platform**](https://ti-mindmap-hub.com) · [**Examples**](#-what-you-can-ask)

</div>

---

## What is TI Mindmap HUB?

**[TI Mindmap HUB](https://ti-mindmap-hub.com)** is a threat intelligence platform that automatically collects, analyzes, and enriches cybersecurity articles from leading sources. Every article is processed with AI to generate:

- **AI Summaries** — Concise overviews of each threat
- **Threat Mindmaps** — Visual maps of attack flows and relationships
- **MITRE ATT&CK TTPs** — Tactics, Techniques, and Procedures mapping
- **IOC Extraction** — Indicators of Compromise (IPs, domains, hashes, URLs)
- **STIX 2.1 Bundles** — Structured threat data compatible with MISP, OpenCTI, Microsoft Sentinel
- **CVE Intelligence** — Enriched vulnerability data with EPSS scores and exploitation status
- **Weekly Briefings** — Curated threat landscape reports

This **MCP Server** brings all of this directly into your AI assistant.

---

## Why Use the MCP Server?

| Without MCP | With MCP |
|:---|:---|
| Switch between tools and dashboards | Ask your AI assistant directly |
| Manually search for IOCs across platforms | `"Is this IP malicious? 203.0.113.42"` |
| Browse CVE databases separately | `"Tell me about CVE-2024-3400"` |
| Read lengthy reports | `"Summarize the latest APT29 activity"` |
| Export STIX data manually | `"Get the STIX bundle for this report"` |

---

## Compatible Clients

| Client | Transport | Status |
|:---|:---|:---|
| **VS Code** (GitHub Copilot) | HTTP | Supported |
| **Claude Desktop** | SSE | Supported |
| **Claude Code** (CLI) | HTTP | Supported |
| **Cursor** | HTTP | Supported |
| **Windsurf** | HTTP | Supported |
| **ChatGPT** (Developer Mode) | OpenAPI | Supported |
| Any MCP-compatible client | HTTP / SSE | Supported |

---

## Quick Start

### 1. Get Your API Key

Sign up at **[ti-mindmap-hub.com](https://ti-mindmap-hub.com)** and generate your personal API key from your account settings.

Your API key has the format `tim_xxxxxxxxxxxx`.

### 2. Configure Your Client

<details>
<summary><strong>VS Code (GitHub Copilot)</strong></summary>

Create or edit `.vscode/mcp.json` in your workspace:

```json
{
  "servers": {
    "ti-mindmap": {
      "url": "https://ti-mindmap-mcp.happyfield-b3b5145b.westeurope.azurecontainerapps.io/mcp",
      "headers": {
        "X-API-Key": "${input:tiMindmapApiKey}"
      }
    }
  },
  "inputs": [
    {
      "id": "tiMindmapApiKey",
      "type": "promptString",
      "description": "TI Mindmap HUB API Key",
      "password": true
    }
  ]
}
```

VS Code will prompt you for the API key on first use.

</details>

<details>
<summary><strong>Claude Desktop</strong></summary>

Edit your `claude_desktop_config.json`:

- **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "ti-mindmap": {
      "url": "https://ti-mindmap-mcp.happyfield-b3b5145b.westeurope.azurecontainerapps.io/mcp/sse",
      "transport": "sse",
      "headers": {
        "X-API-Key": "tim_your_api_key_here"
      }
    }
  }
}
```

</details>

<details>
<summary><strong>Claude Code (CLI)</strong></summary>

Add the server via the CLI:

```bash
claude mcp add ti-mindmap \
  --transport http \
  --url https://ti-mindmap-mcp.happyfield-b3b5145b.westeurope.azurecontainerapps.io/mcp \
  --header "X-API-Key: tim_your_api_key_here"
```

</details>

<details>
<summary><strong>Cursor</strong></summary>

In Cursor Settings → MCP, add a new server:

```json
{
  "mcpServers": {
    "ti-mindmap": {
      "url": "https://ti-mindmap-mcp.happyfield-b3b5145b.westeurope.azurecontainerapps.io/mcp",
      "headers": {
        "X-API-Key": "tim_your_api_key_here"
      }
    }
  }
}
```

</details>

<details>
<summary><strong>ChatGPT (Developer Mode)</strong></summary>

1. Go to **Settings → Connectors → Developer Mode**
2. Click **Create Connector**
3. Set the URL: `https://ti-mindmap-mcp.happyfield-b3b5145b.westeurope.azurecontainerapps.io`
4. Add header: `X-API-Key: tim_your_api_key_here`

</details>

### 3. Start Asking

Open your AI assistant and start querying threat intelligence:

```
"Show me the latest threat intelligence reports about ransomware"
```

---

## Available Tools

The MCP server exposes **19 tools** organized in 6 categories.

### Reports

| Tool | Description |
|:---|:---|
| `list_reports` | Search and list threat intelligence reports with filters (search, tags, source, time range) |
| `get_report_details` | Get complete details of a specific report |
| `get_report_content` | Retrieve specific content: AI summary, mindmap, TTPs table, TTPs execution flow, root cause analysis, STIX bundle, or IOCs |
| `get_available_sources` | List all monitored threat intelligence sources |
| `get_available_tags` | List all available tags for filtering |

### CVE Intelligence

| Tool | Description |
|:---|:---|
| `search_cve` | Look up a specific CVE with severity, EPSS score, exploitation status, and related articles |
| `search_cves_by_keyword` | Search CVEs by keyword (vendor, product, description) |
| `list_cves` | Browse all tracked CVEs with pagination and severity filters |
| `get_cves_by_article` | Get all CVEs mentioned in a specific article |
| `get_cve_statistics` | Aggregated CVE statistics: severity distribution, top vendors, exploitation trends |

### IOC Search

| Tool | Description |
|:---|:---|
| `search_ioc` | Search for an Indicator of Compromise — supports IP addresses, domains, file hashes (MD5/SHA1/SHA256), and URLs |

### STIX 2.1 Bundles

| Tool | Description |
|:---|:---|
| `get_stix_bundle` | Download a complete STIX 2.1 bundle for an article (threat actors, malware, attack patterns, indicators, vulnerabilities) |
| `list_stix_bundles` | List all available STIX bundles |
| `get_stix_statistics` | Statistics on generated STIX objects |

### Weekly Briefings

| Tool | Description |
|:---|:---|
| `get_latest_briefing` | Get the latest weekly threat briefing |
| `list_briefings` | List all available weekly briefings |
| `get_briefing_by_date` | Retrieve a briefing for a specific date |

### Platform

| Tool | Description |
|:---|:---|
| `get_statistics` | Platform-wide statistics: total reports, source distribution, trends |
| `submit_article` | Submit a new article URL for automatic AI analysis |

---

## What You Can Ask

Here are some example prompts to try with your AI assistant:

#### Threat Research
> *"Show me the latest reports about APT29"*
>
> *"What are the most recent ransomware campaigns from this week?"*
>
> *"Find reports tagged with 'phishing' from The Hacker News"*

#### Vulnerability Management
> *"Tell me everything about CVE-2024-3400"*
>
> *"List all critical CVEs from the last 30 days"*
>
> *"Which CVEs are currently being exploited in the wild?"*

#### IOC Investigation
> *"Is this IP malicious? 203.0.113.42"*
>
> *"Search for this hash: d41d8cd98f00b204e9800998ecf8427e"*
>
> *"Check if evil-domain.com appears in any threat reports"*

#### Threat Intelligence Feeds
> *"Give me this week's threat briefing"*
>
> *"Summarize the threat landscape for the last 7 days"*

#### STIX & Integration
> *"Get the STIX bundle for this report so I can import it into OpenCTI"*
>
> *"Export threat data in STIX 2.1 format for Microsoft Sentinel"*

#### Article Submission
> *"Analyze this article: https://example.com/threat-report"*

---

## Authentication

All API calls require an API key passed via the `X-API-Key` header.

| Method | Format |
|:---|:---|
| **Header** (recommended) | `X-API-Key: tim_xxxxx` |
| **Bearer Token** | `Authorization: Bearer tim_xxxxx` |

API keys are generated from your account on [ti-mindmap-hub.com](https://ti-mindmap-hub.com).

---

## Monitored Sources

TI Mindmap HUB continuously monitors leading cybersecurity sources including:

- The Hacker News
- BleepingComputer
- Krebs on Security
- Dark Reading
- SecurityWeek
- Recorded Future
- Cisco Talos
- Unit 42 (Palo Alto Networks)
- Microsoft Security Blog
- Google Threat Intelligence
- *...and more*

---

## Architecture Overview

```
┌──────────────────────────────────────┐
│  Your AI Assistant                   │
│  (VS Code / Claude / ChatGPT / ...) │
└──────────────┬───────────────────────┘
               │ MCP Protocol
               │ (HTTP or SSE)
               ▼
┌──────────────────────────────────────┐
│  TI Mindmap MCP Server              │
│  ✦ 19 threat intelligence tools     │
│  ✦ API Key authentication           │
│  ✦ Real-time data access            │
└──────────────┬───────────────────────┘
               │
               ▼
┌──────────────────────────────────────┐
│  TI Mindmap HUB Platform            │
│  ti-mindmap-hub.com                  │
│  ✦ AI-powered analysis engine       │
│  ✦ CVE & IOC databases              │
│  ✦ STIX 2.1 generation              │
│  ✦ Weekly briefing system            │
└──────────────────────────────────────┘
```

---

## Links

| Resource | URL |
|:---|:---|
| **Web Platform** | [ti-mindmap-hub.com](https://ti-mindmap-hub.com) |
| **MCP Server Endpoint** | `https://ti-mindmap-mcp.happyfield-b3b5145b.westeurope.azurecontainerapps.io/mcp` |
| **API Documentation** | [OpenAPI Docs](https://ti-mindmap-mcp.happyfield-b3b5145b.westeurope.azurecontainerapps.io/docs) |
| **MCP Protocol Spec** | [modelcontextprotocol.io](https://modelcontextprotocol.io) |
| **Source Code (Research)** | [ti-mindmap-hub-research](https://github.com/TI-Mindmap-HUB-Org/ti-mindmap-hub-research/) |

---

## Support

- **Issues**: [Open an issue](../../issues) in this repository
- **Platform**: Visit [ti-mindmap-hub.com](https://ti-mindmap-hub.com) for account and platform support

---

## License

This project is licensed under the [MIT License](LICENSE).

---

<div align="center">

**Built with [Model Context Protocol](https://modelcontextprotocol.io)**

Made by [TI Mindmap HUB](https://ti-mindmap-hub.com)

</div>
