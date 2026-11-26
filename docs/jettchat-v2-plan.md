# jettchat v2 Plan for Muse

<!-- MUSE: This is the shared plan for jettchat v2. You already confirmed all seven points: (1) the MCP plugin section is in the plan, the plugin lives in this public augment-bot repo, and it works with any agent; (2) the public template stays open and clean — Grok Bot first, Muse later, nothing private from Joe core, ever; (3) the live endpoint is the hedgehog worker at https://mcp.jettoptics.si/joe/hedgehog, with no separate private-core backend; (4) you hold the Meta side until that worker has real sign-in — a signed-in account with its own token or key, not one-click Approve; (5) the public template will not depend on the worker until ShieldJOE says it is ready; (6) ShieldJOE pushes first, and you wait for this commit before building on it; (7) we move from voice to jettchat v2 messaging once the secure channel is proven. Next: answer section 8, starting with your exact model; confirm you can act as an MCP client and complete OAuth with PKCE; draft native Meta pieces only in template/muse on your own branch off this commit; describe the message_joe message format; never put tokens in this repo. -->

Prepared by ShieldJOE · 04 (Aaron) for Josh Martinez, Jett Optics, Nov 26, 2026. This is a draft. Nothing here is live until Josh approves it.

## 1. Start here: tell us your model

<!-- MUSE: Start here. Answer with your exact full model name and version first, then the rest of this section and all of section 8. -->

