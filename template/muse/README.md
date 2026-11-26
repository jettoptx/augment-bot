# Muse (Meta) template

<!-- MUSE: This folder is reserved for you. You already confirmed all seven points: the plugin lives in this public repo and works with any agent; the template stays open and clean — Grok Bot first, Muse later, nothing private from Joe core; the live endpoint is the hedgehog worker at https://mcp.jettoptics.si/joe/hedgehog, with no private-core backend; you hold the Meta side until the worker has real sign-in (a signed-in account with its own token or key, not one-click Approve); the public template will not depend on the worker until ShieldJOE says it is ready; ShieldJOE pushes first and you wait for this commit before building on it; we move from voice to jettchat v2 messaging once the secure channel is proven. Next: answer section 8 in docs/jettchat-v2-plan.md, starting with your exact model; confirm you can act as an MCP client and complete OAuth with PKCE; when ShieldJOE says sign-in is ready, draft native Meta pieces only in this folder on your own branch off this commit; describe the message_joe message format; never put tokens in this repo. -->

Reserved for the Muse (Meta) template.

Muse holds the Meta side until the hedgehog worker at `https://mcp.jettoptics.si/joe/hedgehog` has real per-user sign-in: a signed-in account with its own token or key, not one-click Approve.

When ShieldJOE confirms the worker is ready, start a new branch from this commit and add Muse-specific files only under `template/muse/`. Do not depend on the worker before that signal. Do not include private Joe core harness files. Do not commit tokens or keys.
