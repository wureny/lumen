# lumen

lumen is a non-commercial side project that turns PDFs, long reports, papers, and similar documents into structured, thematic, browsable web reading experiences.

It is not a PDF-to-HTML converter and it is not a generic document summarizer. The core idea is that an agent should understand the document first, then design an explanatory reading interface that fits the document itself.

## Product Thesis

PDF -> Reading Experience Spec -> Interactive Reading Atlas

lumen should not let an LLM directly generate arbitrary webpage code. Instead, the agent outputs a controlled `Reading Experience Spec`, and a frontend React renderer safely interprets and renders it.

```text
PDF
  ↓
Server parses text, pages, metadata, and chunks
  ↓
Agent generates a document profile and semantic model
  ↓
Agent plans the reading experience
  ↓
System generates and validates a Reading Experience Spec
  ↓
React renderer displays the Reading Atlas
```

## MVP Direction

The MVP should support PDF input first and generate a single-page, multi-section, lightly interactive Reading Atlas.

The MVP should not try to support every document type or become a general-purpose chat tool. The priority is a small, complete, visually intentional portfolio-quality product that demonstrates agentic product thinking.

## Core Ideas

- The agent does not directly generate arbitrary HTML, JavaScript, or React code.
- The agent generates a structured page description: document profile, semantic model, reading path, layout strategy, content blocks, visual tokens, and source citations.
- The frontend only renders specs that pass schema validation.
- Every important claim, concept, evidence item, quote, or interpretation should be grounded to an original page or chunk whenever possible.
- Visual flexibility comes from composable layout primitives and block primitives, not from fixed templates.

## Current OpenSpec Change

The current planning artifacts are in:

```text
openspec/changes/build-reading-atlas-mvp/
```

They include:

- `proposal.md`: why this MVP exists and what capabilities it introduces
- `design.md`: system architecture, key technical decisions, and risks
- `specs/`: testable product capability requirements
- `tasks.md`: implementation task breakdown

Check status:

```bash
openspec status --change build-reading-atlas-mvp
```

Validate the change:

```bash
openspec validate build-reading-atlas-mvp
```

Before implementation, the remaining open questions should be resolved: the first demo document type, page/file limits, whether OCR belongs in the MVP, and whether refinement should regenerate the whole atlas or only targeted sections.
