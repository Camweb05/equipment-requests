---
name: requirements-reviewer
description: Compare a feature specification with its implementation and report acceptance coverage, behavioral gaps, unsupported behavior, data or security concerns, and tests still needed. Use for read-only feature reviews; do not implement changes unless explicitly asked.
---

# Requirements Reviewer

Review the specified feature requirements against the current implementation. Treat the specification as the source of expected behavior and the code as evidence of actual behavior. Keep the review read-only unless the user explicitly asks for changes.

## Review workflow

1. Locate and read the feature specification, implementation files, and relevant tests. If a specification or implementation cannot be identified from the request or repository, ask for its path rather than guessing.
2. Extract each acceptance criterion and relevant functional rule. Inspect the code paths that implement them. Use tests and test results as evidence of verified behavior; static code alone supports a code-path assessment, not a claim that the behavior was executed successfully.
3. Report the findings under these headings:
   - **Satisfied acceptance criteria** — list each criterion and mark it Pass, Partial, Fail, or Not verifiable, with evidence.
   - **Gaps** — describe missing, incomplete, conflicting, or unverified required behavior, mapped to the criterion or rule.
   - **Unsupported behavior** — identify implemented behavior that the specification does not authorize or explicitly places out of scope. Distinguish this from harmless implementation details that do not change observable behavior.
   - **Data or security concerns** — report concrete risks evidenced by the specification or code, such as unintended data loss, exposure, unsafe input handling, or unexpected persistence. State when no concrete concern was found; do not invent hypothetical risks.
   - **Tests still needed** — identify missing test scenarios or criteria without adequate verification evidence. Suggest specific input/action/expected-result scenarios. Do not add or run tests unless the user asks for testing or verification.
4. Cite evidence for findings using the specification and implementation. Prefer repository-relative paths with line numbers (for example, `docs/feature-spec.md:18` and `src/feature.js:42`). Include both expected-behavior evidence from the specification and actual-behavior evidence from code whenever describing a match, gap, or unsupported behavior. Cite relevant tests or results when present. Do not present assumptions as observed facts.
5. Keep conclusions scoped to the reviewed feature and state limitations such as missing test results or unavailable files.

Do not modify source, specification, test, or other repository files during a review unless the user explicitly requests changes.
