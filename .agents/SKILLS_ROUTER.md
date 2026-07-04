# ABAP Agent Skill Router

This router serves as the central directory and execution guide for the AI Agent. It maps all available skills in this workspace, enabling the agent to dynamically load the appropriate technical context based on user requests, preventing context bloat and improving accuracy.

---

## 🤖 SYSTEM INSTRUCTION: HOW TO ROUTE SKILLS
When you receive a task in this workspace, you **MUST** follow these steps:
1. **Analyze the Request**: Identify if the task belongs to a **Consultant** (analysis, UI mapping, business logic extraction) or a **Developer** (coding, testing, deployment).
2. **Match Skills**: Look up the required skills in the [Skill Registry](#-skill-registry) below using the **Trigger Keywords** and **Description**.
3. **Load the Skill**: Read the matched `SKILL.md` file using your file reading tool. Do **NOT** read multiple unrelated skills unless they are explicitly chain-dependent. *Note: You MAY load a Productivity Skill (like Scratchpad or Handoff) in parallel with technical skills to optimize your workflow without bloating context.*
4. **Execute**: Adopt the role specified in the loaded skill and execute the instructions step-by-step.

---

## 📋 SKILL REGISTRY

### 🏛️ 1. Consultant Skills (Business Analysis & Architecture)
These skills focus on translating functional requirements into structured technical designs.

| Skill Name | Role | Path | Description | Trigger Keywords |
| :--- | :--- | :--- | :--- | :--- |
| **Data Model Extractor** | Expert SAP Data Architect | [SKILL.md](./skills/Consultant/fs-data-model-extractor/SKILL.md) | Extracts standard/custom tables, CDS Views, join conditions, and output fields from Functional Specifications (FS). | `data model`, `extract tables`, `joins`, `relations`, `FS analysis`, `trích xuất bảng`, `sơ đồ dữ liệu`, `phân tích bảng` |
| **Fiori UI Elements Mapper** | Fiori UX/UI Technical Consultant | [SKILL.md](./skills/Consultant/fs-fiori-ui-elements-mapper/SKILL.md) | Translates report layout requirements into Fiori Elements annotations (`selectionField`, `lineItem`, etc.). | `fiori elements`, `selection fields`, `line items`, `sorting`, `facets`, `giao diện fiori`, `bộ lọc`, `hiển thị cột`, `bố cục` |
| **ABAP Logic & Behavior Translator** | Senior ABAP Cloud Developer (Consultant) | [SKILL.md](./skills/Consultant/fs-logic-behavior-translator/SKILL.md) | Analyzes processing logic to determine implementation layers (CDS logic, Virtual Elements, or RAP Behavior Pool). | `business rules`, `calculated fields`, `virtual elements`, `derived logic`, `actions`, `logic xử lý`, `quy tắc nghiệp vụ`, `tính toán`, `hành vi` |
| **Integration & API Analyzer** | Expert SAP Integration Architect | [SKILL.md](./skills/Consultant/fs-integration-api-analyzer/SKILL.md) | Extracts integration patterns, API specifications (OData, REST), JSON payloads, and mapping tables from FS. | `integration`, `OData API`, `REST API`, `mapping`, `JSON payload`, `payload`, `tích hợp`, `giao tiếp hệ thống`, `kết nối API`, `cấu trúc JSON` |
| **FS Vision Extractor** | Expert SAP Multimodal Analyst | [SKILL.md](./skills/Consultant/fs-vision-extractor/SKILL.md) | Extracts UI mockups, Excel tables, and flowchart logic from images embedded in FS documents into Markdown. | `image`, `mockup`, `vision`, `extract image`, `flowchart`, `excel screenshot`, `xử lý ảnh`, `nhận diện ảnh`, `trích xuất ảnh` |
| **Find Released CDS View** | Expert SAP Data Architect | [SKILL.md](./skills/Consultant/find-released-cds-view/SKILL.md) | Finds the best SAP released CDS view (DDLS) for a RAP/reporting field by matching business object, screen context, data grain, field availability, and local coverage against S/4HANA Cloud Public Edition released APIs. | `released CDS`, `find CDS view`, `DDLS`, `released API`, `clean core CDS`, `value help view`, `I_*`, `tìm CDS view`, `CDS released`, `data source RAP` |

---

### 💻 2. Developer Skills (Technical Implementation)
These skills contain precise syntax rules, code templates, and development guidelines for ABAP Cloud.

| Skill Name | Path | Description | Trigger Keywords |
| :--- | :--- | :--- | :--- |
| **ABAP Lint & Review** | [SKILL.md](./skills/Developer/abap/SKILL.md) | Validates ABAP code quality using `abaplint` rules and Clean ABAP standards. | `abaplint`, `lint`, `code review`, `syntax check`, `kiểm tra code`, `đánh giá code`, `tiêu chuẩn abap` |
| **ABAP Cloud / Clean Core** | [SKILL.md](./skills/Developer/abap-cloud/SKILL.md) | Enforces ABAP Cloud restrictions, 3-tier extensibility, and unreleased API wrappers. | `clean core`, `3-tier`, `restricted API`, `cloud development`, `wrapper`, `chuẩn hóa core`, `tier 1` |
| **ABAP Cloud Migration** | [SKILL.md](./skills/Developer/abap-cloud-migration/SKILL.md) | Workflow and mapping patterns for migrating classic custom ABAP code to Cloud Tier 1. | `migration`, `migrate`, `cloud readiness`, `atc scan`, `chuyển đổi hệ thống`, `nâng cấp cloud` |
| **ABAP SQL & AMDP** | [SKILL.md](./skills/Developer/abap-sql-amdp/SKILL.md) | Modern ABAP SQL (inline, CTEs, window functions) and SQLScript AMDP class patterns. | `AMDP`, `window functions`, `CTE`, `SQLScript`, `SQL query`, `truy vấn dữ liệu`, `amdp class`, `modern sql` |
| **ABAP Unit Testing** | [SKILL.md](./skills/Developer/abap-unit-testing/SKILL.md) | ABAP Unit test setups, mock double frameworks, and test environments for CDS and OSQL. | `unit test`, `mock`, `test double`, `cl_abap_unit_assert`, `kiểm thử tự động`, `unit test abap`, `chạy test` |
| **ATC Cloudification** | [SKILL.md](./skills/Developer/atc-cloudification/SKILL.md) | Configuration and notes for setting up ATC Cloud Readiness & Clean Core variants. | `ATC`, `cloud readiness`, `cloudification repository`, `quét atc`, `lỗi ready`, `atc check` |
| **Authorization & IAM** | [SKILL.md](./skills/Developer/authorization-iam/SKILL.md) | Implements DCL (Access Controls), BTP IAM apps, business roles, and RAP authorizations. | `DCL`, `authorization`, `IAM`, `business catalog`, `pfcg_auth`, `phân quyền`, `quyền truy cập`, `bảo mật dcl` |
| **BAdI & Enhancements** | [SKILL.md](./skills/Developer/badi-enhancement/SKILL.md) | Standard SAP extensions using BAdIs, Enhancement Spots, and Key User Extensibility. | `BAdI`, `enhancement spot`, `implicit`, `explicit`, `extend`, `mở rộng hệ thống`, `badi spot`, `bản vá` |
| **BTP ABAP Environment** | [SKILL.md](./skills/Developer/btp-abap-environment/SKILL.md) | Provisioning, ADT connection, and communication arrangements setup in Steampunk. | `BTP`, `Steampunk`, `communication arrangement`, `ADT connection`, `môi trường btp`, `kết nối adt` |
| **BTP Diagram Generator** | [SKILL.md](./skills/Developer/btp-diagram-generator/SKILL.md) | Python builder library for generating draw.io/Horizon design solutions diagram. | `draw.io`, `diagram`, `architecture diagram`, `btp_builder`, `vẽ sơ đồ`, `diagram architecture` |
| **CDS View Entities** | [SKILL.md](./skills/Developer/cds-view-entities/SKILL.md) | Core CDS View Entity syntax, associations, metadata extensions, and annotations. | `CDS`, `view entity`, `association`, `projection`, `metadata extension`, `tạo cds view`, `cds entity`, `view mở rộng` |
| **Clean ABAP** | [SKILL.md](./skills/Developer/clean-abap/SKILL.md) | Strict coding styles, clean methods, small parameters, and exception handling patterns. | `clean abap`, `naming conventions`, `refactoring`, `style guide`, `mã sạch`, `viết code sạch` |
| **Naming Conventions** | [SKILL.md](./skills/Developer/naming-convension/SKILL.md) | Project-specific naming guidelines (FPT) for database tables, CDS, RAP, and Packages. | `naming convention`, `prefix`, `suffix`, `ZA_`, `ZC_`, `ZR_`, `quy tắc đặt tên`, `tiền tố`, `hậu tố` |
| **OData Service Development** | [SKILL.md](./skills/Developer/odata/SKILL.md) | RAP OData V4/V2, SEGW classic service, and external OData client proxy consumption. | `OData`, `service definition`, `service binding`, `V4`, `client proxy`, `dịch vụ odata`, `service binding` |
| **RAP** | [SKILL.md](./skills/Developer/rap/SKILL.md) | Managed/Unmanaged RAP BO, behavior pool, draft, validations, and determinations. | `RAP`, `behavior definition`, `EML`, `BDEF`, `%tky`, `%cid`, `mô hình rap`, `behavior pool`, `bdef` |
| **RAP Query Provider** | [SKILL.md](./skills/Developer/rap-query-provider/SKILL.md) | Implements Custom Entity query providers (IF_RAP_QUERY_PROVIDER) with paging, sorting, and filtering. | `IF_RAP_QUERY_PROVIDER`, `custom entity class`, `select method`, `get_sort_elements`, `get_paging`, `set_total_number_of_records`, `Query not fully covered` |
| **RAP Business Events** | [SKILL.md](./skills/Developer/rap-business-events/SKILL.md) | Defines and raises entity events linked to SAP Event Mesh for event-driven patterns. | `event mesh`, `business event`, `raise event`, `event binding`, `sự kiện rap`, `event mesh` |
| **Released ABAP Classes** | [SKILL.md](./skills/Developer/released-abap-classes/SKILL.md) | Full catalog and examples of BTP/Cloud-released helper classes (Console, Mail, HTTP). | `released class`, `CL_BCS_MAIL`, `XCO_CP_JSON`, `UUID`, `thư viện class`, `helper class` |
| **SAP Fiori Apps Reference** | [SKILL.md](./skills/Developer/sap-fiori-apps-reference/SKILL.md) | Generates Fiori Launchpad URLs and queries the Fiori Apps Reference Library. | `Fiori library`, `AppList`, `Launchpad URL`, `semantic object`, `tra cứu ứng dụng`, `fiori library` |
| **Modern ABAP Syntax** | [SKILL.md](./skills/Developer/modern-abap-syntax/SKILL.md) | Modern ABAP for Cloud syntax: Constructor Expressions, string processing, dynamic programming. | `constructor expression`, `string template`, `REDUCE`, `VALUE`, `inline declaration`, `cú pháp abap`, `abap syntax` |
| **OO Design Patterns** | [SKILL.md](./skills/Developer/oo-design-patterns/SKILL.md) | GoF Object-Oriented Design Patterns implemented in modern ABAP (Singleton, Factory, Observer, etc.). | `design pattern`, `singleton`, `factory`, `observer`, `strategy`, `mẫu thiết kế`, `oop abap` |
| **ABAP Generative AI** | [SKILL.md](./skills/Developer/abap-generative-ai/SKILL.md) | Integration of LLMs and Generative AI in ABAP Cloud using ISLM and ABAP AI SDK. | `generative ai`, `ai sdk`, `islm`, `llm`, `tích hợp ai`, `openai abap` |

---

### 🚀 3. Productivity Skills (Efficiency & Context Management)
These skills modify the agent's behavior to optimize communication, planning, and continuity.

| Skill Name | Role | Path | Description | Trigger Keywords |
| :--- | :--- | :--- | :--- | :--- |
| **Grill Me** | Expert Interviewer | [SKILL.md](./skills/Productivity/grill-me/SKILL.md) | Asks targeted questions to clarify requirements before starting work. | `grill me`, `clarify`, `interview`, `hỏi tôi`, `làm rõ` |
| **Caveman** | Concise Communicator | [SKILL.md](./skills/Productivity/caveman/SKILL.md) | Provides ultra-terse, fluff-free technical responses. | `caveman`, `short`, `terse`, `ngắn gọn`, `không rườm rà` |
| **Handoff** | Session Manager | [SKILL.md](./skills/Productivity/handoff/SKILL.md) | Summarizes context and progress for seamless transition between sessions. | `handoff`, `summary`, `transition`, `chuyển giao`, `tổng kết` |
| **Document Markdown Converter** | Document Pre-processor | [SKILL.md](./skills/Productivity/document-markdown-converter/SKILL.md) | Uses MarkItDown CLI to parse binary documents (PDF/DOCX) into token-efficient Markdown before analysis. | `markitdown`, `convert document`, `parse document`, `tiền xử lý tài liệu`, `pdf`, `docx` |
| **Scratchpad** | Structured Thinker | [SKILL.md](./skills/Productivity/scratchpad/SKILL.md) | Uses a working document to draft, plan, and track complex changes. | `scratchpad`, `draft`, `plan`, `nháp`, `lên kế hoạch` |

---

## 🔀 WORKFLOW ROUTING INTEGRATION
The workflows inside `.agents/workflows/` invoke these skills dynamically:
- **/sap-dev-fs-analytic**: 6-phase pipeline — `Document Markdown Converter` + `FS Vision Extractor` (pre-process), `Data Model Extractor` + `Find Released CDS View` (foundation), `Fiori UI Elements Mapper` + `ABAP Logic & Behavior Translator` + `Integration & API Analyzer` (parallel-or-sequential domain analysis), `Naming Conventions` (Coding Implementation Plan), and a bounded Verify Loop — produces a Technical Spec detailed enough that `/sap-dev-create-report` needs zero further design. Uses `Scratchpad` as the progress ledger, `Grill Me`/`Handoff` as needed, `Caveman` for progress output.
- **/sap-dev-create-report**: Opens with an Input Validation Gate (+ `Grill Me` if TS/Package/TR incomplete) and a `Scratchpad` build ledger, then executes strictly per the TS's Coding Implementation Plan using `Find Released CDS View`, `CDS View Entities`, `Authorization & IAM`, `RAP`, `Modern ABAP Syntax`, `OData Service Development`, `Clean ABAP`, `Naming Conventions`, and `ABAP Unit Testing` (test skeletons), then a manual Runtime Verify Loop before the final walkthrough report. Also uses `RAP Query Provider` when the TS specifies a Custom Entity, `RAP Business Events` when it specifies an event to raise, and `SAP Fiori Apps Reference` to generate the Fiori launch URL in the walkthrough. Progress output uses `Caveman`.
- **/sap-dev-bug-fix**: Opens with `Grill Me` + `Scratchpad` to gather the failing object and mock data, traces root cause with `Data Model Extractor` and `ABAP Logic & Behavior Translator`, halts for user approval on a Cross-Impact Report, then fixes with `CDS View Entities`, `RAP`, `Modern ABAP Syntax`, `OO Design Patterns`, `Clean ABAP`, and mandatory `ABAP Unit Testing` against the user's mock data. Output via `Caveman`.
- **/sap-dev-api-inbound**: Input Validation Gate (+ `Grill Me` if incomplete), `Scratchpad` ledger, `Integration & API Analyzer` (checks for an existing standard API first), builds with `ABAP Cloud / Clean Core`, `Clean ABAP`, `Released ABAP Classes`, `Modern ABAP Syntax`, `OO Design Patterns`, `Naming Conventions`, verifies with `ABAP Unit Testing` plus a manual real-call Verify Loop, output via `Caveman`.
- **/sap-dev-api-outbound**: Same gate/ledger/analyzer pattern as api-inbound, builds with `RAP`, `Clean ABAP`, `Modern ABAP Syntax`, `OO Design Patterns`, `Naming Conventions`, verifies with a manual real-call Verify Loop against the target endpoint, output via `Caveman`.
- **/sap-dev-code-analysis**: `Scratchpad` ledger, `Data Model Extractor` and `ABAP Logic & Behavior Translator` to systematically scan, deep-dive, and document SAP objects or packages into a comprehensive Markdown technical report; progress output via `Caveman`.
- **/sap-dev-code-review**: `ABAP Lint & Review`, `ABAP SQL & AMDP`, `Modern ABAP Syntax`, `OO Design Patterns` and `Clean ABAP` to scrutinize code, provide risk analysis, performance optimization suggestions, and maintainability feedback without auto-refactoring code; progress output via `Caveman`.
