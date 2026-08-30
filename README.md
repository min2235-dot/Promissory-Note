# Promissory Note

這個 repo 目前有兩部分：

- `index.html`：本票產生器網頁工具（用 pdf-lib 產生本票 PDF）。
- `.claude/skills/bznk-whitelist-check/`：BZNK 新送審案件「白名單快速通道」
  判定的 Claude Skill。

## bznk-whitelist-check skill

判斷 BZNK 新送審案件（票貼/客票融資、應收帳款融資）是否可以走白名單快速
通道，取代逐案人工翻歷史資料。使用者只要打出借款人姓名/公司名稱，技能會
自動跑完歷史信用、目前曝險、金額異常、第三方監控燈號四個維度，並給出
🟢快速通道／🟡人工覆核／🔴完整審查三級結論。細節見
[`SKILL.md`](.claude/skills/bznk-whitelist-check/SKILL.md)。

### 搭配 Claude Code + Google Drive 使用

1. 在 Claude Code 中把這個 GitHub repo 設為專案來源，這樣 `.claude/skills/`
   底下的技能會自動載入，不用每次手動貼 SKILL.md。
2. 連接 Google Drive connector 後，技能會多一步比對：搜尋 Drive 上的
   內部黑名單/風控名單試算表，命中就直接判定 🔴（見 SKILL.md 步驟 8）。
   沒連接 Google Drive 或找不到檔案時，技能仍會照原本四維度流程正常運作。

### 更新流程

技能內容若有調整，直接修改
`.claude/skills/bznk-whitelist-check/SKILL.md`，commit 後 push 回這個
repo 的分支，讓其他人與之後的 Claude Code session 都能抓到最新版本。
