---
name: authorized-source-access
description: Use when research needs login-dependent, workspace-only, or account-specific content, or would send authenticated browser state through a service.
---
<!-- Copyright (c) 2026 2q9e. See ../../LICENSE for terms. -->

# Authorized source access

Choose a legitimate route for the exact content the user requested. Read the access section of [`../../references/integration-map.md`](../../references/integration-map.md) for the companion-plugin handoff.

## Route selection

1. Define the target site/platform, data requested, relevant account or workspace, and whether public content is sufficient.
2. Check current host tools and source capabilities. A listed integration is not necessarily connected, and an API may support only specific account roles or data types.
3. Prefer these routes in order when they support the request:
   - A documented anonymous public endpoint or feed.
   - A first-party API or OAuth/MCP connector, with the narrowest available read scope and the user's own access.
   - A user-authorized browser session only when the host supports it and the target site's rules permit it. The user signs in and handles MFA in the browser; do not ask them to paste credentials or session material into chat.
4. Treat a crawler/search API key as authorization to that retrieval service, not as a login to the target website. Treat OAuth scopes, connected-app permissions, platform approval, account role, plan limits, and returned content scope as separate constraints.
5. Before sending signed-in page content or persistent browser state to a cloud service, explain which service receives it and check its current terms, retention, processing region, and deletion controls. Make this transfer only when the user has authorized that route. Do not infer that a privacy label or retention mode covers every endpoint, data class, or plan.
6. If no authorized path is available, state what is inaccessible and offer a supported alternative such as public evidence, an official connector, or a user-provided export.

## Stop conditions

Respect the site's published access rules and crawler directives such as `robots.txt`. Stop when a source presents a login requirement the available connector cannot handle, an access denial, a CAPTCHA, a paywall, an admin approval requirement, or another policy restriction. Do not continue by using stealth or anti-detection modes, proxy rotation, fingerprint changes, CAPTCHA-solving, copied cookies, password reuse, or another access-control workaround. Do not silently retry after a clear block.

Do not submit forms, change account data, post, message, or trigger another external action when the user asked only to research or read.

## Evidence and handoff

For each source used, carry forward:

- The canonical URL or platform item ID and its title/author when available.
- The access class: public, official API/OAuth, connected app/MCP, user-supervised browser, partial, or blocked.
- Retrieval time and publication time when available.
- The account or permission scope that bounds the result, without recording a credential.
- Pagination, rate-limit, coverage, and partial-result warnings.

Keep public web evidence distinct from content visible only to the user's account. Cite the original item when it can be inspected. If a connector returned derived or truncated data, label that fact and avoid claiming full coverage.

When handing findings to Deep Research Engine, pass source links and limits rather than credentials or unnecessary private page content. When recording progress in Context Window Manager, save only the minimal decision and evidence needed to resume.
