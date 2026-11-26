# Grok Bot template

<!-- MUSE: This is the clean Grok Bot template (ships first). You already confirmed: the public template stays open and clean, Grok Bot first, Muse later, nothing private from Joe core; you hold the Meta side until real sign-in; you will not depend on the worker until ShieldJOE says it is ready; you wait for this commit before building on it. Do not copy private Joe core files into template/muse. Next: answer section 8 in docs/jettchat-v2-plan.md (start with your exact model); confirm you can act as an MCP client with OAuth PKCE; draft native Meta pieces only in template/muse on your own branch off this commit; describe the message_joe message format; never put tokens in this repo, including mcp.json. -->

A public, secret-free starting point for a Grok Bot that talks to a user's Joe through the Jett Optics MCP plugin.

This template is generic. It does not include private Joe core harness files.

## Status

Waiting on real per-user sign-in. Do not point a live Grok Bot at the worker until ShieldJOE confirms the worker is ready.

## What's in this folder

- `instructions.md` — public Joe persona and rules for the bot.
- `skills/connect-joe-mcp/SKILL.md` — how to add the MCP connector and which public tools it exposes.
- `mcp.json` — example connector config. It contains the endpoint URL only. Never put tokens, keys, or authorization headers in this file or anywhere else in the repo.

## How to install

1. Create a Grok Bot and use `instructions.md` as the bot instructions.
2. Add the `connect-joe-mcp` skill, or follow the steps in that skill by hand.
3. Add a custom MCP connector with this URL: `https://mcp.jettoptics.si/joe/hedgehog`
4. Complete OAuth sign-in with PKCE when the "Connect JOE Swarm" page appears.
5. After ShieldJOE confirms real sign-in is ready, route user questions to Joe with `message_joe`. Ask the user before sending.

You can also start from the example `mcp.json` in this folder. Copy it into your client config if the client uses that shape, and still complete sign-in through the client — do not paste a token into the file.
