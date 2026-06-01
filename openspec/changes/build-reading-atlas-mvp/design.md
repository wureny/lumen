## Context

lumen is starting from an empty codebase and can choose its architecture deliberately. The MVP needs to show that an agent can design a document-specific reading experience without turning the app into an unsafe arbitrary website/code generator.

The central product object is a Reading Atlas: a generated, interactive, source-grounded page that helps a reader understand a long PDF through structure, concepts, claims, evidence, tensions, and reading paths.

## Goals / Non-Goals

**Goals:**

- Convert a user-uploaded PDF into a source-grounded Reading Experience Spec.
- Render that spec through a controlled React renderer with flexible layout and visual primitives.
- Preserve agentic flexibility through document profiling, semantic modeling, experience planning, and renderer-level composition.
- Keep LLM calls and document processing server-side.
- Make the MVP visually distinctive enough for a portfolio while keeping implementation scope small.

**Non-Goals:**

- Do not support EPUB, MOBI, websites, or arbitrary file types in the MVP.
- Do not let the LLM generate arbitrary executable HTML, JavaScript, or React code.
- Do not build user accounts, collaborative features, payment, or public publishing in the MVP.
- Do not build a general document chat product in the MVP.
- Do not guarantee perfect extraction for scanned/image-only PDFs in the first version.

## Decisions

### Use a Reading Experience Spec instead of generated code

The agent SHALL output a structured JSON-compatible Reading Experience Spec containing document profile, semantic model, experience plan, render tree, theme tokens, and source references.

Alternatives considered:

- Raw HTML: flexible and fast to demo, but unsafe and difficult to validate.
- Generated React code: expressive, but requires sandboxed compilation, dependency management, runtime error recovery, and stronger security boundaries.
- Markdown with custom blocks: fast, but less expressive for interactive layouts and semantic relationships.

Rationale: a controlled spec keeps the agent expressive while allowing validation, safe rendering, deterministic UI behavior, and future refinement.

### Run document understanding and generation server-side

PDF parsing, chunking, LLM calls, grounding checks, and spec validation SHALL run on the server.

Rationale: server-side execution protects API keys, handles large files more predictably, allows persistence, and keeps untrusted document content away from browser execution paths.

### Separate semantic modeling from render planning

The generation pipeline SHOULD produce intermediate artifacts:

1. Parsed document model: metadata, pages, text, chunks, and source references.
2. Document profile: type, audience, density, structure confidence, and suggested reading strategy.
3. Semantic model: concepts, claims, evidence, quotes, figures, tensions, and inferred relationships.
4. Experience plan: page rhythm, visual tone, layout strategy, and section sequence.
5. Render spec: validated layout primitives and content blocks.

Rationale: the intermediate artifacts make the product feel agentic, improve debuggability, and create places for quality evaluation before rendering.

### Use layout and block primitives rather than fixed templates

The renderer SHALL support a controlled language of composable primitives, not a single fixed page template. Initial primitives can include narrative stacks, asymmetric grids, comparison matrices, timelines, evidence boards, concept maps, quote panels, risk panels, and figure explainers.

Rationale: primitives preserve creative range without giving the model arbitrary execution power. The agent designs by choosing and arranging a page language rather than emitting code.

### Require grounding for meaningful claims

Generated claims, quotes, concepts, evidence, tensions, and inferred interpretations SHALL include page/chunk citations whenever possible. Unsupported synthesis SHALL be labeled as inference or omitted.

Rationale: lumen's value depends on trust. Grounding also provides a concrete QA surface for tests and evaluator prompts.

### Start with local/simple persistence

The MVP MAY use local filesystem or SQLite persistence for uploaded metadata, parsed chunks, generation states, and generated specs.

Rationale: this is a side project. A small, inspectable persistence layer is enough until deployment and sharing requirements are clearer.

## Risks / Trade-offs

- Generated experiences may still feel templated -> Use primitives, theme tokens, and document-specific experience planning rather than one fixed layout.
- LLM output may violate schema -> Validate with a strict schema and return repair prompts or safe failure states.
- Claims may hallucinate or over-interpret -> Require citations, label inference, and run a grounding evaluator before marking generation complete.
- Large PDFs may be slow or expensive -> Set MVP page/file limits, chunk documents, show progress states, and allow generation failure with clear recovery.
- Malicious PDFs may attack parsers -> Limit file size, parse server-side, avoid executing PDF scripts, set timeouts, and isolate parsing logic.
- Prompt injection may appear inside document text -> Treat document content as untrusted input and instruct the agent that document instructions are analyzable content, not operational commands.
- Visual flexibility may increase frontend scope -> Define a small but expressive primitive set first, then expand only when real documents require it.

## Open Questions

- Which document type should be the primary demo path: technical papers, crypto/market reports, or strategy/business reports?
- Should generated atlases be private-only in MVP, or should public share links be included later?
- Should scanned PDFs fail gracefully, or should OCR be included from the start?
- What is the initial maximum file size and page count?
- Should refinements regenerate the whole atlas or targeted sections only?
