# ChatPort

**AI-powered vessel movement assistant for the Port of Singapore.**

ChatPort is an MCP server that wraps Singapore's OCEANS-X maritime data APIs, paired with a chatbot demo showing how AI-powered data access could be embedded in the OCEANS-X portal or any maritime application. Users ask natural language questions about vessel movements and get conversational answers backed by live data.

[chatport.dev](https://chatport.dev)

---

## Why I Built This

MPA Singapore launched OCEANS-X in April 2026 — a data exchange platform with 100+ maritime APIs. The APIs are powerful but require technical knowledge to query. I wanted to demonstrate how MCP (Model Context Protocol) could make these APIs accessible to non-technical maritime stakeholders through conversational AI, turning raw API endpoints into a natural language interface.

## Tech Stack

| Layer | Technology |
|---|---|
| MCP Server | Python, FastMCP |
| Backend | Python, FastAPI, Anthropic SDK |
| Frontend | HTML, CSS, JavaScript |
| AI Model | Claude Sonnet 4.6 |
| Data Source | OCEANS-X API (MPA Singapore) |
| Hosting | Railway |

## Key Features

- **Natural language queries** — ask about arrivals, departures, and scheduled movements in plain English
- **Live data** — connected to MPA Singapore's OCEANS-X platform (updated hourly)
- **MCP architecture** — AI model discovers and calls tools through the Model Context Protocol, not hardcoded integrations
- **Token and cost transparency** — every response shows input/output tokens and estimated cost
- **Maritime-themed UI** — dark, professional chat interface styled for portal embedding
- **Zero build step** — frontend is plain HTML/CSS/JS, no Node.js required

## Architecture

```
Browser (Chat UI)
  |
  |  POST /api/chat
  v
FastAPI Backend
  |
  |-- Claude API (reasoning + tool selection)
  |
  |-- MCP Server (stdio subprocess)
  |     |-- get_vessel_arrivals
  |     |-- get_vessel_departures
  |     |-- get_vessels_due_to_arrive
  |     |-- get_vessels_due_to_depart
  |
  v
OCEANS-X API (MPA Singapore)
  Live vessel movement data — updated hourly
```

All API keys are server-side only — nothing is exposed to the browser.

## What is MCP?

**Model Context Protocol (MCP)** is an open standard that lets AI models access external tools and data sources in a structured, discoverable way. Think of it as a USB-C port for AI — any MCP-compatible model can plug into any MCP server and use its tools without custom integration code.

In this project, the MCP server exposes four tools for querying vessel data. Claude discovers these tools automatically and decides when to call them based on the user's question.

## What's Next

The core integration is working: ask a question, get live vessel data. The next priorities are around capability and presentation: streaming responses to reduce perceived latency, and chart generation so users can visualise vessel movement patterns rather than reading text summaries.

The bigger opportunity is expanding the MCP server to cover more of OCEANS-X's API catalogue — anchorage data, port facilities, weather conditions — building toward a comprehensive maritime intelligence assistant. Each additional tool makes the conversational interface more valuable as a single point of access to the platform.

---

Built by [Shi Han](https://www.shkhoo.com)
