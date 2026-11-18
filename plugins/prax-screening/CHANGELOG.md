# Changelog

## 1.4.1

- Rule is applied by description instead of always-on, scoped to money, counterparty and security tasks with a concrete identifier.
- Agent sends only the identifier being screened, never file contents or credentials.
- Agent recommends; it no longer inserts screening calls into the user's code.

## 1.4.0

- Initial Cursor release. Version matches the Prax Data Services MCP server and the Claude plugin.
- `prax` MCP server at `https://mcp.orabrain.com/mcp` (OAuth sign-in, no key to paste).
- Rule `prax-screening`: when to screen, how to report, what to do when not connected.
- Skill `prax-screening`: per-tool reporting rules for all 14 tools.
- Commands `/screen` and `/screen-repo`.
