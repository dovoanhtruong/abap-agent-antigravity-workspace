# ABAP Agent Skill Router

This router serves as the central directory and execution guide for the AI Agent. It maps all available skills in this workspace, enabling the agent to dynamically load the appropriate technical context based on user requests, preventing context bloat and improving accuracy.

---

## 🤖 SYSTEM INSTRUCTION: HOW TO ROUTE SKILLS
When you receive a task in this workspace, you **MUST** follow these steps:
1. **Analyze the Request**: Identify if the task belongs to a **Consultant** (analysis, UI mapping, business logic extraction) or a **Developer** (coding, testing, deployment).
2. **Match Skills**: Look up the required skills in the [Skill Registry](#-skill-registry) below using the **Trigger Keywords** and **Description**.
3. **Load the Skill**: Read the matched `SKILL.md` file using your file reading tool. Do **NOT** read multiple unrelated skills unless they are explicitly chain-dependent.
4. **Execute**: Adopt the role specified in the loaded skill and execute the instructions step-by-step.

---

## 📋 SKILL REGISTRY

### 🏛️ 1. Consultant Skills (Business Analysis & Architecture)
These skills focus on translating functional requirements into structured technical designs.

| Skill Name | Role | Path | Description | Trigger Keywords |
| :--- | :--- | :--- | :--- | :--- |
| **Data Model Extractor** | Expert SAP Data Architect | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Consultant/fs-data-model-extractor/SKILL.md) | Extracts standard/custom tables, CDS Views, join conditions, and output fields from Functional Specifications (FS). | `data model`, `extract tables`, `joins`, `relations`, `FS analysis` |
| **Fiori UI Elements Mapper** | Fiori UX/UI Technical Consultant | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Consultant/fs-fiori-ui-elements-mapper/SKILL.md) | Translates report layout requirements into Fiori Elements annotations (`selectionField`, `lineItem`, etc.). | `fiori elements`, `selection fields`, `line items`, `sorting`, `facets` |
| **ABAP Logic & Behavior Translator** | Senior ABAP Cloud Developer (Consultant) | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Consultant/fs-logic-behavior-translator/SKILL.md) | Analyzes processing logic to determine implementation layers (CDS logic, Virtual Elements, or RAP Behavior Pool). | `business rules`, `calculated fields`, `virtual elements`, `derived logic`, `actions` |
| **Integration & API Analyzer** | Expert SAP Integration Architect | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Consultant/fs-integration-api-analyzer/SKILL.md) | Extracts integration patterns, API specifications (OData, REST), JSON payloads, and mapping tables from FS. | `integration`, `OData API`, `REST API`, `mapping`, `JSON payload`, `payload` |

---

### 💻 2. Developer Skills (Technical Implementation)
These skills contain precise syntax rules, code templates, and development guidelines for ABAP Cloud.

