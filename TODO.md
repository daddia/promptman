# TODO - Promptman

*Last updated: 30 Aug 2025*  

---

## Conventions

- **Priority:** P1 (urgent/critical), P2 (high), P3 (normal), P4 (low)
- **Status:** Not started · In progress · Blocked · In review · Done
- **Estimates:** S (≤2h), M (≤1d), L (≤3d), XL (>3d)
- **DoD (Definition of Done):** Tests updated · Docs updated · Review approved · Deployed/Released (as applicable)

---

## Current Sprint

### Sprint 0 — **Bootstrap & Scaffolding** → Release v0.1.0-alpha

- [ ] **Repo scaffold & housekeeping** (P2 · S · Status: Not started)  
  Create base tree (`config/`, `reference/`, `docs/`, `agent/`, `.github/workflows/`), `.gitignore`, `LICENSE`, `CONTRIBUTING.md`.

- [ ] **MkDocs setup** (P3 · S · Status: Not started)  
  Add `mkdocs.yml`, `docs/index.md`, minimal nav; ensure `mkdocs build --strict` passes.

- [ ] **Python runtime & deps** (P2 · S · Status: Not started)  
  Add `requirements.txt`, `.env.example`, `Makefile` targets (`dev`, `site`).

- [ ] **Agent CLI skeleton** (P1 · M · Status: Not started)  
  `agent/__main__.py` with `plan-run` and `fetcher` subcommand (no-op); logging + basic arg parsing.

- [ ] **Sample configs** (P1 · S · Status: Not started)  
  Provide `config/targets.yaml` examples (Anthropic/OpenAI/MCP), plus comments for `selector`, rate limits.

- [ ] **Pre-commit & lint** (P3 · S · Status: Not started)  
  Add `ruff` + `black` + `isort` (or `ruff format`), pre-commit hooks; pin versions.

---

## Next Sprint

### Sprint 1 — **Reference Collector MVP** (fetch → convert → index → commit) → Release v0.1.0

- [ ] **HTTP fetcher with ETag/IMS** (P1 · M · Status: Not started)  
  `agent/tools/http_fetch.py` supporting `If-Modified-Since`/`If-None-Match`, polite headers, retries, backoff.

- [ ] **Robots & rate limiting** (P1 · S · Status: Not started)  
  Respect `robots.txt`; per-site QPS & concurrency; user-agent string.

- [ ] **Sitemap ingestion** (P2 · M · Status: Not started)  
  Parse `<sitemap.xml>` and nested indexes; normalise to URL set; fallback to seeds when absent.

- [ ] **Topic filter & page selection** (P1 · M · Status: Not started)  
  Build fetch list by allow-listing keywords (e.g., “prompt engineering”, “model context protocol”, “agent”, “tools”) and path regexes.

- [ ] **Extractor → Markdown** (P1 · M · Status: Not started)  
  `agent/tools/extract.py` to select `selector` region, strip chrome, convert to Markdown (front-matter: `url`, `title`, `site`, `slug`, `content_hash`, `last_fetched_at`).

- [ ] **Slug & hash stability** (P1 · S · Status: Not started)  
  Deterministic slug from URL; `content_hash` over normalised Markdown; redirects map for moved pages.

- [ ] **Reference writer & index** (P1 · S · Status: Not started)  
  Write to `reference/{site}/pages/{slug}.md`; update `reference/{site}/index.jsonl`.

- [ ] **Commit gating** (P1 · S · Status: Not started)  
  Commit only when `content_hash` changes; conventional message `feat(reference): {site}/{slug}`.

- [ ] **Fetcher role orchestrator** (P1 · S · Status: Not started)  
  `agent/roles/fetcher/orchestrator.py` to tie config → selection → fetch → write → commit.

- [ ] **Weekly GitHub Action (fetch-only)** (P1 · S · Status: Not started)  
  `.github/workflows/weekly.yml` to run `python -m agent fetcher --date $(date +%F)`; use `actions/checkout@v4` with `fetch-depth: 2`.

- [ ] **Unit tests (MVP scope)** (P2 · M · Status: Not started)  
  Tests for sitemap parse, slug/hash stability, extractor selection, index append idempotency.

- [ ] **Docs: Getting Started (collector)** (P3 · S · Status: Not started)  
  `docs/GETTING_STARTED.md` covering config, running locally, and weekly workflow.

---

### Sprint 2 — **Seed Expansion & Hardening** → Release v0.1.1

- [ ] **Headless fetch fallback (Playwright)** (P2 · M · Status: Not started)  
  Opt-in dynamic rendering for JS-heavy pages; 30s cap; feature flag per site.

- [ ] **Per-site selectors & transforms** (P2 · S · Status: Not started)  
  Configurable CSS selectors; per-site cleansing rules (e.g., strip version banners).

