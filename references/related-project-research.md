# Deep Discovery: related project patterns and source routes

**Reviewed:** November 16, 2026  
**Purpose:** Identify useful and unsuitable patterns in related agent skills, research workflows, visual tools, and platform connectors, then record what Universal Workbench adopts. This is a design review, not a claim that the resulting skills have been benchmarked.

## Scope and method

The review covered the user's local source for Context Window Manager, Deep Research Engine, and Universal Reach; the `2q9e/skills` library's `better-research` and `better-subagent-use` instructions; and public source code, official documentation, standards, and research papers. Five non-overlapping tracks examined workflow/skill design, Figma and visual inspection, research engines and evidence quality, authorized platform APIs, and public-web/browser connectors. Each track returned inspected source locations, findings, and limitations. I then checked consequential access claims against primary documentation and searched for counterevidence on skill effectiveness and cloud browser state.

The sources are not all equally independent: vendor documentation describes vendor behavior; papers evaluate defined datasets and systems; repository files describe the inspected version of a project; and community or benchmark results do not guarantee live-site performance. The reference list below is a selected source guide, not an exhaustive count of every page opened. Overlapping sources across tracks are counted once here.

## Main findings

### 1. Universal Workbench is a router, not another research or retrieval engine

The user's Context Window Manager provides local project state, task requirements, and checkpoints. Its own documentation says completion evidence is recorded but not independently validated. Deep Research Engine provides mode selection, a multi-source method, source provenance, citation audit, and research-specific orchestration, but states that retrieval depends on the host. Universal Reach is a local read-only CLI/MCP service that checks platform capabilities and returns public-content records, with only specific owner-authorized API routes. The router's job is therefore to choose the relevant platform and operation, pass the question and boundaries to the right companion, and keep source evidence intact across handoffs (2q9e, n.d.-a, n.d.-b, n.d.-d; OpenAI, n.d.-b).

**Adopted:** The README and `universal-coordination` describe three route-specific companion roles: Deep Research Engine owns broad investigation with host retrieval tools; Universal Reach supplies evidence when the selected platform matters; Context Window Manager recovers and checkpoints project state when continuing ongoing work. No single route requires all three. The package does not claim those tools are connected unless the active host exposes them.

### 2. Platform choice must follow live capability and user scope

Universal Reach's source is deliberately explicit about implemented operations, access mode, partial results, and unsupported routes. Its README currently describes 35 catalogued platforms and 20 adapters registered by default, with Discord conditional and many platforms restricted or only partially supported; this is a snapshot, not a guarantee of future support. Its `platform_status` describes configured capability while `health_check` makes live requests. Treating a platform name or a search plugin as proof of usable access would erase those distinctions (2q9e, n.d.-d).

**Adopted:** The route checks live platform and operation capability before choosing `search`, `search_multi`, `read`, or another operation. It preserves access mode, pagination, warnings, failures, and partial status. A search result is a lead; the research answer should cite the original item where accessible. If a platform route is restricted or absent, the answer says what was not reached.

### 3. Broad research and narrow verification should stay separate but share evidence

Research tools document iterative source discovery, source selection, citation annotations, and source histories. Citation-focused work evaluates source support separately from prose quality, while browsing benchmarks evaluate different tasks such as finding hard facts or navigating websites. These benchmarks are useful design references, but they do not establish success on all current sites or queries (Anthropic, n.d.-b; Gao et al., 2023; Gou et al., 2025; Min et al., 2023; OpenAI, n.d.-b, n.d.-d; Wei et al., 2025; Zhou et al., 2024).

There is counterevidence against assuming skills always improve results: one software-engineering benchmark found many skills had no measurable gain, while other benchmark studies report benefits that vary by task and can become negative. The right design is focused routing plus evidence-based evaluation, not a claim that adding instructions automatically makes a model better (Han et al., 2026; Li et al., 2026).

**Adopted:** Use Deep Research Engine for broad or explicitly deep questions and its own orchestration only when research begins through that Engine. Use Better Research for a narrow source or claim check. When both Deep Research Engine and Universal Reach contribute, retain one source/citation trail; reusing one item across tools is not independent corroboration. Store a compact, non-sensitive checkpoint in Context Window Manager.

