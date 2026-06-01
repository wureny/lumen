## 1. Project Foundation

- [ ] 1.1 Scaffold a Next.js, React, TypeScript application in the repository.
- [ ] 1.2 Add Tailwind CSS and establish the base visual system for lumen.
- [ ] 1.3 Add project configuration for environment variables, linting, formatting, and TypeScript validation.
- [ ] 1.4 Define the initial application routes for upload, generation status, and Reading Atlas viewing.

## 2. Document Ingestion

- [ ] 2.1 Implement PDF upload intake with file type, size, and page-count validation.
- [ ] 2.2 Implement server-side PDF parsing into metadata, page text, and stable page/chunk references.
- [ ] 2.3 Add ingestion failure states for unsupported, oversized, unreadable, or low-text PDFs.
- [ ] 2.4 Persist uploaded document metadata, extracted page text, chunks, and processing status.

## 3. Reading Experience Spec Model

- [ ] 3.1 Define TypeScript types for the Reading Experience Spec.
- [ ] 3.2 Define a JSON schema for document profile, semantic model, experience plan, render tree, theme tokens, and citations.
- [ ] 3.3 Add schema validation and safe failure behavior for invalid generated specs.
- [ ] 3.4 Add fixture specs for representative technical paper, market report, and strategy report experiences.

## 4. Agent Generation Pipeline

- [ ] 4.1 Implement server-side document profiling from parsed chunks.
- [ ] 4.2 Implement semantic model extraction for concepts, claims, evidence, quotes, figures, tensions, and relationships.
- [ ] 4.3 Implement experience planning that selects reading path, layout strategy, page rhythm, and visual tone.
- [ ] 4.4 Implement Reading Experience Spec generation using structured LLM output.
- [ ] 4.5 Add prompt-injection guardrails that treat document text as untrusted content.
- [ ] 4.6 Add grounding checks for claims, quotes, concepts, evidence, tensions, and inferred interpretations.

## 5. Controlled React Renderer

- [ ] 5.1 Implement the renderer shell that loads and interprets a validated Reading Experience Spec.
- [ ] 5.2 Implement initial layout primitives such as narrative stack, asymmetric grid, comparison matrix, timeline, evidence board, and concept map.
- [ ] 5.3 Implement initial block primitives such as thesis, claim, concept, quote, evidence, figure, risk, counterargument, definition, and reading step.
- [ ] 5.4 Implement approved theme token mapping for density, mood, accent, typography scale, contrast, and spacing.
- [ ] 5.5 Implement graceful fallback behavior for unknown or unsupported primitives.

## 6. Reading Atlas UX

- [ ] 6.1 Build the upload page with clear PDF-only MVP constraints.
- [ ] 6.2 Build generation progress states for parsing, profiling, extracting, planning, validating, and rendering.
- [ ] 6.3 Build the generated Reading Atlas page with section navigation and source citation display.
- [ ] 6.4 Add lightweight interactions for expanding supporting evidence, viewing citations, and navigating the reading path.
- [ ] 6.5 Add user-facing error states for parsing, generation, validation, and rendering failures.

## 7. Safety, Quality, and Verification

- [ ] 7.1 Add server-side safeguards for file limits, parse timeouts, and passive PDF content extraction.
- [ ] 7.2 Add tests or fixtures proving that arbitrary HTML, JavaScript, React code, and unsupported CSS are not rendered.
- [ ] 7.3 Add validation tests for required citations and inference labeling.
- [ ] 7.4 Add renderer tests using fixture Reading Experience Specs.
- [ ] 7.5 Run end-to-end smoke tests for upload-to-render flow with at least one sample PDF.
