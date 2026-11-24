# 專案環境設定

## 專案根目錄

在 VS Code 開啟包含 `.git`、`AGENTS.md` 和 `.githooks` 的資料夾。在終端機確認位置並啟用此倉庫的 Git hooks。代理程式的 Bash 防護 hook 也需能從執行環境找到 `jq`。

```bash
git rev-parse --show-toplevel
git config --local core.hooksPath .githooks
git config --local --get core.hooksPath
```

最後一行應回傳 `.githooks`。使用 Claude Code 或 Codex 的 VS Code 擴充套件，或從同一個根目錄啟動相應的 CLI。

## Windows

Codex 從 `.agents/skills` 讀取共用技能。這個路徑在 Git 內是一個相對符號連結，指向 `../.claude/skills`。先在 Windows 設定啟用「開發人員模式」，或使用具建立符號連結權限的終端機。

新 clone 時可為此次操作啟用連結，將下方的 URL 換成你的 Git 倉庫網址。

```powershell
git clone -c core.symlinks=true 'https://github.com/OWNER/REPOSITORY.git'
```

如果你已有工作副本，且 `.agents/skills` 是內容只有 `../.claude/skills` 的普通文字檔，請先確認它沒有自己的修改。從專案根目錄執行下列指令，只重建該路徑。

```powershell
git status --short -- .agents/skills
git config --local core.symlinks true
git checkout-index --force -- .agents/skills
Get-Item -Force .agents/skills | Select-Object LinkType, Target
Test-Path .agents/skills/compass/SKILL.md
```

第一行應無輸出。完成後應顯示 `SymbolicLink`，最後一行應回傳 `True`。若建立連結仍出現權限錯誤，先確認 Windows 已允許建立符號連結，再執行重建。

## 自訂專案

- 填寫 [AGENTS.md](AGENTS.md) 的專案目標、規格位置、安裝、執行與測試指令。技術、執行環境和部署方式由專案自己決定。
- 需要設定領域文件或發布規格、工作票時，執行 Claude Code 的 `/setup-skills` 或 Codex 的 `$setup-skills`。可選擇本機檔案、遠端議題追蹤器或團隊已有的流程。確認後，技能會將位置與操作方式寫進 `docs/agents/`。
- 依 [工作流程](02-WORKFLOW.md) 選擇當前階段，或者呼叫 `/compass`（Codex 用 `$compass`）。

## 驗證模板

檢查腳本使用 Git、Bash、Python 3（`python3` 或 `python`）及 `jq`。Windows 可在具備這些工具的 Bash 環境執行。

```bash
git --version
python3 --version  # Windows Git Bash 也可用 python --version
jq --version
bash scripts/check.sh
```

這組檢查涵蓋技能定義、路由、Claude Code／Codex 設定對應，以及 hooks 的回歸案例。缺少 `jq` 時，腳本會標記 hooks 測試已略過。