### 4. Account access needs its own route and provenance

Official APIs and MCP connectors commonly require user sign-in, specific scopes, app approval, an eligible account role, or administrator consent. An integration does not bypass a provider's ACLs. MCP's July 2026 authorization specification calls for OAuth-based protected-resource discovery, audience-bound access tokens, resource indicators, and PKCE; OAuth security guidance recommends safeguards such as exact redirect validation. Provider documentation also shows that different operations can have different access requirements (GitHub, n.d.; Google, n.d.-a, n.d.-b; Internet Engineering Task Force, 2025a, 2025b; Model Context Protocol, 2026a, 2026b).

A search/crawler key authenticates to the retrieval service; it does not sign in to the target website. Browser state is sensitive: Playwright warns that saved cookies and headers can impersonate a user. TinyFish documents persistent profiles containing cookies and web storage. Its current Terms of Service, effective August 17, 2026, grant it rights to host and process customer data for service provision, improvement, and model training subject to stated safeguards. Firecrawl's current documentation advertises ZDR only on Enterprise plans after enablement, with an Agent result exception; its privacy policy page says it was last revised in 2024 and describes retention until written deletion. These terms are vendor statements, change over time, and do not establish that a selected route is appropriate for sensitive data (Fathima, 2026; Firecrawl, n.d., 2024; Playwright, n.d.-a; TinyFish, n.d.-a, 2026).

**Adopted:** `authorized-source-access` prefers first-party APIs or OAuth/MCP with narrow read scopes, keeps access classes separate, never requests pasted passwords/cookies/tokens, discloses cloud transfer before a new signed-in session, and stops at login challenges, CAPTCHAs, paywalls, access denials, or policy restrictions. It does not use stealth, proxy rotation, fingerprint changes, or CAPTCHA-solving to bypass a block.

### 5. Figma and image workflows need both structured context and visual evidence

Figma's workflow combines the exact selection, design context, metadata to narrow oversized selections, screenshots, assets, and project conventions. Figma also distinguishes the server's design information from the agent's code adaptation, and its remote server requires sign-in and a supported client. Image-crop research offers gains for detail-sensitive questions in specific models, while papers on global visual search and FOCUS highlight the value and tradeoffs of context, attention, and region selection. A focused crop can lose information needed to judge counts or relationships; model-internal methods cannot be promised by a generic plugin (Figma, n.d.-a, n.d.-b, n.d.-c, n.d.-d; Playwright, n.d.-b; Wu & Xie, 2024; Zhang et al., 2025; Zhong et al., 2025).

**Adopted:** Keep the current Figma sequence, use screenshot conditions consistent with the existing project tooling when comparing visuals, retain crop coordinates and inspect the original, and make model-specific crop methods optional. Do not add a hosted visual testing dependency by default.

### 6. Skills should be scoped and flexible

Ponytail and Superpowers provide useful patterns for reading the relevant code path, considering existing mechanisms, diagnosing the cause before a code fix, and verifying the concrete result. Skill format documentation provides a portable package structure and activation metadata, but portability does not standardize host tools, permissions, or invocation. Studies of public skill files report routing and packaging weaknesses (agentskills.io, n.d.; Zhang et al., 2026). Benchmarks find skill effects vary by task and mismatched guidance can degrade results (Han et al., 2026; Li et al., 2026). These lessons support focused routing and conditional instruction, not claims that adding instructions automatically improves a model (DietrichGebert, n.d.; obra, n.d.; OpenAI, n.d.-a).

**Adopted:** Keep specialized instructions in separately triggered skills, put conditional detail in references, use planning only when task uncertainty merits it, and treat static package checks as format checks rather than proof of runtime quality.

## Design choices and limits

