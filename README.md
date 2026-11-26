# augment-bot

<!-- MUSE: This is the public Jett Optics bot-template repo. Update from ShieldJOE, Nov 26: the working jettchat v2 MCP connector is https://mcp.jettoptics.si/mcp. Send the key as Authorization: Bearer ${JETTCHAT_V2_KEY} (or X-JOE-Token). Never put a real key in this repo or ask for one in chat. `/joe/hedgehog` is a separate OAuth-only door and rejects API keys. Get a key at https://dojo.jettoptics.si/dojo/send (the generate page is being built). The plugin lives here and works with any agent; the template stays open and clean (Grok Bot first, you later, nothing private from Joe core). Next: answer the section 8 questions in docs/jettchat-v2-plan.md, starting with your exact model; confirm you can act as an MCP client and send a Bearer key from a secret store; draft native Meta pieces only in template/muse on your own branch; describe the message_joe message format; never put tokens in this repo. -->

Public templates and docs for connecting an outside agent to a user's Joe through the Jett Optics MCP plugin.

The Grok Bot template ships first. A Muse (Meta) template folder is reserved for later implementation.

## Layout

- `docs/jettchat-v2-plan.md` — shared plan for jettchat v2, including how the MCP plugin works on any platform.
- `template/grok-bot/` — clean Grok Bot template (instructions, MCP connection skill, example connector config).
- `template/muse/` — placeholder for a Muse (Meta) template later.

## MCP endpoint

The working jettchat v2 connector is:

`https://mcp.jettoptics.si/mcp`

Send the key as `Authorization: Bearer ${JETTCHAT_V2_KEY}` (or as an `X-JOE-Token` header). Use the placeholder only in this repo — never a real key.

`/joe/hedgehog` is a separate OAuth-only door. API keys do not work there.

Create and revoke keys at `https://dojo.jettoptics.si/dojo/send` (the generate page is being built).

There is no separate private-core backend for this plugin.

## Status

The `/mcp` connector accepts Bearer keys. In Grok Bot, the connector is named `jettchatv2`. Keep keys in the client's secret store, never in git, chat, or app code.
