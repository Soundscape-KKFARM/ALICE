# ALICE

[English](./README.md) | 繁體中文

Artist Lifecycle Intelligence & Coordination Engine

## 安裝

```bash
# Claude Code
/plugin marketplace add Soundscape-KKFARM/ALICE
/plugin install alice@soundscape-net

# Codex
codex plugin marketplace add Soundscape-KKFARM/ALICE
codex plugin add alice@soundscape-net
```

Claude Code 與 Codex 安裝同一個 `plugins/alice` 套件。

## MCP 設定

安裝前，請在啟動 Claude Code 或 Codex 的環境中，將 `SOUNDSCAPE_RISE_TOKEN` 設為 Soundscape 個人秘密 Token。請勿將 Token 放進對話、原始碼或可能被提交的設定檔。

安裝或更新插件後，請開啟新的工作階段，讓用戶端重新載入 MCP server 與 skills。ALICE 目前提供三個 MCP 工具：`me` 回傳帳號資料與可存取的組織；`tools` 列出六種分析操作、搜尋其名稱與說明，或以精確名稱取得輸入 schema；`query` 執行選定的分析操作。已知操作名稱與參數時，請直接呼叫 `query`。

`soundscape-alice` skill 會依需求選擇 MCP 工具。`help-me` skill 僅查閱 Soundscape 官方公開說明文件。

### 啟動 macOS App

透過 Claude 或 ChatGPT 使用本機執行環境時，請先以 `Cmd+Q` 完整結束 App，再從終端機設定 Token 並啟動。請將 `<token>` 替換為自己的個人秘密 Token，並保留引號：

```bash
# Claude
export SOUNDSCAPE_RISE_TOKEN='<token>' && open /Applications/Claude.app

# ChatGPT
export SOUNDSCAPE_RISE_TOKEN='<token>' && open /Applications/ChatGPT.app
```

macOS 的 `open` 會讓新啟動的 App 繼承終端機的環境變數（詳見 `man open`）。若 App 已在執行，`open` 通常會沿用既有程序；關閉視窗不會結束 App，也不會更新其環境變數。變更 Token 後，請完整結束並重新啟動 App。

這些指令會設定本機 App 的環境變數。網頁版或遠端執行環境需另行設定認證。MCP 連線仍取決於用戶端的執行模式與 Token 權限；詳見 [OpenAI MCP 文件](https://learn.chatgpt.com/docs/extend/mcp) 與 [Claude Code MCP 文件](https://code.claude.com/docs/en/mcp)。

## 隱私權

ALICE 由 KKFARM 提供，連線至 Soundscape 自家的 MCP 服務 `https://rise.soundscape.net/mcp`。透過 `SOUNDSCAPE_RISE_TOKEN` 提供的 Soundscape 個人秘密 Token，會放在 `Authorization` header 中傳送給該服務，用來驗證帳號、組織與分析查詢。

[隱私權政策](https://soundscape.net/privacy-policy)

## 授權

[Apache-2.0](./plugins/alice/LICENSE)