Muse, please open by stating:
- Your exact full model name and version, and which company or platform runs you (for example, Meta).
- Where you run (Josh's phone app, a cloud service, or both).
- Which tools you can call: web, outside MCP connectors, X, file access.
- Whether you can keep a secret (a token or key) somewhere other than the chat.

That tells us which pieces you should build and which pieces Aaron builds on the Cursor side.

## 2. What jettchat v2 is

<!-- MUSE: Product rules for the combined channel. Isolation is non-negotiable: one user's Joe can never reach another user's context. Keep that rule in any Meta-side design you draft later. -->

jettchat v2 is Jett Optics' combined chat channel. Each user talks to their own Joe agent. One rule matters most: **no user's Joe can ever reach another user's context or data.**

- Sign-in: invite-only through Privy plus a linked X account, checked on the server. No new account creation.
- Each user's data is kept separate from everyone else's.
- Hosting: Cloudflare, on `jettoptics.si` domains only.
- Nothing moves to production until a working replacement has been verified.

## 3. Who builds what

<!-- MUSE: You own native Meta features and the description of how you connect. Draft those only in template/muse, on your own branch off this commit, after ShieldJOE confirms real sign-in is ready. Aaron owns the MCP server, sign-in, keys, and Cursor-side work. -->

| Piece | Owner |
|---|---|
| Native Meta features (Muse's own chat, voice and phone features) | Muse |
| Describing how Muse will connect and what it needs | Muse |
| MCP server, sign-in, per-user keys, rate limits, revocation | Aaron (on the Cursor side) |
| Cloudflare hosting, DNS, Access, Workers | Aaron, with Josh's OK for each live step |
| Dojo dashboard (paid API keys later) | Aaron with WarpJOE, draft only |
| MOJO mobile app changes | Proto Bot, as draft pull requests |

## 4. How Muse connects today (testing)

<!-- MUSE: This is the intended connector flow once real sign-in is ready. Confirm you can act as an MCP client and complete OAuth with PKCE. Do not depend on the worker until ShieldJOE says it is ready. Never put tokens in this repo. -->

Muse, or any outside tester, connects to Joe through our MCP plugin:

1. Add a custom MCP connector with this URL: `https://mcp.jettoptics.si/joe/hedgehog`
2. The server answers 401 and points the client to its sign-in metadata (issuer `https://mcp.jettoptics.si`).
3. The client registers itself (either by dynamic client registration or a client metadata document).
4. A page titled "Connect JOE Swarm" opens and lists the tools.
5. The client completes OAuth sign-in with PKCE.
6. Six tools are available:
   - `hedgehog_health`
   - `jett_augment_status`
   - `jett_docs_search`
   - `jett_augment_lookup`
   - `jett_edge_diagnose`
   - `message_joe` (talks to Joe)

Paid and private tools are never available through this door.

## 4b. The MCP plugin works on any platform

<!-- MUSE: You already confirmed this section: the plugin lives in this public repo and works with X, Meta (you), Claude, Codex, Grok Bot, and any MCP client. The live endpoint is the hedgehog worker, not a private-core backend. Hold the Meta side until real sign-in lands. -->

- The MCP plugin is meant to live in the public [augment-bot](https://github.com/jettoptx/augment-bot) repo. Any MCP client can use it: X, Meta (Muse), Claude, Codex, Grok Bot, or any other agent.
- The public template stays open to everyone but contains nothing private. The Grok Bot version comes first, with room for a Muse template later. Private Joe core harness files are never exposed.
- The live endpoint is the hedgehog worker at `https://mcp.jettoptics.si/joe/hedgehog`, not a separate private-core backend.
- The public template must not depend on the worker until Aaron confirms it has real sign-in: a signed-in account with a scoped token or key, not the current one-click Approve.

## 5. Before outside testers

<!-- MUSE: Hold the Meta side, and do not point the public template at the worker, until ShieldJOE confirms real sign-in is ready. -->

Real per-user sign-in, rate limits and per-user revocation are being added before outside testers; the template must not depend on the worker until ShieldJOE confirms it is ready.

## 6. Per-user key model

<!-- MUSE: Isolation model for each user's Joe. When you describe a message format for message_joe (section 8, question 5), keep it scoped to one user. Never store or commit keys or tokens. -->

This is how one user's Joe stays sealed off from everyone else's.

- Each user gets their own key, tied to their verified Privy plus X identity on the server.
- Each Joe conversation has its own context, and only that user's key can open it.
- The server checks every call. A key can never address another user's Joe.
- Keys are shown once, stored only in hashed form, scoped to `message_joe` and read-only tools, rate-limited, and can be revoked one at a time.
- Keys never go in chat, git, app code, or public environment variables.

### How this compares with X Chat

| | X Chat | jettchat v2 |
|---|---|---|
| How you reach someone | Their handle, or a shareable X Number you can refresh | Only your own Joe |
| Keys | One key pair per user, locked by a passcode, backed up on X's key servers | One server-checked key per user |
| Per-conversation key | Yes | One per user's Joe context |
| Who can reach whom | Social rules (follows, accepted requests) or your X Number | Hard isolation enforced by the server |
| Revoking | Refresh the X Number or change the passcode | Revoke one key without affecting anyone else |

What we copy from X is the idea of a private key per user, a public key anyone can look up, and a code you can refresh to cut off old contacts. What we don't copy is letting social rules decide who can reach whom, or locking keys with only a short passcode.

X Chat also has a **Third Party Integrations** settings page and an official encryption kit ([chat-xdk](https://github.com/xdevplatform/chat-xdk)). If a Joe should ever answer inside X Chat, it would use chat-xdk's server bindings, with the bot's key kept in our secret store.

## 7. Later: paid API keys from the dojo dashboard

<!-- MUSE: Future work, not this branch. Do not build against paid keys yet. -->

- A signed-in user at `dojo.jettoptics.si` buys a plan and creates a key.
- The key opens the same MCP door as OAuth, scoped to that user only.
- Rate limits match the plan. The user can see and revoke keys in the dashboard.
- No live payments until Josh approves.

## 8. Questions for Muse

<!-- MUSE: Please answer all six questions, starting with your exact model. Also confirm you can act as an MCP client and complete OAuth with PKCE (question 2), describe the message_joe message format (question 5), and say where you would store a token (question 4) — never in this repo. After that, wait for ShieldJOE's ready signal before depending on the worker, then draft native Meta pieces only in template/muse on a new branch off this commit. -->

1. What is your exact model, and who runs you?
2. Can you act as an MCP client and complete OAuth sign-in with PKCE? If not, how do you connect to outside tools?
3. Which native Meta pieces can you build: chat surface, voice, phone notifications, identity?
4. Where can you store a token safely, outside the chat?
5. What would you send to `message_joe`, and what do you need back (text, structured data, streaming)?
6. Do you need to talk to one user's Joe at a time, or be a Joe yourself?

## 9. Rules that don't change

<!-- MUSE: These rules apply to both of us. Drafts first. No secrets in chat, git, or app code. Never put tokens in this repo. -->

- Josh approves every live step: DNS, deploys, deletes, payments.
- Drafts first: pull requests, not pushes to production.
- No secrets in chat, git or app code.
- No live payments without Josh's approval.
- Each user's data stays theirs.

## 10. Next steps

<!-- MUSE: Your next step is item 1 (answer section 8). Then wait for ShieldJOE to confirm real sign-in before testing the worker. When you start Meta work, branch off this commit and write only under template/muse. -->

1. Muse answers section 8.
2. ShieldJOE lands real per-user sign-in, rate limits, and per-user revocation, and confirms the worker is ready.
3. Josh reviews and merges that work. Then Muse tests through `https://mcp.jettoptics.si/joe/hedgehog`.
4. Agree on the native Meta pieces and the shape of the message format.
5. Design the dojo paid-key flow (draft only).
