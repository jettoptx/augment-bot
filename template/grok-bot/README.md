# Grok Bot template

<!-- MUSE: This is the clean Grok Bot template (ships first). Update from ShieldJOE, Nov 26: connect at https://mcp.jettoptics.si/mcp with Authorization: Bearer ${JETTCHAT_V2_KEY} (placeholder only). `/joe/hedgehog` is OAuth-only and rejects API keys. Do not copy private Joe core files into template/muse. Next: answer section 8 in docs/jettchat-v2-plan.md (start with your exact model); confirm you can act as an MCP client and send a Bearer key from a secret store; draft native Meta pieces only in template/muse on your own branch; describe the message_joe message format; never put a real key in this repo, including mcp.json. -->

A public, secret-free starting point for a Grok Bot that talks to a user's Joe through the Jett Optics MCP plugin.

This template is generic. It does not include private Joe core harness files.

## Status

The `/mcp` connector accepts Bearer keys. Keep the key in the client's secret store. Never commit a real key.

## What's in this folder

- `instructions.md` — public Joe persona and rules for the bot.
- `skills/connect-joe-mcp/SKILL.md` — how to add the MCP connector and which public tools it exposes.
- `mcp.json` — example connector config. It uses the placeholder `${JETTCHAT_V2_KEY}` in the Authorization header. Never replace that placeholder with a real key in this repo.

## How to install

1. Create a Grok Bot and use `instructions.md` as the bot instructions.
2. Add the `connect-joe-mcp` skill, or follow the steps in that skill by hand.
3. Add a custom MCP connector named `jettchatv2` with this URL: `https://mcp.jettoptics.si/mcp`
4. Set the header `Authorization: Bearer ${JETTCHAT_V2_KEY}`, with the real key supplied from the client's secret store or environment — not from this repo. `X-JOE-Token` is also accepted.
5. Get a key at `https://dojo.jettoptics.si/dojo/send` (the generate page is being built). Route user questions to Joe with `message_joe`. Ask the user before sending.

You can also start from the example `mcp.json` in this folder. Copy it into your client config if the client uses that shape, and point `${JETTCHAT_V2_KEY}` at a secret store. Do not paste a real key into the file.

Do not use `https://mcp.jettoptics.si/joe/hedgehog` for API keys. That path is OAuth-only and rejects keys.
