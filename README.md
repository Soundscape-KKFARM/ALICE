# ALICE by Soundscape

English | [繁體中文](README.zh-TW.md)

**Artist Lifecycle Intelligence & Coordination Engine**

ALICE is Soundscape's open-source MCP package. It lets musicians use Soundscape's distribution and music operations capabilities inside the AI tools they already use:

- **Release preparation**: create a release draft, upload audio and artwork, and use Soundscape's release check to find what's missing, then fill the gaps through conversation
- **Release submission**: submit once everything is ready; just like releases submitted through the member dashboard, every release is reviewed by Soundscape staff before it is delivered to platforms
- **Distribution and marketing knowledge**: answers distribution and marketing questions based on the public articles in Soundscape's official help center
- **Platform performance data**: query and compare streaming data by song, artist, platform, or period; data updates as often as each platform reports it and is kept separate from final royalty statements

Royalty settlement features are planned to roll out from Q1 2027.

## Who can use ALICE

ALICE is in invitation-only testing. Through the end of 2026, it is available to journalist demo accounts and invited Soundscape clients; there is no public application. From Q1 2027, ALICE will gradually open to all Soundscape members who have signed a distribution agreement.

Anyone can install the plugin, but accounts that haven't been invited can't complete sign-in for now. Not a Soundscape member yet? Sign up for free and sign the agreement online at [soundscape.net](https://soundscape.net/).

## Install (desktop apps)

1. Claude desktop app: open Settings → Plugins, search for "ALICE by Soundscape," and install it
2. ChatGPT desktop app: search the plugin marketplace for "ALICE by Soundscape" and install it
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

ALICE is provided by Soundscape (KKFARM CO., LTD.). After you approve access, your AI tool uses an OAuth access token to query and work with your Soundscape account, release, and analytics data. Your conversations are processed by the AI service you choose and are subject to its data policy. Let your AI tool manage the access token; never paste it into a chat or a file. You can revoke access at any time.

[Privacy Policy](https://soundscape.net/privacy-policy)

## What's open source

This repository is open source under the Apache 2.0 license and contains the MCP plugin configuration and the Skill packages (soundscape-alice, help-me). Distribution, analytics, and knowledge services run on Soundscape's cloud; this repository contains no customer data.

## License

[Apache-2.0](plugins/alice/LICENSE)
