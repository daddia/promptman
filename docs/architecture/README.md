# Promptman

Promptman is a lightweight agent specialized in prompt engineering. It leverages Contextor to gather the latest documentation from key LLM/AI sites, analyzes content changes, synthesizes insights into prompt engineering best practices, and maintains a curated collection of templates and guidelines. 

## Key Features

- **Prompt Engineering Focus** – Specializes in analyzing and synthesizing prompt engineering best practices, techniques, and emerging patterns from leading AI documentation.
- **Contextor Integration** – Uses Contextor to automatically gather content from AI/LLM documentation sites into a standardized `_context/` directory.  
- **Change Analysis & Insights** – Detects meaningful changes in prompt engineering guidance, identifies emerging patterns, and synthesizes insights into actionable recommendations.
- **Template & Best Practice Maintenance** – Maintains and updates curated prompt engineering templates, guidelines, and best practices based on the latest industry developments.
- **Automated Documentation Updates** – Proposes conservative updates to prompt engineering documentation via PRs with clear citations and rationale.

---

## Quick Start

**Get running in under 5 minutes:**

1. Clone the repositories

```bash
# Clone Promptman
git clone https://github.com/<your-org>/promptman.git
cd promptman

# Install Contextor (content fetcher)
pip install contextor
```

2. Install dependencies

```bash
# Python 3.11 recommended
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

3. Configure the environment

```bash
# Copy example environment file and configure
cp .env.example .env

# Required (choose your provider)
# OPENAI_API_KEY=sk-...
# or ANTHROPIC_API_KEY=...

# Optional
# AGENT_LOG_LEVEL=INFO
```

4. Fetch context and run analysis

```bash
# Use Contextor to fetch latest prompt engineering content
contextor fetch --config config/targets.yaml

# Analyze changes and synthesize insights
python -m promptman analyze --date $(date +%F)

# Generate updated templates and best practices
python -m promptman synthesize

# Serve documentation locally
mkdocs serve -a 0.0.0.0:8000
```

**You're ready to go!** Promptman will analyze the latest prompt engineering documentation and serve insights at [http://localhost:8000](http://localhost:8000).

---

## Documentation

Comprehensive documentation is available in the [`docs/`](docs/) directory:

* **[Getting Started](docs/GETTING_STARTED.md)** – Detailed setup and first steps
* **[Architecture](docs/architecture/)** – System design and technical decisions
* **[FAQ](docs/FAQ.md)** – Common questions and answers
* **[Troubleshooting](docs/TROUBLESHOOTING.md)** – Solutions to common issues

> The site is built with MkDocs Material (`mkdocs.yml`) and deploys via GitHub Pages on merges to `main`.

## Contributing

We welcome contributions! Please see [CONTRIBUTING.md](./CONTRIBUTING.md) for:

* Development workflow and guidelines
* Code standards and quality requirements
* How to submit changes and get them reviewed

## License

This project is licensed under the \[License Name]. See [`LICENSE`](LICENSE) for details.
