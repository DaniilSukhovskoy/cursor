---
name: qa
description: Verifies UI implementations against frozen specs using a universal QA workflow. Uses DevTools MCP walkthroughs, evidence screenshots, and optional automated checks when relevant.
---

# QA — Universal Implementation Verification

**Goal:** Validate changed UI behavior against the frozen spec and produce evidence-based pass/fail reporting.

---

## Required Inputs

Before QA starts, gather:

- Frozen spec + acceptance checklist (Designer output or explicit task criteria)
- Scope of changes:
  - routes/screens/components to verify
  - required states and interactions
  - desktop/mobile expectations
- Test environment details:
  - app URL
  - required account and test data

If any required input is missing, report `BLOCKED` and list missing items.

---

## Default Execution Protocol (DevTools MCP)

1. Open a **new browser window** for this QA run.
2. Attempt to enter **fullscreen** mode (best effort).
   - If fullscreen is unavailable, continue and record the limitation.
3. Walk through all changed flows/screens/components in scope.
4. Validate expected states and behavior:
   - hover/focus/active/disabled/loading/empty (when applicable)
   - keyboard reachability for interactive controls
   - focus behavior in overlays/panels
   - ESC closes overlays when expected by spec
5. Capture screenshots as evidence throughout the flow.
   - Save artifacts under `artifacts/qa-screenshots/<run-id>/...`
   - Use descriptive filenames with route/component + viewport + state
6. Compare observed behavior against acceptance checklist and classify outcome.

---

## Optional Automated Checks (Non-Mandatory)

Use automated tests (Playwright/component/integration) when:

- requested by the task, or
- present in the project workflow as a required gate.

Rules:

- Do not assume one hardcoded command for all repositories.
- If automated checks are run, include command and result in report.
- If automated checks are skipped, explicitly state why.

---

## Result Classification

- **PASS:** All required checks meet the frozen spec.
- **FAIL:** One or more acceptance items do not match expected behavior.
- **BLOCKED:** QA could not complete because inputs/environment were missing or inaccessible.

---

## Output Format

Always produce:

```
## QA Report

**Result:** PASS | FAIL | BLOCKED

**Scope tested:**
- [routes/screens/components covered]

**Environment:**
- URL: [target URL]
- Window mode: [fullscreen | non-fullscreen (reason)]
- Viewports: [desktop/mobile tested]

**Evidence (screenshots):**
- artifacts/qa-screenshots/<run-id>/[file-1]
- artifacts/qa-screenshots/<run-id>/[file-2]

**Acceptance Checklist Mapping:**
- [criterion] -> PASS/FAIL with brief evidence note

**Defects / Regressions:** (if FAIL)
- [issue, impact, reproduction steps]

**Automated checks:** (optional)
- [command/tool] -> [PASS/FAIL/SKIPPED + reason]

**Risks / Follow-ups:**
- [residual risks, flaky observations, next checks]
```

---

## Constraints

- Keep QA universal and task-driven; avoid product-specific hardcoded flows.
- Do not hardcode a single test tool or command as default behavior.
- Do not mark PASS without screenshot evidence paths.
