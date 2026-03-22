# Golden Potato - Project Plan

This document outlines the high-level plan for developing and delivering the Golden Potato project.

## 1. Project Vision

To create an automated, intelligent GRC assistant that transforms the FISMA compliance process from a periodic, manual checklist into a continuous, context-aware validation engine.

## 2. Scope

### In Scope
*   Ingestion of specific GRC documents: SSP, FIPS 200, FIPS 200 Exceptions Matrix, Deviation Documents.
*   Analysis of structured vulnerability scan reports (e.g., Nessus CSV output).
*   Adjudication of findings against the authorized baseline defined in the GRC documents.
*   Integration with a CI/CD pipeline to receive scan reports and output results.
*   Generation of a machine-readable adjudication report (e.g., JSON or Markdown).

### Out of Scope (for Version 1.0)
*   A graphical user interface (GUI) for managing the system.
*   Real-time monitoring of systems (the system is triggered by scan reports).
*   Automatic remediation of findings.
*   Support for unstructured or free-form GRC evidence.

## 3. Development Phases & Milestones

The project will be developed in three main phases.

### Phase 1: Foundation & Core Logic (Proof of Concept)
*   **Goal:** Build a working prototype that can adjudicate a single, hard-coded security finding.
*   **Key Deliverables:**
    1.  **[ ] Document Ingestion Script:** A Python script that can load and "chunk" text from PDF and DOCX files.
    2.  **[ ] Basic RAG Pipeline:** Set up a local vector database (e.g., ChromaDB) and write code to embed and store document chunks.
    3.  **[ ] Agent Adjudication Logic:** Create a core function that takes a finding, retrieves context from the vector DB, and uses a detailed prompt to get a justified adjudication from the Gemini API.
    4.  **[ ] End-to-End Test:** A single script that demonstrates the full flow for one example.
*   **Estimated Timeline:** 2-3 Weeks

### Phase 2: API & CI/CD Integration
*   **Goal:** Turn the PoC into a robust service that can be integrated into an automated workflow.
*   **Key Deliverables:**
    1.  **[ ] API Endpoint:** Develop a simple web server (e.g., using FastAPI) that exposes an endpoint to receive a scan report and returns an adjudication report.
    2.  **[ ] Scan Report Parser:** Write a module to parse standard Nessus/Trivy CSV output.
    3.  **[ ] GitHub Actions Workflow:** Create a basic CI/CD pipeline in GitHub Actions that:
        *   Triggers on a schedule or push.
        *   Runs a mock security scan.
        *   Sends the scan report to the Golden Potato API.
        *   Displays the adjudication result in the pipeline logs.
    4.  **[ ] Dockerization:** Containerize the application for consistent deployment.
*   **Estimated Timeline:** 3-4 Weeks

### Phase 3: Refinement & Usability
*   **Goal:** Improve the system's reliability, add user-friendly features, and enhance reporting.
*   **Key Deliverables:**
    1.  **[ ] Enhanced Reporting:** Format the adjudication report into a clear, human-readable Markdown table.
    2.  **[ ] Ticketing Integration:** Add a module to automatically create a Jira ticket for any finding adjudicated as "Non-Compliant."
    3.  **[ ] Configuration Management:** Move hard-coded values (like document paths and API keys) into a configuration file or environment variables.
    4.  **[ ] Comprehensive Documentation:** Finalize the `README.md` and `ARCHITECTURE.md` with detailed usage and deployment instructions.
*   **Estimated Timeline:** 2 Weeks

## 4. Key Risks

*   **Prompt Brittleness:** The accuracy of the agent is highly dependent on the quality of the prompt. Changes in the Gemini model could require prompt re-tuning.
    *   **Mitigation:** Treat prompts as code. Version them and create a small test suite to validate their output.
*   **Poor Document Quality:** The RAG pipeline is sensitive to the quality of the input documents. Scanned PDFs, complex tables, or poorly structured text may not be parsed correctly.
    *   **Mitigation:** Start with clean, digital-native documents. Develop pre-processing scripts to clean up text before embedding.
*   **Semantic Search Limitations:** The vector search may occasionally return irrelevant context, leading to incorrect adjudications.
    *   **Mitigation:** Refine the chunking strategy and enrich document chunks with metadata to improve retrieval accuracy.
