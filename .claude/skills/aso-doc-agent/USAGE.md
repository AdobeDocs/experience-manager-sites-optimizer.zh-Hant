---
source-git-commit: ed1960cc0364dc4169a454a4860b7463890e3b74
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 0%

---
# ASO檔案代理程式 — 使用方式

內容、運作方式，以及需要您時該做什麼。

## 作用

此代理程式每天都會從以下專案挑選最高優先順序的未記錄ASO功能：
[網站 — 49539](https://jira.corp.adobe.com/browse/SITES-49539)的待處理專案(39張票證，例如
&quot;Canonical opportunity how-to&quot;、&quot;Slack notifications&quot;)，撰寫一段檔案
PR — 指派兩者中的任一者
已設定的檢閱者(`sandsinh_adobe` / `kanishka_adobe`)目前開啟的檢閱者較少
檢閱來自此代理程式的請求。 如果功能需要熒幕擷圖或影片，則會要求
請在完成PR前在Slack上操作。

每次執行也會檢查每個開啟PR的稽核狀態：核准的PR會被合併
立即，而且會讀取變更要求的意見反應，當它是可泛化的
課程（不是一次性的錯字），如此一來，未來的草稿就不會重複相同的錯誤。

單次執行=一次功能=最多一個PR。 每次執行不會涉及超過一個票證，
且一次不會開啟超過3個PR （會等待現有規則先合併/關閉）。

## 生活的一切

| 什麼 | 路徑 |
|---|---|
| 它如何決定要做什麼 | `.claude/skills/aso-doc-agent/SKILL.md` |
| 確切的逐步說明 | `.claude/skills/aso-doc-agent/references/pipeline.md` |
| 團隊特定設定（編輯此項以變更稽核者、上限、向上呈報時間） | `.claude/skills/aso-doc-agent/config.yml` |
| 從PR稽核意見回饋中學到的課程（在Git中追蹤，在每個草稿前閱讀） | `.claude/skills/aso-doc-agent/references/review-learnings.md` |
| 本機執行狀態（已授權 — 可安全刪除，將會重建） | `.claude/skills/aso-doc-agent/state/` |
| 每日排程安裝程式 | `.claude/scripts/aso-doc-agent-setup.sh` |
| Headless執行的許可權允許清單 | `.claude/settings.local.json` （已授權，機器本機） |

## 正在執行

- **手動，在正常工作階段中：** `/aso-doc-agent` （或`/aso-doc-agent --ticket SITES-XXXXX`）
- **Headless，一次性：** `claude -p "/aso-doc-agent"` （來自存放庫根目錄）
- **每日，自動的：**&#x200B;已透過`launchctl`安裝（請參閱下文） — 每天當地時間07:53執行，不需要採取任何動作

### 安裝/變更每日排程

```bash
bash .claude/scripts/aso-doc-agent-setup.sh
```

安裝`launchd`工作(`~/Library/LaunchAgents/com.sandsinh.aso-doc-agent.plist`)
每天從這個存放庫執行`claude -p "/aso-doc-agent"`。 您隨時可以重新執行指令碼
編輯其內的排程（預設值：07:53本機）。 這只有在您的電腦處於以下狀態時才有效
此時開啟並喚醒 — launchd不會回溯執行遺漏的工作，但會執行
正常排定的下一個時間。

```bash
launchctl list | grep com.sandsinh.aso-doc-agent   # confirm it's loaded
launchctl start com.sandsinh.aso-doc-agent         # trigger a run right now, don't wait for 07:53
launchctl unload ~/Library/LaunchAgents/com.sandsinh.aso-doc-agent.plist  # stop it
```

中每個排定執行地段的記錄 `.claude/skills/aso-doc-agent/state/launchd.out.log`
和`launchd.err.log`。

## 系統會要求您做什麼

