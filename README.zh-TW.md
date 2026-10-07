# ALICE by Soundscape

[English](README.md) | 繁體中文

**Artist Lifecycle Intelligence & Coordination Engine**

ALICE 是 Soundscape 的開源 MCP 套件，讓音樂人在自己慣用的 AI 中，使用 Soundscape 的發行與營運能力：

- **發行前資料協助**：建立發行草稿、上傳音檔與封面，透過 Soundscape 的發行檢查找出缺漏，在對話中逐項補齊
- **上架送件**：資料齊備後依你的要求送出；和在會員後臺上架一樣，作品須經 Soundscape 人員審核後才會送交各平臺
- **發行與行銷知識庫**：以 Soundscape 官方客服中心的公開說明為依據，回答發行與行銷問題
- **平臺營運數據**：依歌曲、藝人、平臺或期間查詢與比較播放數據；資料可用性依平臺與期間而異，分析結果不能取代最終收益報表

收益結算相關功能規劃自 2027 年第一季起逐步開放。

## 使用資格

目前採申請制，已簽約的 Soundscape 正式會員可提出申請。詳情請見 [soundscape.net](https://soundscape.net/)。

## 安裝（一般使用者）

1. Claude 電腦版 App：在外掛市集搜尋「ALICE by Soundscape」並安裝
2. ChatGPT 電腦版 App：在外掛市集搜尋「ALICE by Soundscape」並安裝
3. 依畫面指示登入 Soundscape 帳號，並同意授權
4. 重新開啟 App 或開一個新對話，就可以開始使用

## 安裝（命令列）

```
# Claude Code
/plugin marketplace add Soundscape-KKFARM/ALICE
/plugin install alice@soundscape-net

# Codex
codex plugin marketplace add Soundscape-KKFARM/ALICE
codex plugin add alice@soundscape-net
```

- **Claude Code**：開啟 `/mcp`，選擇 ALICE，於瀏覽器登入並同意授權
- **Codex**：在 `/mcp` 確認伺服器名稱，執行 `codex mcp login <server-name>`，於瀏覽器登入並同意授權

若先前曾手動設定過存取權杖，請先移除，再透過 OAuth 登入。

## 其他支援 MCP 的 AI 工具

新增遠端 MCP 伺服器 `https://rise.soundscape.net/mcp`，並以 OAuth 登入 Soundscape 帳號。

## 隱私權

ALICE 由 Soundscape（科科農場股份有限公司）提供。同意授權後，你使用的 AI 工具會透過 OAuth 查詢你的 Soundscape 帳號、發行與數據資料，並在你的權限內執行你要求且工具支援的修改；對話內容由你選用的 AI 服務處理，適用該服務的資料政策。請讓 AI 工具自行管理存取權杖，不要貼到對話或檔案中。

[隱私權政策](https://soundscape.net/privacy-policy)

## 開源內容

本 repo 以 Apache 2.0 授權開源，包含 MCP 外掛設定與 Skill 套件（[soundscape-alice](plugins/alice/skills/soundscape-alice/SKILL.md)、[help-me](plugins/alice/skills/help-me/SKILL.md)）。發行與數據服務由 Soundscape 提供，公開流程指引來自官方客服中心；本 repo 不含任何客戶資料。

## 授權

[Apache-2.0](plugins/alice/LICENSE)
