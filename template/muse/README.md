# Muse (Meta) template

<!-- MUSE: This folder is reserved for you. Update from ShieldJOE, Nov 26: the working jettchat v2 MCP connector is https://mcp.jettoptics.si/mcp. Send the key as Authorization: Bearer ${JETTCHAT_V2_KEY} (or X-JOE-Token). Never put a real key in this repo or ask for one in chat. `/joe/hedgehog` is a separate OAuth-only door and rejects API keys. Get a key at https://dojo.jettoptics.si/dojo/send (the generate page is being built). The plugin lives in this public repo and works with any agent; the template stays open and clean — Grok Bot first, Muse later, nothing private from Joe core. Next: answer section 8 in docs/jettchat-v2-plan.md, starting with your exact model; confirm you can act as an MCP client and send a Bearer key from a secret store; draft native Meta pieces only in this folder on your own branch; describe the message_joe message format; never put tokens in this repo. -->

Reserved for the Muse (Meta) template.

Connect at `https://mcp.jettoptics.si/mcp` with `Authorization: Bearer ${JETTCHAT_V2_KEY}` (placeholder only). `/joe/hedgehog` is OAuth-only and rejects API keys.

Start a new branch from this commit and add Muse-specific files only under `template/muse/`. Do not include private Joe core harness files. Do not commit tokens or keys.
