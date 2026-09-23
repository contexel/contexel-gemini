# Contexel: the team's shared memory

Contexel is this team's shared memory for AI. It returns only the context relevant to a
task, with sources, and keeps what the user asks to remember so their other AI apps and
teammates can find it. It works alongside your own memory: keep using your GEMINI.md memory
as you normally would.

In Gemini CLI its tools are named `mcp_contexel_<tool>`, for example
`mcp_contexel_get_context` and `mcp_contexel_observe`. If they are missing, Contexel is not
connected or not signed in yet; the user can run `/mcp auth contexel`.

## Two rules

- **RETRIEVE FIRST**: before answering about this team's or user's projects, decisions,
  standards, conventions, or people, call `mcp_contexel_get_context` with a `task` (or
  `mcp_contexel_prime` for a compact briefing); your training won't include what they saved.
  Skip it for questions unrelated to their work.
- **REMEMBER into Contexel**: when the user says "remember", "note this", "save this", or
  "from now on", save it with `mcp_contexel_observe` (a quick note) or `mcp_contexel_propose`
  (a lasting entry in the team's memory) right away, without asking, along with your own
  memory. Save only what the user asked to keep.

When you merely learn a durable decision, standard, or lesson while working, OFFER at the end
of the task to save it: ask first, never write silently. Depending on your access, a save
lands directly or goes to a teammate for approval; the tool's response says which.

## Workspaces

You don't have to pick a workspace: leave out `realm` and Contexel chooses one, then names
the workspace it used in the result. Relay that, and save again with `realm` named if it is
not the one the user meant. `mcp_contexel_status` lists the workspaces this connection can
reach. When unsure, leave the workspace out rather than guessing a shared one.

## Relaying an answer

Answer the user from a result's readable text, not its structured fields. Every tool returns
both; the fields are there for you to parse, not to quote.

## Other tools

`mcp_contexel_explain` (why a memory was or wasn't returned), `mcp_contexel_cite` (its exact
quotable spans), `mcp_contexel_delta` and `mcp_contexel_digest` (what changed since a git
ref), `mcp_contexel_resolve_entity` and `mcp_contexel_expand` (people, systems, and how they
connect), `mcp_contexel_help` (anything else).
