# Prax Screening

Cursor plugin that connects the agent to [Prax Data Services](https://mcp.orabrain.com/?src=cursor), the security and compliance intelligence server for financial-services teams, and makes it screen every counterparty **before** code or a workflow pays, signs, ships or onboards. Verdicts come with reasons and references, never a bare score.

## Install

1. Open **Cursor Settings → Plugins**, search for **Prax Screening**, click **Install**.
2. When the `prax` server shows **Needs login**, click it. It opens mcp.orabrain.com: create a free account (no card) or sign in, approve.

Or run `/add-plugin prax-screening` in chat.

Only the MCP server, without the rules: [![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=prax&config=eyJ1cmwiOiAiaHR0cHM6Ly9tY3Aub3JhYnJhaW4uY29tL21jcCJ9)

## MCP

```json
{
  "mcpServers": {
    "prax": {
      "type": "http",
      "url": "https://mcp.orabrain.com/mcp"
    }
  }
}
```

Auth is OAuth 2.1 with dynamic client registration. Cursor registers itself and prompts for the Prax sign-in when the plugin connects; there is no API key to configure. Connected apps are listed in the portal under Account → Connected apps and can be disconnected any time.

## What the agent can do

| Tool | Screens |
| --- | --- |
| `screen_bank` | BIC / IBAN / ABA routing number / LEI: resolution, jurisdiction lists (FATF, EU high-risk, FinCEN 311), sanctions on bank and beneficiary, enforcement |
| `screen_entity` | A person, company, vessel or address against sanctions lists and US export controls (BIS Entity List, Denied Persons, Unverified, MEU, State nonproliferation, ITAR debarred, OFAC non-SDN) |
| `screen_company` | Does the company exist, is it active, who runs it (GLEIF, Companies House, SEC EDGAR) |
| `screen_adverse_media` | Negative news with date, source and link |
| `screen_enforcement` | Regulatory enforcement history of a firm |
| `screen_licence` | MSB, BitLicense, MiCA, VARA, SFC and FCA registrations |
| `screen_country` | FATF, EU, FinCEN 311, OFAC programmes and export-control footprint of a country |
| `screen_domain` / `screen_ip` | Domains, e-mail addresses and IPs before trusting a sender, a payment-instruction change or a login |
| `screen_securities` | ISIN / CUSIP / SEDOL / ticker: NS-CMIC, sectoral sanctions, trading suspensions |
| `screen_cve` | Severity, CISA KEV exploitation, EPSS and fixed versions for a CVE or advisory |
| `screen_package` / `screen_packages` | Known vulnerabilities for a dependency at a version, or an SBOM of up to 50 |
| `screen_wallet` / `screen_transfer` / `analyze_transaction` | EVM addresses, contracts, pre-signature transfers and transaction hashes against Prax threat intelligence; batch variants for 50 at a time |

The hosted server is the source of truth for tool names and schemas. `screen_country` with `{"country": "VN"}` is a free read-only smoke test after connecting.

## Components

- **Rule** `rules/prax-screening.mdc` (always on): the triggers that call for a screen, how to report a verdict, what to do when the server is not connected.
- **Skill** `skills/prax-screening/SKILL.md`: per-tool reporting rules.
- **Commands** `/screen <value>` and `/screen-repo` (every 0x address and direct dependency in the repo, in batches).

## Notes

- Lookups cost 1 credit, batches 10. The free plan includes 10 credits a day; paid plans unlock the company, adverse-media, domain / IP, securities and package tools (`status: upgrade_required` names the gap).
- Prax is read-only intelligence: it never moves funds, signs anything or changes your code.
- Output is licensed for use inside your own product; no resale, redistribution or training. Terms: https://mcp.orabrain.com/portal/terms

## Docs

- Technical reference and plans: https://mcp.orabrain.com
- Server URL: https://mcp.orabrain.com/mcp
- Source and REST examples: https://github.com/Prax-Labs-com/mcp-data-services

## License

MIT
