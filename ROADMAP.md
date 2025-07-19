# ROADMAP.md – ADAgentic Project

A high-level development strategy outlining phases, milestones, and goals. The roadmap is designed to gradually increase security, autonomy, and reliability while maintaining modularity for future model improvements.

## PHASE 1 — Core Setup & Minimal Loop

**Goal:** Get DevStral + OpenHands + shared ChromaDB working with *testable prompt → output → file*


Outcome: Single-agent run working + environment is stable

**Tasks:**

* Set up DevStral and confirm local inference works
* Set up OpenHands agent interface
* Configure docker-compose to run:

  * agent-llm (OpenHands + DevStral)
  * crawl4AI
  * ChromaDB
* Test basic RAG with a **pre-filled .md** file
* Trigger single prompt: “Generate hello world project with tests”
* Check it writes .py, .md, .test file into /output

**Safety Gate:**

* Manual review of output
* Print/log raw prompt and retrieved context
* Confirm RAG doesn’t leak anything weird

---

**PHASE 2 — Security + Validation Foundation**

**Goal:** Prevent unsafe ingestion or code generation


Outcome: Clean pipeline with trust boundaries and testable filters

**Tasks:**

* Add prompt\_validator.py to sanitize all .md + web input
* Add rag\_validator.py to filter markdown and code before Chroma
* Add code\_scanner.py (Bandit, Ruff, MyPy)
* Add test\_threat\_vectors.sh to simulate threats
* Add model\_policy\_enforcer.py to block untrusted models
* Add fingerprint\_manager.py to track project integrity

**Safety Gate:**

* Threat test must pass
* Crawl one known repo and confirm:

  * Clean .md saved
  * Nothing sketchy enters the vector store

---

**⚙️ PHASE 3 — Multi-Agent Buildout**

**Goal:** Enable structured prompting and reliable modular output


Outcome: AI builds real project scaffolds in steps

**Tasks:**

* Activate OpenHands multi-agent via taskflow\.yaml
* Define Planning Agent → Doc Agent → Code Agent → Test Agent
* Build/use component\_stub.md, unit\_tests\_stub.md, CODER\_RULES.md
* Add template\_validator.py to enforce structure
* Use prompt\_debugger.py to track failures

**Safety Gate:**

* All agent outputs must:

  * Follow stub format
  * Pass static scan
  * Be traceable to prompt/context chunks
* Prompt failures must be logged and readable

---

**PHASE 4 — Retrieval, Expansion, and Reuse**

**Goal:** Support real RAG + crawling with safe vectorization


Outcome: Clean data comes in, is used safely, and reused efficiently

**Tasks:**

* Enable full crawl4AI flow with trusted\_sources.yaml
* Add crawl\_rate\_limiter.py to stop crawl loops
* Use context\_audit\_logger.py to log RAG chunk influence
* Confirm deduplication and re-query logic in context\_searcher.py

**Safety Gate:**

* All crawled sources must:

  * Be allowlisted
  * Pass sanitizers
  * Log origin and chunk hash
* RAG logs must trace back to file/chunk/prompt that triggered them

---

**PHASE 5 — MCP Integration Layer**

**Goal:** Incorporate Modular Constructive Processes (MCPs) to improve reasoning, adaptation, and modular build pipelines


Outcome: Agent cognition and project construction become smarter and more reusable

**Tasks:**

* Design minimal MCP structure for planning + code adaptation
* Integrate MCP-aware agent or replace OpenHands stage with MCP-compatible planner
* Allow MCPs to suggest structured project transformations
* Ensure RAG + validator components are MCP-compatible

**Safety Gate:**

* MCP reasoning outputs logged and explainable
* No direct code execution until passed through validation stack
* MCP decisions traceable to agent logs or audit trail

---

**PHASE 6 — Toward Self-Maintaining System**

**Goal:** Let system iterate on and improve itself safely


Outcome: You become the supervisor, not the builder

**Tasks:**

* Create internal “Watchdog Agent” to monitor logs and suggest fixes
* Let agent refactor its own \*.py scripts (with versioned backup)
* Log “code smells” and retry/fix suggestions via agents
* Ultimately Extend run\_tests.sh to validate its own generated components

**Safety Gate:**

* You approve all self-modifications until confidence is high
* Self-generated updates go through full validation stack
* Fingerprints + logs track every change

---

## potential additions

* Optional: Build CLI menus for system navigation
* Optional: Streamlit dashboard for visual control
* Optional: Export project plans to .html for external sharing

---

> Last updated: 2025-07-16
