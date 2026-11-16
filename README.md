<!-- Copyright (c) 2026 2q9e. See LICENSE for terms. -->

# Universal Workbench

Universal Workbench is the routing and coordination layer for the user's companion packages. It tells the model which platform, source, and workflow to use, carries task constraints between them, and keeps project state aligned.

Universal Workbench depends on **Context Window Manager**, **Deep Research Engine**, **Universal Reach**, and host retrieval tools for the routes that use them. Each task uses only the companions that fit: broad research uses the Deep Research Engine skill with host web/search/retrieval tools; Universal Reach adds platform-specific public-content retrieval when that evidence matters; and Context Window Manager supplies continuity when continuing multi-step work. Universal Workbench does not replace or bundle them.

Before using a route, it checks the live host for the relevant skills and tools and checks current platform capabilities. A name in the integration map is not proof that a skill is loaded, a tool is connected, or a platform operation is available. If a required route is missing, it reports the exact missing capability and marks dependent work incomplete rather than claiming that it ran.

## Included skills

- **universal-coordination** routes cross-tool requests and keeps project context aligned when Context Window Manager is available.
- **authorized-source-access** selects legitimate public and account-authorized retrieval routes and records their access limits.
- **engineering-flow** applies a flexible inspect, plan, implement, and verify workflow to nontrivial code work.
- **figma-to-code** turns available Figma context into project-native implementation and uses image inspection tools for small visual details when connected.
- **skill-workshop** creates or updates focused, portable agent skills and skill-based plugins.

## Companion plugins and supporting integrations

Its core companion routes are Context Window Manager, Deep Research Engine, and Universal Reach. The existing `2q9e/skills` library supplies supporting research and delegation skills when available. GitHub, Figma, and Image Vision Local are additional capability-checked routes. See [`references/integration-map.md`](references/integration-map.md) for source selection, platform routing, and handoff rules.

The access rules for login-dependent research are in [`skills/authorized-source-access/SKILL.md`](skills/authorized-source-access/SKILL.md). The design findings and inspected sources are recorded in [`references/related-project-research.md`](references/related-project-research.md) and [`references/source-notes.md`](references/source-notes.md). No upstream source code is included.
