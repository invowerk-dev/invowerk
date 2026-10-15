---
name: "invowerk"
description: "E-invoice checker for ZUGFeRD, Factur-X, XRechnung and Peppol BIS. Free web tool, API and MCP. Use it through the invowerk MCP server at https://api.invowerk.dev/mcp/ — the anonymous tier needs no key."
license: "MIT"
compatibility: "Needs network access to https://api.invowerk.dev/mcp/; an API key is optional."
---

# invowerk

invowerk creates and checks e-invoices. In the browser it creates ZUGFeRD PDFs and XRechnung from a form and checks each file before download. It checks ZUGFeRD 2.5.2 and Factur-X 1.09.2 PDFs, XRechnung 3.0.2 (UBL and CII) and Peppol BIS Billing 3.0.21. XRechnung goes through the KoSIT validator; PDFs are also checked for PDF/A. Each check returns a report with the file's SHA-256, rule sets and result. Invoices are processed in memory, not stored. Free web tool; REST API and MCP server with 500 free credits a month.

## Connect

- MCP endpoint (streamable HTTP): https://api.invowerk.dev/mcp/ — the anonymous tier works without a key.
- An API key raises the limits: send it in the `X-API-Key` header. The Claude Code plugin reads it from `INVOWERK_API_KEY`.
- API reference: https://api.invowerk.dev/docs

Maintained by the invowerk team.
