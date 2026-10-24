# AutoCalendarEntry

由活動、課程、文件或圖片資料加入／更新 Google Calendar，供 Claude 同 Codex 共用。

## 日曆分流（2026-10-24 確認）

按資料內容判斷，唔按儲存路徑：

| 內容 | 日曆 |
|---|---|
| HKYCA | `ycamail@gmail.com` |
| NOVEL／Novel Experience／歷新（包括 Novel Invoice、EL072DS） | `neccl.mail@gmail.com` |
| 兩者都冇 | 主日曆 `netunewong@gmail.com` |
| 兩者都有 | 先問用戶 |

呢套分流取代舊版本「全部加入主日曆」偏好。預設香港時區及日／月／年；先查重；ICS 只作補充。報告時間衝突但唔阻擋明確要求新增，唔擅自改其他活動。

## 工作入口及同步

- Claude 讀 [CLAUDE.md](CLAUDE.md)；Codex 先讀 [AGENTS.md](AGENTS.md)，再讀共用完整規則 CLAUDE.md。
- 開工：`git status --short --branch`，然後 `git pull --ff-only`；保留未提交工作。
- 完成：檢查差異、commit，然後 `git push origin HEAD:main`，確認 push 成功及本機／遠端一致。
- 新環境：`git clone https://github.com/OttoWongAI/AutoCalendarEntry.git`，再設定 Google Calendar 連接。登入憑證唔儲存喺 repo。
- `records/calendar_log.csv` 保存已確認成功操作嘅 event ID 等紀錄；現存 ICS 唔代表已匯入日曆。
- 根目錄保留現有 ICS／圖片；[同步前備份](backup/pre-sync-2026-10-24/) 保留原本機所有檔案及 SHA-256 清單，包括舊 README。還原原檔可由該目錄複製；舊 README 只作歷史參考，唔係現行規則。
- 呢次同步只備份檔案同更新指引，冇執行日曆新增、修改或刪除。

## 從 InstructionGenerate 維護及同步

2026-10-24 用戶已授權固定安排：喺 InstructionGenerate 修改本專案指引或補充資料時，實際更新本 repo，並喺 InstructionGenerate 保留完整可攜副本；兩邊分別 commit、push 及確認成功，唔使再問係咪要套用或同步。Claude／Codex 均遵守 [維護及同步流程](instructions/AutoCalendarEntry-maintenance.md)。補充資料保存來源及確認日期；文件同步唔代表授權修改 Google Calendar，用戶要求暫時唔改日曆時保持原樣。

## 已確認報價活動資料

先到 CLAUDE.md 指定嘅 OneDrive `Novel_New` 資料夾查對應報價、確認版本、編號表及相關活動資料；搵唔到或唔清楚先問用戶。完整查找及核對規則見 [CLAUDE.md](CLAUDE.md)。

有 Quotation 嘅活動喺 InstructionGenerate 出 Invoice 時，按 CLAUDE.md 固定安排同步 NOVEL 日曆，先查重、記錄實際事件 ID；指引同步本身唔補入歷史活動。
