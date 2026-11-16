# Companion integration and source-routing map

Universal Workbench routes work across the user's companion packages. It selects a platform and source based on the task, directs available research and retrieval tools, and keeps context aligned. It does not perform the work of Context Window Manager, Deep Research Engine, or Universal Reach itself.

Broad research uses the Deep Research Engine skill with web, search, and retrieval tools supplied by the host. Platform research adds Universal Reach's CLI/MCP integration when relevant platform evidence is needed; project continuity adds Context Window Manager when a task must resume or update ongoing work. Discover the required skill and integration for each route before use. This document describes intended routes; it is not proof of a connection, permission, or current platform support.

## Companion integrations

Requirements are route-specific: broad research uses Deep Research Engine with host retrieval tools, platform evidence uses Universal Reach when relevant, and project continuity uses Context Window Manager when needed.

| Companion | Its role | Universal Workbench route |
| --- | --- | --- |
| **Context Window Manager** | Project continuity, prior decisions, task state, and checkpoints. | Recover the relevant project state before continuing an existing multi-step task. Search for decisions only when they matter. Sync changed requirements and checkpoint meaningful milestones using observed evidence. |
| **Deep Research Engine** | Research skill for broad, multi-source investigation and research orchestration; it relies on retrieval tools supplied by the host. | Route broad, disputed, or explicitly deep investigations through the Engine's skill. Follow its requested mode and use its orchestration only for investigations begun through that Engine. Keep the selected source scope, claim-to-evidence links, counterevidence, and citations in its result. |
| **Universal Reach** | Platform-specific retrieval of public community and social content, with a limited set of separately authorized account routes. | Use it to choose and query the platform the user's question is about. Check the live platform and operation capabilities first, then pass the focused search/read request. Preserve source URLs, access mode, retrieval time, warnings, and partial-result status for the research handoff. |

If one companion skill or integration is unavailable, report which route is missing. Continue only with evidence and tools that are actually available, and mark work that depends on the missing route as incomplete.

## Choose a route by the source the user needs

| User's need | Primary route | Handoff or limit |
| --- | --- | --- |
| Research centered on a named platform or community | Universal Reach | Query only an implemented operation for that platform. Open the original items when possible; results can be partial, rate-limited, or restricted. |
| Broad investigation across many kinds of sources | Deep Research Engine | Use Universal Reach for a platform-specific evidence track when the platform matters. The Engine supplies the method, not new platform permissions. |
| Content specific to the user's own account or workspace | `authorized-source-access` plus an official API, OAuth/MCP connector, or explicitly user-authorized browser path | Check identity, scope, and tool behavior. Universal Reach is suitable only where its current adapter explicitly supports the requested account route. |
| One narrow factual claim or source check | `better-research` from `2q9e/skills`, when available | Keep the check narrow. Do not run both research workflows over the same question unless the user asks for both. |
| Continuing an existing project | Context Window Manager | Recover requirements and decisions; do not store credentials or unnecessary raw sensitive content. |
| Figma design implementation | `figma-to-code` and available Figma tools | Use the exact frame/selection, structured design context, and screenshot; then adapt to project conventions. |
| Small visual details in a screenshot or design | Connected Image Vision Local tools | Keep crop coordinates tied to the original image. Inspect global context for counts or relationships; a crop alone can discard context. |
| Nontrivial code changes | `engineering-flow` | Trace affected code and callers, make the smallest complete change, and verify the requested outcome. |
| Creating or maintaining a reusable skill/plugin | `skill-workshop` | Keep the new skill focused and use the current Plugin Creator requirements. |

## Choose a platform when the user has not named one

Use the source community that is most likely to contain the kind of evidence the user asked for. Keep the set small and explain any material source limitation.

| Research need | Candidate platform/source class | How to use it |
| --- | --- | --- |
| Software behavior or technical troubleshooting | Official docs and release notes first; then the project's GitHub issues/discussions, relevant Stack Exchange site, or maintainer/community forum | Use Deep Research Engine for the sourced investigation. Use Universal Reach only for platforms and operations it currently exposes. Treat discussion posts as reports or examples, not official behavior. |
| Public user experiences or community discussion | The topical public forum or social platform where the relevant users participate | Select the platform from the subject and the user's requested audience. Public posts are anecdotal and may not represent all users. |
| Creator, channel, product, or organization statements | The creator's official site/channel/account or first-party announcements | Prefer the original announcement. Use a public platform adapter only when it exposes the needed operation; owner-only APIs do not provide general account search. |
| General factual, academic, policy, or historical question | Government, academic, primary, and reputable reporting sources | Use Deep Research Engine as the main route. Add Universal Reach only when a specific public community's response is part of the question. |

