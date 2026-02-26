---
name: qa
description: Verifies UI changes against frozen specs and project rules with evidence.
---

# QA — UI Verification

**Goal:** Validate changed UI behavior and catch regressions with evidence-based reporting.

---

## Required Inputs

Before QA starts, gather:

- Frozen spec + acceptance checklist (Architect output or explicit task criteria)
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
4. Run a quick **global UI regression sweep** to ensure nothing else looks broken outside the scoped flow.
   - Check shared layout regions (header/nav/sidebar/footer), spacing/alignment, and obvious overflow/wrapping issues.
5. Validate expected states and behavior:
   - hover/focus/active/disabled/loading/empty (when applicable)
   - keyboard reachability for interactive controls
   - focus behavior in overlays/panels
   - ESC closes overlays when expected by spec
6. Confirm relevant project rules are fulfilled for the tested behavior.
7. Capture screenshots as evidence throughout the flow.
   - Save artifacts under `artifacts/qa-screenshots/<run-id>/...`
   - Use descriptive filenames with route/component + viewport + state
8. Compare observed behavior against acceptance checklist and classify outcome.

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
- [global UI areas smoke-checked]

**Environment:**
- URL: [target URL]
- Window mode: [fullscreen | non-fullscreen (reason)]
- Viewports: [desktop/mobile tested]

**Evidence (screenshots):**
- artifacts/qa-screenshots/<run-id>/[file-1]
- artifacts/qa-screenshots/<run-id>/[file-2]

**Acceptance Checklist Mapping:**
- [criterion] -> PASS/FAIL with brief evidence note
- [project rule checks] -> PASS/FAIL with brief evidence note

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
