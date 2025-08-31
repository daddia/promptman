---
title: Design Principles for Promptman
description: Principles and architectural guardrails for Promptman as a prompt engineering specialist
version: 2.0.0
last_reviewed: 2025-08-30
---

# Design Principles for Promptman

These principles guide the design and development of Promptman as a specialized prompt engineering agent.

1. **Prompt Engineering Focus**: Specialize exclusively in analyzing, synthesizing, and maintaining prompt engineering knowledge. Deep expertise over broad functionality.

2. **Contextor Integration**: Leverage Contextor for all content fetching and MCP file generation. Focus on analysis and synthesis, not web scraping infrastructure.

3. **Evidence-Based Best Practices**: All recommendations and templates must be based on documented evidence from authoritative sources with clear citations.

4. **Quality Over Quantity**: Maintain a curated collection of high-quality templates and insights rather than comprehensive coverage of all possible techniques.

5. **Actionable Insights**: Every analysis must produce concrete, actionable recommendations that practitioners can immediately apply to improve their prompt engineering.

6. **Template Excellence**: All templates must include clear instructions, concrete examples, common variations, and guidance on when to use each approach.

7. **Change Significance Analysis**: Focus on meaningful changes in prompt engineering practices. Ignore editorial changes, prioritize technique evolution and best practice updates.

8. **Human-in-the-Loop**: All documentation and template updates require human review. The system proposes, humans decide and approve.

9. **Traceable Citations**: Every update must include source URLs, evidence snippets, and rationale to enable fast, informed review decisions.

10. **Version Control as History**: Use Git to track the evolution of prompt engineering knowledge. MCP files provide snapshots, Git provides the narrative.

11. **Conservative Updates**: Prefer incremental, well-justified updates over major rewrites. Maintain continuity while incorporating new knowledge.

12. **Multi-Source Analysis**: Synthesize insights from multiple authoritative sources (Anthropic, OpenAI, research papers) to provide balanced perspectives.

13. **Technique Classification**: Systematically categorize and organize prompt engineering techniques by use case, complexity, and effectiveness.

14. **Reproducible Analysis**: The same MCP input files must produce consistent analysis results. Deterministic processing with documented decision rules.

15. **Performance Awareness**: Weekly analysis should complete efficiently. Use embeddings and caching judiciously to manage computational costs.

16. **Schema Compliance**: All outputs must conform to documented schemas. Fail fast on validation errors to maintain data quality.

17. **Accessibility First**: Generated documentation must be clear, scannable, and accessible. Prioritize practitioner usability over academic completeness.

18. **Popular Library Integration**: Build on proven libraries (pandas, scikit-learn, OpenAI, Anthropic) for analysis and synthesis capabilities.

19. **Insight Longevity**: Focus on identifying lasting principles and patterns, not just trending techniques. Build knowledge that remains valuable over time.

20. **Community Value**: Generate insights and templates that benefit the broader prompt engineering community. Open source knowledge for collective advancement.

---

## Quality Standards for Prompt Engineering Content

### Template Requirements
- **Clear Purpose**: Every template must state its intended use case and context
- **Concrete Examples**: Include 2-3 complete, realistic examples showing the template in action
- **Variations**: Show how to adapt the template for different scenarios
- **Anti-patterns**: Document what NOT to do and common mistakes to avoid
- **Evaluation Guidance**: Provide criteria for assessing output quality

### Best Practice Documentation
- **Evidence-Based**: All claims must be supported by examples from authoritative sources
- **Comparative Analysis**: Show advantages/disadvantages relative to alternative approaches  
- **Context Sensitivity**: Explain when techniques work well and when they don't
- **Progressive Complexity**: Order from basic to advanced techniques
- **Cross-References**: Link related techniques and templates appropriately

### Insight Generation
- **Trend Analysis**: Identify patterns across multiple sources and time periods
- **Impact Assessment**: Evaluate the practical significance of changes and new techniques
- **Recommendation Clarity**: Provide specific, actionable next steps for practitioners
- **Future Implications**: Consider how developments might affect prompt engineering practices

---

## Integration Philosophy

Promptman is designed as a specialized component in a larger ecosystem:

- **Contextor Dependency**: Relies on Contextor for content acquisition and MCP file generation
- **Focused Responsibility**: Handles only prompt engineering analysis, synthesis, and documentation
- **Standard Interfaces**: Uses MCP files as input, generates standard documentation formats as output
- **Composable Design**: Can be integrated with other tools and workflows through clear APIs

This separation of concerns allows each tool to excel at its specific purpose while enabling powerful combinations through composition.
