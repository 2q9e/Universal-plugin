---
name: universal-coordination
description: Use when a request needs routing across Context Window Manager, Deep Research Engine, Universal Reach, or other tools and stages.
---
<!-- Copyright (c) 2026 2q9e. See ../../LICENSE for terms. -->

# Universal coordination

Universal Workbench is the routing layer for the user's companion plugins. It chooses the platform and workflow that fit the task, passes the scope to the right tools, and keeps project context aligned. It does not replace Context Window Manager, Deep Research Engine, or Universal Reach. Read [`../../references/integration-map.md`](../../references/integration-map.md) when selecting or joining those routes.

## Workflow

1. Identify the deliverable, the evidence needed to answer it, any named platform/source, timeframe, user constraints, and whether the request is public, account-specific, or project-continuity work. For an existing multi-step project, recover its relevant decisions and task state from Context Window Manager when available.
2. Discover the tools and skills available in the active host. Treat the integration map as routing guidance; check live tools and returned capability data before depending on a platform, operation, or permission. A platform name in the map is only a candidate, not proof of support.
3. Choose the route by task:
   - **Broad, multi-source or explicitly deep research:** use the Deep Research Engine skill with the host's available retrieval tools. Preserve the user-selected mode; otherwise follow the Engine's mode selection. Use its orchestration only for investigations started through the Engine.
   - **Platform or community evidence:** honor the platform the user named. If they did not name one, choose a small relevant set from the integration map's evidence-to-platform examples; prefer a primary source unless community experience is itself the evidence needed. Check `platforms_list` or `platform_status`, then use Universal Reach only for supported operations. Use `health_check` only when current upstream availability matters.
   - **Broad research plus a specific platform:** let Deep Research Engine own the investigation and use Universal Reach for the relevant platform evidence. Carry source URLs, retrieval time, access mode, partial flags, and warnings into the research handoff. Treat repeated results as one source, not independent confirmation.
   - **Account-specific or login-dependent research:** load `authorized-source-access`. Prefer a supported first-party API/OAuth/MCP connector with narrow read scope. Do not treat a search provider's API key as a target-site login.
   - **Narrow factual verification:** use `better-research` when available. Do not duplicate a broad investigation through both research workflows.
   - **Figma, visual, code, and skill tasks:** use `figma-to-code`, available image tools, `engineering-flow`, or `skill-workshop` only when the requested work needs them.
4. Follow dependencies. Resolve source/platform capability before assigning a query; gather design or research context before implementation. Do not invent missing tools, adapters, or permissions.
5. For a multi-route request, keep a compact route record: the evidence need, chosen source/platform and reason, live capability result and operation, access scope, canonical links and relevant dates, and any partial-result warnings or missing route. Pass only the fields the next tool needs; never pass credentials or unnecessary private content.
6. Reconcile tool outputs against original sources where possible. Preserve publication dates, retrieval dates, access mode, scope limits, and incomplete results. Context Window Manager can store a compact checkpoint using evidence actually observed; do not store secrets.
7. Report what each companion route did, what was verified, and any unavailable integration that materially limits the result. If a requested route is missing, name the exact missing capability and mark dependent work incomplete.

## Boundaries

- Never claim that a companion plugin, integration, or platform operation ran unless the tool was available and returned a result.
- Connector presence does not expand the user's permission or platform approval. Stop at access denial, login challenge, CAPTCHA, paywall, or site restriction; do not try to bypass it.
- A Context Window Manager checkpoint records progress; it does not verify the recorded evidence.
- The user's current instructions and scope take precedence over this routing guide.
