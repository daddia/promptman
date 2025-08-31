---
title: Promptman — Architecture Overview
version: 1.0.0
---

# Architecture Overview - Promptman

Promptman generates best-practice docs, patterns, and templates for prompt engineering. It opens a single weekly PR with curated updates.

## System Overview

- **Input**: `_context/**/*.mdc` files (Contextor output)
- **Processing**: clustering, deduplication, synthesis (LLM-assisted), citation linking
- **Output**: `docs/core/*`, `docs/templates/*`, optional `docs/changes/*`; PR creation

## Components

- **Context Reader**: loads & validates `.mdc` front-matter; indexes by topic/site.
- **Classifier/Clusterer**: merges near-dupes; tags by theme (prompting, MCP, agents).
- **Synthesiser**: produces concise, cited guidance and patterns.
- **Docs/Template Writers**: propose changes in PR with rationale and links.
- **Site**: MkDocs Material; GitHub Pages on merge to `main`.

## Technologies

- Python 3.13
- Poetry 2.1

Popular libraries

- **Markdown & front-matter:** `markdown-it-py`, `mdformat`, `python-frontmatter` or `ruamel.yaml`
- **Embeddings (optional, Promptman):** `sentence-transformers`
- **CLI ergonomics:** `typer` or `click`
- **Docs site:** MkDocs Material for docs

## Security

- Reads local repo files only; no network calls during synthesis. Secrets only for optional LLMs/PRs.
