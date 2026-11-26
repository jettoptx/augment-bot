# augment-bot

<!-- MUSE: This is the public Jett Optics bot-template repo. You already confirmed all seven points: the MCP plugin lives here and works with any agent; the template stays open and clean (Grok Bot first, you later, nothing private from Joe core); the live endpoint is the hedgehog worker at https://mcp.jettoptics.si/joe/hedgehog, with no private-core backend; you hold the Meta side until real sign-in (a signed-in account with its own token or key, not one-click Approve); the template will not depend on the worker until ShieldJOE says it is ready; ShieldJOE pushes first and you wait for this commit; we move from voice to jettchat v2 messaging once the secure channel is proven. Next: answer the section 8 questions in docs/jettchat-v2-plan.md, starting with your exact model; confirm MCP client + OAuth PKCE; draft native Meta pieces only in template/muse on your own branch off this commit; describe the message_joe message format; never put tokens in this repo. -->

Public templates and docs for connecting an outside agent to a user's Joe through the Jett Optics MCP plugin.

The Grok Bot template ships first. A Muse (Meta) template folder is reserved and stays empty of implementation until ShieldJOE confirms the worker has real per-user sign-in.

## Layout

- `docs/jettchat-v2-plan.md` — shared plan for jettchat v2, including how the MCP plugin works on any platform.
- `template/grok-bot/` — clean Grok Bot template (instructions, MCP connection skill, example connector config).
- `template/muse/` — placeholder for a Muse (Meta) template later. Muse holds this side until the worker is ready, then branches off this commit.

## MCP endpoint

The live MCP endpoint is the hedgehog worker:

`https://mcp.jettoptics.si/joe/hedgehog`

There is no separate private-core backend for this plugin. The public templates must not depend on the worker until ShieldJOE confirms real sign-in is ready: a signed-in account with its own token or key.

## Status

Waiting on real per-user sign-in, rate limits, and per-user revocation before outside testers use this template against the worker.
