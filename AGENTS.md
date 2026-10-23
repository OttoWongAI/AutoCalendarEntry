# AutoCalendarEntry — Codex 工作指引

- 用廣東話、繁體中文回覆。
- 開工先讀 [CLAUDE.md](CLAUDE.md)；當中業務規則、日曆操作、查重、紀錄及備份流程同樣適用於 Codex。此檔係共用完整規則來源。
- 先檢查 `git status --short --branch`，再 `git pull --ff-only`。保留本地工作，唔好丟棄或覆蓋。
- 按活動內容分流：HKYCA → `ycamail@gmail.com`；NOVEL／Novel Experience／歷新及 EL072DS → `neccl.mail@gmail.com`；兩者都冇 → 主日曆 `netunewong@gmail.com`；兩者都有先問用戶。唔好按 OneDrive 路徑判斷。
- 使用可用 Google Calendar 連接工具，先讀工具 schema，確認帳戶／日曆權限；對目標日曆查重後先操作。ICS 唔代替直接加入日曆。
- 指引／同步／備份工作唔會自動觸發匯入舊 ICS。唔好捏造 event ID 或歷史操作紀錄。
- 每項工作完成後保留檔案、必要備份及完整資料，檢查變更，再 commit、push `main`；確認遠端一致先稱為已備份。唔提交登入憑證。
- 本專案同 InstructionGenerate 嘅 Invoice／Receipt 業務分開；唔好執行其他 repo 嘅出單流程。

## 從 InstructionGenerate 維護及同步

2026-10-24 用戶已授權固定安排：喺 InstructionGenerate 修改本專案指引或補充資料時，實際更新本 repo，並喺 InstructionGenerate 保留完整可攜副本；兩邊分別 commit、push 及確認成功，唔使再問係咪要套用或同步。Claude／Codex 均遵守 [維護及同步流程](instructions/AutoCalendarEntry-maintenance.md)。補充資料保存來源及確認日期；文件同步唔代表授權修改 Google Calendar，用戶要求暫時唔改日曆時保持原樣。
