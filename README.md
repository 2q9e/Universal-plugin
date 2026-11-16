# Universal Workbench

Universal Workbench is a private, skills-only plugin for coordinating research, project continuity, design implementation, engineering work, and reusable skills.

It routes work to tools and skills that are already available in the host. It does not bundle or replace their MCP servers, credentials, or private source code. Integrations are optional and capability-checked at use time.

## Included skills

- **universal-coordination** routes cross-tool requests and keeps project context aligned when Context Window Manager is available.
- **engineering-flow** applies a flexible inspect, plan, implement, and verify workflow to nontrivial code work.
- **figma-to-code** turns available Figma context into project-native implementation and uses image inspection tools for small visual details when connected.
- **skill-workshop** creates or updates focused, portable agent skills and skill-based plugins.

## Existing integrations

The package includes a map for the user's existing Context Window Manager, `2q9e/skills`, Deep Research Engine, Universal Reach, GitHub, Figma, and Image Vision Local tools. Their names and availability are checked against the active host each time. See [`references/integration-map.md`](references/integration-map.md).

The package's workflow ideas and research reference are recorded in [`references/source-notes.md`](references/source-notes.md). No upstream source code is included.
