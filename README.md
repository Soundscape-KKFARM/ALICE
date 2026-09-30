# ALICE

English | [繁體中文](./README.zh-TW.md)

Artist Lifecycle Intelligence & Coordination Engine

## Installation

```bash
# Claude Code
/plugin marketplace add Soundscape-KKFARM/ALICE
/plugin install alice@soundscape-net

# Codex
codex plugin marketplace add Soundscape-KKFARM/ALICE
codex plugin add alice@soundscape-net
```

Claude Code and Codex install the same `plugins/alice` package.

## MCP setup

ALICE authenticates with a Soundscape personal secret token. Do not put the token in conversations, source code, or configuration files that may be committed.

- **Claude Code**: when the plugin is enabled, Claude Code prompts for the token, masks the input, and stores it in the system's secure credential store. To change it later, run `/plugin configure alice`.
- **Codex**: before launching Codex, set `SOUNDSCAPE_RISE_TOKEN` to the token in the environment that launches it.

Start a new session after installing or updating the plugin so the client reloads the MCP server and skills. ALICE currently exposes three MCP tools: `me` returns profile details and accessible organizations; `tools` lists six analytics operations, searches their names and descriptions, or returns the input schema for an exact name; and `query` runs a selected analytics operation. When the operation name and arguments are known, call `query` directly.

The `soundscape-alice` skill selects MCP tools as needed. The `help-me` skill consults only official public Soundscape documentation.

### Launching the ChatGPT app on macOS

When using a local runtime through ChatGPT, fully quit the app with `Cmd+Q`, then set the token and launch it from Terminal. Replace `<token>` with your personal secret token, keeping the quotes:

```bash
export SOUNDSCAPE_RISE_TOKEN='<token>' && open /Applications/ChatGPT.app
```

macOS `open` lets a newly launched app inherit the Terminal environment (see `man open`). If the app is already running, `open` usually reuses that process; closing its window does not quit it or update its environment. Fully quit and relaunch the app after changing the token.

These commands configure the local app environment. Web or remote execution environments require separate authentication setup. MCP connectivity still depends on the client's execution mode and token permissions; see the [OpenAI MCP documentation](https://learn.chatgpt.com/docs/extend/mcp) and [Claude Code MCP documentation](https://code.claude.com/docs/en/mcp).

## Privacy

ALICE is provided by KKFARM and connects to Soundscape's MCP service at `https://rise.soundscape.net/mcp`. A Soundscape personal secret token, saved in the Claude Code plugin configuration or supplied through `SOUNDSCAPE_RISE_TOKEN` in Codex, is sent to that service in the `Authorization` header to authenticate account, organization, and analytics requests.

[Privacy policy](https://soundscape.net/privacy-policy)

## License

[Apache-2.0](./plugins/alice/LICENSE)
