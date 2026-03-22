# Golden Potato 🥔

**A Gemini-Powered GRC Automation Agent for Continuous FISMA Compliance**

[![Build Status](https://img.shields.io/badge/build-passing-brightgreen)](https://github.com/vypr907/golden-potato)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Project Status: Planning](https://img.shields.io/badge/status-planning-lightgrey.svg)](https://github.com/vypr907/golden-potato)

Golden Potato is a project designed to automate and streamline Governance, Risk, and Compliance (GRC) tasks for Information System Security Officers (ISSOs) managing FISMA systems within the NOAA/NESDIS environment.

It leverages a sophisticated Gemini Agent to continuously analyze security artifacts, adjudicate findings against an authorized baseline, and integrate seamlessly into a CI/CD pipeline.

---

### 📖 The Problem

GRC work is often a manual, time-consuming process of cross-referencing findings from security scans against a complex set of documents. For any given FISMA system, an ISSO must constantly check vulnerabilities against:

*   The **System Security Plan (SSP)** to understand how controls are implemented.
*   The **FIPS 200 Exceptions Matrix** for documented deviations.
*   **Deviation Documents** and **Accepted Risk** memos for authorized exceptions.

This manual process is slow, prone to error, and creates a significant delay between identifying a finding and determining its true compliance status.

### ✨ The Solution

Golden Potato introduces a "Compliance-as-Code" approach. It uses a Gemini Agent equipped with a **Retrieval-Augmented Generation (RAG)** architecture. This allows the agent to ingest and understand the specific context of your FISMA system.

Instead of just flagging a vulnerability, the agent can **adjudicate** it by checking its private knowledge base, which is built from your uploaded GRC documents.

**Core Features:**
*   **🤖 Context-Aware Analysis:** The agent doesn't just know NIST 800-53; it knows *your implementation* of it, including tailored controls and accepted risks.
*   **🔍 Automated Adjudication:** For each finding, the agent determines if it is a true "Non-Compliant" issue, "Compliant (Tailored)", or "Not a Finding (Risk Accepted)" and provides justification.
*   **🔄 CI/CD Integration:** The agent is designed to be a step in your CI/CD pipeline. Scan reports are automatically fed to the agent, which can then generate reports, create tickets, or even fail a build.
*   **⬆️ Always Up-to-Date:** The agent's knowledge base is refreshed every time you update your core GRC documents, ensuring its analysis is always based on the current authorized baseline.

---

### 🚀 Getting Started

This project is currently in the planning and initial development phase. The immediate next steps involve setting up the core architecture for the RAG pipeline and the Gemini Agent.

**Prerequisites (for development):**
*   Python 3.10+
*   Access to Google AI Studio or Vertex AI for Gemini API.
*   A vector database solution (e.g., ChromaDB, Pinecone).

**Installation (coming soon):**
```bash
# Clone the repository
git clone https://github.com/vypr907/golden-potato.git
cd golden-potato

# Install dependencies
pip install -r requirements.txt
