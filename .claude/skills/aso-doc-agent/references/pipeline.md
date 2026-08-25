---
source-git-commit: ed1960cc0364dc4169a454a4860b7463890e3b74
workflow-type: tm+mt
source-wordcount: '2275'
ht-degree: 0%

---
# ASO檔案代理程式 — 管道

從`SKILL.md`引用。 這是執行順序的真實來源； SKILL.md為
摘要。 開始前先讀取`config.yml` — 下面`{braces}`中的每個值都是
設定金鑰。

**錯誤處理（套用至下列每個步驟）。** 發生錯誤（驗證）的工具/API呼叫
失敗、逾時、格式錯誤的查詢、非預期的結構描述)絕非與
合法的空白結果，且絕對不可允許無訊息墜入
「空白」或「無事可做」分支(例如步驟1.2的「這裡沒有事可做」、步驟3.3的
「epic待處理專案已完整涵蓋或全部在傳輸中」)。 當呼叫發生錯誤時，請停止並記錄
執行摘要中的實際錯誤，而不是繼續執行，就像它完全返回一樣。

## 步驟0 — 預檢

1. `pwd`和檢查`guidelines.md` + `.claude/skills/aso-doc-agent/config.yml`都存在。 如果沒有，請停止 — 錯誤的目錄。
2. `gh auth status` — 確認`sandsinh_adobe`帳戶在此主機上具有有效的Token。 **永遠不執行`gh auth switch`** — 這會反向整個機器上作用中的`gh`帳戶，造成副作用，因此可能會自動將這台機器上的任何其他終端機/處理程式串連到錯誤的帳戶上，造成每日自動執行。 相反地，此範圍僅會執行： `export GH_TOKEN=$(gh auth token --user sandsinh_adobe)`一次，因此以下每個`gh`呼叫都會透過`GH_TOKEN`環境變數使用該權杖，無論哪個帳戶是全域作用中。
3. 如果遺失，則為`mkdir -p {state_dir}`。
4. 讀取`{state_dir}/run-state.json` （如果存在） （否則視為`{"runs_completed": 0, "tracked_prs": []}`）。 `tracked_prs`是此代理程式針對其開啟的PR所擁有的`{number, headRefName, key}`清單 — 僅用於偵測未合併即關閉的PR （步驟1.5），因為只有`gh pr list --state open`在它消失後無法檢視。 媒體要求計時存在於另一個檔案中，`{state_dir}/media-requests.json` （步驟5） — GitHub和Jira仍為其他所有專案（PR狀態、票證狀態）的真實來源。
5. `--ticket KEY`出現 — >跳過步驟3的自動挑選，直接使用KEY （仍執行步驟4-7）。 否則在步驟3中自動撿料。

## 步驟1 — 協調先前執行

每次都執行此動作，即使是在封閉式執行或其他空的執行。

1. `gh pr list --repo {github.repo} --label {github.pr_label} --state open --json number,url,isDraft,headRefName,title,reviewDecision`
2. **檢閱檢查 — 每個開啟的PR、每個回合** (`pr.check_reviews_every_run`)：
   - `gh pr view <number> --repo {github.repo} --json reviewDecision,reviews,comments`
   - `reviewDecision == "APPROVED"` ->立即合併： `gh pr merge <number> --repo {github.repo} --merge`。 驗證合併是否實際著陸(`gh pr view <number> --json state,mergedAt` — `state == "MERGED"`)，再將其視為完成；即使呼叫`gh pr merge`，受保護分支拒絕或仍然擱置的必要檢查仍可讓PR開啟，且必須記錄為失敗，不會報告給Jira作為合併（這是一般的人類核准合併，不是以逾時為基礎的合併）。 在確認合併：在它合併的連結Jira票證上加上註解時，從`tracked_prs`刪除PR。
   - `reviewDecision == "CHANGES_REQUESTED"` -> **不**&#x200B;在此版本中自動修正PR。 閱讀稽核意見（`gh api repos/{github.repo}/pulls/<number>/comments`為內嵌意見，加上`reviews`欄位中的最上層稽核內文），然後執行下面的&#x200B;**學習意見反應**。 在執行摘要中將PR記錄為等待作者動作。 如果此PR已`CHANGES_REQUESTED`超過`pr.stale_after_hours`且沒有更新，請將它標示為Step 2 cap gate已過時 — 它對於人類保持開啟狀態，但不再佔用cap槽。
   - 其他任何專案（尚無評論，`REVIEW_REQUIRED`沒有已提交的評論） ->此處沒有任何要執行的動作。
