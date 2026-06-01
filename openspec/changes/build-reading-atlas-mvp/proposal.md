## Why

Long documents are difficult to understand because their structure, claims, evidence, concepts, and tensions are buried inside linear pages. Existing AI document tools often collapse the work into summaries, while PDF-to-HTML tools preserve form without creating understanding.

lumen should prove a more memorable interaction model: an agent reads a PDF, plans an appropriate reading experience, and renders a grounded, theme-aware interactive Reading Atlas.

## What Changes

- Add a PDF upload and generation flow for creating a Reading Atlas from a long document.
- Parse PDFs into page-aware text, metadata, and chunk references.
- Add a server-side agent pipeline that profiles the document, extracts a semantic model, plans the reading experience, and emits a validated Reading Experience Spec.
- Add a controlled React renderer that interprets the Reading Experience Spec instead of executing arbitrary LLM-generated HTML, JavaScript, or React code.
- Add source grounding so generated claims, quotes, concepts, and evidence can reference original page/chunk locations.
- Add generation status and error states for long-running document processing.
- Add MVP safety constraints for malicious PDFs, prompt injection inside documents, unsafe generated markup, hallucinated claims, privacy, and large-document cost.

## Capabilities

### New Capabilities

- `document-ingestion`: Upload and parse PDF documents into metadata, page text, chunks, and stable source references.
- `reading-experience-generation`: Analyze a parsed document and generate a grounded Reading Experience Spec that captures document profile, semantic model, experience plan, and render instructions.
- `reading-experience-rendering`: Render a validated Reading Experience Spec as an interactive, visually intentional web reading experience using controlled React components and layout primitives.

### Modified Capabilities

- None.

## Impact

- New Next.js/React application surface for upload, generation status, and generated reading pages.
- New server-side PDF parsing and document chunking pipeline.
- New LLM integration for structured document profiling, extraction, planning, and PageSpec generation.
- New JSON schema validation layer for generated Reading Experience Specs.
- New persistence for uploaded document metadata, extracted chunks, generated specs, and generation state.
- New safety and quality checks for untrusted PDFs, untrusted document text, citation grounding, and generated page specs.
