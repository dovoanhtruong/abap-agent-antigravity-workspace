# 🚀 SAP ABAP Cloud Agent Workspace

Welcome to the **SAP ABAP Cloud Agent Workspace**. This is an intelligent workspace specifically optimized for Pair-Programming between you and the AI Agent (Antigravity) to develop applications on the **SAP BTP ABAP Environment** and **S/4HANA Cloud (Clean Core)** platforms.

This workspace comes with built-in strict governance rules, a deep knowledge base of Skills, and automated Workflows to transform Functional Specification (FS) documents into high-quality ABAP RAP source code, ensuring strict adherence to **Clean Core & Clean ABAP** standards.

> ### ⭐ For best results, pair this workspace with 2 MCP servers
> Several skills (`find-released-cds-view`, `fs-logic-behavior-translator`, `fs-integration-api-analyzer`, `sap-fiori-apps-reference`, `atc-cloudification`, and the "verify before use" rule in `sap-dev-rule.md` §9) are written to call "whichever MCP server/tool your environment exposes" for SAP CDS/documentation search — they work without one, but are far faster and more accurate with these two connected:
>
> | MCP Server | What it gives the Agent |
> |---|---|
> | **[cds-kb-mcp](https://github.com/dovoanhtruong/cds-kb-mcp)** | Semantic search across 7,355 released S/4HANA Cloud CDS views (`search_cds`, `get_cds_view`, `get_views_by_tag`, `get_taxonomy`) — this is what powers `find-released-cds-view` and the Clean-Core-replacement checks in the FS-analysis skills, instead of the Agent guessing a CDS view name. |
> | **[mcp-sap-docs](https://github.com/dovoanhtruong/mcp-sap-docs)** | Hybrid search over SAP Help Portal, SAP Accelerator Hub (OData/REST/SOAP APIs), the Fiori Apps Library, and Clean Core released-object data — this is what backs the "search official SAP documentation before proposing an API/CDS replacement" steps required across the Consultant skills and workflows. |
>
> Both are hosted MCP servers (no local data download); see each repo's README for the exact `mcpServers` config snippet for your MCP client (Claude Desktop, Cursor, Antigravity, etc.). Without them, the Agent will ask you to point it at whatever MCP/ADT tool your environment does expose (per rule §9) rather than guessing an API name.

---

## 📂 Workspace Directory Structure

The project is scientifically organized around the `.agents/` configuration directory:

```text
abap_workspaces/
├── .agents/                        # 🧠 Artificial Intelligence Coordination Center (Agent Hub)
│   ├── SKILLS_ROUTER.md            # 🔀 Dynamic skill routing guide for the Agent
│   ├── rules/
│   │   └── sap-dev-rule.md         # 🛡️ Mandatory rules (Clean Core, Custom Only, TR...)
│   ├── skills/                     # 📚 Deep specialized skill library for the Agent
│   │   ├── Consultant/             # 🏛️ Business Analysis & Architecture skills
│   │   │   ├── fs-data-model-extractor/
│   │   │   ├── fs-fiori-ui-elements-mapper/
│   │   │   ├── fs-logic-behavior-translator/
│   │   │   ├── fs-integration-api-analyzer/
│   │   │   ├── fs-vision-extractor/
│   │   │   └── find-released-cds-view/   # uses cds-kb-mcp when available
│   │   ├── Developer/              # 💻 Development & Technical ABAP Cloud skills
│   │   │   ├── abap/ , abap-cloud/ , clean-abap/ , naming-convension/ , modern-abap-syntax/ , oo-design-patterns/ ...
│   │   │   └── rap/ , cds-view-entities/ , odata/ , authorization-iam/ , abap-generative-ai/ ...
│   │   └── Productivity/           # 🚀 Performance Optimization & Context Management skills
│   │       └── grill-me/ , caveman/ , handoff/ , scratchpad/
│   └── workflows/                  # ⚙️ Business process automation scripts
│       ├── sap-dev-fs-analytic.md  # Process for analyzing FS into Technical Spec
│       ├── sap-dev-create-report.md# Process for auto-generating ABAP RAP reports
│       ├── sap-dev-api-inbound.md  # Process for Inbound API integration based on Z_API_FWK
│       ├── sap-dev-api-outbound.md # Process for Outbound API integration based on Z_API_FWK
│       ├── sap-dev-bug-fix.md      # Process for root-cause debugging & regression-safe fixes
│       ├── sap-dev-code-analysis.md # Process for analyzing SAP system architecture
│       └── sap-dev-code-review.md  # Process for strict Code Review & QA
├── artifacts/                       # 📦 Single root for all input/output artifacts (gitignored)
│   ├── fs_docs/                     # 📄 Input Functional Specification (FS) documents
│   ├── technical_specifications/    # Technical Specifications (TS_*.md)
│   ├── scratchpads/                 # Architectural drafts, planning & progress ledgers
│   │   └── review/                  # Code Review reports (review_*.md)
│   ├── walkthroughs/                # Deployment guides, testing & task checklists
│   ├── metadata_extensions/         # Generated Metadata Extension (DDLX) source, pending manual ADT creation
│   └── system_analysis/             # System/package analysis reports
└── README.md                       # 📖 User documentation (This file)
```

---

## 🛠️ Core Components & How They Work

### 1. Agent Capability Router (`SKILLS_ROUTER.md`)
This is the central directory managing all Skills. When you assign a task, the Agent automatically matches keywords in your request with this directory to dynamically load the necessary technical context, avoiding context bloat and optimizing token usage.
* **Context Optimization:** The system supports parallel loading of **Productivity** skills (e.g., `Scratchpad` for drafting before coding, `Handoff` for context transition, `Grill Me` for interview-style clarification, `Caveman` for terse chat narration) alongside technical skills, helping maintain coherent system thinking.

### 2. Automated Development Rules (`rules/sap-dev-rule.md`)
A single, deliberately compact rule file (11 short sections, always loaded) — kept dense on purpose so it doesn't get lost in a long session. It forces the Agent to strictly follow:
* **Modern ABAP & Design Patterns:** Enforce the use of modern ABAP syntax (Constructor Expressions, String Templates) and GoF OO Design Patterns.
* **Clean Core:** Use CDS Views to read data and EML (Entity Manipulation Language) to write data. Absolutely no direct modification of physical tables.
* **Custom Only (Z/Y):** Only operate on custom Z/Y objects of the project. Do not modify SAP standard objects.
* **TR & Package:** Every new/modified object must clearly declare a Package and a Transport Request.
* **Evidence-Based Reporting:** "Activated" ≠ "Correct" — every completion claim must cite actual evidence (command run, output observed, or a real payload the user provided), never "should work / probably fine."
* **Token Efficiency:** Chat narration uses the `Caveman` skill (see below) to stay terse — but never on code, saved reports, or security/consent warnings.

### 3. Automation Scripts (Workflows)
Use dedicated Slash Commands designed for complex processes:
* `/sap-dev-fs-analytic`: Automatically triggers the Consultant skill chain to deeply analyze Word/PDF FS files, extract the Data Model structure, Fiori Elements layout, balance calculation/fallback logic, and output a standard Technical Specification.
* `/sap-dev-create-report`: Takes a Technical Spec as input, automatically triggers the Developer skill chain to write clean code, create CDS View Entities, Access Controls (DCL), Business Services, RAP BO Behavior Pools, and perform automated testing.
* `/sap-dev-bug-fix`: Root-causes a reported bug against user-provided mock data, gets explicit approval on a Cross-Impact Report before touching anything, then fixes it with a mandatory ABAP Unit Test as regression proof.
* `/sap-dev-api-inbound`: Build external API receiving functionalities adhering to the `Z_API_FWK` architecture.
* `/sap-dev-api-outbound`: Build outbound calls to other systems ensuring logging mechanisms and response handling via `execute_api`.
* `/sap-dev-code-analysis`: Automatically scan, deep-dive, and generate comprehensive architecture documentation for objects/packages.
* `/sap-dev-code-review`: Perform rigorous source code reviews (including Cross-Impact Check), evaluate potential risks, and propose performance/maintainability optimizations.

---

## 🚀 Quick Start Guide

### Step 1: Prepare Input Documents
Ensure you have placed the Functional Specification (FS) document into the `artifacts/fs_docs/` directory of the workspace (e.g., a `.docx` Word file or Text file).

### Step 2: Trigger the FS Analysis Process
Send an analysis request to the Agent with the document path.
* *Example:* `"Please trigger the /sap-dev-fs-analytic workflow to analyze the FS document [SAPER_2025_PM_FS.docx](./artifacts/fs_docs/SAPER_2025_PM_FS.docx) belonging to Package Z_INVENTORY_REPORT"`

### Step 3: Evaluate Technical Spec & Generate Code
After the Agent completes the analysis and returns a standard Technical Specification structure, please review it. Then, trigger the `/sap-dev-create-report` command for the Agent to automatically generate comprehensive ABAP RAP code for you.

---

## ⚙️ Notes for Developers
* **Relative Paths:** All configuration documents in this project use Relative Paths so you can move the workspace to any personal computer or Cloud environment without breaking links.
* **Inheritance & Development:** You can easily add new Skills to the `.agents/skills/` directory and declare them in the registration table within `SKILLS_ROUTER.md` to upgrade your Agent's intelligence.
* **MCP Servers:** See the highlighted callout near the top of this README — connect `cds-kb-mcp` and `mcp-sap-docs` for the best experience; several skills degrade gracefully (asking you for a tool/manual lookup) without them, but work best with them.