3. **從意見反應中學習。** 對於讀為&#x200B;*可泛化的*&#x200B;語氣、結構或內容備註的每個評論評論或評論內文，不是該PR專屬的一次性修正（比較「永遠提及忽略支援的機會的Ignored索引標籤」與「第12行錯字」），將已日期、票證連結的專案附加至`references/review-learnings.md`。 略過純粹的機械式回饋（錯字、連結損壞、線條） — 修正PR本身中的回饋，這些回饋不需要耐用的課程。 該檔案中會記錄確切的登入格式。
4. 針對該清單中的每個&#x200B;**草稿** PR，從分支名稱(`{github.branch_prefix}<KEY>-...`)擷取Jira金鑰。
   - 該索引鍵上的`mcp__Corp-Jira__list_attachments` + `mcp__Corp-Jira__get_jira_comments`。
   - 尋找：符合要求之擷取的新影像附件，或包含`video.tv.adobe.com` URL的註解。
   - 如果找到： `git fetch`/`checkout`分支，請將影像新增至`help/**/assets/` （如果是影像附件，透過`download_attachment`下載）或填入`>[!VIDEO](...)`預留位置（如果是視訊URL註解）、針對`experience-league-markdown`驗證、認可、推播、`gh pr ready <number>`、PR註解「媒體已新增 — 準備好檢閱」。將`{state_dir}/media-requests.json`專案更新為`resolved`。
   - 如果未找到：檢查自`{state_dir}/media-requests.json`中的要求以來經過的時間。 在此處也套用步驟5的上報/放棄邏輯（在執行階段中保持開啟的PR草稿仍需要追蹤其媒體） — 包括放棄路徑的`gh pr ready`呼叫，因此放棄的草稿仍可檢閱，而不是停留在。
5. **偵測未合併而關閉的PR。** 將此回合的公開PR清單（步驟1）與來自`run-state.json`的`tracked_prs`進行比較。 任何從開啟清單中遺失且未在步驟2中確認合併的追蹤PR，都會關閉而不合併 — 在丟棄之前，擷取其最終狀態(`gh pr view <number> --repo {github.repo} --json reviews,comments`)並執行&#x200B;**最後一次從意見回饋中學習**，因此人類的拒絕推理不會遺失。 然後將其從追蹤中刪除。 票證本身不需要進一步的動作：由於宣告標籤僅在發佈時套用（步驟6.10），因此已關閉但未合併的票證已經沒有標籤，而步驟3.2的檢查（沒有開啟/合併的PR）使其當然有資格在未來執行時再次選取。
6. 將`run-state.json`中的`tracked_prs`設定為目前的open-PR清單（`number`、`headRefName`，以及從分支名稱剖析的Jira金鑰），以供下次執行的步驟5比較之用。

## 步驟2 — PR上限閘道

1. 從步驟1的`gh pr list`輸出計算開啟的PR，排除步驟1.2中標示為過時 — `CHANGES_REQUESTED` （開啟時間超過`pr.stale_after_hours`且沒有更新）的任何PR — 這些PR對人而言保持開啟狀態，但不再佔用Cap槽。
2. 如果count >= `{pr.max_open}` (3)：記錄`"cap reached ({count}/{pr.max_open} open) — skipping new ticket this run"`，跳至步驟7。
3. 否則請繼續步驟3。

## 步驟3 — 選擇票證

如果傳遞了`--ticket KEY`，則完全略過（使用KEY）。

```
JQL: "Epic Link" = {jira.epic} AND status = "{jira.open_status}"
     ORDER BY priority DESC, created ASC
```

