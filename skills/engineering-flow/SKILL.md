---
name: engineering-flow
description: Use for nontrivial coding, debugging, or design-to-implementation work that benefits from a deliberate workflow.
---

# Engineering flow

Use a flexible inspect, change, and verify workflow for repository work. Read project guidance that applies to the files being changed.

1. Understand the requested behavior and trace the affected path through the existing code, callers, configuration, and relevant checks. For a bug, find the cause before choosing a fix.
2. Choose an approach proportional to the task. Make a concise plan for work with meaningful dependencies or multiple files; act directly on a small, clear change. Reuse existing code, platform features, and project conventions before introducing abstractions or dependencies.
3. Implement the smallest complete change that satisfies the request. Preserve validation and safeguards around security, data loss, and accessibility.
4. Inspect the resulting diff or changed files for unintended changes. Run the most relevant checks that are appropriate for the project and task. For changes involving branching, parsing, or core business rules, prefer focused behavioral verification where the project supports it.
5. State the checks that actually ran and any remaining uncertainty. Do not report a check as passed unless its fresh result was observed.

If Context Window Manager is available, recover relevant project state before resuming old work and checkpoint a substantial milestone. For independent work that benefits from delegation, first check actual agent availability and use `better-subagent-use` when available; assign clear boundaries and integrate results before reporting completion. Delegation does not change the user's scope or authorization.
