# invowerk

**E-Rechnung prüfen: ZUGFeRD und XRechnung**

invowerk checks e-invoices: ZUGFeRD 2.5.2 and Factur-X 1.09.2 PDFs, XRechnung 3.0.2 (UBL and CII) and Peppol BIS Billing 3.0.21. XRechnung goes through the KoSIT validator. PDFs are also checked for PDF/A and against their embedded invoice data. Common rule messages come with cause and fix in German. Each check returns a report with the file's SHA-256, time, rule sets and result. The Prüfstand test files and their expected results are public. Invoices are processed in memory, not stored. Free web tool; REST API and MCP server with 500 free credits per month.

## Links

- **Website:** https://invowerk.dev/go/github
- **API docs:** https://api.invowerk.dev/docs · [OpenAPI](https://api.invowerk.dev/openapi.json)
- **Pricing:** https://invowerk.dev/pricing
- **E-Rechnung kostenlos prüfen:** https://invowerk.dev/tools/e-rechnung-pruefen
- **llms.txt:** https://invowerk.dev/llms.txt

## MCP server

Streamable-HTTP endpoint: `https://api.invowerk.dev/mcp/` — the anonymous
tier works without a key; an API key raises the limits.

Claude Code:

```sh
claude mcp add --transport http invowerk https://api.invowerk.dev/mcp/
```

Cursor / Windsurf / Cline / Claude Desktop:

```json
{
  "mcpServers": {
    "invowerk": {
      "url": "https://api.invowerk.dev/mcp/"
    }
  }
}
```

One-click installs for every client: https://invowerk.dev/connect

## API

Base URL `https://api.invowerk.dev/` — authenticate with an `X-API-Key` header;
anonymous calls work at a lower rate limit.
