# Source notes

Universal Workbench adapts operating patterns from the projects and documentation below. It does not copy their source code, package other plugins' skills, or claim their capabilities when the corresponding tool is unavailable.

## What was adapted

- **Ponytail:** inspect affected code and callers before changing behavior; prefer the smallest complete change and existing project mechanisms (DietrichGebert, n.d.).
- **Superpowers:** use structured planning when uncertainty or dependencies justify it, diagnose causes before patching, and report only outcomes that were actually verified (obra, n.d.). Keep these practices proportional to the task rather than mandatory phases for every request.
- **Skill Creator and Agent Skills:** keep skill triggers specific, instructions focused, and deeper detail in small referenced resources. The specification standardizes a package shape but does not guarantee host discovery, permissions, or tool availability (agentskills.io, n.d.; Anthropic, n.d.; OpenAI, n.d.-a).
- **Deep Research Engine and Better Research:** keep broad investigation separate from narrow fact-checking; preserve mode, source provenance, claim-level evidence, limitations, and counterevidence when the scope warrants it (2q9e, n.d.-b, n.d.-c; Gao et al., 2023; Min et al., 2023).
- **Universal Reach:** route by the live platform capability and operation, carry access mode and partial-result metadata, and avoid treating a catalog entry as proof of full coverage. Its current local source is a read-only CLI/MCP service with public retrieval as the default and a few explicitly owner-authorized routes (2q9e, n.d.-d).
- **Figma and visual research:** use the exact frame, structured design context, metadata when selection is too large, and a screenshot; translate output into project conventions. Retain crop coordinates and original-image context; model-specific crop strategies are optional, not capabilities of this generic plugin (Figma, n.d.-a, n.d.-b; Wu & Xie, 2024; Zhang et al., 2025).
- **Authorized access:** prefer official APIs and scoped OAuth/MCP connectors. Treat search/crawl keys separately from target-site permissions, and treat persistent browser state as credential-equivalent. Hosted browser sessions need explicit user authorization and current provider terms reviewed before signed-in content is sent off-device (Internet Engineering Task Force, 2025a, 2025b; Model Context Protocol, 2026a; Playwright, n.d.; TinyFish, 2026).

These choices keep Universal Workbench as a coordinator: Context Window Manager carries project state, Deep Research Engine conducts broad research, and Universal Reach fetches platform material where its current adapter allows it. The coordinator carries constraints and evidence between them; it does not replace their tools (2q9e, n.d.-a, n.d.-b, n.d.-d).

## Source code and research record

- The user's Universal Reach source was inspected, including its README, capability catalog, adapter/service contracts, and MCP tool definitions. Its own package status and policy notes are preferable to assumptions from upstream platform names.
- The user's Deep Research Engine package was inspected, including its engine and orchestration skills, evaluation scenarios, privacy note, and plugin manifest.
- The user's local `better-research` and `better-subagent-use` skills were used as workflow guidance, not copied into this package.
- Multi-track source notes, counterevidence, the full source guide, APA references, and source limitations are in [`related-project-research.md`](related-project-research.md).

## Selected references

2q9e. (n.d.-a). *Context Window Manager* [Source code]. GitHub. https://github.com/2q9e/context-plugin

2q9e. (n.d.-b). *Deep Research Engine* [Source code]. GitHub. https://github.com/2q9e/deep-research-plugin

2q9e. (n.d.-c). *Skills* [Source code]. GitHub. https://github.com/2q9e/skills

2q9e. (n.d.-d). *Universal Reach* [Source code]. GitHub. https://github.com/2q9e/universal-reach

agentskills.io. (n.d.). *Agent Skills specification*. https://agentskills.io/specification

Anthropic. (n.d.). *Skill creator* [Source code]. GitHub. https://github.com/anthropics/skills/tree/main/skills/skill-creator

DietrichGebert. (n.d.). *Ponytail* [Source code]. GitHub. https://github.com/DietrichGebert/ponytail

Figma. (n.d.-a). *Add custom rules and instructions*. Figma Developer Docs. https://developers.figma.com/docs/figma-mcp-server/add-custom-rules/

Figma. (n.d.-b). *Tools and prompts*. Figma Developer Docs. https://developers.figma.com/docs/figma-mcp-server/tools-and-prompts/

Gao, T., Yen, H., Yu, J., & Chen, D. (2023). Enabling large language models to generate text with citations. In *Proceedings of the 2023 Conference on Empirical Methods in Natural Language Processing* (pp. 6465–6488). Association for Computational Linguistics. https://doi.org/10.18653/v1/2023.emnlp-main.398

Internet Engineering Task Force. (2025a). *Best current practice for OAuth 2.0 security* (RFC 9700). https://www.rfc-editor.org/rfc/rfc9700

Internet Engineering Task Force. (2025b). *OAuth 2.0 protected resource metadata* (RFC 9728). https://www.rfc-editor.org/rfc/rfc9728

Min, S., Krishna, K., Lyu, X., Lewis, M., Yih, W.-T., Koh, P. W., Iyyer, M., Zettlemoyer, L., & Hajishirzi, H. (2023). FActScore: Fine-grained atomic evaluation of factual precision in long form text generation. In *Proceedings of the 2023 Conference on Empirical Methods in Natural Language Processing* (pp. 12076–12100). Association for Computational Linguistics. https://doi.org/10.18653/v1/2023.emnlp-main.741

Model Context Protocol. (2026a). *Authorization*. https://github.com/modelcontextprotocol/modelcontextprotocol/blob/main/docs/specification/2026-07-28/basic/authorization/index.mdx

obra. (n.d.). *Superpowers* [Source code]. GitHub. https://github.com/obra/superpowers

OpenAI. (n.d.-a). *Build skills*. OpenAI Developers. https://developers.openai.com/plugins/build/skills

OpenAI. (n.d.-b). *Deep research in ChatGPT*. OpenAI Help Center. https://help.openai.com/en/articles/10500283-deep-research-in-chatgpt

Playwright. (n.d.). *Authentication*. Playwright Docs. https://playwright.dev/docs/auth

TinyFish. (2026). *Terms of service* (effective August 17, 2026). https://www.tinyfish.ai/terms

Wu, P., & Xie, S. (2024). V*: Guided visual search as a core mechanism in multimodal LLMs. In *Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition*. https://openaccess.thecvf.com/content/CVPR2024/papers/Wu_V_Guided_Visual_Search_as_a_Core_Mechanism_in_Multimodal_CVPR_2024_paper.pdf

Zhang, J., Khayatkhoei, M., Chhikara, P., & Ilievski, F. (2025). MLLMs know where to look: Training-free perception of small visual details with multimodal LLMs. In *Proceedings of the International Conference on Learning Representations*. https://openreview.net/forum?id=DgaY5mDdmT
