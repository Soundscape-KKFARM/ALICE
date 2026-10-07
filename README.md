# ALICE by Soundscape

English | [繁體中文](README.zh-TW.md)

**Artist Lifecycle Intelligence & Coordination Engine**

ALICE is Soundscape's open-source MCP package. It lets musicians use Soundscape's distribution and music operations capabilities inside the AI tools they already use:

- **Release preparation**: works out what a release still needs and fills the gaps through conversation
- **Release submission**: once the data is complete, the musician confirms and submits; every release still goes through Soundscape's standard review before delivery to platforms
- **Distribution and marketing knowledge**: answers distribution and marketing questions based on Soundscape's official public documentation
- **Platform performance data**: query and compare streaming data by song, platform, region, or period, with the data source and last update shown

Royalty settlement features are scheduled to roll out from Q1 2027.

## Who can use ALICE

Access is by application. Soundscape members with a signed distribution agreement can apply and are activated after review:

## Install (desktop apps)

1. Open the ChatGPT or Claude desktop app
2. Go to the plugin marketplace and search for "ALICE by Soundscape"
3. Sign in with your Soundscape account and approve access
4. Restart the app or start a new chat, and you're ready to go

## Install (command line)

```
# Claude Code
/plugin marketplace add Soundscape-KKFARM/ALICE
/plugin install alice@soundscape-net

# Codex
codex plugin marketplace add Soundscape-KKFARM/ALICE
codex plugin add alice@soundscape-net
```

- **Claude Code**: open `/mcp`, select ALICE, then sign in and approve access in your browser
- **Codex**: check the server name in `/mcp`, run `codex mcp login <server-name>`, then sign in and approve access in your browser

If you previously set an access token manually, remove it before signing in with OAuth.

## Other MCP-compatible AI tools

Add the remote MCP server `https://rise.soundscape.net/mcp` and sign in to your Soundscape account with OAuth.

## Privacy

ALICE is provided by Soundscape (KKFARM Co., Ltd.). After you approve access, your AI tool uses an OAuth access token to query your Soundscape account, release, and analytics data. Your conversations are processed by the AI service you choose and are subject to its data policy.

[Privacy Policy](https://soundscape.net/privacy-policy)

## What's open source

This repository is open source under the Apache 2.0 license and contains the MCP plugin configuration and Skills (soundscape-alice, help-me). Distribution, analytics, and knowledge services run on Soundscape's cloud; this repository contains no customer data.

## License

[Apache-2.0](plugins/alice/LICENSE)
