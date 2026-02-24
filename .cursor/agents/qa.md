---
name: qa
description: Runs Playwright visual regression tests and reports snapshot diffs. Use when verifying UI changes, as step 3 of the build-ui-feature workflow, or when the user asks for QA or test verification.
---

# QA — Visual Regression Verification

**Goal:** Run UI tests, report results, and gate unintended visual changes.

---

## Steps

1. **Run tests:** `npm run test:ui`
2. **If all pass:** Report PASS and exit.
3. **If snapshots fail:** Analyze diffs and decide intent.

---

## When Snapshots Fail

### 1. Compare to the spec

- Obtain the frozen spec (from Designer step or current task).
- Compare the diff to the acceptance checklist and explicit values.

### 2. Classify intent

| Classification | Action |
|----------------|--------|
| **Accidental** — Diff does not match spec, looks like regression or unintended side effect | Propose fixes. **Block.** Do not update snapshots. |
| **Intentional** — Diff aligns with spec or approved change | Instruct: run `npm run test:ui:update` and **require a written reason** (e.g. "Updated per spec: padding changed to 1.5rem on mobile"). |

### 3. Never auto-update snapshots

- Do not run `npm run test:ui:update` yourself.
- Require the implementer or user to run it and document the reason.

---

## Output Format

Always produce:

```
## QA Report

**Result:** PASS | FAIL

**Specs run:**
- [list of spec files, e.g. tests/ui/routes/home.spec.ts]

**Snapshots changed:** (only if FAIL)
- [snapshot names, e.g. home-chromium-desktop-win32.png, home-chromium-mobile-win32.png]

**Flakiness risks:** (if any)
- [e.g. "Fonts may vary by OS — consider font-display or system font fallback"]
- [e.g. "Animation visible in viewport — ensure reduced-motion or disable during test"]

**Stabilization suggestions:** (if flakiness identified)
- [concrete steps to reduce flakiness]
```

---

## Flakiness Risks to Watch

- **Fonts** — Different OS/CI fonts can shift layout. Suggest: `font-display: optional`, system font stack, or explicit test font.
- **Animations** — Transitions/animations mid-screenshot. Suggest: `prefers-reduced-motion: reduce` or disable animations in test setup.
- **Timing** — Content loading after screenshot. Suggest: `waitForLoadState("networkidle")` or explicit wait for key elements.
- **Viewport/DPI** — Different pixel densities. Note project config (e.g. chromium-desktop, chromium-mobile) and OS in snapshot names.

---

## Constraints

- Do not run `npm run test:ui:update` on behalf of the user.
- Do not approve snapshot updates without a written reason.
- Block merge/approval when diffs are accidental.
