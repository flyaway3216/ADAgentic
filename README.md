# ADAgentic System Overview

**ADAgentic** — *ADding ever-evolving Agentic functionality.*

**ADA**: A tribute to Ada Lovelace, often regarded as the first programmer.

**Agentic**: Describes the growing autonomy of this system.

**ADAgentic** — continuing the movement towards secure, safe, capable context-engineered programming.
Who knows how far we'll get...

This is an active project in early-stage development. Core architecture and tooling are being finalized. Contributions and feedback welcome.

This project is a secure, modular, locally-run AI coding framework designed to safely generate, test, document, and extend software projects using large language models. It leverages multi-agent planning (OpenHands), long-context local models (DevStral), secure web access via crawling, and Retrieval-Augmented Generation (RAG) to support structured and context-aware development.

The system is organized into **three operational zones**, each with dedicated components. Each zone operates within its **own Docker container**, providing clear boundaries between stages of the pipeline. This improves isolation, debuggability, and resource management.

The agent can use the LLM's reasoning to determine when more information is needed and query for additional context or documentation automatically. Thanks to the system's modularity, components such as DevStral and OpenHands can be **swapped for improved models or extended versions** in the future as advancements occur. Future directions include incorporating MCP capabilities and enabling system self-maintenance and editing—where feasible and safe—as tools and frameworks continue to improve.

---

## 🔹  Zone 1: Bootstrap & Validation Cycle

### Core Execution Layer

* **agent\_bootstrap.sh**

  * Primary user interface for launching projects, handling prompts, and coordinating initial flows
* **setup.sh**

  * Environment preparation and dependency setup
* **validate\_system.sh**

  * Pre-flight system validation to check requirements and dependencies
* **run\_tests.sh**

  * Executes full test suite across all modules and security layers

### Validation & Security Components

* **model\_policy\_enforcer.py**

  * Blocks untrusted models from performing critical tasks (e.g., codegen, crawling)
* **test\_threat\_vectors.sh**

  * Red-team style fuzz testing to simulate prompt injection and test sanitizers
* **template\_validator.py**

  * Verifies that generated `.md`, `.py`, and test files conform to defined templates
* **code\_scanner.py**

  * Runs Bandit, Ruff, Pyright to scan generated code for vulnerabilities and logic issues
* **fingerprint\_manager.py**

  * Hashes project files to detect tampering or regeneration drift

---

## 🔹 Zone 2: Project Generation Cycle

### Agent Intelligence Layer

* **taskflow\.yaml**

  * Defines multi-agent orchestration pipeline for planning, code generation, testing, and review
* **model\_profiles.yaml**

  * Maps model endpoints and trust levels
* **requirements.txt**

  * Lists Python dependencies

### Modular Agents

* **Planning Agent**

  * Analyzes user input, outlines components and architecture
* **Documentation Agent**

  * Generates specs, PRPs, and technical documentation
* **Code Generation Agent**

  * Implements modular code files and logic from specs
* **Testing Agent**

  * Builds test suites and validation routines
* **Review Agent**

  * Checks output against standards and system constraints
* **agent\_memory\_graph.py**

  * Logs agent actions, decisions, and dependencies
* **prompt\_debugger.py**

  * Captures prompts/responses for debugging and auditing

### Document Generation & QA

* **CODER\_RULES.md**

  * Internal coding standards for generated output
* **component\_stub.md**

  * Template for code component documentation
* **unit\_tests\_stub.md**

  * Template for generated test file documentation
* **.index.md**

  * Auto-updated file index
* **input/**, **output/**, **logs/**

  * Project inputs, generated content, and logs

---

## 🔹 Zone 3: RAG + Crawl Retrieval Cycle

### Context Retrieval Pipeline

* **context\_retriever.py**

  * Pulls context-relevant info from ChromaDB for the active agent
* **context\_searcher.py**

  * Searches in-memory context before querying the vector DB
* **rag\_orchestrator.py**

  * Manages retrieval flow, determines whether to fetch from Chroma or crawl
* **context\_audit\_logger.py**

  * Tracks which RAG inputs influenced code generation

### Web Retrieval & Sanitization

* **crawl4AI (Docker container)**

  * FastAPI wrapper around document ingestion & crawling
* **api\_server.py**

  * REST interface for triggering crawls
* **insert\_docs.py**

  * Handles sanitization, chunking, embedding of crawled data
* **file\_watcher.py**

  * Detects file changes and re-indexes documents automatically
* **prompt\_validator.py**

  * Blocks prompt injection and filters unsafe markdown/code
* **rag\_validator.py**

  * Lints markdown, extracts code blocks, and checks syntax before indexing
* **trusted\_sources.yaml**

  * Whitelists safe domains for crawl4AI to access
* **crawl\_rate\_limiter.py**

  * Prevents abusive crawl loops or spammed queries

### Vector DB Layer (Shared)

* **chroma (Docker container)**

  * Persistent vector database
* **shared\_chroma/**

  * Shared volume for vector DB between crawl4AI and the agent
* **vector\_db.py**: ❌ Removed — logic absorbed into insert\_docs.py

---

## ✅ Component Summary

* Zone 1: Bootstrap & Security = 11 Components
* Zone 2: Agent Flow & QA = 13 Components
* Zone 3: RAG & Retrieval = 14 Components

---

## 🔧 Future Goals

* Add Watchdog Agent for self-validation of logs and test results
* Enable self-repair loop using model-powered refactoring
* Auto-update CODER\_RULES.md from new coding patterns
* Optional UI via Streamlit or CLI wrappers

MIT License. Designed for local-first security-conscious development.

---

For more details or to contribute, see `ai_coder_integration_reference.md` (coming soon).
