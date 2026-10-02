# invowerk

[![smithery badge](https://smithery.ai/badge/podshalocef/invowerk)](https://smithery.ai/servers/podshalocef/invowerk)

**German e-invoice checker: ZUGFeRD/Factur-X PDFs incl. PDF/A, XRechnung via the KoSIT validator, Peppol BIS. Free web tool, API, MCP.**

invowerk checks e-invoices: ZUGFeRD 2.5.2 and Factur-X 1.09.2 PDFs, XRechnung 3.0.2 (UBL and CII) and Peppol BIS Billing 3.0.21. XRechnung goes through the KoSIT validator. PDFs are also checked for PDF/A and against their embedded invoice data. Common rule messages come with cause and fix in German. Each check returns a report with the file's SHA-256, time, rule sets and result. The Prüfstand test files and their expected results are public. Invoices are processed in memory, not stored. Free web tool; REST API and MCP server with 500 free credits per month.

## Quickstart

Check an e-invoice in one call. The anonymous tier needs no key; add
`-H "X-API-Key: $INVOWERK_API_KEY"` for your plan's limits.

```sh
curl -sO https://invowerk.dev/app-static/demo/beispiel-xrechnung.xml
curl -F file=@beispiel-xrechnung.xml https://api.invowerk.dev/v1/validate
```

```json
{
  "valid": true,
  "verdict_source": "official",
  "official_verdict": "valid",
  "scenario": {"config": "kosit-xrechnung", "name": "EN16931 XRechnung (UBL Invoice)"},
  "detection": {"kind": "xml", "syntax": "ubl_invoice", "flavor": "xrechnung"},
  "errors": {"format": [], "business_rules": [], "carrier": []},
  "findings": [],
  "evidence": {"document_sha256": "259e3eff…", "checked_at": "2026-10-01T22:36:49Z"}
}
```

The same call takes a ZUGFeRD or Factur-X PDF. A failed check is still HTTP 200,
with `valid: false` and each problem in `findings`.

## Use it from

### MCP server

Streamable-HTTP endpoint: `https://api.invowerk.dev/mcp/` — the anonymous
tier works without a key; an API key raises the limits.

Claude Code:

```sh
claude mcp add --transport http invowerk https://api.invowerk.dev/mcp/
```

Claude Code: `/plugin marketplace add invowerk-dev/invowerk` then `/plugin install invowerk@invowerk` (set `INVOWERK_API_KEY` for your key).

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

**Integrations** (n8n, Zapier, Make, Dify, SDKs and templates): https://github.com/invowerk-dev/invowerk-integrations

## Links

- **Website:** https://invowerk.dev/go/github
- **API docs:** https://api.invowerk.dev/docs · [OpenAPI](https://api.invowerk.dev/openapi.json)
- **Pricing:** https://invowerk.dev/pricing
- **E-Rechnung kostenlos prüfen:** https://invowerk.dev/tools/e-rechnung-pruefen
- **llms.txt:** https://invowerk.dev/llms.txt
- **Privacy policy:** https://invowerk.dev/privacy
- **Support:** https://invowerk.dev/support

## API

Base URL `https://api.invowerk.dev/` — authenticate with an `X-API-Key` header;
anonymous calls work at a lower rate limit.

## About the files here

- `.claude-plugin/` — Claude Code plugin, with this repo as its own marketplace.
- `.mcp.json` — the MCP server the Claude Code plugin connects to.
- `gemini-extension.json` — Gemini CLI extension manifest.
- `glama.json` — Glama server claim (names the maintainer).
- `mcp.json` — Agent Plugins 1.0 MCP server config.
- `plugin.json` — Agent Plugins 1.0 plugin manifest.
- `server.json` — the entry in the official MCP Registry.
- `skills/` — an Agent Skill (agentskills.io SKILL.md) for skill galleries.
