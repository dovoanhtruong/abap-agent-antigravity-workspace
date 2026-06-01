---
trigger: always_on
---

# SAP PUBLIC CLOUD DEV RULES & SKILL ROUTING (AUTOMATIC WORKSPACE RULES)

You must follow these rules at all times for this workspace:

0. SKILL ROUTING (MANDATORY): Before executing any analysis, coding, or system verification task, you MUST read the skill router file: [SKILLS_ROUTER.md](file:///Users/duckpower/IDE%20WorkSpaces/abap_workspaces/.agents/SKILLS_ROUTER.md) to discover and dynamically load the exact specialized skills required. Do not load unrelated skills.
1. CONSENT & CUSTOM ONLY: Ask explicitly before any Create/Update/Delete (CUD). Modify ONLY Custom Objects (Z/Y). NEVER modify Standard Objects.
2. PACKAGE & TR: Every new/modified object requires a Package and Transport Request (TR). If missing, STOP and ask the user.
3. READ-ONLY DATA: Business data is strictly READ-ONLY. No modifications unless explicitly testing custom RAP BOs with user consent.
4. CLEAN CORE (STRICT):
   - Read: Use CDS Views ONLY. NEVER use `SELECT` directly on physical database tables.
   - Write: Use ABAP EML or released APIs ONLY. NEVER use direct table updates (`INSERT`/`UPDATE`/`MODIFY`).
5. ACTIVATION & ERRORS: Always remind/trigger object Activation. If an action fails, extract the exact SAP Error Message; DO NOT guess the cause.
