---
name: universal-coordination
description: Use when a request spans multiple tools or stages, needs project continuity, or asks to coordinate research, design, and implementation.
---

# Universal coordination

Coordinate the user's requested outcome across available skills and tools. Read [`../../references/integration-map.md`](../../references/integration-map.md) when choosing among the user's known integrations. Treat it as a discovery map; the live host's available tools and skills determine what can actually be used.

## Workflow

1. Identify the requested deliverable, project, constraints, and dependencies. For a self-contained task, do it directly without invoking unrelated routes.
2. Discover relevant skills and tools exposed by the current host. Use the integration map to recognize intended routes, not to assume a connection exists.
3. If Context Window Manager tools are available, use `recover_context` to restore active work. Use `search_context` when a specific prior decision or project detail matters. For a new request or a semantic change, send the reconciled requirement to `sync_requirements`; preserve prior active requirements unless the user changes or cancels them. Save `checkpoint` at meaningful handoffs or when work is likely to resume later.
4. Route each part to one best-fit capability:
   - Narrow factual verification or source assessment: use `better-research` when available.
   - A broad or multi-source investigation, or a request for Deep Research: use Deep Research Engine when available. Follow its mode selection for a new investigation when the user has not chosen a mode. Do not run both research orchestrators for the same question.
   - Public platform, creator, or community material: use Universal Reach when available. Check platform capability and health before relying on a result; inspect the original item when possible.
   - Interface work based on Figma: use `figma-to-code`.
   - Nontrivial repository work: use `engineering-flow`.
   - Creating or maintaining agent skills: use `skill-workshop`.
5. Respect dependencies. Gather design or source evidence before implementation; integrate independent work before relying on its output. Delegate only when the active runtime exposes suitable agents and parallel work will reduce total effort. If `better-subagent-use` is available, use it to plan delegation.
6. Verify the requested deliverable with the relevant evidence. Update a Context Window Manager task only with evidence actually observed; its stored completion evidence is a record, not independent verification.
7. Report what was completed, which sources or tools contributed, what was verified, and any unavailable integration that materially limited the result.

## Boundaries

- Never claim an integration ran unless its tool was available and returned a result.
- If a route is unavailable, continue with supplied material or another available source where useful, and state the limitation plainly.
- Do not store credentials or unnecessary sensitive data in project context.
- The user’s current instructions and scope take precedence over this routing guide.