1. 執行搜尋（`mcp__Corp-Jira__search_jira_issues`， `minimizeOutput: true`，欄位限製為`key,summary,priority,status,labels`）。
2. 依序逐步執行結果。 略過任何符合以下條件的票證：
   - 已有`{jira.picked_label}`標籤，或
   - 在遠端(`git ls-remote --heads origin '{github.branch_prefix}<KEY>-*'`)上已有分支`{github.branch_prefix}<KEY>-*`，或者
   - 已有開啟或合併的PR （對照步驟1的清單/ `gh pr list --state all --search <KEY>`進行交叉檢查）。
3. 通過所有三張支票的第一張票是選擇票。 如果因為搜尋確實傳回零個合格票證&#x200B;**，所以沒有傳遞**，請記錄`"epic backlog fully covered or all in flight"`並移至步驟7。 如果搜尋本身失敗（驗證錯誤、逾時、格式錯誤的JQL），則不是這種情況 — 改為記錄實際錯誤（請參閱上面的錯誤處理）。
4. 請&#x200B;**還不**&#x200B;標籤票證 — 宣告標籤只會在分支和PR實際存在時套用至步驟6.10。 步驟4-5 （研究/草稿/媒體）可能會失敗或當機，而不會在票證上留下任何痕跡；步驟6之前唯一進行中的訊號是上述分支存在/PR存在檢查，這足以讓此從沒有實際並行性的單一電腦執行以防範這種情況。

## 步驟4 — 研究+草稿

研究排在首位，而且是&#x200B;**多來源** — 永遠不要從單一輸入草稿(Jira
單獨（或只是閱讀同層級檔案）。 以下每個來源都會確認或
更正其他錯誤；信任原始程式碼> Wiki/PR檔案>即可解決衝突
Slack討論>檔案撰寫者自己的推斷（按該順序），並內嵌標幟
當無法解析時為`<!-- CONFIRM -->`。

&#x200B;0. **累積的評論課程。** 請先讀取`references/review-learnings.md`。 在起草之前套用其中與本票證主題相關的任何內容 — 這就是來自過去PR稽核的意見如何改善未來草稿，而不是重複相同的校正。

### 研究（一切適用 — 請勿直接跳至草圖）

1. **Source程式碼（其實際運作方式的基礎真相）。** 搜尋config.yml中的主要UI存放庫(`research.code_repos`)以取得功能的介面卡/處理常式(`*OpportunityAdapter.tsx`， `*SuggestionAdapter.tsx`)、其資料連結(`use*Data.ts`)及其`.l10n.ts`/`.I10n.ts`標題/說明字串。 這是欄位名稱、資料形狀、類別和確切產品副本的許可權 — 當來源不同時，會優先於其他內容。
2. **Wiki （設計意圖、規格、決定）。** `mcp__Adobe-Wiki__search_wiki_content`具有功能/機會名稱和epic/票證金鑰。 閱讀相符頁面(`get_wiki_content`)，以瞭解：功能存在的原因、產品團隊使用的術語、任何記錄的UX流程或邊緣案例，以及任何可建立真實UI外觀的內嵌熒幕擷取畫面（告知步驟5中的媒體擷取規格，除非頁面為最新狀態，否則不會取代實際的新鮮熒幕擷取畫面）。
3. **Slack （團隊實際談論它的方式、未完成的問題、最近的變更）。** `mcp__Slack__slack_search_messages`具有功能/機會名稱和票證金鑰，不受管道限制，除非`research.slack_channels`在config.yml中將其縮小。 尋找：公告訊息（通常具有乾淨的客戶專用框架）、設計討論對話串，以及任何指出功能最近已變更的內容，其同層級檔案或程式碼評論尚無法反映。
4. **GitHub PR歷程記錄（實作原理、熒幕擷取畫面、評論討論）。** `research.code_repos`中的`gh search prs --repo <repo> "<feature name>"`或`gh pr list --repo <repo> --search "<ticket key OR feature name>" --state all`。 閱讀合併的PR說明以了解理由、連結的設計檔案，以及闡明程式碼本身無法說明之行為的熒幕擷取畫面（例如，為何會封鎖修正型別、UI中的邊緣案例看起來是什麼樣子）。
5. **色調類比。** 根據票證摘要，尋找2-3個最近的現有頁面：
   - 「…… opportunity how-to」票證 — >在`help/documentation/opportunities/`中讀取2個同層級檔案（每個機會的實際操作位置 — `help/opportunity-types/*.md`是類別登入頁面，其卡片格線會連結至這些專案，而非操作內容本身）。
   - 設定/工作流程/連線票證 — >讀取`help/documentation/`中的1-2個同層級檔案（檢查`setup/`、`opportunities/`、`settings.md`、`basics.md`以取得最接近的相符專案）。
     映象標題結構、註解方塊使用方式、句子長度、技術細節層級。