| Skill Name | Path | Description | Trigger Keywords |
| :--- | :--- | :--- | :--- |
| **ABAP Lint & Review** | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Developer/abap/SKILL.md) | Validates ABAP code quality using `abaplint` rules and Clean ABAP standards. | `abaplint`, `lint`, `code review`, `syntax check` |
| **ABAP Cloud / Clean Core** | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Developer/abap-cloud/SKILL.md) | Enforces ABAP Cloud restrictions, 3-tier extensibility, and unreleased API wrappers. | `clean core`, `3-tier`, `restricted API`, `cloud development`, `wrapper` |
| **ABAP Cloud Migration** | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Developer/abap-cloud-migration/SKILL.md) | Workflow and mapping patterns for migrating classic custom ABAP code to Cloud Tier 1. | `migration`, `migrate`, `cloud readiness`, `atc scan` |
| **ABAP SQL & AMDP** | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Developer/abap-sql-amdp/SKILL.md) | Modern ABAP SQL (inline, CTEs, window functions) and SQLScript AMDP class patterns. | `AMDP`, `window functions`, `CTE`, `SQLScript`, `SQL query` |
| **ABAP Unit Testing** | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Developer/abap-unit-testing/SKILL.md) | ABAP Unit test setups, mock double frameworks, and test environments for CDS and OSQL. | `unit test`, `mock`, `test double`, `cl_abap_unit_assert` |
| **ATC Cloudification** | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Developer/atc-cloudification/SKILL.md) | Configuration and notes for setting up ATC Cloud Readiness & Clean Core variants. | `ATC`, `cloud readiness`, `cloudification repository` |
| **Authorization & IAM** | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Developer/authorization-iam/SKILL.md) | Implements DCL (Access Controls), BTP IAM apps, business roles, and RAP authorizations. | `DCL`, `authorization`, `IAM`, `business catalog`, `pfcg_auth` |
| **BAdI & Enhancements** | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Developer/badi-enhancement/SKILL.md) | Standard SAP extensions using BAdIs, Enhancement Spots, and Key User Extensibility. | `BAdI`, `enhancement spot`, `implicit`, `explicit`, `extend` |
| **BTP ABAP Environment** | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Developer/btp-abap-environment/SKILL.md) | Provisioning, ADT connection, and communication arrangements setup in Steampunk. | `BTP`, `Steampunk`, `communication arrangement`, `ADT connection` |
| **BTP Diagram Generator** | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Developer/btp-diagram-generator/SKILL.md) | Python builder library for generating draw.io/Horizon design solutions diagram. | `draw.io`, `diagram`, `architecture diagram`, `btp_builder` |
| **CDS View Entities** | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Developer/cds-view-entities/SKILL.md) | Core CDS View Entity syntax, associations, metadata extensions, and annotations. | `CDS`, `view entity`, `association`, `projection`, `metadata extension` |
| **Clean ABAP** | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Developer/clean-abap/SKILL.md) | Strict coding styles, clean methods, small parameters, and exception handling patterns. | `clean abap`, `naming conventions`, `refactoring`, `style guide` |
| **Naming Conventions** | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Developer/naming-convension/SKILL.md) | Project-specific naming guidelines (FPT) for database tables, CDS, RAP, and Packages. | `naming convention`, `prefix`, `suffix`, `ZA_`, `ZC_`, `ZR_` |
| **OData Service Development** | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Developer/odata/SKILL.md) | RAP OData V4/V2, SEGW classic service, and external OData client proxy consumption. | `OData`, `service definition`, `service binding`, `V4`, `client proxy` |
| **RAP Model** | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Developer/rap/SKILL.md) | Managed/Unmanaged RAP BO, behavior pool, draft, validations, and determinations. | `RAP`, `behavior definition`, `EML`, `BDEF`, `%tky`, `%cid` |
| **RAP Business Events** | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Developer/rap-business-events/SKILL.md) | Defines and raises entity events linked to SAP Event Mesh for event-driven patterns. | `event mesh`, `business event`, `raise event`, `event binding` |
| **Released ABAP Classes** | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Developer/released-abap-classes/SKILL.md) | Full catalog and examples of BTP/Cloud-released helper classes (Console, Mail, HTTP). | `released class`, `CL_BCS_MAIL`, `XCO_CP_JSON`, `UUID` |
| **SAP Fiori Apps Reference** | [SKILL.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/skills/Developer/sap-fiori-apps-reference/SKILL.md) | Generates Fiori Launchpad URLs and queries the Fiori Apps Reference Library. | `Fiori library`, `AppList`, `Launchpad URL`, `semantic object` |

---

## 🔀 WORKFLOW ROUTING INTEGRATION
The workflows inside `.agents/workflows/` invoke these skills dynamically:
- **/sap-dev-analytic-fs**: Sequentially loads `Data Model Extractor`, `Fiori UI Elements Mapper`, and `ABAP Logic & Behavior Translator` to generate Technical Specs from an FS.
- **/sap-dev-create-report**: Steps reference `CDS View Entities`, `Authorization & IAM`, `RAP Model`, `OData Service Development`, and `Clean ABAP` to write and deploy code.
