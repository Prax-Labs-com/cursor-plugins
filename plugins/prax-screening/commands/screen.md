---
name: screen
description: Screen a bank (BIC / IBAN / ABA / LEI), company, person, country, domain, IP, security, CVE, package, 0x address, tx hash or transfer with Prax Data Services
---
Screen the value(s) the user typed after this command with the `prax` tools and report per the prax-screening rule (verdict and reason first, then evidence, then the action):

- BIC (8 or 11 chars), IBAN, 9-digit routing number or 20-char LEI: `screen_bank` (pass a beneficiary name if given)
- company or firm name with words like bank, payments, exchange, fintech, MSB: `screen_entity`, `screen_enforcement`, `screen_licence`, `screen_company`
- any other person or company name: `screen_entity` and `screen_adverse_media`
- country name or ISO code: `screen_country`
- domain, URL or e-mail address: `screen_domain`
- IPv4 or IPv6 address: `screen_ip`
- ISIN, CUSIP, SEDOL or ticker: `screen_securities`
- CVE-YYYY-NNNN or GHSA id: `screen_cve`
- ecosystem/name@version (e.g. npm/lodash@4.17.20): `screen_package`
- 40-hex address: `screen_wallet` (chain eth unless the user said otherwise)
- 64-hex hash: `analyze_transaction`
- "from to amount [asset]": `screen_transfer`

If nothing was typed after the command, ask what to screen.
