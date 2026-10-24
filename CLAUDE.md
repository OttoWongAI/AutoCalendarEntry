# AutoCalendarEntry — 自動加 / 改 Google Calendar

用戶俾 Claude / Codex 任何資料（相片、PDF、Word、Excel、文字、email 截圖……），
Claude / Codex 讀內容，自動將活動加入或者更新 Google Calendar，並將紀錄 backup 上 GitHub。

用戶用廣東話落指令，回覆都用廣東話（繁體中文）。

> 呢個 repo 同 `InstructionGenerate`（出 Invoice / Receipt）分開，唔好將兩邊嘅指引混埋。

---

## 0. 每次開工先做

1. 先 `git status --short --branch`，再 `git pull --ff-only`（攞最新指引 / 紀錄）。保留未提交改動；遇到衝突先處理，唔好 reset、覆蓋或丟棄用戶工作。
2. Google Calendar connector 用 `netunewong@gmail.com` 登入，有權寫入第 2 節三個日曆。
   Claude / Codex 都按實際可用嘅 Google Calendar 連接工具操作；先確認登入帳戶及目標日曆寫入權限。工具不可用就清楚報告未完成，唔好只生成 ICS 當作已加入。

---

## 1. 自動做

- 用戶俾嘅資料入面有活動 / 會議 / 課堂嘅日期，就直接加入日曆，唔使等用戶講「加入日曆」。
- 資料係改動（改期、改時間、改地點、取消）：喺 `records/calendar_log.csv` 搵返嗰個 event 嘅 `event_id`，
  用 `update_event` 改（取消就 `delete_event`）。log 搵唔到就用 `list_events` 喺嗰個日曆搵同名 event。
- 以下情況停低問：日期 / 時間睇唔清、資料有矛盾、日期已經過咗、同時有 HKYCA 同 NOVEL、搵唔到要改嘅 event。
- 一份資料有幾個活動就逐個加。ICS 只係補充，唔可以代替直接加入 Google Calendar。
- 時段同其他活動有衝突就報告，但唔阻擋用戶明確要求嘅新增；唔好擅自改其他活動。
- 維護指引、Git 同步或備份本身唔代表要求匯入 repo 內既有 ICS／歷史資料；只喺用戶要求處理活動資料時執行。

---

### 已確認報價活動：先查 Novel_New 資料（2026-10-24 固定安排）

- 用戶提到已確認活動報價時，先自行到以下資料夾及其子目錄搵報價同相關活動資料，搵唔到或唔清楚先問用戶，唔要求用戶重打一遍已存在嘅資料：
  `/Users/brown_fung/Library/CloudStorage/OneDrive-HongKongYouthCounsellingAssociation/NEC_歷新體驗顧問有限公司/Administration/Account Form/Novel_New`
- 優先查 `Quotation-Novel/` 嘅對應報價文件、確認／簽署版本，以及 `-Quotation No. List.xlsx`；按報價編號、客戶／學校、活動名或日期交叉核對，必要時再讀相關 Invoice、時間表或其他來源。
- 由實際資料取回活動名、客戶、確認狀態、日期、起訖時間、地點、聯絡人及導師等適用欄位；未寫明就唔作。確認版本同其他版本有矛盾、多份可能配對、日期／時間／地點唔清楚，或者資料夾讀唔到，先問用戶需要釐清嘅項目。
- 記錄實際來源檔案及版本；保存本次使用嘅必要資料／可攜副本，唔批量搬走或修改 OneDrive 原檔，唔因查資料而更改財務 Excel。
- 呢條係資料查找規則；日曆仍按分流、查重及用戶當次授權處理。用戶要求暫時唔改日曆時，只查資料同更新文件紀錄。

---

### 有 Quotation 出 Invoice 同步 NOVEL 日曆（2026-10-25 用戶授權）

- 往後 InstructionGenerate 為有 Quotation 嘅活動出 Invoice 時，一併將活動加入 NOVEL 日曆 `neccl.mail@gmail.com`，唔使逐次再問係咪加入。
- 活動日期用實際服務日期，唔用 Invoice 發出日期。由確認報價、用戶更正及 Invoice 取回活動名、起訖時間、地點、聯絡人、Quotation / Invoice 編號及來源。
- 先查目標日曆及活動時間範圍；已有相同活動唔重複新增，資料有更新就更新對應事件，包括補上 Invoice 編號；唔改其他活動。撞期按既有規則報告。
- 有確實時間就用香港時間；只有日期或約數時長（例如 Around 6 hours）但冇開始時間，就按既有規則用全日事件，描述註明時間待確認，唔自行估開始時間。有必要資料缺漏、矛盾或活動日期已過則先問。
- 提醒、標題及地點處理沿用本指引。成功後保留 event ID、更新 calendar_log.csv 並備份；工具不可用或操作失敗清楚報告日曆未完成，唔當作 Invoice 未出或重複開單。
- 呢個係往後出單時嘅固定授權；今次更新指引本身唔觸發補入舊 Invoice / 舊活動，亦唔改 Invoice / Receipt Excel。

