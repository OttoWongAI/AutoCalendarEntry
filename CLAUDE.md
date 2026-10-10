# AutoCalendarEntry — 自動加 / 改 Google Calendar

用戶俾 Claude 任何資料（相片、PDF、Word、Excel、文字、email 截圖……），
Claude 讀內容，自動將活動加入或者更新 Google Calendar，並將紀錄 backup 上 GitHub。

用戶用廣東話落指令，回覆都用廣東話（繁體中文）。

> 呢個 repo 同 `InstructionGenerate`（出 Invoice / Receipt）分開，唔好將兩邊嘅指引混埋。

---

## 0. 每次開工先做

1. `git pull`（攞最新指引 / 紀錄）。
2. Google Calendar connector 用 `netunewong@gmail.com` 登入，有權寫入第 2 節三個日曆。
   Local（Mac 嘅 Claude Desktop app）同雲端 session 都用得。

---

## 1. 自動做

- 用戶俾嘅資料入面有活動 / 會議 / 課堂嘅日期，就直接加入日曆，唔使等用戶講「加入日曆」。
- 資料係改動（改期、改時間、改地點、取消）：喺 `records/calendar_log.csv` 搵返嗰個 event 嘅 `event_id`，
  用 `update_event` 改（取消就 `delete_event`）。log 搵唔到就用 `list_events` 喺嗰個日曆搵同名 event。
- 以下情況停低問：日期 / 時間睇唔清、資料有矛盾、日期已經過咗、同時有 HKYCA 同 NOVEL、搵唔到要改嘅 event。
- 一份資料有幾個活動就逐個加。

---

## 2. 入邊個日曆

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
- **時間**：香港時間（`timeZone: Asia/Hong_Kong`）。有開始 / 完結時間就照填；只有日期或者「One Day」就開全日 event。
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

（`search_events` 只搜主日曆，查唔到另外兩個日曆，唔好靠佢查重。）

---

## 5. 紀錄同 backup

1. 每加 / 改 / 刪一個 event，喺 `records/calendar_log.csv` 加一行：
   `created,action,calendar_id,event_id,summary,start,end,location,source`
   - `action` = `add` / `update` / `delete`；`source` = 檔名、Invoice 編號或者「用戶訊息」。
2. 用戶俾嘅原始資料唔使放入 repo。
3. 做完即刻 commit + push **入 `main`**，唔使問用戶（用戶 2026-10-10 授權）：
   ```bash
   git add -A && git commit -m "Calendar: 活動名" && git push origin HEAD:main
   ```
   雲端 session 就算開喺 `claude/…` 分支，都係直接 push 入 `main`。push 失敗就話俾用戶知。
4. 改指引（呢個 `CLAUDE.md`）都一樣：改完直接 commit + push 入 `main`。

---

## 6. 回覆用戶

列出每個 event：動作（加 / 改 / 刪）、日曆、標題、日期時間、地點、提醒；有咩要問嘅就講清楚。
