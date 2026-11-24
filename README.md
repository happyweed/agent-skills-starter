# agent-skills-starter

供 Claude Code 與 Codex 共用的專案模板。包含 38 個技能、從構想到交付的工作流程、文件範本，以及 Git 和代理程式的防護 hooks。可用來製作網站、應用程式、工具、自動化流程，也能用於既有專案的功能變更。

## 開始使用

1. 在 GitHub 選 **Use this template** 建立新倉庫，或 clone 一份來調整。Windows 請先看[符號連結設定](01-SETUP.md#windows)。
2. 用 VS Code 開啟包含 `.git` 的專案根目錄，依 [環境設定](01-SETUP.md) 啟用 Git hooks。
3. 將 [AGENTS.md](AGENTS.md) 的佔位符換成專案目的、規格位置、執行方式與限制。需要設定議題追蹤或領域文件時，在 Claude Code 輸入 `/setup-skills`，或在 Codex 輸入 `$setup-skills`。
4. 從[工作流程](02-WORKFLOW.md) 選擇當前階段。不確定該用哪個技能時，在 Claude Code 輸入 `/compass`，或在 Codex 輸入 `$compass`。

## 可自訂的內容

| 位置 | 用途 |
|---|---|
| [AGENTS.md](AGENTS.md) | 專案目的、規格來源、技術限制與驗證指令。`CLAUDE.md` 匯入這份規則。 |
| [02-WORKFLOW.md](02-WORKFLOW.md) | 依工作規模選擇步驟，並查找各階段輸入、產出與驗收條件。 |
| [prompts/](prompts/) | 可複製到聊天框的階段提示詞。 |
| [templates/](templates/00-README.md) | 需求、設計、測試、追溯與經驗紀錄範本。 |
| [.claude/skills/](.claude/skills/README.md) | 技能來源及維護方式。`.agents/skills` 連到同一份來源，供 Codex 使用。 |
| [.githooks/](.githooks/README.md) | Git 提交與推送檢查。Claude Code 和 Codex 的代理程式 hooks 另由各自的設定檔登記。 |

調整技能後，依[環境設定](01-SETUP.md#驗證模板)執行 `bash scripts/check.sh`。來源與授權見 [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md)。
