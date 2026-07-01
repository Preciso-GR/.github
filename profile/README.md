<div align="center">

# Preciso

**Precise knowledge graphs from your documents.**

*Named after Bruno Fernandes. Every pass lands exactly where it needs to.*

[![](https://img.shields.io/badge/Codex-Agent-111111?style=for-the-badge)](https://github.com/Preciso-GR/preciso-graphrag)
[![](https://img.shields.io/badge/Claude%20Code-Agent-C8102E?style=for-the-badge)](https://github.com/Preciso-GR/preciso-graphrag)
[![](https://img.shields.io/badge/Copilot-Agent-7F1D1D?style=for-the-badge)](https://github.com/Preciso-GR/preciso-graphrag)

</div>

---

## What is Preciso

Preciso turns unstructured documents into structured, queryable knowledge graphs — without a fixed extraction pipeline baked into the server. Instead, an **agent** (with its own file tools and an LLM) reads a **skill** — a plain-markdown spec describing what entities and relationships matter for a given domain — and writes structured extractions to disk. The MCP server never parses the domain logic itself; it only ingests the resulting extraction JSON, reconciles it against the graph, and serves it back for querying.

This split keeps the core engine small, auditable, and domain-agnostic, while the extraction logic stays swappable, versionable, and community-owned.

**Benchmark:** 95.4% accuracy with zero hallucinations across 23 test cases on a Walmart 10-K extraction benchmark.

---

## How it fits together

```
                 ┌─────────────────────┐
   documents ──► │   skill (markdown)   │  ← domain-specific extraction spec
                 │   read by an agent    │     (financial, general, research…)
                 └──────────┬───────────┘
                             │ writes extraction JSON
                             ▼
                 ┌─────────────────────┐
                 │   preciso-graphrag    │  ← MCP server: ingest, reconcile,
                 │   (core engine)        │     store, query the graph
                 └──────────┬───────────┘
                             │ MCP tools
                             ▼
                 ┌─────────────────────┐
                 │       Preciso          │  ← web frontend + visualizer
                 │   (marketing + UI)      │     (d3-force graph, streaming LLM)
                 └─────────────────────┘
```

---

## Repositories

| Repo | What it is | Visibility |
|---|---|---|
| **[preciso-graphrag](https://github.com/Preciso-GR/preciso-graphrag)** | The core MCP server — ingestion, patch-based reconciliation, storage, and query tools. Apache 2.0, with BUSL 1.1 attribution for adapted LightRAG code. | Public |
| **[skills_for_preciso](https://github.com/Preciso-GR/skills_for_preciso)** | Community-contributed extraction skills — markdown specs defining entity/relationship schemas per domain (financial filings, codebases, research papers, and more). | Public |
| **[preciso-agent-](https://github.com/Preciso-GR/preciso-agent-)** | A showcase agent built on Preciso, integrating OpenBB and Groq to demonstrate real-world graph-backed financial analysis. | Public |


---

## Design principles

- **The graph creation process is the tool.** Extraction isn't a hidden pipeline — it's a markdown skill the agent can read, reason about, and follow, the same way a human analyst would follow a style guide.
- **Provider-agnostic.** Bring your own LLM, embedding model, and coding agent. Preciso doesn't lock you into a single stack.
- **File-based handoff.** Agents write extractions to disk; the server ingests and reconciles. This keeps agent reasoning and server logic decoupled and independently testable.
- **Skills are content, not code.** New domains ship as `.md` files, not server changes — anyone can contribute a skill without touching the core engine.

---

## Getting started

```bash
git clone https://github.com/Preciso-GR/preciso-graphrag.git
cd preciso-graphrag
# see the repo README for MCP server setup and skill configuration
```

Point your `.mcp.json` at the server, drop a skill from `skills_for_preciso` (or write your own) into `skills/`, and start extracting.

---

## Contributing

Skill contributions are the easiest way to extend Preciso to a new domain — see [skills_for_preciso](https://github.com/Preciso-GR/skills_for_preciso) for the format and examples (financial-graph-extraction, general-graph-extraction, research-paper-graph-extraction). Core engine contributions and issues go to [preciso-graphrag](https://github.com/Preciso-GR/preciso-graphrag).

</div>
