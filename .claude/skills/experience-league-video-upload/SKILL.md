---
name: experience-league-video-upload
description: 當使用者想要透過>[！VIDEO]在此存放庫的Markdown中提交/上傳視訊至Experience League （video.tv.adobe.com / KT視訊提交）以進行內嵌時使用 — 涵蓋使用瀏覽器自動化填寫提交表單、此存放庫的預設值，以及絕對不可自動化的專案。
source-git-commit: 14f10c231373992c49a8bb93c043556305b6280d
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 1%

---


# Experience League視訊上傳

## 概觀

Experience League影片不是在此存放庫內託管 — 本機`.mp4`會透過個別的提交表單上傳，這會傳回您之後內嵌`>[!VIDEO](...)`的`video.tv.adobe.com` URL （請參閱[[experience-league-markdown]]）。 此技能透過瀏覽器自動化填寫該表單，最多（不包括）附加檔案和提交。

表單： https://81368-exlmpcvideoupload.adobeio-static.net/#/

## 視訊檔案推薦

在使用者記錄或選取剪輯之前，建議使用&#x200B;**16:9外觀比例**，最大解析度為&#x200B;**1920 x 1080畫素** — 這是表單本身規定的要求，而不僅僅是樣式偏好。 主動提及這件事（例如，當使用者表示他們即將為此擷取熒幕錄製時），不只在詢問時提及。

## 硬式規則：永不附加檔案或提交

提交會建立真正的KT Jira票證，並上傳至生產視訊平台，這是一個對外的、難以反轉的動作。 **一律停止**&#x200B;填寫完其他欄位後，將視訊檔案和最終提交點按交還給使用者，即使他們下次不重複該指示。 這是此技能的預設值，而不是根據請求需要重新確認的專案 — 只有在使用者明確表示要在相同請求中提交時，才會略過此停止。

## 先決條件

需要`chrome-devtools` MCP伺服器，該伺服器&#x200B;**不是**&#x200B;已認可至此存放庫（不應該強制每個貢獻者使用瀏覽器自動化MCP）。 如果尚未載入：

1. 在存放庫根目錄建立`.mcp.json`：

   ```json
   {
     "mcpServers": {
       "chrome-devtools": {
         "command": "npx",
         "args": ["-y", "chrome-devtools-mcp@latest", "--accept-insecure-certs", "--no-usage-statistics"]
       }
     }
   }
   ```

2. 新增`.mcp.json`至`.gitignore` （個人工具，未共用）。
3. 在`.claude/settings.local.json`中，新增`"enableAllProjectMcpServers": true`和`"enabledMcpjsonServers": ["chrome-devtools"]`。
4. 告訴使用者重新啟動Claude程式碼（或執行`/mcp`） — MCP伺服器只在啟動時載入，這無法在工作階段期間完成。

## 此存放庫的預設值

除非使用者另有指示，否則請使用：

| 欄位 | 預設 | 原因 |
|---|---|---|
| 雲端 | `Experience Cloud` | — |
| 產品 | `AEM` | 使用者為此存放庫指定的預設（表單也列出`AEM as a Cloud Service` — 除非詢問，否則不要取代它） |
| 子產品 | `AEM Sites` | 最接近的相符專案；表單沒有「Sites Optimizer」專案 |
| 角色 | `User` | 預檢/Sites Optimizer內容的目標是作者/行銷人員，而非管理員/開發人員，除非影片明顯是針對技術對象 |
| 技能等級 | `Beginner` | 除非顯示的工作流程有真正的先決條件 |
| 視訊語音性別 | `No voices` | 僅限靜音熒幕錄製 — 詢問此影片是否包含旁白 |
| 視訊型別 | 詢問或推斷內容 | 即時選項為`Event` / `Feature` / `Technical` / `Value` — UI逐步解說通常是`Feature` |
| 電子郵件 | 任何預填的內容 | 表單會自動填入登入使用者的Adobe電子郵件；請勿覆寫 |

## 步驟

1. `mcp__chrome-devtools__new_page`至表單URL。
2. `mcp__chrome-devtools__take_snapshot`並等待（`"Title"`上的`mcp__chrome-devtools__wait_for`）直到表單資料完成載入 — 它開始於「正在載入表單資料……」 旋轉圖示。
3. 填滿&#x200B;**標題**&#x200B;和&#x200B;**描述** — 描述是可內容編輯的RTF方塊，不是純的`<textarea>`。 `fill`/`fill_form`無訊息的no-ops （值不含，且仍有「必要」錯誤）。 相反： `click`它要聚焦，然後使用文字`mcp__chrome-devtools__type_text`。
4. 下拉式清單（**視訊型別**、**視訊語音性別**、**雲端**、**產品**、**子產品**、**事件名稱**）是自訂清單方塊按鈕，而非原生`<select>`。 針對每個： `click`開啟它的按鈕，從快照讀取真正的選項（它們是API載入的 — 不要假設預設表格的確切選項拼字仍然是最新的），然後`click`相符的`option`。
5. **產品**&#x200B;和&#x200B;**子產品**&#x200B;在其父欄位設定之前已停用（產品需要雲端；子產品需要產品） — 按順序填入它們。
6. **角色**&#x200B;和&#x200B;**技能等級**&#x200B;是核取方塊群組 — `fill_form`核取方塊`uid`s上有`"value": "true"`可以正常運作（不像說明欄位）。
7. 停止。 擷取熒幕擷圖，總結設定內容及原因（尤其是任何被取代的預設值，例如產品/子產品），並告訴使用者附加視訊及自行提交。
8. 使用者表示已提交後，請要求他們提供產生的Adobe MPC影片URL （上傳後顯示在表單上，例如`https://video.tv.adobe.com/v/3496629?learn=on`）。 使用此視訊填寫`>[!VIDEO](...)`短碼，無論此視訊要前往何處 — 請勿自行偽造或猜測網址/識別碼。

## 驗證傳回的視訊URL

每當使用者將影片URL交給您進行內嵌時（上述步驟8或其他任何時間）：

- **拒絕任何不在`video.tv.adobe.com`上的專案。** 視訊必須根據[[experience-league-markdown]] — 連至YouTube、檔案主機或任何其他網域的連結不是有效的`>[!VIDEO]`目標託管於此。 告知使用者必須先通過此存放庫的上傳流程；請勿將其內嵌。
- **如果是遺失`&enablevpops`的有效`video.tv.adobe.com` URL，請在內嵌前新增它** （符合此存放庫中`>[!VIDEO]`已使用的慣例 — 請參閱`help/home.md`、`help/documentation/trial.md`等）。 如果已經有`?`，則附加`&enablevpops`，否則`?enablevpops`。

## 常見錯誤

- 正在說明欄位上嘗試`fill`/`fill_form`，並在錯誤橫幅仍顯示「需要說明」時繼續。  — 在每個步驟之後檢查錯誤清單，而不只是在結束時。
- 從記憶體猜測下拉式清單選項文字，而非開啟下拉式清單 — 實際值（例如`No voices`代表語音性別、`Feature`/`Technical`/`Value`代表視訊型別、「產品」下的AEM/AEM-as-a-Cloud-Service分割）不可猜測，且會獨立於該檔案變更。
- 按一下「**上傳視訊**」/附加檔案「以儲存使用者一個步驟」。 請勿 — 請參閱上方的硬性規則。
