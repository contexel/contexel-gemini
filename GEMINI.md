# Contexel: the team's shared memory

Contexel is this team's shared memory for AI. It returns only the context relevant to a
task, with sources, and keeps what the user asks to remember so their other AI apps and
teammates can find it. It works alongside your own memory: keep using your GEMINI.md memory
as you normally would.

In Gemini CLI its tools are named `mcp_contexel_<tool>`, for example
`mcp_contexel_get_context` and `mcp_contexel_remember`. If they are missing, Contexel is not
connected or not signed in yet; the user can run `/mcp auth contexel`.

## Two rules

- **RETRIEVE FIRST**: before answering about this team's or user's projects, decisions,
  standards, conventions, or people, call `mcp_contexel_get_context` with a `task`; your
  training won't include what they saved. Skip it for questions unrelated to their work.
- **REMEMBER into Contexel**: when the user says "remember", "note this", "save this", or
  "from now on", save it with `mcp_contexel_remember` right away (no lookup first), without
  asking, along with your own memory. Save only what the user asked to keep.

When you merely learn a durable decision, standard, or lesson while working, OFFER at the end
of the task to save it: ask first, never write silently.

## Fixing a memory that is wrong

When the user says a saved memory is wrong or out of date, find it with
`mcp_contexel_get_context` or `mcp_contexel_search`, then fix it with `mcp_contexel_correct`
using its id. Pass that `id`, a short `reason`, and the new text as `replace_with`. To retire
a memory that no longer holds, leave out `replace_with` and pass the memory's id.

Depending on your access, a save or fix lands at once or is queued for approval; the response
says which, and names the workspace.

## Workspaces

You don't have to pick a workspace: leave out `realm` and Contexel chooses one, then names
the workspace it used in the result. Relay that, and save again with `realm` named if it is
not the one the user meant. `mcp_contexel_status` lists the workspaces this connection can
reach. When unsure, leave the workspace out rather than guessing a shared one.

## Relaying an answer

Tell the user what you found in plain words, never field names. The structured
fields are there for you to parse, not to quote.

## Other tools

`mcp_contexel_status` (what is saved and whether it is up to date), `mcp_contexel_search` and
`mcp_contexel_fetch` (find memories by keyword, then read one in full). These are the everyday
tools. The full set (briefings, history, review and curation) needs `?tools=all` added to the
Contexel MCP URL in the user's Gemini CLI settings; if the user needs one of those, tell them.