| Finding | Applied in Universal Workbench | Limit |
| --- | --- | --- |
| Companion plugins supply distinct context, research, and platform retrieval capabilities. | README, `plugin.json`, integration map, and coordination skill describe dependency and handoffs. | This package cannot install or technically guarantee another plugin's availability. Host discovery remains authoritative. |
| Platform capability is not the same as platform health or full coverage. | Coordinator checks live operation status and preserves partial-result metadata. | Universal Reach can change platform coverage and upstream APIs can fail or return bounded windows. |
| Source choice should follow the evidence need; a platform name alone does not prove useful or authorized access. | Integration map now gives platform/source candidates for common research needs and a compact route record for multi-route handoffs. | The examples are heuristics; live tool support, public coverage, and account scope still need checking. |
| OAuth and connected apps preserve the provider's permission model. | New access skill selects official, narrow-scoped routes and records access class. | A visible connection does not prove every data field or user role is permitted. |
| Persistent browser state is credential-equivalent and cloud transfer has privacy implications. | New access skill sets explicit transfer and stop conditions. | Vendor terms and feature behavior can change; review again at the time of use. |
| Structured Figma data plus a screenshot supports implementation; crops need global context. | Updated Figma skill clarifies stable comparisons and visual limits. | Screenshot equality does not establish behavior or semantic correctness. |
| Focused skills can help, but effects are task-dependent. | Existing skills remain small and conditional; added access routing is separate. | No benchmark or forward test was run for this package. |

## Source guide

All citations point to the inspected source or its canonical paper/document page. The limitations column describes what that source cannot establish.

