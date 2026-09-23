# Contexel for Gemini CLI

Contexel is AI memory for teams: one shared memory that Gemini CLI, Claude, ChatGPT, Cursor
and your teammates' AI apps can all read from and save to, with the source of every memory
shown. This extension connects Gemini CLI to Contexel and teaches it when to use it, in one
install.

Once it is installed, Gemini CLI will:

- **Look things up first:** before answering a question about your team's projects,
  decisions, standards or people, it checks what your team has saved in Contexel.
- **Remember what you ask it to:** when you say "remember this", "note this" or "from now
  on", it saves the point to Contexel as well as to its own memory, so your other AI apps and
  your teammates can find it too. It saves only what you asked it to keep.
- **Fix what is wrong:** when you say a saved memory is wrong or out of date, it corrects
  that memory in Contexel, or retires it if it no longer holds. Depending on your access in
  that workspace, a save or a fix lands at once or waits for a teammate's approval; Gemini
  CLI tells you which.

Contexel works alongside Gemini CLI's own memory (its GEMINI.md files). It never tells Gemini
to stop using that memory; it keeps a shared copy that travels with you and your team.

## Install

```shell
gemini extensions install https://github.com/contexel/contexel-gemini
```

> This extension is published at
> [github.com/contexel/contexel-gemini](https://github.com/contexel/contexel-gemini). Inside the
> Contexel source repository the same files live under `clients/gemini-cli/`.

Restart Gemini CLI after installing. To try a local checkout without installing it, link the
folder instead: `gemini extensions link /path/to/contexel-gemini`.

## Sign in on first use

The extension points Gemini CLI at the hosted Contexel service. The first time Gemini CLI
connects, Contexel asks it to sign in, and Gemini CLI opens your browser to the Contexel
sign-in page. Sign in with your Contexel account and your workspace is picked for you. You can
also start or repeat the sign-in yourself with `/mcp auth contexel` inside Gemini CLI.

Browser sign-in needs a browser on the same machine. It does not work on a headless machine,
over SSH without a forwarded display, or in a container without a browser. On those machines,
sign in on a computer with a browser instead.

## Using it

Just work as usual. Ask "what did we decide about the uploads bucket?" and Gemini CLI looks it
up in Contexel before answering. Say "remember that we deploy on Tuesdays and Thursdays" and
it saves that to Contexel along with its own memory. Every result names the workspace it came
from or went to, so you can always see where your memory lives.

In Gemini CLI the Contexel tools appear with a `mcp_contexel_` prefix, for example
`mcp_contexel_get_context`, `mcp_contexel_remember` and `mcp_contexel_correct`. `/mcp` lists
them and shows whether Contexel is connected.

The extension connects with Contexel's everyday tools: look up, save, fix, check status,
search and fetch. For every tool (briefings, history, review and curation), define the
`contexel` server yourself in `~/.gemini/settings.json`, as in "Self-hosting Contexel" below,
with `"httpUrl": "https://contexel.ai/mcp?tools=all"`.

For project-specific rules (such as which workspace your team's knowledge belongs in), copy
the rules text from the Contexel console's "Connect your agent" panel into your project's
`GEMINI.md`.

## Privacy

The extension holds no keys, tokens or passwords. It is two text files: a manifest that names
the hosted endpoint, `https://contexel.ai/mcp`, and a short `GEMINI.md` with the guidance
above. Your sign-in token is kept by Gemini CLI itself, in `~/.gemini/mcp-oauth-tokens.json`,
not in the extension. What you save goes to your Contexel workspace on the hosted service and
nowhere else.

## Self-hosting Contexel

If you run your own Contexel server, point Gemini CLI at it by defining a server with the same
name, `contexel`, in your Gemini CLI settings file (`~/.gemini/settings.json`). A server in
`settings.json` takes precedence over one of the same name from an extension, so your server
replaces the hosted one and the guidance in this extension still applies:

```json
{
  "mcpServers": {
    "contexel": {
      "httpUrl": "https://contexel.example.com/mcp"
    }
  }
}
```

Keep the name `contexel`: the guidance refers to the tools as `mcp_contexel_...`.

## Gallery listing

This repository carries the `gemini-cli-extension` topic, so it appears in the Gemini CLI
extension gallery at [geminicli.com/extensions](https://geminicli.com/extensions). The gallery
crawls tagged public repositories daily; there is no separate submission.

## Layout

```
.
├── gemini-extension.json   # manifest: name, version, the Contexel MCP server
├── GEMINI.md               # the guidance Gemini CLI loads every session
├── LICENSE
└── README.md
```

## License

Apache-2.0; see `LICENSE`.
