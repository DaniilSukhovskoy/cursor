# build-ui-feature

Workflow:
1. Run Designer subagent to freeze spec + acceptance checklist.
2. Run Implementer subagent to implement exactly the spec.
3. Run QA subagent to validate the implementation flow/screens/components and produce screenshot-backed evidence.
4. Run Reviewer subagent to approve or block.

Do not skip steps.
Do not refactor unrelated code.
End with final summary and verification steps.