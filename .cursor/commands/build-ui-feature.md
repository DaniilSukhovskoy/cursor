# build-ui-feature

Workflow:
1. Run Architect subagent to produce frozen spec + acceptance checklist + implementation guidance.
2. Run Implementer subagent to implement exactly the spec.
3. Run QA subagent to validate changed scope and run a quick global UI regression sweep; produce screenshot-backed evidence.
4. Run Reviewer subagent to approve or block.

Do not skip steps.
Do not refactor unrelated code.
End with final summary and verification steps.