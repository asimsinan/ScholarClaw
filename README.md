![ScholarClaw logo](logo.png)

# ScholarClaw

Proposal-first research, grounded in evidence.

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

## Full Feature List

| Area | Feature | What It Does |
| --- | --- | --- |
| Workflow | 29-stage pipeline | Moves work from topic framing through literature, synthesis, experiment design, execution, writing, review, revision, verification, and export. |
| Workflow | Bucketed execution | Separates work into `proposal`, `execution`, `publication`, `review`, and `revision` buckets so users can run focused parts of the system. |
| Literature | OpenAlex-first retrieval | Uses OpenAlex as the primary API search backend, backed by Semantic Scholar and arXiv for broader literature coverage. |
| Literature | Agentic browser retrieval | Searches scholarly websites directly through browser automation when browser-based source access is preferred. |
| Literature | Browser target registry | Supports default browser targets including Semantic Scholar, arXiv, Elsevier / ScienceDirect, Springer, IEEE Xplore, Google Scholar, and Web of Science. |
| Literature | Year and depth controls | Lets users constrain literature review by recent-year presets or explicit ranges, and adjust breadth with `fast`, `standard`, `deep`, and `exhaustive` modes. |
| Literature | Search hardening | Generates grounded search strategies, hardens weak queries, expands search coverage, and applies unified filtering and deduplication. |
| Literature | Goal grounding | Collects candidate evidence early and can export verified-only references to support proposal shaping. |
| Screening | Multiple screening modes | Supports `deterministic`, `llm`, and `hybrid` screening configurations for different judgment and safety preferences. |
| Research judgment | Novelty and positioning checks | Tests ideas against gathered literature, surfaces novelty risks, and helps identify weak framing or missing comparisons. |
| Citation hygiene | Citation verification | Verifies citations through DOI, arXiv IDs, title matching, and OpenAlex-backed confirmation paths. |
| Citation hygiene | Relevance pruning | Scores verified citations for topical relevance and can drop weak references instead of keeping every valid citation. |
| Writing | Publication-aware writing | Supports publication-family aware writing behavior, publication templates, and custom LaTeX template paths. |
| Experiments | BenchmarkAgent | Helps benchmark-style ML work by selecting datasets and baselines and injecting validated benchmark choices into experiment planning. |
| Figures | FigureAgent | Plans and generates figures early enough for the drafting stage to reference visuals, with fallback chart generation when needed. |
| Review | Parallel reviewer workflows | Runs multiple reviewer perspectives in parallel and synthesizes them through an editor-style decision stage. |
| Review | Resumable review state | Persists reviewer outputs and review manifests so completed reviews can be reused instead of rerun. |
| Revision | Structured revision workflow | Builds revision plans from editor `must_fix` items and reviewer feedback, then supports response and apply stages. |
| Runtime | Stage-specific model routing | Allows different models to be assigned to different stage groups through YAML configuration. |
| Runtime | Local-model friendly operation | Works with local OpenAI-compatible endpoints such as LM Studio and Ollama, including browser retrieval against local endpoints. |
| Runtime | ACP-compatible execution | Supports ACP-style execution paths for agent-oriented integrations. |
| Resilience | Checkpoint and resume | Stores pipeline checkpoints and supports resumable progress for long, expensive runs. |
| Resilience | Sub-stage recovery | Persists state for expensive work like drafting, iterative refinement, code generation, and external review artifacts. |
| Tooling | CLI utilities | Includes `run`, `list-stages`, `validate`, `doctor`, and `report` commands for execution, validation, health checks, and reporting. |
| Tooling | Execution controls | Supports controls like bucket-scoped runs, one-stage runs, auto-approval, skipping noncritical failures, and skipping preflight checks. |
| Learning | EvolutionStore | Extracts lessons from prior runs and builds prompt overlays so the system can learn from past failures and quality issues. |

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

For a fuller product tour, see `FEATURES.md`.

## Documentation Roadmap

- More usage examples
- More workflow walkthroughs
- More configuration guidance
- More stage-by-stage operational docs

## Foundation

ScholarClaw builds on the foundation of [AutoResearchClaw](https://github.com/aiming-lab/AutoResearchClaw) and is evolving into its own more focused, evidence-grounded research product.
