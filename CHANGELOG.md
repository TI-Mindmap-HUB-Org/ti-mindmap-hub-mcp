# Changelog

All notable changes to the TI Mindmap MCP Server will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [2.1.0] - 2026-02-14

### Added
- **MCP Integration documentation** from [ti-mindmap-hub-research](https://github.com/TI-Mindmap-HUB-Org/ti-mindmap-hub-research/tree/main/mcp-integration):
  - `mcp-integration/README.md` — Full protocol details, session management, authentication flow, all 19 tool parameters, architecture diagram, and error codes
  - `mcp-integration/CLAUDE_DESKTOP_SETUP.md` — Step-by-step Claude Desktop setup guide with stdio-to-HTTP bridge
  - `mcp-integration/VSCODE_SETUP.md` — VS Code + GitHub Copilot setup guide with example workflows
  - `mcp-integration/mcp-bridge.js` — Node.js bridge script for stdio-based MCP clients (Claude Desktop)
- Updated main README with links to the new integration docs and setup guides
- Added `mcp.ti-mindmap-hub.com` custom domain endpoint reference

### Changed
- Restricted Compatible Clients table to tested clients only (VS Code, Claude Desktop)
- Removed untested client configurations (Claude Code, Cursor, Windsurf, ChatGPT) from docs and examples
- Replaced GitHub Issues references with email contact (info@ti-mindmap-hub.com) across all files
- Added community contribution note inviting PRs for other MCP client guides

## [2.0.0] - 2025-06-01

### Added
- **19 MCP tools** across 6 categories: Reports, CVE Intelligence, IOC Search, STIX Bundles, Weekly Briefings, and Platform
- **Tested client support**: VS Code (GitHub Copilot), Claude Desktop
- **HTTP and SSE transport** for broad client compatibility
- **API Key authentication** with secure key management
- **CVE Intelligence tools**: search by ID, keyword, severity, and article association
- **STIX 2.1 bundle export** compatible with MISP, OpenCTI, and Microsoft Sentinel
- **IOC search** across IP addresses, domains, file hashes, and URLs
- **Weekly threat briefings** with curated threat landscape analysis
- **Article submission** for on-demand AI analysis
- **Report content access**: summaries, mindmaps, TTPs, root cause analysis
- **Platform statistics** and aggregated analytics
