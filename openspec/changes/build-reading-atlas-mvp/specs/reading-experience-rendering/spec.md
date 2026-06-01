## ADDED Requirements

### Requirement: Controlled spec rendering
The system SHALL render Reading Experience Specs through controlled React components rather than executing arbitrary model-generated code.

#### Scenario: Renderable spec is opened
- **WHEN** the user opens a generated Reading Atlas
- **THEN** the renderer displays the atlas by interpreting approved layout primitives, block primitives, theme tokens, and content fields

#### Scenario: Spec contains unknown primitive
- **WHEN** the renderer encounters an unknown layout or block primitive
- **THEN** it fails gracefully for that primitive without executing arbitrary code

### Requirement: Flexible layout primitives
The renderer SHALL support composable layout primitives that allow document-specific experiences without fixed page templates.

#### Scenario: Agent selects a layout strategy
- **WHEN** a valid spec uses approved layout primitives
- **THEN** the renderer composes sections according to the spec's selected strategy

### Requirement: Source citation display
The renderer SHALL expose source grounding for generated content.

#### Scenario: User views grounded content
- **WHEN** a rendered claim, quote, concept, evidence item, or interpretation has citations
- **THEN** the UI displays or makes available the referenced page or chunk source

### Requirement: Interactive reading controls
The renderer SHALL provide lightweight interactions that help users navigate the Reading Atlas.

#### Scenario: User expands dense content
- **WHEN** a section contains expandable details
- **THEN** the user can reveal supporting details without leaving the atlas

#### Scenario: User navigates sections
- **WHEN** the Reading Atlas contains multiple sections
- **THEN** the user can move through the generated experience in a clear reading order

### Requirement: Safe visual theming
The renderer SHALL apply visual styling through approved theme tokens rather than arbitrary CSS from the model.

#### Scenario: Spec includes theme tokens
- **WHEN** a valid spec defines mood, density, accent, typography scale, or spacing tokens
- **THEN** the renderer maps those tokens to approved styles

#### Scenario: Spec includes unsupported style values
- **WHEN** the spec includes unsupported style values
- **THEN** the renderer ignores or normalizes them