- [ ] **Error budget & telemetry** (P3 · S · Status: Not started)  
  Emit simple metrics JSON (fetch count, changed count, errors) into `changes/{date}/metrics.json`.

- [ ] **Docs: Reference conventions** (P3 · S · Status: Not started)  
  Document front-matter schema, slugging, and commit etiquette.

---

## Backlog

### Sprint 3 — **Change Detection & Weekly Report** → Release v0.2.0

- [ ] **Markdown AST differ** (P1 · M · Status: Not started)  
  Implement structural diff for headings, lists, tables, and code blocks; normalise whitespace to reduce noise.

- [ ] **Semantic delta (optional)** (P2 · M · Status: Not started)  
  Pluggable embeddings to flag meaningfully changed chunks; cache by `content_hash`.

- [ ] **Significance classifier (heuristics-first)** (P1 · S · Status: Not started)  
  Rules for `breaking`, `deprecation`, `feature`, `correction`, `editorial`; LLM fallback only if ambiguous.

- [ ] **Weekly report generator** (P1 · S · Status: Not started)  
  Produce `changes/{date}/report.md` with per-site bullets and citations to source URLs and diffs.

- [ ] **Docs summary copy** (P3 · S · Status: Not started)  
  Optionally copy the weekly summary to `docs/changes/{date}.md` and add to MkDocs nav.

- [ ] **Unit tests: differ/classifier/report** (P2 · M · Status: Not started)  
  Golden tests for typical change scenarios; verify schema.

- [ ] **Workflow update (fetch → diff → synthesise)** (P1 · S · Status: Not started)  
  Extend `weekly.yml` to chain roles; fail fast on schema errors.

---

### Sprint 4 — **Docs & Template PR Automation** → Release v0.3.0

- [ ] **Mapping rules application (core/templates)** (P1 · S · Status: Not started)  
  Use `mapping.core.yaml` and `mapping.templates.yaml` to route changes to target docs.

- [ ] **Docs writer orchestrator** (P1 · M · Status: Not started)  
  Generate conservative edits to `docs/core/*` with citations and rationale.

- [ ] **Template writer orchestrator** (P2 · M · Status: Not started)  
  Suggest `<!-- SUGGESTED: ... -->` tweaks to `docs/templates/*`; keep diffs minimal.

- [ ] **Single PR per week** (P1 · S · Status: Not started)  
  Create/update a branch and PR: `chore(docs): weekly refresh {YYYY-MM-DD}`; append run summary.

- [ ] **PR labelling & CODEOWNERS gates** (P2 · S · Status: Not started)  
  Apply labels (`area:*`, `type:*`); require Docs + Eng approvals.

- [ ] **Integration test (dry-run)** (P2 · S · Status: Not started)  
  Simulate a small change set and verify PR content and checks.

---

### Sprint 5 — **Governance, CI & Quality Gates** → Release v0.4.0

- [ ] **Schema validation check** (P1 · S · Status: Not started)  
  Validate weekly report output against JSON schema; fail PR if invalid.

- [ ] **MkDocs build check in PRs** (P1 · S · Status: Not started)  
  Ensure `mkdocs build --strict` passes on PR branches.

- [ ] **Conventional commits & changelog** (P3 · S · Status: Not started)  
  Enforce commit format; auto-generate release notes for tags.

- [ ] **Dependency automation** (P3 · S · Status: Not started)  
  Enable Dependabot/Renovate; weekly updates with grouped PRs.

- [ ] **Pre-commit in CI** (P2 · S · Status: Not started)  
  Run `ruff`/format checks; block on style violations.

---

### Sprint 6 — **Site Hardening & Publishing** → Release v0.5.0

- [ ] **Docs IA & navigation polish** (P2 · S · Status: Not started)  
  Refine nav structure, add landing pages for Core, Templates, and Changes.

- [ ] **Theme & accessibility** (P3 · S · Status: Not started)  
  Ensure readable contrast, consistent headings, and keyboard navigation.

- [ ] **Pages deployment workflow** (P1 · S · Status: Not started)  
  Harden `.github/workflows/pages.yml`; optional custom domain & HTTPS.

- [ ] **Authoring guidelines** (P3 · S · Status: Not started)  
  Add `docs/CONTRIBUTING_DOCS.md` for tone, citations, and PR etiquette.

---

### Sprint 7 — **MCP Read-Only API** → Release v0.6.0

- [ ] **MCP server skeleton** (P2 · S · Status: Not started)  
  Minimal server in `mcp/` exposing: `list_changes(since)`, `get_snapshot(site, path, date)`, `get_diff(site, path, date)`.

- [ ] **Adaptors to reference/changes** (P2 · S · Status: Not started)  
  Read directly from repo files; no extra DB.

- [ ] **Contracts & examples** (P3 · S · Status: Not started)  
  Document request/response examples; add simple client snippet.