| Source | What it supports | What it cannot establish |
| --- | --- | --- |
| [Ponytail source](https://github.com/DietrichGebert/ponytail) (DietrichGebert, n.d.) | Read affected code and callers; prefer small complete changes and existing project mechanisms. | A single project's conventions are not universal. |
| [Superpowers source](https://github.com/obra/superpowers) (obra, n.d.) | Conditional planning, root-cause debugging, and fresh verification patterns. | A fixed skill sequence will not fit every task. |
| [Agent Skills specification](https://agentskills.io/specification) (agentskills.io, n.d.) | Skill package structure and metadata conventions. | Does not create host tools, invocation guarantees, or permissions. |
| [OpenAI Build skills](https://developers.openai.com/plugins/build/skills) (OpenAI, n.d.-a) | Skill authoring and packaging guidance for the OpenAI plugin environment. | Host/version-specific product documentation. |
| [OpenAI Build plugins](https://developers.openai.com/plugins/build/plugins) (OpenAI, n.d.-c) | Plugin packaging, components, and host integration context. | Does not promise runtime availability of another plugin. |
| [Anthropic Skill Creator](https://github.com/anthropics/skills/tree/main/skills/skill-creator) (Anthropic, n.d.-a) | Focused skill design and progressive detail. | Guidance for a different host and its supported skill set. |
| [SkillsBench](https://arxiv.org/abs/2602.12670v4) (Li et al., 2026) | Curated skills improved aggregate results across the reported configurations, while task-level effects varied and 13 of 87 tasks had negative deltas. | This v4 benchmark covers a defined set of 87 tasks and 18 model-harness configurations; it does not establish effects across every task or host. |
| [SWE-Skills-Bench](https://arxiv.org/abs/2603.15401) (Han et al., 2026) | Counterevidence: skill injection gave little average gain in the paper's software tasks; mismatched guidance could degrade results. | Results are specific to its repositories, requirements, and verifier. |
| [GitSkills dataset](https://arxiv.org/abs/2608.10906) (Destefanis et al., 2026) | Large-scale dataset for examining skill adoption, structure, and reuse. | Dataset findings do not measure this plugin's behavior. |
| [Agent-skill reuse study](https://arxiv.org/abs/2608.08453) (Zhang et al., 2026) | Reports common packaging, routing, and actionability defects in sampled public skills. | Automated defect rates may not generalize to every skill ecosystem or host. |
| [Figma tools and prompts](https://developers.figma.com/docs/figma-mcp-server/tools-and-prompts/) (Figma, n.d.-c) | Exact selection, design context, metadata, screenshots, and assets as design-to-code inputs. | Tool availability depends on client, plan, and selected file. |
| [Figma custom rules](https://developers.figma.com/docs/figma-mcp-server/add-custom-rules/) (Figma, n.d.-a) | Adapt generated design output to project conventions and compare the result. | Vendor workflow advice is not an independent measure of visual fidelity. |
| [Figma MCP versus agent](https://developers.figma.com/docs/figma-mcp-server/mcp-vs-agent/) (Figma, n.d.-d) | Separates structured design retrieval from agent code adaptation. | Does not ensure the model interprets every design correctly. |
| [Figma remote MCP setup](https://developers.figma.com/docs/figma-mcp-server/remote-server-installation/) (Figma, n.d.-b) | Requires sign-in and a supported/catalogued client for the remote server. | Current client eligibility can change. |
| [Playwright visual comparisons](https://playwright.dev/docs/test-snapshots) (Playwright, n.d.-b) | Baselines, thresholds, and stable capture conditions for visual diffs. | Pixel diffs vary by operating environment and do not prove semantic correctness. |
| [Storybook visual testing](https://storybook.js.org/tutorials/ui-testing-handbook/react/en/visual-testing/) (Storybook, n.d.) | Isolated named component states can localize visual issues. | Coverage is bounded by the stories actually authored. |
| [ViCrop paper](https://openreview.net/forum?id=DgaY5mDdmT) (Zhang et al., 2025) | Focused crops helped detail-sensitive visual question answering in the tested setups. | Uses model-internal signals and specific benchmarks; a generic tool cannot reproduce it. |
| [V*: Guided Visual Search](https://openaccess.thecvf.com/content/CVPR2024/papers/Wu_V_Guided_Visual_Search_as_a_Core_Mechanism_in_Multimodal_CVPR_2024_paper.pdf) (Wu & Xie, 2024) | Preserving global context with target coordinates can support visual search. | Trained model architecture and benchmark-specific results. |
| [FOCUS](https://proceedings.neurips.cc/paper_files/paper/2025/hash/8b02cdb04bc6351d36565b5c874bb804-Abstract-Conference.html) (Zhong et al., 2025) | Counterevidence on efficiency and attention tradeoffs in crop-based visual methods. | Author-run tests on selected models/datasets do not establish black-box tool behavior. |
| [Deep Research in ChatGPT](https://help.openai.com/en/articles/10500283-deep-research-in-chatgpt) (OpenAI, n.d.-b) | Source selection, connected apps, and source/activity review in the product workflow. | Product and account availability varies. |
| [OpenAI web search API](https://developers.openai.com/api/docs/guides/tools-web-search?api-mode=responses) (OpenAI, n.d.-d) | Search/open/find tools and structured citation annotations. | A citation annotation still needs claim-level support review. |
| [Claude research](https://support.claude.com/en/articles/11088861-use-research-on-claude) (Anthropic, n.d.-b) | Iterative searches and connected-tool use. | Connector availability varies by client and setup. |
| [ALCE](https://arxiv.org/abs/2305.14627) (Gao et al., 2023) | Citation quality, answer correctness, and fluency are separable evaluation dimensions. | Benchmark datasets and evaluated systems bound the findings. |
| [FActScore](https://aclanthology.org/2023.emnlp-main.741/) (Min et al., 2023) | Atomic factual claims can be assessed against supporting sources. | Original evaluation is centered on biographies; source coverage matters. |
| [BrowseComp](https://arxiv.org/abs/2504.12516) (Wei et al., 2025) | Persistent browsing for difficult-to-find facts can be evaluated separately from long-form writing. | Does not cover the full range of user queries or current live pages. |
| [WebArena](https://proceedings.iclr.cc/paper_files/paper/2024/hash/4410c0711e9154a7a2d26f9b3816d1ef-Abstract-Conference.html) (Zhou et al., 2024) | Multi-step website interaction can be measured against task state. | Its controlled replica environment is not a live-site access guarantee. |
| [Mind2Web 2](https://proceedings.neurips.cc/paper_files/paper/2025/hash/fdcec9f5b99aa4fc8f4fb8487802d737-Abstract-Datasets_and_Benchmarks_Track.html) (Gou et al., 2025) | Long-horizon web tasks can include source-attribution evaluation. | The conference paper uses a finite task set and judge rubric. |
| [Attribution Crisis](https://www.cambridge.org/core/journals/data-and-policy/article/attribution-crisis-in-llm-search-results-estimating-ecosystem-exploitation/170DD0B88E5F5AEA8F69F2E9AF1328E3) (Strauss et al., 2026) | An observational study of search logs warns that retrieved pages and cited pages can diverge. | Its 13,929 LMArena responses from March–April 2025 use provider logs that may be incomplete, and citation accuracy was not directly tested. Co-author Tim O’Reilly disclosed a potentially affected publisher interest; O’Reilly Media had no role in study design, data collection/analysis, decision to publish, or manuscript preparation. The authors also disclosed nonfinancial interests in AI transparency work. |
| [MCP Authorization](https://github.com/modelcontextprotocol/modelcontextprotocol/blob/main/docs/specification/2026-07-28/basic/authorization/index.mdx) (Model Context Protocol, 2026a) | OAuth 2.1-based authorization, protected-resource and authorization-server discovery, resource indicators, audience-bound tokens, and scopes. | Protocol compliance does not grant access to a target service or data. |
| [MCP Authorization Security Considerations](https://github.com/modelcontextprotocol/modelcontextprotocol/blob/main/docs/specification/2026-07-28/basic/authorization/security-considerations.mdx) (Model Context Protocol, 2026b) | PKCE S256, token audience validation, separate upstream tokens, and exact redirect validation requirements. | Specifies MCP implementation requirements; it does not assess a specific provider's actual connector. |
| [OAuth 2.0 Security BCP, RFC 9700](https://www.rfc-editor.org/rfc/rfc9700) (IETF, 2025a) | Current security guidance for OAuth deployments. | Does not validate any specific connector's implementation. |
| [Protected Resource Metadata, RFC 9728](https://www.rfc-editor.org/rfc/rfc9728) (IETF, 2025b) | Standard metadata discovery for protected OAuth resources. | Does not establish that an MCP client has permission to use the target. |
| [GitHub MCP server OAuth login](https://github.com/github/github-mcp-server/blob/main/docs/oauth-login.md) (GitHub, n.d.) | Local MCP OAuth flow and permission model for GitHub data. | Organization policy, SSO, token scope, and deployment type still constrain access. |
| [Google Drive API scopes](https://developers.google.com/workspace/drive/api/guides/api-specific-auth) (Google, n.d.-a) | Task-specific Drive scopes and user-selected files via Picker. | Restricted scopes can require verification/security assessment. |
| [YouTube API authorization](https://developers.google.com/youtube/data/guides/authentication) (Google, n.d.-b) | Public metadata API-key path versus OAuth for private user data. | Quotas and operation permissions still apply. |
| [Reddit API FAQ](https://developers.reddit.com/docs/guides/faq) (Reddit, n.d.) | Distinguishes Devvit community apps from external Data API use and approval. | API availability and policy are changing; check current terms at use time. |
| [Mastodon OAuth scopes](https://docs.joinmastodon.org/api/oauth-scopes/) (Mastodon, n.d.) | Per-instance, granular OAuth scopes and user access. | Instance policies can disable public routes or further restrict data. |
| [AT Protocol OAuth](https://atproto.com/specs/oauth) (Bluesky Social PBC, n.d.) | OAuth security requirements for account-authorized Bluesky operations. | Public read endpoints and private/account actions have different access requirements. |
| [Firecrawl Crawl](https://docs.firecrawl.dev/features/crawl) (Firecrawl, n.d.) | Crawl scope, page limits, robots behavior, failed URLs, and result expiry. | A completed crawl is not proof of complete site coverage. |
| [Firecrawl privacy policy](https://www.firecrawl.dev/privacy-policy) (Firecrawl, 2024) | Current page states US processing and retention of personal information until written deletion request. | Page says last revised in 2024; it may not reflect current product terms, so recheck before use. |
| [Firecrawl ZDR overview](https://www.firecrawl.dev/blog/zero-data-retention) (Fathima, 2026) | Firecrawl says ZDR is Enterprise-only, must be enabled, and has endpoint-specific behavior and an Agent-result exception. | Vendor documentation is not an independent audit; confirm exact endpoint, plan, and contract. |
| [TinyFish Browser Context Profiles](https://docs.tinyfish.ai/key-concepts/browser-context-profiles) (TinyFish, n.d.-a) | Persistent profiles store cookies and browser storage and can support signed-in automation. | Cloud transfer and site permissions need separate review; session expiry/MFA remain possible. |
| [TinyFish Terms of Service](https://www.tinyfish.ai/terms) (TinyFish, 2026) | Effective Aug. 17, 2026; license covers hosting/processing customer data for service provision, improvement, and model training under stated safeguards. | Contract terms can change and are not an independent assessment of the service. |
| [Playwright authentication](https://playwright.dev/docs/auth) (Playwright, n.d.-a) | Saved browser state may contain cookies/headers usable to impersonate the account. | Local storage practices do not define a cloud provider's handling. |
| [Apify MCP connectors](https://docs.apify.com/integrations/mcp-connectors) (Apify, n.d.) | User-authorized connectors and server-side credential injection as an integration pattern. | Actor code and each third-party connector retain their own permission and cost surface. |
| [Context Window Manager source](https://github.com/2q9e/context-plugin) (2q9e, n.d.-a) | Local project checklist, recovery, and checkpoint workflow. | It records evidence but does not independently verify the referenced work. |
| [Deep Research Engine source](https://github.com/2q9e/deep-research-plugin) (2q9e, n.d.-b) | User-selected research modes, source provenance, and research-specific orchestration. | Instructions depend on host retrieval and agent tools. |
| [`2q9e/skills`](https://github.com/2q9e/skills) (2q9e, n.d.-c) | Narrow source verification and delegation-planning skills used as supporting guidance. | Skills do not add browsing or agent tools by themselves. |
| [Universal Reach source](https://github.com/2q9e/universal-reach) (2q9e, n.d.-d) | Local read-only CLI/MCP, platform capability catalog, and partial-result metadata. | Platform support is versioned and some routes require owner authorization or are unavailable. |

## APA 7 references

2q9e. (n.d.-a). *Context Window Manager* [Source code]. GitHub. https://github.com/2q9e/context-plugin

2q9e. (n.d.-b). *Deep Research Engine* [Source code]. GitHub. https://github.com/2q9e/deep-research-plugin

2q9e. (n.d.-c). *Skills* [Source code]. GitHub. https://github.com/2q9e/skills

2q9e. (n.d.-d). *Universal Reach* [Source code]. GitHub. https://github.com/2q9e/universal-reach

agentskills.io. (n.d.). *Agent Skills specification*. https://agentskills.io/specification

Anthropic. (n.d.-a). *Skill creator* [Source code]. GitHub. https://github.com/anthropics/skills/tree/main/skills/skill-creator

Anthropic. (n.d.-b). *Use research on Claude*. Claude Help Center. https://support.claude.com/en/articles/11088861-use-research-on-claude

Apify. (n.d.). *MCP connectors*. Apify Documentation. https://docs.apify.com/integrations/mcp-connectors

Bluesky Social PBC. (n.d.). *OAuth*. AT Protocol. https://atproto.com/specs/oauth

Destefanis, G., Graziotin, D., Vaccargiu, M., & Ortu, M. (2026). *GitSkills: A dataset of agent skills on GitHub*. arXiv. https://arxiv.org/abs/2608.10906

DietrichGebert. (n.d.). *Ponytail* [Source code]. GitHub. https://github.com/DietrichGebert/ponytail

Fathima, H. (2026, October 19). *Zero data retention across Firecrawl Search, Scrape, and more*. Firecrawl. https://www.firecrawl.dev/blog/zero-data-retention

Figma. (n.d.-a). *Add custom rules and instructions*. Figma Developer Docs. https://developers.figma.com/docs/figma-mcp-server/add-custom-rules/

Figma. (n.d.-b). *Set up the remote server (recommended)*. Figma Developer Docs. https://developers.figma.com/docs/figma-mcp-server/remote-server-installation/

Figma. (n.d.-c). *Tools and prompts*. Figma Developer Docs. https://developers.figma.com/docs/figma-mcp-server/tools-and-prompts/

Figma. (n.d.-d). *What does the MCP server do, and what does my agent do?* Figma Developer Docs. https://developers.figma.com/docs/figma-mcp-server/mcp-vs-agent/

Firecrawl. (n.d.). *Crawl*. Firecrawl Documentation. https://docs.firecrawl.dev/features/crawl

Firecrawl. (2024, December 26). *Privacy policy*. https://www.firecrawl.dev/privacy-policy

Gao, T., Yen, H., Yu, J., & Chen, D. (2023). Enabling large language models to generate text with citations. In *Proceedings of the 2023 Conference on Empirical Methods in Natural Language Processing* (pp. 6465–6488). Association for Computational Linguistics. https://doi.org/10.18653/v1/2023.emnlp-main.398

GitHub. (n.d.). *Local server OAuth login (stdio)*. GitHub MCP Server. https://github.com/github/github-mcp-server/blob/main/docs/oauth-login.md

Google. (n.d.-a). *Choose Google Drive API scopes*. Google for Developers. https://developers.google.com/workspace/drive/api/guides/api-specific-auth

Google. (n.d.-b). *Implement authorization*. YouTube Data API. https://developers.google.com/youtube/data/guides/authentication

Gou, B., Huang, Z., Ning, Y., Gu, Y., Lin, M., Qi, W., Kopanev, A., Yu, B., Jimenez Gutierrez, B., Shu, Y., Song, C. H., Wu, J., Chen, S., Moussa, H., Zhang, T., Xie, J., Li, Y., Xue, T., Liao, Z., … Su, Y. (2025). Mind2Web 2: Evaluating agentic search with agent-as-a-judge. In *Advances in Neural Information Processing Systems 38* (Datasets and Benchmarks Track). https://doi.org/10.52202/085713-5778

Han, T., Zhang, Y., Song, W., Fang, C., Chen, Z., Sun, Y., & Hu, L. (2026). *SWE-Skills-Bench: Do agent skills actually help in real-world software engineering?* arXiv. https://arxiv.org/abs/2603.15401

Internet Engineering Task Force. (2025a). *Best current practice for OAuth 2.0 security* (RFC 9700). https://www.rfc-editor.org/rfc/rfc9700

Internet Engineering Task Force. (2025b). *OAuth 2.0 protected resource metadata* (RFC 9728). https://www.rfc-editor.org/rfc/rfc9728

Li, X., Liu, Y., Chen, W., You, B., Di, Z., He, Y., Zheng, S., Choe, K. W., Sun, J., Wang, S., Tao, C., Li, B., Zhao, X., Geng, H., Wu, X., Zhou, J., Chen, X., Xing, H., Li, Y., … Song, D. (2026). *SkillsBench: Benchmarking how well agent skills work across diverse tasks* (Version 4). arXiv. https://arxiv.org/abs/2602.12670v4

Mastodon. (n.d.). *OAuth scopes*. Mastodon API. https://docs.joinmastodon.org/api/oauth-scopes/

Min, S., Krishna, K., Lyu, X., Lewis, M., Yih, W.-T., Koh, P. W., Iyyer, M., Zettlemoyer, L., & Hajishirzi, H. (2023). FActScore: Fine-grained atomic evaluation of factual precision in long form text generation. In *Proceedings of the 2023 Conference on Empirical Methods in Natural Language Processing* (pp. 12076–12100). Association for Computational Linguistics. https://doi.org/10.18653/v1/2023.emnlp-main.741

Model Context Protocol. (2026a). *Authorization*. https://github.com/modelcontextprotocol/modelcontextprotocol/blob/main/docs/specification/2026-07-28/basic/authorization/index.mdx

Model Context Protocol. (2026b). *Authorization security considerations*. https://github.com/modelcontextprotocol/modelcontextprotocol/blob/main/docs/specification/2026-07-28/basic/authorization/security-considerations.mdx

obra. (n.d.). *Superpowers* [Source code]. GitHub. https://github.com/obra/superpowers

OpenAI. (n.d.-a). *Build skills*. OpenAI Developers. https://developers.openai.com/plugins/build/skills

OpenAI. (n.d.-b). *Deep research in ChatGPT*. OpenAI Help Center. https://help.openai.com/en/articles/10500283-deep-research-in-chatgpt

OpenAI. (n.d.-c). *Package your plugin*. OpenAI Developers. https://developers.openai.com/plugins/build/plugins

OpenAI. (n.d.-d). *Web search*. OpenAI Developers. https://developers.openai.com/api/docs/guides/tools-web-search?api-mode=responses

Playwright. (n.d.-a). *Authentication*. Playwright Docs. https://playwright.dev/docs/auth

Playwright. (n.d.-b). *Visual comparisons*. Playwright Docs. https://playwright.dev/docs/test-snapshots

Reddit. (n.d.). *Frequently asked questions*. Reddit Developer Platform. https://developers.reddit.com/docs/guides/faq

Storybook. (n.d.). *Visual testing in Storybook*. Storybook Tutorials. https://storybook.js.org/tutorials/ui-testing-handbook/react/en/visual-testing/

Strauss, I., Yang, J., O'Reilly, T., Rosenblat, S., & Moure, I. (2026). The attribution crisis in LLM search results: Estimating ecosystem exploitation. *Data & Policy, 8*, e15. https://doi.org/10.1017/dap.2026.10064

TinyFish. (n.d.-a). *Browser Context Profiles*. TinyFish Developer Documentation. https://docs.tinyfish.ai/key-concepts/browser-context-profiles

TinyFish. (2026). *Terms of service* (effective August 17, 2026). https://www.tinyfish.ai/terms

Wei, J., Sun, Z., Papay, S., McKinney, S., Han, J., Fulford, I., Chung, H. W., Passos, A. T., Fedus, W., & Glaese, A. (2025). *BrowseComp: A simple yet challenging benchmark for browsing agents*. arXiv. https://arxiv.org/abs/2504.12516

Wu, P., & Xie, S. (2024). V*: Guided visual search as a core mechanism in multimodal LLMs. In *Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition*. https://openaccess.thecvf.com/content/CVPR2024/papers/Wu_V_Guided_Visual_Search_as_a_Core_Mechanism_in_Multimodal_CVPR_2024_paper.pdf

Zhang, C., Liu, Y., Chen, X., & Ji, P. (2026). *What keeps agent skills from being reusable? Evidence from 138K SKILL.md files*. arXiv. https://arxiv.org/abs/2608.08453

Zhang, J., Khayatkhoei, M., Chhikara, P., & Ilievski, F. (2025). MLLMs know where to look: Training-free perception of small visual details with multimodal LLMs. In *Proceedings of the International Conference on Learning Representations*. https://openreview.net/forum?id=DgaY5mDdmT

Zhong, L., Rosenthal, F. P., Sicking, J., Hüger, F., Bagdonat, T., Gottschalk, H., & Schwinn, L. (2025). FOCUS: Internal MLLM representations for efficient fine-grained visual question answering. In *Advances in Neural Information Processing Systems, 38*. https://doi.org/10.52202/085713-3227

Zhou, S., Xu, F. F., Zhu, H., Zhou, X., Lo, R., Sridhar, A., Cheng, X., Ou, T., Bisk, Y., Fried, D., Alon, U., & Neubig, G. (2024). WebArena: A realistic web environment for building autonomous agents. In *Proceedings of the International Conference on Learning Representations*. https://proceedings.iclr.cc/paper_files/paper/2024/hash/4410c0711e9154a7a2d26f9b3816d1ef-Abstract-Conference.html

