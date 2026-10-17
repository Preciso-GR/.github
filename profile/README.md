<div align="center">
  <h1><img src="https://raw.githubusercontent.com/Preciso-GR/.github/main/profile/assets/preciso-logo.png" alt="PRECISO — document knowledge connected for agents" width="640" /></h1>
  <p><strong>Connect your agent to a persistent graph of document evidence.</strong></p>
  <p>Local-first GraphRAG · Model Context Protocol · Reviewed document updates</p>
  <p>
    <a href="https://github.com/Preciso-GR/preciso-graphrag">Core server</a> ·
    <a href="https://pypi.org/project/preciso-graphrag/">PyPI</a> ·
    <a href="https://github.com/Preciso-GR/preciso-graphrag/blob/main/docs/simple-setup.md">Setup guide</a>
  </p>
</div>

## What PRECISO does

PRECISO is a **GraphRAG MCP server for AI agents**. GraphRAG combines graph
connections with retrieval of relevant text. MCP (Model Context Protocol) lets
your agent call the server's tools.

Your agent reads authorized documents and extracts entities, relationships, and
source passages. PRECISO validates and stores that extraction. The agent can then
retrieve evidence, follow connections, and maintain the collection across sessions.

```text
Documents → Your agent extracts facts → PRECISO validates and stores
                                               ↓
Questions → Your agent retrieves evidence ← Graph + source passages
                         ↓
                Answer with source evidence
```

The agent controls the work. The server does not parse raw PDFs, crawl URLs, watch
folders, or continue reasoning after the agent disconnects. No separate extraction
language model or web frontend is required by the core server.

## Who can use it?

PRECISO is intended for people who repeatedly investigate document collections.
These are possible workflows; they are not validated outcomes for every domain.

| Audience | Example investigation |
|---|---|
| Financial and business analysts | How did risks and segment performance change across these filings? |
| Researchers and research engineers | Which studies support this claim, and where do findings disagree? |
| Healthcare and life-sciences researchers | How do these studies differ in population, intervention, outcomes, and limitations? |
| Supply-chain and procurement analysts | Which products depend on this supplier, according to these documents? |
| Consultants and diligence teams | Which source supports each conclusion in this assessment? |
| Legal and compliance professionals | Which documents support this obligation or control? |
| Product and support teams | Which customer problems relate to this release and its known limitations? |
| Developers and maintainers | Why was this design chosen, and which constraints still apply? |

Start with a small, reviewed corpus and one recurring question. Financial reports
are closest to the existing evaluations. Healthcare examples concern public
research synthesis; patient-care workflows are not validated. The core server
contains no supply-chain application or domain-specific business workflow.

An individual analyst inside a company fits the current local workflow. A shared
company knowledge service requires additional authorization, isolation, and
concurrent-access design.

## Try it with your agent

The **0.3.0rc2 release candidate** has guided setup for **macOS with Codex CLI,
Claude Code CLI, or both**. Install uv, Python 3.11 or later, and your chosen agent
CLI. Run this command from your project directory:

```sh
uvx --from preciso-graphrag==0.3.0rc2 preciso-graphrag setup --project .
```

No repository clone is required. The wizard asks which agent to connect and whether
to use local or API embeddings. It asks before model downloads and agent
registration, then verifies the provider and MCP connection.

- **Built-in local default:** IBM Granite Small English R2 through FastEmbed. One model download; no Ollama or embedding API key.
- **Ollama:** use a supported installed model. Setup can start an installed but stopped local service after confirmation.
- **API:** use OpenAI or Cohere credentials. Text is sent to the selected provider and usage can incur charges.

Reload your agent and give it access to your documents. Start with:

```text
Call get_server_status and get_document_workflow.
Prepare these documents using the returned extraction requirements.
Show the source IDs, extraction counts, validation results, and unresolved concerns.
Ingest the reviewed extractions within this task, then answer my question
with source evidence. State when the evidence is insufficient.
```

Guided registration does not require a project `.mcp.json`. Selecting both agents
points them to the same collection. **Only one active runtime may own a collection.**
Stop one agent's PRECISO server before switching to the other.

See the [setup and recovery guide](https://github.com/Preciso-GR/preciso-graphrag/blob/main/docs/simple-setup.md)
for downloads, credentials, and project storage.

## Keep your knowledge current

Add new documents later. Replace a tracked document with its complete corrected
extraction, or delete its contribution. Inspect and maintain graph records through
supported isolation, restoration, removal, rename, merge, and disconnect operations.

Changes use previews and workspace revisions. Replacement, deletion, and graph
edits rebuild derived data from retained extractions and require a complete
contribution ledger. Isolation can withhold other claims in the same passage.
These operations do not provide secure erasure or user authorization.

Read the [document lifecycle guide](https://github.com/Preciso-GR/preciso-graphrag/blob/main/docs/document-lifecycle.md)
for operation-specific limits.

## Repositories

| Repository | Role |
|---|---|
| [preciso-graphrag](https://github.com/Preciso-GR/preciso-graphrag) | Core MCP server: document lifecycle, graph storage, retrieval, evidence, and optional exports |
| [skills_for_preciso](https://github.com/Preciso-GR/skills_for_preciso) | Agent extraction instructions for financial, research, and general documents |
| [preciso-agent-](https://github.com/Preciso-GR/preciso-agent-) | Separate financial reference agent; not required for the core server |
| [Preciso-web-](https://github.com/Preciso-GR/Preciso-web-) | Separate frontend and visualization project; not required for the core server |

Related applications have their own dependencies and setup instructions. Their
availability does not mean they share the core server's verification status.

## Current scope

- Individual local use, with one runtime per collection. Shared multi-user authorization is not implemented.
- Guided setup is verified on macOS. Windows and Linux automated setup remain unverified.
- A Linux Docker image is available. Native Windows support needs additional work.
- The default embedding model targets English. Retrieval quality depends on your corpus and extraction quality.
- Retrieved passages are evidence candidates, not proof that an answer is correct. Review the sources.
- Historical financial evaluations do not establish accuracy across domains or for the current default model.

See [evaluation methodology](https://github.com/Preciso-GR/preciso-graphrag/blob/main/docs/eval-guide.md),
[embedding measurements](https://github.com/Preciso-GR/preciso-graphrag/blob/main/docs/embedding-model-selection.md),
and [production readiness](https://github.com/Preciso-GR/preciso-graphrag/blob/main/docs/production-readiness.md)
for evidence and remaining release gates.

## Contribute

Report core defects and propose focused improvements in
[preciso-graphrag](https://github.com/Preciso-GR/preciso-graphrag).
Include a reproducible example and remove private document content from public
reports. Read the [contribution guide](https://github.com/Preciso-GR/preciso-graphrag/blob/main/CONTRIBUTING.md).

To extend extraction to another domain, contribute instructions and reviewed
examples to [skills_for_preciso](https://github.com/Preciso-GR/skills_for_preciso).
