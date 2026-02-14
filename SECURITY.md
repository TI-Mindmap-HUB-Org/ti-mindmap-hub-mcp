# Security Policy

## Reporting a Vulnerability

If you discover a security vulnerability related to the TI Mindmap MCP Server or the TI Mindmap HUB platform, please report it responsibly.

**Do NOT open a public issue for security vulnerabilities.**

Instead, please send an email to [info@ti-mindmap-hub.com](mailto:info@ti-mindmap-hub.com).

### What to Include

- Description of the vulnerability
- Steps to reproduce
- Potential impact
- Suggested fix (if any)

### Response Timeline

- **Acknowledgment**: Within 48 hours
- **Initial Assessment**: Within 5 business days
- **Resolution**: Dependent on severity and complexity

## API Key Security

- Never commit API keys to version control
- Use environment variables or secret management tools to store keys
- Rotate your API key immediately if you suspect it has been compromised
- Each API key is scoped to your account and can be revoked from your [account settings](https://ti-mindmap-hub.com)

## Supported Versions

| Version | Supported |
|:--------|:----------|
| 2.x     | Yes       |
| < 2.0   | No        |
