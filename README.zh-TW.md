# ALICE

[English](./README.md) | 繁體中文

Artist Lifecycle Intelligence & Coordination Engine

ALICE 協助 Soundscape 創作者查詢帳號與組織資訊、查看即時分析資料，以及取得公開的操作指引。

## 安裝

```bash
# Claude Code
/plugin marketplace add Soundscape-KKFARM/ALICE
/plugin install alice@soundscape-net

# Codex
codex plugin marketplace add Soundscape-KKFARM/ALICE
codex plugin add alice@soundscape-net
```

## 連線至 Soundscape

插件已設定 `https://rise.soundscape.net/mcp`，使用 OAuth 連結帳號。

- **Claude Code**：開啟 `/mcp`，選擇 ALICE，再於瀏覽器登入並同意授權。
- **Codex**：在 `/mcp` 確認伺服器名稱，執行 `codex mcp login <server-name>`，再於瀏覽器登入並同意授權。
- **ChatGPT**：使用其支援的 OAuth 連線流程，連接上述 MCP URL。安裝本機插件不會連結 ChatGPT 帳號。

安裝或更新插件後，請開啟新的用戶端工作階段。如果先前為此伺服器設定了 bearer token 覆寫值，請先移除，再透過 OAuth 登入。

## 隱私權

ALICE 由 KKFARM 提供。同意授權後，用戶端會將 OAuth access token 傳送至 Soundscape 的 MCP 服務，以查詢帳號、組織和分析資料。請讓用戶端管理 Token，不要將 Token 貼入對話或插件檔案。

[隱私權政策](https://soundscape.net/privacy-policy)

## 授權

[Apache-2.0](./plugins/alice/LICENSE)
