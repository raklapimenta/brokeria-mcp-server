# BrokerIA MCP Server

**The first real estate MCP server in Brazil.** Search properties, simulate financing, qualify leads, and schedule visits — directly from Claude, Gemini, ChatGPT, or any MCP-compatible AI assistant.

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![MCP](https://img.shields.io/badge/MCP-1.0-green.svg)](https://modelcontextprotocol.io)

## What it does

| Tool | Description |
|------|-------------|
| `brokeria_buscar_imoveis` | Search 309+ properties across 10+ agencies with natural language or filters |
| `brokeria_detalhes_imovel` | Full property details: photos, specs, pricing, location |
| `brokeria_simular_financiamento` | Brazilian mortgage calculator (SAC/PRICE systems) |
| `brokeria_qualificar_lead` | Register leads in the CRM with automatic broker assignment |
| `brokeria_agendar_visita` | Schedule property visits |

## Quick Start

### Gemini CLI

```bash
gemini extensions install https://github.com/raklapimenta/brokeria-mcp-server
```

### Claude Desktop / Claude Code

Add to your MCP settings:

```json
{
  "mcpServers": {
    "brokeria-imoveis": {
      "url": "https://mcp.brokeria.com.br/mcp"
    }
  }
}
```

### Any MCP Client (Streamable HTTP)

Connect to: `https://mcp.brokeria.com.br/mcp`

No authentication required for property search. The server uses Streamable HTTP transport (JSON-RPC 2.0).

## Example Queries

Try asking your AI assistant:

- "Find me a 2 bedroom apartment in Campinas under R$ 300,000"
- "Show me houses for sale in Jardim Botanico with at least 3 bedrooms"
- "Simulate a R$ 500,000 mortgage with R$ 100,000 down payment"
- "What properties does KasaMais have available?"

## Architecture

- **Runtime**: Cloudflare Workers (global edge)
- **Database**: Supabase (PostgreSQL + pgvector for semantic search)
- **Search**: Hybrid — vector embeddings (OpenAI) + traditional filters
- **Transport**: Streamable HTTP (MCP 2025-03-26 spec)
- **Security**: Anonymous read access, service-key for writes (lead/visit creation)

## Endpoints

| Path | Method | Description |
|------|--------|-------------|
| `/` | GET | Health check + server info |
| `/mcp` | POST | MCP JSON-RPC endpoint |
| `/mcp` | GET | Session initialization |
| `/mcp` | DELETE | Session termination |
| `/docs` | GET | API documentation |
| `/privacy` | GET | Privacy policy (LGPD compliant) |

## Privacy

- Property searches are anonymous — no personal data collected
- Lead registration and visit scheduling store only voluntarily provided contact info
- Multi-tenant data isolation via Row Level Security (RLS)
- LGPD compliant — full privacy policy at [mcp.brokeria.com.br/privacy](https://mcp.brokeria.com.br/privacy)

## About BrokerIA

BrokerIA is a SaaS platform for Brazilian real estate agencies, providing WhatsApp automation, CRM, AI-powered sales assistants, and Meta Ads management. This MCP server makes our property catalog accessible to any AI assistant.

**Website**: [brokeria.com.br](https://brokeria.com.br)
**MCP Endpoint**: [mcp.brokeria.com.br](https://mcp.brokeria.com.br)

## License

MIT
