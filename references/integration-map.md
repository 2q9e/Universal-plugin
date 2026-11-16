# Integration map

This map was prepared from the user's project documentation and the plugin/tool listings visible during authoring. It identifies intended routes; it does not guarantee that an integration is enabled in a future host. Discover the live tools and skills before each use.

## Project continuity: Context Window Manager

This is the preferred continuity route for ongoing multi-step project work. When connected, use:

- `recover_context` to restore the latest checkpoint, active tasks, and recent project notes.
- `search_context` for a targeted prior decision or file context.
- `sync_requirements` to reconcile new requirements, changes, and cancellations with existing tasks.
- `list_tasks` and `set_task_status` to inspect and update task state.
- `checkpoint` to save a compact resume point at a meaningful milestone.

The tool records verification evidence but does not independently validate it. Only record evidence that was actually observed. Avoid storing credentials or unnecessary sensitive material. Context Window Manager is local-first and project-scoped; it does not enlarge the model's physical context limit.

## The user's `2q9e/skills`

When available, use `better-research` for narrow factual verification, source tracing, and claim assessment. Use `better-subagent-use` to decide whether and how to delegate independent coding or research work. These are existing skills, not bundled copies. Their installation does not itself provide browsing or agent-runtime tools.

## Deep Research Engine

Use `deep-research-engine` for investigations that need a broad, sourced report or when the user requests Deep Research. Use its `deep-research-orchestration` only within investigations started through that engine. Follow its Official, Mixed, or Deep Discovery mode choice when required. It supplies a research workflow, not a search engine; use available retrieval tools and cite only sources actually inspected. Do not route a narrow claim check through both this engine and Better Research.

## Universal Reach

For public platform and community material, use the available Universal Reach tools. The documented route includes `platforms_list`, `platform_status`, `search`, `search_multi`, `read`, `replies`, `profile`, `profile_posts`, `media`, `transcript`, `archive`, and `health_check`. Check the selected platform's current availability and tool result before depending on it. Search results are leads; inspect and cite the original public item when available. Do not infer that every catalogued platform has a working adapter.

## GitHub

For remote repository discovery and source inspection, use the GitHub tools actually exposed by the host. Known tool names include `github_search`, `github_fetch_file`, `github_search_issues`, and `github_search_prs`. Local repository work can proceed from the checked-out files. Do not infer private-repository access from the presence of a GitHub skill.

## Figma

When the Figma MCP server is connected, the design-to-code route commonly uses `get_design_context`, `get_metadata`, `get_screenshot`, `download_assets`, `get_variable_defs`, and Code Connect tools. `get_design_context` is the main source for a selected design; metadata can narrow a large frame. Tool availability varies by server. Use Figma write tools only for a user-requested Figma edit.

## Image Vision Local

When this local image plugin is connected, its documented tools include `inspect`, `crop`, `zoom`, `tile`, `ocr`, `decode_codes`, `detect`, `ground_text_query`, `segment`, `compare_regions`, `denoise`, `sharpen`, `contrast`, `upscale`, and `doctor`. Optional backends may be absent. Check availability before requesting a backend; use source-mapped crops and original-image context for precise visual claims. It handles still images, not video sequences.

## Missing integrations

If an expected skill or tool is absent, do not imitate its result or claim it is connected. Continue with available project material when useful. If missing access blocks the result, name the exact input or connection needed.
