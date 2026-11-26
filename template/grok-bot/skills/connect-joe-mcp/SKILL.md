# Connect the Joe MCP plugin

<!-- MUSE: This skill is how any agent, including you, adds the public MCP connector. Update from ShieldJOE, Nov 26: the working endpoint is https://mcp.jettoptics.si/mcp with Authorization: Bearer ${JETTCHAT_V2_KEY} (placeholder only). `/joe/hedgehog` is OAuth-only and rejects API keys. Never put a real key in this repo. -->

Connect a client to a user's Joe through the public Jett Optics MCP plugin.

## Endpoint

Custom MCP connector URL:

`https://mcp.jettoptics.si/mcp`

Send the key as `Authorization: Bearer ${JETTCHAT_V2_KEY}` (or as an `X-JOE-Token` header). Use the placeholder only in this repo — never a real key.

This is the public jettchat v2 connector. There is no separate private-core backend for this plugin.

Do not use `https://mcp.jettoptics.si/joe/hedgehog` for API keys. That path is OAuth-only and rejects keys.

## Status

The `/mcp` connector accepts Bearer keys. Get a key at `https://dojo.jettoptics.si/dojo/send` (the generate page is being built). Keep the key in the client's secret store.

## Steps

1. Add a custom MCP connector named `jettchatv2` with the URL above.
2. Set the header `Authorization: Bearer ${JETTCHAT_V2_KEY}`. Point the placeholder at the client's secret store or environment. `X-JOE-Token` is also accepted.
3. If the server answers 401, the key is missing, invalid, or being sent to the wrong path.
4. Keep the key in the client's secure store, never in chat, git, or as a literal value in `mcp.json`.

## Public tools

Once connected, these six public tools are available:

| Tool | Purpose |
|---|---|
| `hedgehog_health` | Worker health check |
| `jett_augment_status` | Augment status |
| `jett_docs_search` | Search Jett Optics docs |
| `jett_augment_lookup` | Look up augment records |
| `jett_edge_diagnose` | Edge diagnostics |
| `message_joe` | Send a message to the user's Joe |

Paid and private tools are never available through this door.

When calling `message_joe`, draft the message, show it to the user, and ask before sending. One user's Joe cannot reach another user's context.
