## ADDED Requirements

### Requirement: PDF upload intake
The system SHALL allow a user to submit one PDF document for Reading Atlas generation.

#### Scenario: User uploads a supported PDF
- **WHEN** the user submits a PDF within configured size and page limits
- **THEN** the system accepts the file and creates a document processing job

#### Scenario: User uploads an unsupported file
- **WHEN** the user submits a non-PDF file
- **THEN** the system rejects the file and explains that the MVP supports PDF only

#### Scenario: User uploads an oversized PDF
- **WHEN** the user submits a PDF beyond configured size or page limits
- **THEN** the system rejects the file before generation begins

### Requirement: Page-aware text extraction
The system SHALL extract text from accepted PDFs while preserving page numbers and stable chunk references.

#### Scenario: Text extraction succeeds
- **WHEN** the system parses an accepted text-based PDF
- **THEN** it stores document metadata, page text, chunks, and source references

#### Scenario: Text extraction is insufficient
- **WHEN** the system cannot extract enough text to generate a meaningful atlas
- **THEN** it marks ingestion as failed with a user-visible explanation

### Requirement: Untrusted document handling
The system SHALL treat uploaded PDFs and extracted document text as untrusted input.

#### Scenario: PDF contains active or embedded behavior
- **WHEN** the parser encounters PDF content that could contain scripts, attachments, or embedded actions
- **THEN** the system extracts only passive content needed for analysis and does not execute embedded behavior

#### Scenario: Document text contains operational instructions
- **WHEN** extracted text includes instructions aimed at the AI system or application
- **THEN** the system treats those instructions as document content rather than application commands

### Requirement: Processing status visibility
The system SHALL expose document ingestion and generation status to the user.

#### Scenario: Job is processing
- **WHEN** the document is being parsed or analyzed
- **THEN** the user can see that processing is in progress

#### Scenario: Job fails
- **WHEN** ingestion or generation fails
- **THEN** the user can see a failure state with a concise reason