- **來自代理程式的Slack DM** （以您的身分傳送給您 — 先傳送沙心，接著再傳送卡尼什卡）
escalation)要求熒幕擷圖或影片，其中包含確切的擷取步驟和要擷取的URL
use. **在連結的Jira票證上回覆，而不是在Slack中**：直接附加熒幕擷圖，
如果是視訊，請透過一般的Experience League視訊表單將其上傳
（`experience-league-video-upload`技能）並貼上結果 `video.tv.adobe.com`
連結為Jira註解。 下次執行會自動擷取它。
- 如果沒有人在&#x200B;**5天**&#x200B;內回應，則請求會從沙新升級至卡尼什卡
自動。 在&#x200B;**10天**&#x200B;之後，代理程式沒有回應，就會送出檔案
不含媒體，並新增內嵌附註。 沒有以逾時為基礎的自動合併 — PR
仍會等待實際的人類評論，無論這可能需要多久。
- **要檢閱的PR** — 指派給你們中較少代理程式開啟的PR
目前正在等待檢閱。 草稿PR表示媒體仍在擱置中；它們翻轉到
資產顯示後會自動可供檢閱。 核准，代理程式合併
下次執行 — 不需要您另外執行合併步驟。
- **如果您要求變更**，代理程式會在下次執行時讀取您的註解。 可泛化
回饋意見（不是錯字/連結修正）會寫入`references/review-learnings.md`，所以
相同的更正不需要在未來的PR上重複。

## 調整行為

編輯`.claude/skills/aso-doc-agent/config.yml` (在Git中追蹤 — 變更影響每個
未來在此電腦上執行，或複製存放庫的其他人)：

- `pr.max_open` — 在代理程式暫停挑選新票證前開啟的PR數目（預設為3）
- `pr.stale_after_hours` — `CHANGES_REQUESTED` PR在停止計入`pr.max_open`之前，可以坐多久（預設為336 = 14天）；它保持開啟狀態，這只會解除封鎖新的選擇
- `github.reviewers` — 指派對象，以及取得何種平衡
- `media.contacts_in_order` / `escalate_after_hours` （預設值120 = 5天） / `give_up_after_hours` （預設值240 = 10天） — 詢問對象的順序、耐心程度；兩者都是從原始請求中測量，因此向上呈報並不會推後放棄日期
- `pr.check_reviews_every_run` — 關閉檢閱檢查步驟（不建議使用；這是合併和學習的方式）

## 如果它在許可權提示時停頓

Headless (`claude -p`， launchd)執行沒有要提示的終端機 — 未列出的工具呼叫
只會失敗而非擱置。 如果執行的記錄檔顯示命令的許可權遭拒
管道的正當需求，請將其新增至中的`permissions.allow`清單
`.claude/settings.local.json` (未在Git中追蹤 — 機器本機；每個開發人員執行
此代理程式需要有其專屬的復本（含其專屬範圍的允許清單）。

## 如果進度完全停止

請依序勾選：
1. `gh pr list --repo Adobe-Enterprise-Docs/experience-manager-sites-optimizer.en --label aso-doc-agent --state open` — 如果此項顯示3，表示它正在等待稽核，而不是停滯。
2. Jira：在SITES-49539下是否還有尚未`aso-doc-agent-picked`的合格`New`票證？ 唯有在分支和PR存在時，才會套用標籤(pipeline.md Step 6.10)，因此當機的執行不應留下已標籤但未發佈的票證 — 如果您仍然找到票證（例如手動新增標籤），請手動移除該標籤，使票證再次合格。
3. `.claude/skills/aso-doc-agent/state/launchd.err.log`最近一次執行的錯誤。
4. 如果執行的摘要顯示「重大待處理專案已完全涵蓋」或「此處無工作可做」，但您知道應有符合條件的工作，請將其視為可疑專案 — 這些訊息會保留給真正空白的結果。 實際的Jira/GitHub/Slack錯誤會單獨記錄，並應在`launchd.err.log`中顯示為自己的行，而不是隱藏在這些訊息之一後面。