6. **格式規則。** 在撰寫前重新閱讀`experience-league-markdown`技能的快速參考。 每個標題/附註/影像/連結都必須完全符合其語法。

### 草稿

&#x200B;7. **目標檔案決定。** 比起建立新檔案，偏好擴充現有頁面的相關區段，除非票證符合現有獨立頁面的詳細程度（例如，每個機會在`help/documentation/opportunities/`下取得自己的檔案 — 新機會會遵循現有同層級專案的確切結構）。 擴充現有頁面時，僅觸控此票證的單一區段 — 請勿編輯不相關的區段，即使這些區段看起來已過時亦然。 如果新的獨立頁面，也將其卡片新增到相關的`help/opportunity-types/*.md`登陸頁面（來源評論清單+產生的HTML區塊，符合現有卡片的確切模式）並在`help/main-toc/TOC.md`中註冊。
&#x200B;8. **草稿v1.** 立即寫入內容（在記憶體/草稿中，尚未寫入存放庫檔案 — 這會在媒體決策後的步驟6中發生，因此媒體擱置檔案與媒體解析檔案會透過相同的寫入路徑）。 綜合所有步驟1-6 — 不要只重述Jira票證說明。
&#x200B;9. **重複。** 針對步驟1-4的每個研究發現重新閱讀v1草稿：草稿是否遺漏了Slack或Wiki浮出水面的內容？ 這是否與原始程式碼的實際功能相矛盾？ 它是否儘可能符合約層級膚色？ 在繼續之前修訂 — 這是真正的第二次傳遞，不是形式。 在此傳遞後仍真正未確認的任何內容（在四個來源中找不到）會獲得內嵌`<!-- CONFIRM -->`註解，而非猜測。
&#x200B;10. **媒體決定。** 決定`mediaNeeded: true|false`。
    - `true`如果功能是多步驟UI工作流程，其中單獨文字說明將很難遵循（符合`guidelines.md`的「當文字說明不足時審慎使用」）。
    - 如果`true`，產生： `mediaType` （`screenshot`或`video`）、`captureSteps` （重現要擷取之狀態的確切步驟）、`urls` (客戶面對的應用程式URL和/或達到該狀態所需的內部頁面URL — 從Jira票證說明/註解、Wiki或`open-aso-devmode-url`慣例中提取真正的URL （如果此處參考）；絕對不要偽造URL)。
    - 若`false`，請略過此票證的步驟5。

## 步驟5 — Media gate

只有在步驟4設定`mediaNeeded: true`時才執行。 中的所有時間戳記
`{state_dir}/media-requests.json`是UTC ISO-8601 (`date -u +%Y-%m-%dT%H:%M:%SZ`) —
請一律以此格式撰寫和比較，以便下方的經過時間數學無歧義
跨回合。

1. 檢查`{state_dir}/media-requests.json`是否有此票證金鑰的現有專案。 如果沒有，則為全新請求。
2. **新要求：**
   - `media.contacts_in_order[0].email` (sandsinh)上的`mcp__Slack__slack_lookup_user`以取得Slack使用者ID。
   - `mcp__Slack__slack_send_dm`包含訊息，內含： Jira票證索引鍵+連結、要擷取的確切專案(`captureSteps`)、要使用的URL以及答案應該前往何處（「在Jira票證上回覆 — 直接附加熒幕擷圖，或針對視訊，透過一般Experience League視訊表單上傳並貼上產生的`video.tv.adobe.com`連結以作為註解」）。
   - 寫入`{state_dir}/media-requests.json[KEY] = {requestedTo: "sandsinh", requestedAt: <UTC ISO-8601 now>, escalated: false}`。
