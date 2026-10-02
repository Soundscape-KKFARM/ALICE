# ALICE

English | [繁體中文](./README.zh-TW.md)

Artist Lifecycle Intelligence & Coordination Engine

ALICE helps Soundscape creators view account and organization information, explore real-time analytics, and find public workflow guidance.

## Installation

```bash
# Claude Code
/plugin marketplace add Soundscape-KKFARM/ALICE
/plugin install alice@soundscape-net

# Codex
codex plugin marketplace add Soundscape-KKFARM/ALICE
codex plugin add alice@soundscape-net
```

## Connect to Soundscape

The plugin configures `https://rise.soundscape.net/mcp` for OAuth account linking.

- **Claude Code**: open `/mcp`, select ALICE, then sign in and grant access in your browser.
- **Codex**: check the server name in `/mcp`, run `codex mcp login <server-name>`, then sign in and grant access in your browser.
- **ChatGPT**: use its supported OAuth connection flow with the MCP URL above. Installing the local plugin does not link your ChatGPT account.

Start a new client session after installing or updating the plugin. If you previously configured a bearer-token override for this server, remove it before signing in with OAuth.

## Privacy

ALICE is provided by KKFARM. After you grant access, your client sends an OAuth access token to Soundscape's MCP service for account, organization, and analytics requests. Let your client manage tokens; do not paste them into conversations or plugin files.

[Privacy policy](https://soundscape.net/privacy-policy)

## License

[Apache-2.0](./plugins/alice/LICENSE)
