---
name: skill-workshop
description: Use when creating, updating, or packaging reusable agent skills or skill-based plugins.
---
<!-- Copyright (c) 2026 2q9e. See ../../LICENSE for terms. -->

# Skill workshop

Use the installed `skill-creator` skill when it is available. For a plugin package, use the available Plugin Creator workflow and its current package requirements. This skill provides a portable fallback, not a substitute for host validation.

1. Define the specific user goal, what should trigger the skill, required inputs, and its expected result. Keep unrelated workflows out of the same skill.
2. Write concise metadata that distinguishes the skill from neighboring tools and workflows. Put essential decisions in `SKILL.md`; move substantial, conditional detail to a small referenced guide only when it is useful.
3. Include only resources that directly support the workflow. Prefer instructions and existing tools over adding code or dependencies without a concrete reason.
4. Check that the skill name matches its folder, YAML frontmatter parses, references stay inside the package, and descriptions accurately describe activation. For plugins, parse the manifest and confirm every packaged skill and referenced asset is present.
5. Preserve user intent and existing permissions. State which format or package validation was completed; do not claim host installation or runtime behavior unless it was observed.
