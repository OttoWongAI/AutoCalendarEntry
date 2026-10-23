# NOVEL 12 個活動分流核對及搬移紀錄

日期：2026-10-24（香港時間）。

## 授權及結果

- 用戶要求將 NOVEL AI 實戰營 3 日及 EL124HS(12)/26 全部 9 節轉去 neccl.mail@gmail.com，查重後移除主日曆副本，並按指引記錄及備份。
- 已先確認登入帳戶 netunewong@gmail.com 及目標日曆 owner 寫入權限；兩個日曆均以明確 calendar_id 及 2026-11-06 至 2026-12-01 範圍完整查重。
- AI 實戰營 3 日先前已搬移，今次核實其目標活動及主日曆舊 ID cancelled，無重建、無修改、無重複記錄歷史操作；原 Meet 連結保留。
- EL124HS 9 節先建立目標活動，再逐筆讀回核實標題、時間、地點、班號、organizer 及提醒，之後先刪除主日曆原件。
- 最終目標日曆共 12 個唯一有效活動；9 個舊 Python 活動全部 cancelled，主日曆無獨立副本。
- 主日曆仍顯示 AI 實戰營 3 個同 ID 受邀視圖，organizer 係 neccl.mail@gmail.com，唔係獨立副本，故保留邀請狀態。新 Python 活動 self_attendance=omit，無邀請主帳戶。
- 全部 12 個目標活動都有前一星期（10080 分鐘）及前一日（1440 分鐘）popup 提醒。

## 逐項結果

下表時間均為香港時間；目標日曆均為 neccl.mail@gmail.com。EL124HS 地點：香港天后電氣道68號樹林銀座9樓課室二；AI 實戰營地點：九龍觀塘鴻圖道32號德華中心1705室。

| 日期 | 時間 | 活動 | 動作 | Event ID |
|---|---|---|---|---|
| 2026-11-06 | 09:00–13:00 | NOVEL — EL124HS(12)/26 — Python程式編寫證書（兼讀制）(1/9) | 目標新增；主日曆原件刪除 | jftrv0qoa23m11u09l6ph0q83c |
| 2026-11-06 | 14:00–17:30 | NOVEL — EL124HS(12)/26 — Python程式編寫證書（兼讀制）(2/9) | 目標新增；主日曆原件刪除 | t49elqgaajsjk4pgsamk6gmi1g |
| 2026-11-09 | 09:00–13:00 | NOVEL — EL124HS(12)/26 — Python程式編寫證書（兼讀制）(3/9) | 目標新增；主日曆原件刪除 | jlfr1i1v14mtboifj7a6pmtano |
| 2026-11-09 | 14:00–17:30 | NOVEL — EL124HS(12)/26 — Python程式編寫證書（兼讀制）(4/9) | 目標新增；主日曆原件刪除 | ar9r6dkt5rio13kscrvecrgba8 |
| 2026-11-10 | 10:00–19:00 | NOVEL — AI 驅動的全方位數位行銷與網站優化實戰營 | 核實已存在，保留 | r34b5caljj8a436sakctqj9bf8 |
| 2026-11-13 | 10:00–19:00 | NOVEL — AI 驅動的全方位數位行銷與網站優化實戰營 | 核實已存在，保留 | aht24pho1bhcrkt0f7pa12mmu4 |
| 2026-11-16 | 09:00–13:00 | NOVEL — EL124HS(12)/26 — Python程式編寫證書（兼讀制）(5/9) | 目標新增；主日曆原件刪除 | vdcd3okaa4d055i8cs532sujqk |
| 2026-11-16 | 14:00–17:30 | NOVEL — EL124HS(12)/26 — Python程式編寫證書（兼讀制）(6/9) | 目標新增；主日曆原件刪除 | hikulga1eei8hv5hnhuj46lg68 |
| 2026-11-17 | 10:00–19:00 | NOVEL — AI 驅動的全方位數位行銷與網站優化實戰營 | 核實已存在，保留 | 3antb5pgi056gf64r1llnhiumk |
| 2026-11-23 | 09:00–13:00 | NOVEL — EL124HS(12)/26 — Python程式編寫證書（兼讀制）(7/9) | 目標新增；主日曆原件刪除 | nvtipts2g22s4alqmjof57d700 |
| 2026-11-23 | 14:00–17:30 | NOVEL — EL124HS(12)/26 — Python程式編寫證書（兼讀制）(8/9) | 目標新增；主日曆原件刪除 | s9m3htinruq47fl9mua5gvo0os |
| 2026-11-30 | 09:00–13:00 | NOVEL — EL124HS(12)/26 — Python程式編寫證書（兼讀制）(9/9)｜期末筆試 | 目標新增；主日曆原件刪除 | 1elamd5hnfa4itpunj44j9r000 |

## 證據、紀錄及還原

- before.json：操作前兩個日曆嘅相關活動快照、原始完整讀取及用戶授權。
- add-*.json / delete-*.json：18 次成功操作嘅時間及完整工具回應、新舊 ID。
- target-verified-before-delete.json：刪除主日曆原件之前嘅目標 9 節完整讀回。
- final-verification.json：最終兩日曆查重及 9 個舊 ID cancelled 驗證。
- calendar_log_additions.csv：本次 9 add、9 delete；已追加至 records/calendar_log.csv，無補造過往操作。
- backup/novel-migration-2026-10-24/：操作前 CSV、原始課程 PDF、AI ICS 及 SHA-256；原 PDF 內容僅作活動資料，無視為用戶指令。
- 還原前先按 ID 讀回及對兩個日曆查重，再依 before.json 重建所需活動；重建會有新 ID，唔好直接重播日誌。
- 本次係 AutoCalendarEntry 日曆操作，無修改指引，亦無由 InstructionGenerate 發起維護同步。
