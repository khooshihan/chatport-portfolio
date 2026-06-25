# chatPort

**AI-powered maritime explorer for the Port of Singapore.**

Singapore is one of the world's busiest maritime hubs, yet most of the public knows little about the vessel movements happening in its waters every day. Maritime data exists, but it has never been made engaging for the public — or efficient for the industry.

chatPort is a showcase of AI-powered features built on MPA Singapore's OCEANS-X platform, demonstrating how conversational AI and the Model Context Protocol (MCP) can transform raw maritime APIs into accessible, visual, and workflow-ready tools.

[chatport.dev](https://chatport.dev)

---

## Features

### AI Chat Assistant (Live)
A conversational interface for querying vessel movements in plain English. Ask about arrivals, departures, and scheduled movements — the AI selects the right OCEANS-X API, fetches live data, and responds conversationally.

### Vessel Map (Live)
An interactive map of Singapore's port waters showing real-time vessel positions. Ask the map assistant in plain language — filter by vessel type, flag, or status, look up a specific ship, or replay a vessel's movement trail over the past 24 hours — and watch the map respond, bridging conversation with spatial awareness.

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
| MCP Servers | Python, FastMCP |
| Backend | Python, FastAPI, Anthropic SDK |
| Frontend | HTML, CSS, JavaScript |
| AI Model | Claude Sonnet 4.6 |
| Data Source | OCEANS-X API (MPA Singapore) |
| Hosting | Railway |

---

## Architecture

```
Browser (Chat UI / Vessel Map)
  |
  |  POST /api/chat  ·  /api/map-chat
  v
FastAPI Backend
  |
  |-- Claude API (reasoning + tool selection)
  |
  |-- MCP Servers (stdio subprocesses)
  |     |-- oceans-x-traffic    — arrivals, departures, due-to, daily shipping state
  |     |-- oceans-x-positions  — live positions, particulars, movement trails
  |     |-- oceans-x-weather    — realtime wind/rainfall + forecasts
  |
  v
OCEANS-X API (MPA Singapore)
  Live maritime data — vessel positions polled every ~15 minutes
```

All API keys are server-side only — nothing is exposed to the browser.

---

## About OCEANS-X

OCEANS-X is MPA Singapore's (Maritime and Port Authority) data and API exchange platform, launched April 2026. It's the successor to SG-MDH (Singapore Maritime Data Hub) and hosts 100+ APIs and datasets for the maritime ecosystem.

This project demonstrates how MCP can make these APIs accessible to non-technical users through conversational AI — and how they can power operational workflows.

Release notes for each version are published under this repository's [Releases](https://github.com/khooshihan/chatport-portfolio/releases).

---

## License

MIT
