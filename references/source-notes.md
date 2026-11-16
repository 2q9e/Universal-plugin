# Source notes

This plugin adapts workflow patterns from the projects and documentation below; it does not copy their skill files or source code.

## Source contributions

- **Ponytail:** Read the affected code path and callers before changing behavior, prefer the smallest complete solution, and consider native or existing project mechanisms before adding dependencies (DietrichGebert, n.d.).
- **Superpowers:** Use planning only when the work has meaningful uncertainty or dependencies, investigate the cause of bugs, and verify concrete outcomes before reporting completion. The workflow here keeps those practices conditional rather than imposing a fixed sequence on every task (obra, n.d.).
- **OpenAI Skill Creator:** Keep skill guidance focused, describe clear activation conditions, and disclose detail progressively through references when needed (OpenAI, n.d.-a).
- **Figma MCP documentation:** Use design context for the exact selection, narrow large responses with metadata, use screenshots for visual reference, and translate the result into the host project's conventions (Figma, n.d.).
- **ViCrop research:** The paper studies how focused visual crops can help models perceive small details, using model-internal signals. This plugin adopts only an inspect-original-plus-focused-crop workflow where user-connected image tools allow it; it does not claim to reproduce the paper's methods (Zhang et al., 2025).
- **User-owned integrations:** Context Window Manager, `2q9e/skills`, Deep Research Engine, Universal Reach, GitHub, and Image Vision Local were mapped from the user's supplied project files and repository documentation. These are integration references, not bundled copies or evidence that the tools are connected in every host.

## References

DietrichGebert. (n.d.). *Ponytail* [Source code]. GitHub. https://github.com/DietrichGebert/ponytail

Figma. (n.d.). *Tools and prompts*. Figma Developer Docs. https://developers.figma.com/docs/figma-mcp-server/tools-and-prompts/

obra. (n.d.). *Superpowers* [Source code]. GitHub. https://github.com/obra/superpowers

OpenAI. (n.d.-a). *Build skills*. OpenAI Developers. https://developers.openai.com/plugins/build/skills

OpenAI. (n.d.-b). *Package your plugin*. OpenAI Developers. https://developers.openai.com/plugins/build/plugins

Zhang, J., Khayatkhoei, M., Chhikara, P., & Ilievski, F. (2025). MLLMs know where to look: Training-free perception of small visual details with multimodal LLMs. In *Proceedings of the International Conference on Learning Representations*. OpenReview. https://openreview.net/forum?id=DgaY5mDdmT
