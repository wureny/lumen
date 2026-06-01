## ADDED Requirements

### Requirement: Document profiling
The system SHALL analyze the parsed document and produce a document profile before generating the final reading experience.

#### Scenario: Profile is generated
- **WHEN** a parsed document has sufficient text
- **THEN** the system identifies document type, audience, density, structure confidence, language, and recommended reading strategy

### Requirement: Semantic model extraction
The system SHALL extract a semantic model from the document for use in the Reading Experience Spec.

#### Scenario: Semantic model is generated
- **WHEN** the system analyzes the parsed document
- **THEN** it identifies relevant concepts, claims, evidence, quotes, examples, figures, tensions, and relationships where present

### Requirement: Experience planning
The system SHALL create an experience plan that chooses how the document should be presented.

#### Scenario: Plan selects document-specific presentation
- **WHEN** the system has a document profile and semantic model
- **THEN** it selects an appropriate reading path, page rhythm, layout strategy, and visual tone for the document

### Requirement: Reading Experience Spec generation
The system SHALL generate a structured Reading Experience Spec instead of arbitrary executable page code.

#### Scenario: Spec is generated
- **WHEN** the system completes profiling, semantic extraction, and experience planning
- **THEN** it emits a JSON-compatible spec containing document profile, semantic model, experience plan, render instructions, theme tokens, and citations

#### Scenario: Model proposes executable code
- **WHEN** generated output includes executable HTML, JavaScript, or React code outside the allowed spec format
- **THEN** the system rejects or repairs the output before rendering

### Requirement: Source grounding
The system SHALL ground meaningful generated content to original document sources where possible.

#### Scenario: Claim includes support
- **WHEN** the Reading Experience Spec contains a claim, concept, quote, evidence item, tension, or interpretation
- **THEN** the item includes page or chunk citations unless it is explicitly marked as inference

#### Scenario: Quote is used
- **WHEN** the Reading Experience Spec includes a direct quote
- **THEN** the quote references its source page or chunk

### Requirement: Spec validation
The system SHALL validate generated Reading Experience Specs before making them available to the renderer.

#### Scenario: Valid spec
- **WHEN** a generated spec conforms to schema and grounding requirements
- **THEN** the system stores it as renderable

#### Scenario: Invalid spec
- **WHEN** a generated spec fails schema or grounding validation
- **THEN** the system blocks rendering and records a repairable generation error