---

## 2. 入邊個日曆

2026-10-24 用戶確認：以本節分流為準，取代舊 README「全部主日曆」偏好；Claude 同 Codex 一律遵守。

睇資料**內容**決定（唔好睇 OneDrive 路徑，因為路徑本身有 `HongKongYouthCounsellingAssociation`）：

| 內容有 | 日曆 `calendarId` |
|---|---|
| `HKYCA` | `ycamail@gmail.com` |
| `NOVEL`（大細階都算，包括「Novel Experience」「歷新」；Novel 嘅 Invoice、EL072DS 一律係呢個） | `neccl.mail@gmail.com` |
| 兩樣都冇 | `netunewong@gmail.com` |
| 兩樣都有 | 停低問用戶 |

---

## 3. Event 內容

- **標題**：`活動名 – 客戶 / 機構`（例：`Sport Climb Loading Test 2026 – 葛量洪校友會黃埔學校`）。
- **時間**：預設香港時間（`timeZone: Asia/Hong_Kong`）及日／月／年；資料明確指定其他時區／日期格式就跟來源。有開始 / 完結時間就照填；只有日期或者「One Day」就開全日 event。
  多日活動：每日時間一樣就一個跨日 event；每日唔同就逐日一個。
- **地點**：活動地點；冇寫就用客戶地址，並喺描述註明「地點未確認，暫用客戶地址」。
- **描述**：客戶、聯絡人、電話、Quotation No.、Invoice No.（有就寫）、資料來源（檔名 / 用戶訊息）。
- **提醒**：`overrideReminders` = `[{"method":"popup","minutes":10080},{"method":"popup","minutes":1440}]`（前一星期 + 前一日）。

### EL072DS（ERB 歷奇活動助理基礎證書）

- 讀開班時間表 `EL072DS(班號) 地點 年.xlsx`，**逐堂**一個 event。
  Mac 上面喺：`/Users/brown_fung/Library/CloudStorage/OneDrive-HongKongYouthCounsellingAssociation/NEC_歷新體驗顧問有限公司/Administration/Account Form/Novel_New/EL072DS course admin stuff/EL072DS(班號)/`
  （雲端讀唔到就叫用戶直接俾個 xlsx）。
- 標題 `EL072DS-班號 第N堂：課題`；時間、場地跟時間表；描述寫導師（有就寫）。
- 全部入 `neccl.mail@gmail.com`。

---

## 4. 查重

加之前用 `list_events`（帶 `calendarId` 同嗰日嘅時間範圍）睇吓；已經有同名 / 同時間嘅 event：
- 內容一樣 → 唔好再加，回覆講明。
- 內容唔同 → 當係改動，照第 1 節更新。

查重工具必須明確指定目標 `calendarId` 及時間範圍；唔好假設搜尋結果涵蓋其他日曆。工具名稱／欄位因連接器而異，應先讀實際工具 schema，再用對應功能。

---

## 5. 紀錄同 backup

1. 每加 / 改 / 刪一個 event，喺 `records/calendar_log.csv` 加一行：
   `created,action,calendar_id,event_id,summary,start,end,location,source`
   - `action` = `add` / `update` / `delete`；`source` = 檔名、Invoice 編號或者「用戶訊息」。
2. 本 repo 現有 ICS、圖片、原始檔同必要產出都要保留並 backup 上 GitHub（2026-10-24 用戶授權）。唔好提交密碼、token、私鑰；快取／暫存檔唔使備份。改寫既有文件前保留必要原版，唔好只記本機絕對路徑。
3. 做完即刻 commit + push **入 `main`**，唔使問用戶（用戶 2026-10-10 授權）：
   ```bash
   git add -A && git commit -m "Calendar: 活動名" && git push origin HEAD:main
   ```
   雲端 session 就算開喺 `claude/…` 分支，都係直接 push 入 `main`。push 失敗就話俾用戶知。
4. 改指引（`CLAUDE.md`、`AGENTS.md`、`README.md`）都一樣：保持一致，檢查 diff 後 commit + push 入 `main`。完成後確認本機 HEAD 同遠端 main 一致、工作目錄乾淨；push 失敗要明講尚未備份。
5. 只記錄工具成功完成嘅日曆操作，保留回傳 event ID；未驗證嘅歷史 ICS 唔可以當成已匯入而補造 log。

---

## 6. 回覆用戶

列出每個 event：動作（加 / 改 / 刪）、日曆、標題、日期時間、地點、提醒；有咩要問嘅就講清楚。

## 從 InstructionGenerate 維護及同步

2026-10-24 用戶已授權固定安排：喺 InstructionGenerate 修改本專案指引或補充資料時，實際更新本 repo，並喺 InstructionGenerate 保留完整可攜副本；兩邊分別 commit、push 及確認成功，唔使再問係咪要套用或同步。Claude／Codex 均遵守 [維護及同步流程](instructions/AutoCalendarEntry-maintenance.md)。補充資料保存來源及確認日期；文件同步唔代表授權修改 Google Calendar，用戶要求暫時唔改日曆時保持原樣。