- [ ] **Security & limits** (P3 · S · Status: Not started)  
  Rate-limit, optional token, and path allow-list.

---

### Sprint 8 — **Coverage Expansion & Performance** → Release v0.7.0

- [ ] **Topic expansion** (P2 · M · Status: Not started)  
  Add additional providers/pages (e.g., OpenAI tools/agents deep dive, Anthropic function/tool use, MCP spec updates).

- [ ] **Sitemap + seeds merging** (P2 · S · Status: Not started)  
  Union sitemap discovery with curated seeds; deduplicate; per-site allow/deny lists.

- [ ] **Headless fetch feature flag** (P2 · S · Status: Not started)  
  Enable per-site opt-in Playwright; cap runtime; collect metrics.

- [ ] **Concurrency & backoff tuning** (P2 · S · Status: Not started)  
  Safe parallel fetch; adaptive backoff on throttling.

- [ ] **Cache & ETag persistence** (P2 · S · Status: Not started)  
  Persist last-seen ETag/Last-Modified per URL for faster subsequent runs.

---

### Sprint 9 — **Observability, Cost & Reliability** → Release v0.8.0

- [ ] **Structured logging** (P2 · S · Status: Not started)  
  JSON logs with run id, site, url, status, duration, bytes.

- [ ] **Run metrics artefact** (P2 · S · Status: Not started)  
  `changes/{date}/metrics.json` (fetched, changed, skipped, errors by site).

- [ ] **Alerting hooks** (P3 · S · Status: Not started)  
  Optional: post summary as PR comment; open issue on repeated site failures.

- [ ] **Cost controls** (P2 · S · Status: Not started)  
  Track LLM token usage; hard cap per run; skip LLM when no significant changes.

---

### Sprint 10 — **1.0 Hardening & Release** → Release v1.0.0

- [ ] **Security review** (P2 · S · Status: Not started)  
  Secret handling, dependency scan, audit third-party licences.

- [ ] **Performance budget validation** (P2 · S · Status: Not started)  
  Weekly run time on GitHub runners ≤ 15 minutes (target); document results.

- [ ] **Documentation complete** (P2 · S · Status: Not started)  
  Finalise `docs/GETTING_STARTED.md`, architecture notes, and maintenance guide.

- [ ] **Release process** (P2 · S · Status: Not started)  
  Tag `v1.0.0`, generate changelog, publish site, and announce.

---


## Continuous Items (Track Throughout)

- [ ] **Performance**: Keep weekly run under 15 minutes on GitHub runners; avoid unnecessary headless fetches.
- [ ] **Quality**: Maintain fast unit tests for extractor, sitemap, hashing; keep lint clean.
- [ ] **Security**: Store tokens in GitHub Secrets; never log secrets; respect site terms of use.
- [ ] **Dependencies**: Pin versions; renovate/Dependabot for weekly updates.
- [ ] **Documentation**: Update `docs/` when behaviour or config changes.
- [ ] **Monitoring**: Review weekly run logs and metrics JSON; alert on persistent fetch errors.

---

## Future Enhancement Candidates

### **Change Intelligence**

- [ ] **Structural + semantic diffs**: AST diff + optional embeddings to classify significance (`breaking`, `deprecation`, etc.).
- [ ] **Weekly report**: `changes/{date}/report.md` with per-site bullets and citations.
- [ ] **Richer diff views**: Side-by-side HTML render for complex tables/code.
- [ ] **Breaking change detector**: Stronger heuristics for parameter/table changes.

### **Docs Automation**

- [ ] **Docs writer role**: Propose conservative edits to `docs/core/*` via PR with sources.
- [ ] **Template writer role**: Suggest optional `<!-- SUGGESTED: ... -->` tweaks to `docs/templates/*`.
- [ ] **Auto-link issues**: Open Jira/GitHub issues for `breaking`/`deprecation` items.
- [ ] **Changelog pages**: Auto-compile monthly digests under `docs/changes/`.

### **Ecosystem & Access**

- [ ] **MCP server (read-only)**: Expose snapshots and diffs as tools for other agents.
- [ ] **Topic discovery via embeddings**: Expand fetch list by semantic similarity to tracked topics.
- [ ] **Semantic search**: Local index over `reference/` for human queries.
- [ ] **Slack summary**: Post top 5 changes with links and significance tags.

### **Operations**

- [ ] **Matrix CI**: Test against Python 3.11/3.12; OS matrix if needed.
- [ ] **Container image**: Optional Docker image for reproducible local runs.

---

## Completed
> Move finished items here to keep the active list clean.

### Sprint 0 — **Bootstrap & Scaffolding** → Release v0.1.0-alpha — **COMPLETE**

- [x] **(example)**: Placeholder for completed tasks will appear here.
