# ADAgentic System Overview

**ADAgentic** — *ADding ever-evolving Agentic functionality.*

**ADA**: A tribute to Ada Lovelace, often regarded as the first programmer.

**Agentic**: Describes the growing autonomy of this system.

**ADAgentic** — continuing the movement towards secure, safe, capable context-engineered programming.
Who knows how far we'll get...

This is an active project in early-stage development. Core architecture and tooling are being finalized. Contributions and feedback welcome.

This project is a secure, modular, locally-run AI coding framework designed to safely generate, test, document, and extend software projects using large language models. It leverages multi-agent planning (currently OpenHands), long-context local models (currently DevStral, but swapable too), secure web access via crawling, and Retrieval-Augmented Generation (RAG) to support structured and context-aware development.

The system is organized into **three operational zones**, each with dedicated components. Each zone operates within its **own Docker container**, providing clear boundaries between stages of the pipeline. This improves isolation, debuggability, and resource management.

Work-flow pipeline

A System that can take a prompt disuccion through to full project completion. The aimis for the agent use the reasoning capability of the coding llm to discuss and refine the idea with the user so it has enough info to be able to make all the [agent_instructions.md](agent_instructions.md) files needed for the PRP to be uploaded to RAG. 

  From this the PRP can me made and from that the code components can be made and tested. From the prompt discussion phase the project can be set up as design- and test-driven. The Instructions.md can mean that if different models are switched in due benefit from specific coding strengths, they will keep to the same coding standards rather than default to their separate trainings, which will keep the code coherent. 

  At any part of the process the agent can use the coder llm to reason what is needed and what to prompt the crawl4AI with to get the output from RAG/WEB for the part that is needed during the making of the PRP or code writing. The agent and LLM can retrieve this chunked data from RAG/crawl4AI at any point in the process, and being specific means  it uses efficient token count to get this info. And as Devstral has 128K context all info can hold all this needed info for writing each small component of the component list however large and complex the overall modular system might be for each project.

  The system can securely access the internet for things it doesn’t know having first checked the current context window, then RAG. If answer isn’t found it can pass the request to the crawl4AI in different docker. Info is only returned once it has been checked and sanitised. Examples of this would be for coding examples to have in the .md before writing the code. Making sure this is clean is needed to stop prompt injection issues and malicious/bad code being held in the .md files of the RAG in the third docker.

  Thanks to the system's modularity, components such as DevStral and OpenHands can be **swapped for improved models or extended versions** in the future as advancements occur. Future directions include incorporating MCP capabilities and enabling system self-maintenance and editing—where feasible and safe—as tools and frameworks continue to improve.


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
