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

---

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

---

## Setup

### Prerequisites

- Python 3.12+
- An [OCEANS-X API key](https://oceans-x.mpa.gov.sg) (free registration)
- An [Anthropic API key](https://console.anthropic.com)

### Installation

```bash
# Clone the repo
git clone https://github.com/khooshihan/chatport_demo.git
cd chatport_demo

# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Configure environment
cp .env.example .env
# Edit .env with your API keys
```

### Running

```bash
cd demo-app/backend
uvicorn main:app --reload --port 8000
```

Open http://localhost:8000 in your browser.

The FastAPI backend automatically spawns the MCP server as a subprocess — no separate process needed.

---

## Project Structure

```
chatport_demo/
├── mcp-server/
│   ├── server.py              # FastMCP server — 4 vessel movement tools
│   └── requirements.txt
├── demo-app/
│   ├── backend/
│   │   ├── main.py            # FastAPI app, Claude tool-use loop, cost tracking
│   │   ├── mcp_client.py      # MCP client (stdio subprocess transport)
│   │   └── requirements.txt
│   └── frontend/
│       ├── index.html         # Chat UI
│       ├── style.css          # Maritime dark theme
│       └── app.js             # Chat logic, token display
├── .env.example
├── .gitignore
└── README.md
```

---

## About OCEANS-X

OCEANS-X is MPA Singapore's (Maritime and Port Authority) data and API exchange platform, launched April 2026. It's the successor to SG-MDH (Singapore Maritime Data Hub) and hosts 100+ APIs and datasets for the maritime ecosystem.

This project demonstrates how MCP can make these APIs accessible to non-technical users through conversational AI — and how they can power operational workflows.

---

## Release Notes

**Latest: [v1.5.1](https://github.com/khooshihan/chatport_demo/releases/tag/v1.5.1) — Chat Rendering & Map Narrative Accuracy** (2026-06-25)

- The Vessel Map assistant now describes vessel movements using coordinates and general areas instead of guessing specific terminal names — so its descriptions always match the positions shown on the map
- Chat replies render formatting (headings, tables, lists, links) consistently across both the main chat and the map panel
- Added an automated frontend test suite that runs in CI to catch formatting regressions before release

See the [full release history](https://github.com/khooshihan/chatport_demo/releases) for earlier versions.

---

## License

MIT
