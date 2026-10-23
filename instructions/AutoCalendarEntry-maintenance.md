# AutoCalendarEntry 指引及補充資料維護與同步

## 已授權固定安排

用戶於 2026-10-24 授權：之後喺 InstructionGenerate 修改 AutoCalendarEntry 指引或補充資料，都要實際同步返 AutoCalendarEntry，並喺 InstructionGenerate 保留可攜副本；兩個 repo 分別 commit、push 並確認成功，唔使重複問係咪要套用、同步或備份。只喺對話提供文字，或者只改 InstructionGenerate，唔算完成。

適用範圍包括業務指引、Claude／Codex 入口、日曆分流、活動／導師補充、撞期分析、用戶確認、來源資料及相關紀錄。補充事實要保留來源與確認日期，並同分析／待確認事項分開記錄。

## 專案與副本

| 用途 | 位置 |
|---|---|
| 維護及備份 repo | https://github.com/OttoWongAI/InstructionGenerate |
| 目標運作 repo | https://github.com/OttoWongAI/AutoCalendarEntry |
| 本機目標位置 | `/Volumes/Novel_BrownFung/AutoCalendarEntry` |
| 目標業務指引 | `CLAUDE.md`，Codex 由 `AGENTS.md` 引用 |
| 目標資料／分析 | `records/` 下相關活動或核對目錄 |
| InstructionGenerate 現行指引副本 | `instructions/AutoCalendarEntry.md` |
| InstructionGenerate 目標檔案副本 | `output/AutoCalendarEntry-setup/`，依目標相對路徑保存 |

其他環境可用不同路徑；以 Git remote 確認身份。冇本機 checkout 就 clone 目標 repo，唔好只記本機絕對路徑。既有日期備份保留作歷史版本，唔用舊快照覆蓋較新規則。

## 每次工作流程

1. 兩邊先 `git status --short --branch`，再 `git pull --ff-only`；讀取各自 AGENTS.md、CLAUDE.md 及相關紀錄。保留未提交改動，唔強制覆蓋或丟棄用戶工作。
2. 比對目標最新指引／資料同本 repo 副本。按用戶要求實際修改 AutoCalendarEntry；按需要同步入口文件、README、相關資料及引用。唔將一次性導師事實硬寫成所有活動通用規則。
3. 原日曆快照保持原樣；用戶補充另存來源與日期，再更新分析。只記錄已確認成功嘅日曆操作，唔因文件同步而補造 event ID 或操作 log。
4. InstructionGenerate 保留本次完整相關檔案，唔只留摘要或絕對路徑。目標現行 CLAUDE.md 複製到 `instructions/AutoCalendarEntry.md`；新增／更新嘅目標檔案依相對路徑保存於 `output/AutoCalendarEntry-setup/`。已有本 repo 資料副本亦按需要更新，避免同一份現行分析互相矛盾。
5. 檢查 diff、來源、引用路徑、兩邊副本內容一致性，執行 `git diff --check`。唔提交登入憑證；快取／暫存檔除外。必要大檔案超過 GitHub 限制時採用合適方式並記錄取用／還原方法。
6. 先將目標相關成果 commit、push main，確認本機 HEAD 同遠端 main 一致。在 InstructionGenerate 記錄目標 commit、用途及還原方式，再將本 repo 相關成果 commit、push，確認遠端一致。保留兩邊其他未提交工作；如有其他工作，唔要求為咗目錄乾淨而丟棄佢哋。
7. 回報兩邊備份結果。只有兩邊 push 都成功先稱全部已備份；任何一邊失敗，保留本地成果，清楚交代未完成位置及原因。

## 日曆操作界線

呢個係收到修改要求時執行嘅維護流程，唔係背景同步服務。文件／補充資料嘅同步授權唔等於要求修改 Google Calendar。用戶講「暫時唔好改日曆」時，繼續同步文件及 Git 備份，日曆保持原樣，直至用戶明確授權改動。日曆業務分流及操作仍按目標 CLAUDE.md 執行。

若本次只改 InstructionGenerate 自身維護安排，而目標指引及資料完全冇變，可只提交本 repo，唔建立目標空 commit；有目標相關變更就必須兩邊完成。