3. **現有請求：**&#x200B;以下兩個臨界值都是從原始`requestedAt`測量的 — 向上呈報不會重設時鐘：
   - `now - requestedAt` &lt; `media.escalate_after_hours` ->不執行此回合，繼續發佈媒體仍待處理（草稿PR）。
   - `now - requestedAt` >= `media.escalate_after_hours`且尚未上報 — > DM `media.contacts_in_order[1]` (kanishka)，已在N小時前詢問訊息附註及問題，但無回應。 更新專案： `escalated: true, escalatedAt: <UTC ISO-8601 now>`。
   - `now - requestedAt` >= `media.give_up_after_hours` （無論升級狀態為何） ->設定`mediaNeeded: false`以供發佈之用，在草稿中插入內嵌附註： `>[!TIP]\n>\n>A screenshot for this step is being added in a follow-up update.`如果此票證的PR已存在，且仍為草稿（透過步驟1.4到達此處，而不是新的步驟6發佈）， `git fetch`/簽出分支、套用附註、認可、推播和呼叫`gh pr ready <number>` — 放棄的草稿仍必須變為可檢閱，不能無限期停留。 標籤專案`gaveUp: true`。

## 步驟6 — 發佈

如果在步驟3中完全略過票證，則加以略過（沒有可發佈的內容）。

1. `git fetch origin`和`git checkout -B {github.branch_prefix}<KEY>-<short-slug> origin/main` — `-B` （不是`-b`），因此先前執行中損毀的剩餘本機分支會重設，而非封鎖簽出；直接從`origin/main`分支也會捨棄先前損毀的任何不正常本機狀態，而非執行失敗。
2. 將Step 4草稿寫入在Step 4.3中決定的目標檔案。 逐行重新驗證`experience-league-markdown`的「在認可Markdown變更之前」檢查清單。
3. 如果已設定Markdown Linter （在存放庫根目錄為`markdownlint_custom.json`）且有`markdownlint-cli`/`npx markdownlint`可用，請針對變更的檔案執行它，並在認可之前修正任何違規。
4. 認可： `docs(aso): <ticket summary, lowercase, no trailing period>\n\nSITES-XXXXX`。
5. `git push -u origin <branch>`.
6. 檢閱者選擇： `gh pr list --repo {github.repo} --label {github.pr_label} --state open --json reviewRequests` — 計算目前列出兩個已設定檢閱者中每個檢閱者的數目；指派較少者（時間 — > `sandsinh_adobe`）。
7. PR內文：

   ```
   ## Summary
   [1-2 sentence description of the feature now documented]
   
   ## Source
   Closes documentation gap tracked in [SITES-XXXXX](https://jira.corp.adobe.com/browse/SITES-XXXXX)
   
   ## Media
   [either "No media needed for this update." OR "Screenshot/video requested from {contact} on {date} — PR opened as draft until resolved." OR "Media follow-up pending — shipped without it; see inline note."]
   
   > 🤖 Drafted by aso-doc-agent
   ```

8. 如果媒體仍在等候中，`gh pr create --repo {github.repo} --title "<ticket summary>" --body "<above>" --label {github.pr_label} --reviewer <chosen-github-handle> --draft`，否則請省略`--draft`。
9. 如果標籤標幟未使用（腰帶和吊帶，符合此組織工具中其他位置使用的模式），則為`gh pr edit <number> --add-label {github.pr_label}`。
10. Jira： `add_jira_comment`連結PR URL，現在 — 這是此回合中的第一次 — 新增`{jira.picked_label}` （`update_jira_issue`，與現有標籤合併）。 這是一項宣告，僅於分支和PR同時存在時特意套用：步驟3-5中任何位置的當機都會讓票證完全沒有標籤，並可安全地重新挑選，而不是永久停滯。 不要轉換票證狀態 — 請由檔案團隊自行分類；`{jira.picked_label}`是此代理程式寫入的唯一狀態訊號。

## 步驟7 — 執行摘要

1. 更新`{state_dir}/run-state.json`： `runs_completed += 1`、時間戳記、已挑選票證（或「無」+原因）、已開啟/更新PR （或「無」+原因）、上限狀態。
2. 列印人類看得懂的簡短摘要（票證、採取的行動、PR連結、媒體狀態）。
