# Architecture Decision Register

Below are all the Architecture Decision Records (ADRs) for the helix-go microservice framework.

ADRs document important architectural decisions which govern the project's design and development.

## What is an ADR?

An Architecture Decision Record captures a single architectural decision and its rationale. Each ADR describes:

- The context and problem statement
- The decision made
- The consequences of that decision
- Alternatives that were considered

---

| ID                                           | Title                                 | Status   | Date       | Supersedes | Related ADRs |
|----------------------------------------------|---------------------------------------|----------|------------|------------|--------------|
| [ADR-0001](ADR-0001-lightweight-platform.md) | Lightweight Platform: Library-First   | Accepted | 2025-01-15 | —          | -            |        

---

### Status legend

- **Proposed** — Under review, not yet adopted.
- **Accepted** — Adopted as the standard going forward.
- **Rejected** — Considered but not adopted.
- **Superseded** — Replaced by a newer ADR (link it in *Supersedes*).

---

## Creating a New ADR

Note. You must use template provided [adr-template.md](./adr-template.md) to create a new ADRs.

1. Copy the template to a new file with the naming convention: `ADR-{NUMBER}-{title-with-dashes}.md`

   ```bash
   cp docs/architecture/decisions/adr-template.md docs/architecture/decisions/adr/ADR-{####}-{short-title}.md
   ```

The filenames are following the pattern `ADR-####-title-with-dashes.md`.

- The prefix is `ADR` to identify a Architecture Decision Record (ADR).
- `####` is a consecutive number in sequence.
- The title is stored using dashes and lowercase.
- The filetype is `.md`, because it is a Markdown file.

1. Complete all the sections of the ADR template.
   - **Status**: `Proposed`
   - **Context**: Why was this decision needed?
   - **Decision**: What was decided and why?
   - **Consequences**: What are the trade-offs?
   - **Alternatives**: What else was considered?

1. Submit for review via pull request (PR). Start with **Proposed**.

1. On acceptance:
   - Update the status to **Accepted**.
   - Add a row to this Architecture Decision Register (`decisions/register.md`) index.

---

## Resources

- [Documenting Architecture Decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions)
- [ADR Tools](https://github.com/npryce/adr-tools)
- [ADR GitHub Organization](https://adr.github.io/)
