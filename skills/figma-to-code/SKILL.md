---
name: figma-to-code
description: Use when implementing or reviewing an interface from a Figma design, screenshot, or exported visual reference.
---
<!-- Copyright (c) 2026 2q9e. See ../../LICENSE for terms. -->

# Figma to code

Use connected Figma tools when they are available. Otherwise use the design link, screenshot, export, or specifications the user supplied. Do not imply access to a Figma file that was not opened.

## Figma MCP workflow

1. Identify the exact file and frame, selection, or node that represents the requested state.
2. Call `get_design_context` for that selection. If the result is too large or truncated, use `get_metadata` to find the relevant child nodes, then request context for those nodes.
3. Get a `get_screenshot` reference for the target selection. Use `get_variable_defs` or Code Connect information when it is available and relevant. Download source assets only when implementation needs them.
4. Inspect the existing codebase and translate the design into its framework, components, tokens, and accessibility conventions. Treat generated code as design evidence, not automatically as project-ready code.
5. Compare the completed interface with the design reference when visual comparison is available. Report visual validation only if it was performed.

For screenshot comparisons, keep the viewport, device scale, fonts, and loading state consistent where the existing project tooling allows it. Reuse the project's current Playwright, Storybook, or Chromatic setup instead of adding a visual-testing service by default. A pixel difference is evidence of a visual change, not proof of semantic correctness.

Use Figma write tools only when the user asked to change the Figma document. A request to implement a design in code authorizes the repository change, not an unrelated canvas edit.

## Small visual details

When text, icons, labels, or small geometry are hard to read, use an available Image Vision Local tool such as `inspect`, `crop`, `zoom`, `ocr`, or `compare_regions`. Keep the original image in view, inspect a focused crop, and compare the crop's location and meaning against the full image before making a claim. A crop helps inspect the pixels; it does not by itself prove what an unclear detail means.

If Figma or image tools are unavailable, continue from the supplied reference where possible and note what could not be checked. Ask only for a missing frame, image, or behavior that blocks the requested result.