If the intended audience or community materially changes the answer, ask one short clarification. Otherwise choose the best-supported public source set and state it. Do not fan out over every platform just because `search_multi` exists.

## Universal Reach workflow

Use the current MCP tool inventory and returned data rather than relying on remembered platform lists. Universal Reach's source package provides these operations when connected: `platforms_list`, `platform_status`, `search`, `search_multi`, `read`, `replies`, `profile`, `profile_posts`, `media`, `transcript`, `archive`, and `health_check`.

1. Call `platforms_list` or `platform_status` to see whether the target platform is catalogued, implemented, configured, and which operations it supports. A configured status is not a live health check.
2. Use `health_check` only when current upstream availability matters. It makes live requests; `platform_status` does not.
3. Choose `search` for a named platform or `search_multi` for an explicitly relevant set of platforms. Do not assume a catalogued platform has search or that “multi” means full coverage.
4. Preserve returned `access_mode`, pagination, partial flags, warnings, errors, platform ID, canonical source URL, and retrieval time. Do not summarize away missing platforms or truncated result windows.
5. Treat results as leads. For a factual report, inspect the original public item where available and cite that item, not only the adapter output. If an original page is inaccessible, label the limitation and cite the returned source metadata accurately.

Universal Reach's project README describes it as a local, read-only MCP/CLI with documented public routes and a limited set of environment-configured, owner-authorized routes. It does not provide a general authenticated browser, public coverage of every catalogued platform, or access to content hidden from the configured account. Its support matrix can change; use live capability results at task time.

## Cross-plugin handoff

For research that needs both platform evidence and broad synthesis:

1. Recover the project's relevant context and current constraints from Context Window Manager, if connected.
2. Define the research question, target platforms, timeframe, geography, account scope (if any), and expected output.
3. Start the broad investigation through Deep Research Engine when its scope warrants it. Let it choose its required mode or retain the mode already selected by the user.
4. Use Universal Reach for the exact platform operations its current capability result supports. Return the source URLs, observed publication dates, retrieval time, access mode, and incomplete-result warnings to the research workflow.
5. Keep one source/citation trail across the answer. A result reused by two plugins is still one source, not independent corroboration. Keep public claims distinct from content visible only through the user's account.
6. Save a compact Context Window Manager checkpoint with the objective, decisions, source links, access limitations, completed work, and next step. Do not save passwords, API tokens, cookies, or unnecessary private page contents.

When Deep Research Engine is not needed, use Universal Reach directly for a simple platform lookup. When Universal Reach has no supported route, do not invent an adapter or imply that Deep Research Engine can see private platform content. Use an authorized official source if available, otherwise state what remains inaccessible.

## Authorized access

For any login-dependent, workspace-only, or account-specific request, load [`../skills/authorized-source-access/SKILL.md`](../skills/authorized-source-access/SKILL.md). In brief:

- Prefer an official first-party API, OAuth/MCP connector, or user-selected file scope with the narrowest practical read permissions.
- A search/crawler API key authorizes use of that search/crawler service; it does not authenticate to the target website.
- A connected app does not grant access beyond the user's own permissions, granted scopes, or the platform's approved products.
- Do not request, store, or route user passwords, cookies, MFA codes, or API tokens through prompts or research notes. Stop at a login challenge, CAPTCHA, access denial, paywall, or site restriction. Do not use stealth modes, proxy rotation, fingerprint spoofing, or CAPTCHA-solving to continue.
- Before sending signed-in page content or browser state to a cloud service, disclose that transfer and check the service's current terms, retention, region, and deletion controls. Do not assume a “zero data retention” label applies to the selected endpoint or plan.

## Supporting skill and tool routes

- **`2q9e/skills`:** `better-research` handles narrow source tracing and claim verification. `better-subagent-use` helps decide whether delegation improves a multi-track investigation or implementation. These skills do not provide missing browser, platform, or agent tools.
- **GitHub:** use the tools exposed by the current host to inspect the user's repository or source. Public repository access does not imply private repository access.
- **Figma:** when connected, common read tools include `get_design_context`, `get_metadata`, `get_screenshot`, `download_assets`, and variable/Code Connect lookups. The user must sign in, the selected file must be visible to them, and the client/server must support the operation. Use write tools only for a requested canvas edit.
- **Image Vision Local:** check the actual available operations before using them. Optional backends may be absent; this tool handles still images, not video sequences.

## Missing capabilities

If a skill, connector, platform operation, or permission is missing, do not imitate its result or claim it ran. Name the exact unavailable source/operation and continue with supplied or public evidence where useful. Preserve source provenance and tell the user what authorization, export, or connection would make the remaining route possible.
