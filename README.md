# ALICE

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

## MCP setup

Before installing, set `SOUNDSCAPE_RISE_TOKEN` to a Soundscape personal secret token in the environment that launches Claude Code or Codex. Do not put the token in conversations, source code, or configuration files that may be committed.

Start a new session after installing or updating the plugin so the client reloads the MCP server and skills. ALICE currently exposes three MCP tools: `me` returns profile details and accessible organizations; `tools` lists six analytics operations, searches their names and descriptions, or returns the input schema for an exact name; and `query` runs a selected analytics operation. When the operation name and arguments are known, call `query` directly.

The `soundscape-alice` skill selects MCP tools as needed. The `help-me` skill consults only official public Soundscape documentation.

## License

[Apache-2.0](./plugins/alice/LICENSE)
