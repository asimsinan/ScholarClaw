![ScholarClaw logo](logo.png)

[Türkçe](README.tr.md) / **English**

# ScholarClaw

Proposal-first research, grounded in evidence.

> Terminal-first today. Full end-to-end web interface coming soon.

ScholarClaw is a research system for people who want stronger research judgment, not just faster output.

It is built for a different kind of workflow: one that tests the idea before it tries to finish the paper.

Instead of rushing from prompt to output, ScholarClaw investigates related work, questions novelty, surfaces weak spots, and helps turn rough concepts into stronger, more defensible proposals and papers.

## What It Does

ScholarClaw helps researchers:

- search the literature that actually matters for the field
- see whether an idea is novel, crowded, or still unclear
- strengthen proposals before time is spent on execution
- keep the work grounded in evidence from the start
- carry the work forward through execution, review, revision, and publication when the foundation is strong

## Key Capabilities

- 29-stage research pipeline spanning proposal, execution, publication, review, and revision
- OpenAlex-first API retrieval backed by Semantic Scholar and arXiv, plus agentic browser retrieval across scholarly sites
- Literature year-window and depth controls for tighter, more intentional review
- Novelty checking, citation verification, and citation relevance pruning
- Publication-aware writing with pluggable publication families and custom LaTeX template support
- Parallel reviewer workflows with editor synthesis and structured revision planning
- Stage-specific model routing, checkpoint/resume support, and local-model friendly operation
- Benchmark-aware experiment planning and figure-planning/chart-generation paths

## Full Feature Comparison with AutoResearchClaw

| Feature | ScholarClaw | AutoResearchClaw | Notes |
| --- | --- | --- | --- |
| Staged research pipeline | ✓ | ✓ | ScholarClaw currently uses a 29-stage pipeline; AutoResearchClaw documents a 23-stage pipeline. |
| **Agentic browser retrieval across scholarly sites** | ✓ | ✓ | **Core ScholarClaw emphasis:** both projects support browser-based collection, but ScholarClaw treats source-aware browser retrieval as a first-class literature path rather than a side toggle. |
| Bucketed execution | ✓ | ✗ | ScholarClaw exposes `proposal`, `execution`, `publication`, `review`, and `revision` buckets as direct run scopes. |
| Dedicated external review bucket | ✓ | ✗ | ScholarClaw separates external review into its own post-publication review flow. |
| Dedicated external revision bucket | ✓ | ✗ | ScholarClaw separates external revision into its own follow-up workflow rather than burying it inside publication. |
| OpenAlex / Semantic Scholar / arXiv retrieval | ✓ | ✓ | Both projects use a real multi-source literature path centered on OpenAlex, Semantic Scholar, and arXiv. |
| Headless browser retrieval mode | ✓ | ✗ | ScholarClaw supports visible or headless browser automation for literature search workflows. |
| Explicit browser target registry | ✓ | ✗ | ScholarClaw ships first-class browser targets for Semantic Scholar, arXiv, Elsevier / ScienceDirect, Springer, IEEE Xplore, Google Scholar, and Web of Science. |
| Year window controls | ✓ | ✗ | ScholarClaw supports recent-year presets and explicit `start_year` / `end_year` bounds. |
| Retrieval depth controls | ✓ | ✗ | ScholarClaw supports `fast`, `standard`, `deep`, and `exhaustive` retrieval policies. |
| Search hardening and deduplication | ✓ | ✓ | Both harden search behavior and deduplicate literature results. |
| Proposal / goal grounding | ✓ | ✗ | ScholarClaw explicitly grounds early proposal artifacts with collected and verified evidence. |
| Multiple screening modes | ✓ | ✗ | ScholarClaw exposes `deterministic`, `llm`, and `hybrid` literature screening modes. |
| Novelty and positioning checks | ✓ | ✗ | ScholarClaw explicitly foregrounds novelty and positioning support in the workflow. |
| Citation verification | ✓ | ✓ | Both verify citations through multiple layers rather than trusting raw generation. |
| Citation relevance pruning | ✓ | ✓ | Both include relevance-aware citation cleanup. |
| Publication-aware writing | ✓ | ✓ | AutoResearchClaw focuses on conference-oriented writing; ScholarClaw extends this toward publication-family-aware behavior. |
| Custom LaTeX template path | ✓ | ✗ | ScholarClaw allows a user-provided LaTeX template path in addition to template selection behavior. |
| BenchmarkAgent | ✓ | ✓ | Both include benchmark-aware experiment support. |
| FigureAgent | ✓ | ✓ | Both include figure-generation paths. |
| Parallel reviewer workflows | ✓ | ✓ | Both support multi-agent review. |
| Resumable review manifests | ✓ | ✗ | ScholarClaw persists reviewer outputs and manifests so finished reviews can be reused. |
| Structured revision planning | ✓ | ✗ | ScholarClaw builds revision plans directly from editor and reviewer outputs. |
| Stage-specific model routing | ✓ | ✗ | ScholarClaw lets different model choices be assigned to different stage groups through YAML. |
| Local-model friendly LM Studio / Ollama path | ✓ | ✗ | ScholarClaw explicitly documents local OpenAI-compatible operation with LM Studio and Ollama-style setups. |
| ACP-compatible execution | ✓ | ✓ | Both projects expose ACP-compatible execution paths. |
| Checkpoint and resume | ✓ | ✓ | Both support resumable long runs. |
| Persisted sub-stage recovery | ✓ | ✗ | AutoResearchClaw has repair loops and checkpoint-oriented HITL modes; ScholarClaw additionally persists more fine-grained sub-stage state and review artifacts. |
| `validate` / `doctor` / `report` commands | ✓ | ✗ | ScholarClaw includes explicit config validation, environment health checks, and run report generation. |
| One-stage and bucket-scoped execution | ✓ | ✗ | ScholarClaw exposes exact-stage runs plus bucket-scoped runs as first-class CLI controls. |
| Cross-run learning | ✓ | ✓ | ScholarClaw uses `EvolutionStore`; AutoResearchClaw documents MetaClaw integration. |

