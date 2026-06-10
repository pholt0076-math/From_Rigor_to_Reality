# From Rigor to Reality — Publishing Workflow

## Content lifecycle

All content moves through these stages:

1. **Exploration** — raw material, chat notes, early drafts
2. **Refinement** — structured outlines, computational verification, narrative polish
3. **Canonicalization** — final version committed to the repository as durable source
4. **Publication** — formatted and shared (blog, social, etc.)

## Repository structure

Content is organized by type and subject:

```
posts/              ← Narrative exposition in Markdown
  measure_theory/
  sigma_algebras/
  ...

notebooks/          ← Interactive computation and visualization
  measure_theory/
  sigma_algebras/
  visualizations/

docs/               ← Project guidance and workflow
  project_manifesto.md
  publishing_workflow.md
  backlog_merge_plan.md

src/                ← Reusable utilities and computation
  rigor_to_reality/

assets/             ← Figures, images, diagrams
  images/
  figures/
```

## Creating new content

1. Choose a topic from the primary tracks
2. Start with an outline that connects rigor, intuition, computation, and application
3. Write the narrative in a post file (Markdown)
4. Create supporting notebooks or Python scripts to demonstrate computation
5. Add figures and diagrams to the assets folder if needed
6. Review for clarity, correctness, and alignment with project principles
7. Commit to the repository

## Quality gates

Before committing, verify:

- Mathematical correctness and rigor
- Clear narrative exposition without dilution
- Working code examples (if applicable)
- Consistent Unicode notation usage
- No proprietary or unrelated material

## Backlog merge process

Older chat material or exploratory work should be:

1. Identified and listed in the backlog
2. Reviewed for correctness and relevance
3. Harmonized into the existing repository structure
4. Committed with clear attribution and revision notes

This ensures the repository remains a durable source of truth rather than a collection of raw notes.

## Versioning and publishing

- All changes are committed to the main branch with clear commit messages
- Releases can be tagged when significant milestones are reached
- Published content can reference specific commits for reproducibility
