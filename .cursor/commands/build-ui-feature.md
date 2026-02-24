# build-ui-feature

Workflow:
1. Run Designer subagent to freeze spec + acceptance checklist.
2. Run Implementer subagent to implement exactly the spec.
3. Run QA subagent to execute Playwright tests and report diffs.
4. Run Reviewer subagent to approve or block.

Do not skip steps.
Do not refactor unrelated code.
End with final summary and verification steps.