## Workflow Philosophy

ScholarClaw is for researchers who want help thinking more clearly before they commit to a research direction.

From early idea to proposal, and from execution to publication, the focus is not just speed.

The focus is better research judgment, earlier in the process.

## Quick Start

### 1. Create a Python environment

ScholarClaw requires Python 3.11 or newer.

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
```

### 2. Install ScholarClaw

For the standard API-oriented path:

```bash
pip install -e .
```

If you want browser-based literature retrieval as well:

```bash
pip install -e ".[browser]"
playwright install
```

### 3. Start from the sample config

The sample config already points the sandbox runner at `.venv/bin/python3`, so using a `.venv` keeps setup simple.

```bash
cp config.local.yaml config.yaml
```

Then edit `config.yaml` and set the LLM backend you want to use:

- `openrouter` for hosted OpenRouter models
- `lmstudio` for a local LM Studio OpenAI-compatible server
- `openai-compatible` for another compatible endpoint
- `acp` for ACP agent execution

At minimum, make sure the LLM section and any required API key environment variables are configured for your environment.

### 4. Validate the config

```bash
scholarclaw validate -c config.yaml
```

### 5. Inspect the pipeline

```bash
scholarclaw list-stages
scholarclaw list-stages --bucket proposal
```

### 6. Run your first topic

```bash
scholarclaw run -c config.yaml --topic "Grounded proposal generation for autonomous scientific research"
```

### 7. Useful next commands

```bash
scholarclaw doctor -c config.yaml
scholarclaw report runs/<your-run-dir>
```

If you want to run only part of the workflow, you can scope execution by bucket or by exact stage:

```bash
scholarclaw run -c config.yaml --bucket proposal
scholarclaw run -c config.yaml --only-stage SEARCH_STRATEGY
```

## Why It Exists

Too many research workflows jump straight from idea to output.
They summarize quickly, generate confidently, and move on before the core questions have been tested:

- Has this already been done?
- Is the idea truly different, or just phrased differently?
- What would make the contribution stronger?
- What would a serious reviewer challenge?

ScholarClaw is designed to stay with those questions longer, because that is where better research begins.

It is also designed to ask those questions in the right research context, so ideas are judged against the literature that actually matters for the field.

## CLI Highlights

- `scholarclaw run` for full or bucket-scoped execution
- `scholarclaw list-stages` to inspect the pipeline before running it
- `scholarclaw validate` to validate config early
- `scholarclaw doctor` for environment and configuration health checks
- `scholarclaw report` to generate a readable summary from a completed run

## Current Positioning

ScholarClaw is not meant to be just another paper generator.

It is shaped as a research partner that challenges ideas, surfaces evidence, and helps build stronger work from the beginning.

It is especially useful when you want to:

- map ideas against the literature that matters for the field
- identify novelty risks before time is spent on execution
- suggest stronger positioning when an idea is too close to prior work
- surface weak spots, missing comparisons, and likely reviewer objections early
- help shape proposals with clearer positioning and higher ambition
- keep the work grounded in evidence instead of confident but unsupported claims
- support the path from proposal to experiments and paper when the foundation is strong

## Status

ScholarClaw is currently in active development.

The direction is clear: better research judgment earlier, stronger evidence throughout, and more defensible work by the time a paper is written.

## Coming Soon

- Full-featured web interface that starts with entering a research idea and carries the workflow all the way to a produced paper.
- End-to-end UI for configuring runs, monitoring stage progress, browsing artifacts, and managing long-running review, revision, and approval workflows without living in the terminal.

## Documentation Roadmap

- More usage examples
- More workflow walkthroughs
- More configuration guidance
- More stage-by-stage operational docs

## Foundation

ScholarClaw builds on the foundation of [AutoResearchClaw](https://github.com/aiming-lab/AutoResearchClaw) and is evolving into its own more focused, evidence-grounded research product.
