# chatPort

**AI-powered maritime explorer for the Port of Singapore.**

Singapore is one of the world's busiest maritime hubs, yet most of the public knows little about the vessel movements happening in its waters every day. Maritime data exists, but it has never been made engaging for the public — or efficient for the industry.

chatPort is a showcase of AI-powered features built on MPA Singapore's OCEANS-X platform, demonstrating how conversational AI and the Model Context Protocol (MCP) can transform raw maritime APIs into accessible, visual, and workflow-ready tools.

[chatport.dev](https://chatport.dev)

---

## Features

### AI Chat Assistant (Live)
A conversational interface for querying vessel movements in plain English. Ask about arrivals, departures, and scheduled movements — the AI selects the right OCEANS-X API, fetches live data, and responds conversationally.

### Vessel Map (Coming Soon)
An interactive map of Singapore's port waters showing real-time vessel positions. Query the chat and watch the map respond — bridging conversation with spatial awareness.

### MCP Workflow Exploration (Coming Soon)
Demonstrating how multiple OCEANS-X MCP tools can be chained together for multi-step maritime queries — showing the protocol's potential for orchestrating complex workflows beyond simple Q&A.

---

## Why MCP?

**Model Context Protocol (MCP)** is an open standard that lets AI models discover and use external tools without custom integration code. In chatPort, Claude doesn't have hardcoded knowledge of OCEANS-X APIs — it discovers available tools through MCP and decides which to call based on the user's question.

This matters for maritime: OCEANS-X hosts 100+ APIs. MCP means adding a new data source is adding a tool definition, not rewriting application logic. The workflow exploration extends this further — chaining multiple tools to answer complex queries that span several API calls.

---

## Tech Stack

| Layer | Technology |
|---|---|
| MCP Server | Python, FastMCP |
| Backend | Python, FastAPI, Anthropic SDK |
| Frontend | HTML, CSS, JavaScript |
| AI Model | Claude Sonnet 4.6 |
| Data Source | OCEANS-X API (MPA Singapore) |
| Hosting | Railway |

## Architecture

```
Browser (Chat UI / Map / Clearance POC)
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
  |     |-- (more tools planned)
  |
  v
OCEANS-X API (MPA Singapore)
  Live vessel movement data — updated hourly
```

All API keys are server-side only — nothing is exposed to the browser.

## What's Next

The core chat interface is live. The next priorities are the vessel map — giving spatial context to the data already flowing through the chat — and expanding the MCP server to cover more of OCEANS-X's API catalogue, exploring how tool chaining can answer complex multi-step queries. Each feature extends the same MCP backbone: new tools, same architecture.

---

Built by [Shi Han](https://www.shkhoo.com)
