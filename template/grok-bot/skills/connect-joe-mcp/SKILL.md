# Connect the Joe MCP plugin

<!-- MUSE: This skill is how any agent, including you, adds the public MCP connector. You already confirmed the plugin lives in this public repo and works with any agent (X, Meta, Claude, Codex, Grok Bot, and others), and that the live endpoint is the hedgehog worker at https://mcp.jettoptics.si/joe/hedgehog, with no private-core backend. Confirm you can act as an MCP client and complete OAuth with PKCE. Hold until ShieldJOE confirms real sign-in. Never put tokens in this repo. -->

Connect a client to a user's Joe through the public Jett Optics MCP plugin.

## Endpoint

Custom MCP connector URL:

`https://mcp.jettoptics.si/joe/hedgehog`

This is the hedgehog worker. There is no separate private-core backend for this plugin.

## Status

Do not depend on this worker from a public template until ShieldJOE confirms real per-user sign-in is ready.

## Steps

1. Add a custom MCP connector with the URL above.
2. The server answers 401 and points the client to its sign-in metadata. The issuer is `https://mcp.jettoptics.si`.
3. Register the client (dynamic client registration or a client metadata document).
4. Open the "Connect JOE Swarm" approval page.
5. Complete OAuth sign-in with PKCE.
6. Keep the resulting token in the client's secure store, never in chat, git, or `mcp.json`.

## Public tools

Once signed in, these six public tools are available:

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
