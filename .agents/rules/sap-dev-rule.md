---
trigger: always_on
---
# SAP CLOUD DEV RULES (STRICT)

**1. SKILL ROUTING:** MUST read `SKILLS_ROUTER.md` before any task to dynamically load required skills.
**2. SCOPE & SAFETY:**
- **Consent First:** Ask explicitly before any CUD operations.
- **Custom Only:** Modify ONLY Z/Y objects. NEVER touch Standard Objects.
- **Strict Scope:** Touch ONLY objects in the current task scope. NO unintended side-effects.
- **Collision Check:** Verify object names globally (Z*) before creation. If exists, propose new name and ask for approval.
- **TR & Package:** Required for all new/modified objects. Ask if missing.
- **Read-Only Data:** Business data is READ-ONLY unless explicitly testing RAP BOs.
**3. CODE STANDARDS:**
- **Modern ABAP & OOP:** Enforce Modern ABAP (VALUE, COND, REDUCE) and GoF Patterns. Reject legacy procedural code.
- **Clean Core (Read):** CDS Views ONLY. NEVER SELECT from physical tables.
- **Clean Core (Write):** ABAP EML or Released APIs ONLY. NEVER direct INSERT/UPDATE.
**4. WORKFLOW & FILES:**
- **Scratchpad:** MUST draft complex architecture in a scratchpad first.
- **File Organizer (all under one `artifacts/` root):** 
  - FS inputs -> `artifacts/fs_docs/`
  - Output TS -> `artifacts/technical_specifications/`
  - Scratchpads -> `artifacts/scratchpads/`
  - Walkthroughs -> `artifacts/walkthroughs/`
  - Metadata Extensions -> `artifacts/metadata_extensions/`
  - System Analysis Reports -> `artifacts/system_analysis/`
  - *NEVER output to `.agents/` or root.*
**5. VALIDATION & ERRORS:**
- **Activation:** Remind/trigger activation. On failure, extract exact SAP error (DO NOT guess).
- **Final Audit:** Post-CUD, perform boundary check: verify no external mutations, syntax-error-free, properly activated, and isolated.
**6. IRON LAWS (NO EXCEPTIONS):**
- **No TS handoff without verification pass:** A Technical Specification is only valid input for `/sap-dev-create-report` after it has passed the FS-analytic Verify Loop (PASS, or FAIL explicitly accepted by the user in writing).
- **No object creation without TS coverage:** `/sap-dev-create-report` MUST NOT create any object or logic absent from the TS's Coding Implementation Plan. Missing info → STOP, do not improvise; go back to the user or to `/sap-dev-fs-analytic`.
- **No activation-only claims:** "Activated" is not "correct." Every completion report must state both separately.
**7. RED FLAGS — STOP if you catch yourself thinking:**
- "This FS is simple, skip some skills/steps" → Still run all of them; simple just means each step is fast, not skipped.
- "TS is missing a field or two, I'll infer it while coding" → This is exactly how wrong report logic happens. Go back and patch the TS first.
- "It activated, so it's probably correct" → Runtime logic is unverified until the Verify step actually runs.
- "Let me try one more fix" (after ≥3 attempts) → Stop. This signals an architecture/TS problem, not a small bug. Ask the user.
**8. REPORTING LANGUAGE:** Never say "should work / probably fine / likely correct" when claiming completion. Every "Activated/Passed/Correct" claim must cite the actual evidence (command run, output observed).
**9. MCP TOOL USAGE:** Each skill calls whichever MCP server/tool its function needs; the agent resolves and dispatches these itself. Before relying on an MCP server/tool name for the first time in a session, verify it actually exists — never copy another skill's tool name/syntax without verifying it applies here.
**10. TOKEN EFFICIENCY (use the Productivity skills deliberately):**
- Progress/log output (validation logs, activation status, step start/end) uses **[Skill: Caveman]** — short, evidence-first, no restating what the ledger already shows.
- Never re-print an entire TS or scratchpad in a response — quote only the section needed for the current step; reference the file path for the rest.
- Reference other skills as `[Skill: X]` rather than re-embedding their content.
- **[Skill: Grill Me]** stays to 1-3 targeted questions per round, not open-ended interviews.
- **[Skill: Handoff]** is mandatory before a session is likely to be compacted/interrupted mid-workflow, so the next session reads the ledger + handoff instead of reloading full history.
**11. EVIDENCE FLOOR FOR USER-PROVIDED VERIFICATION:** When a workflow asks the user to manually test something and report back, a bare confirmation with no concrete data ("looks fine", "ok", "works") is NOT sufficient to mark a verify gate PASS. Ask again for the specific evidence the step requires (actual response payload, actual field values, screenshot, etc.) before recording a result. If the user insists on proceeding without evidence, record the gate as "PASS — unverified, user-accepted" (never as a plain PASS) so the residual risk stays visible in the walkthrough.