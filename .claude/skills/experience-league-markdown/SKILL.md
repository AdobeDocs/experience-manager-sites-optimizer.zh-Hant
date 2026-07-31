---
name: experience-league-markdown
description: 在Adobe Experience League / Adobe-Enterprise-Docs存放庫(help/**/*.md) — 控管Frontmatter、標題、附註(NOTE/TIP/IMPORTANT/WARNING/etc.)、標籤(BEGINTABS/TAB/ENDTABS)、影片內嵌、徽章、影像、連結/交叉參照、表格、清單、程式碼區塊以及Experience League驗證管道強制實施的HTML標籤允許清單 — 中撰寫或編輯Markdown檔案時使用。
source-git-commit: 14f10c231373992c49a8bb93c043556305b6280d
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 1%

---


# Experience League Markdown

## 概觀

Experience League檔案使用GitHub風格的Markdown以及一組自訂擴充功能（區塊式短碼、徽章、標籤、視訊內嵌）。 編寫管道&#x200B;**驗證**&#x200B;這些檔案 — 使用不支援的語法（原始`<video>`標籤、`<hr>`、工作清單、混合專案符號字元、略過的標題層級、超大影像）會造成建置/驗證錯誤，而不僅僅是樣式錯誤。

Source真相： https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/markdown-syntax （如果本機reference.md看來過時 — 「上次更新」日期在頂端，請擷取此頁面）。

每個簡短程式碼和規則的完整語法參考： [reference.md](reference.md)。 在撰寫任何非瑣碎專案（標籤、影片、徽章、表格與HTML）之前請先閱讀。

## 快速參考

| 元素 | 語法 | 備註 |
|---|---|---|
| Frontmatter | `---\ntitle: ...\ndescription: ...\n---` | 空白行，則`# Title`必須位於下一個 |
| 標題層級 | `#`, `##`, `###` | `#` =標題（符合frontmatter `title`）， `##` =迷你目錄專案。 絕不略過層級。 前/後空白行。 最多69個字元(EN) |
| 標題ID | `## Heading text {#custom-id}` | 如果標題開頭為/包含數字（例如`## 2026 release notes {#2026-release-notes}`），則為必要 |
| 附註/提示/等 | `>[!NOTE]`然後`>`然後`>Text` （每個都有自己的行） | 型別：注意、提示、重要、警告、警告、管理員、可用性、先決條件、資訊、錯誤、成功 |
| 索引標籤 | `>[!BEGINTABS]` / `>[!TAB Title]` / `>[!ENDTABS]` | 無法巢狀內嵌索引標籤集；無法在清單內巢狀內嵌 |
| 影片 | `>[!VIDEO](https://video.tv.adobe.com/v/ID/?learn=on&enablevpops)` | 必須在video.tv.adobe.com上託管 — 沒有原始`<video>`/檔案連結 |
| 影像 | `![alt text](assets/img.png "hover text"){width="300" align="center"}` | `align`是`center`或僅限`right` （無`left`，無`valign`） |
| 連結（相對） | `[Text](../folder/file.md)` | 來源檔案位置的帳戶 |
| 連結（根） | `[Text](/help/guide/file.md)` | 可在存放庫的任何位置運作；TOC.md badge URL的必要專案 |
| 深層連結 | `[Text](file.md#heading-id)` | 目標標題需要明確的`{#heading-id}` |
| 外部連結（純URL） | `<https://example.com>` | 裸URL不會自動連結 — 以`< >`換行或使用`[text](url)` |
| 項目符號清單 | `* item` （從`*`/`-`/`+`中選擇一個，保持一致性） | 清單前/後空白行；混合標籤=驗證錯誤 |
| 編號清單 | `1. item` （每行重複`1.`） | GitHub會呈現實際數字 |
| 程式碼（內嵌） | `` `code` `` | 針對檔案名稱、命令、值、未驗證的範例URL |
| 代碼（受防護） | ` `&#x200B;``language ` ... ` ``&#x200B;` ` | 一律指定語言；前/後空白行；`{line-numbers="true" start-line="n" highlight="n-m"}`選填 |
| 徽章（內嵌） | `[!BADGE Beta]{type=Informative url="..." tooltip="..."}` | `type`：資訊/正面/負面/中性/警告 |
| 可收合 | `+++Summary` ... `+++` | 沒有巢狀摺疊專案；內部清單/程式碼周圍有空白行 |
| 空白行入侵 | `<br>&nbsp;`在它自己的行 | 一般額外空白行會摺疊/被轉譯器忽略 |
| 評論 | `<!-- text -->` | 從不`<!--> text <-->` — 任何檢視GitHub原始檔案的人都能看見，因此沒有秘密 |

## 常見錯誤

- **原始`<video>`、`<iframe>`或其他未加入允許清單的HTML**→驗證錯誤。 HTML允許清單為： `table tbody td tfoot thead th tr col colgroup p ul ol li br b caption i strong u s span sub sup a img div em pre code codeblock`。 其他任何專案（包括`<video>`/`<source>`）都會遭到拒絕 — 請改用`>[!VIDEO]`短碼，這要求視訊已裝載在video.tv.adobe.com上。
- **`<hr>`/ `***`水準規則、emoji短碼(`:bowtie:`)、工作清單(`- [x]`)** — 不支援任何專案；即使本機預覽轉譯，也不要使用它們。
- **混合專案符號字元** （`*`和`-`在相同清單中） — 驗證錯誤。 為每篇文章挑選一篇。
- **略過標題層級** （`##`直接到`####`） — 不允許。
- **沒有明確識別碼** （例如`## 2026 release notes`）的數字前置標題 — 必須新增`{#some-id}`，否則自動分頁清單可能會發生衝突/中斷。
- **Prose** (`Visit https://example.com for more`)中的空URL將不會呈現為連結。 以`< >`換行或使用`[text](url)`。
- 視覺間距&#x200B;**的**&#x200B;額外空白行 — 由轉譯器摺疊。 使用`<br>&nbsp;`，而非空的`<br>`或重複的新行。
- **超過~5 MB的影像** — 在5 MB出現驗證警告，在20 MB出現錯誤。 一篇文章中有超過100個影像會中斷轉譯（EDS限制）。
- **frontmatter中繼資料中有兩個以上的徽章** — 預設不允許使用。
- **逸出問題**：反斜線逸出只適用於`` # { } [ ] * + - . ! ``。 對於`<` `>`，例如`<filename>`預留位置，請使用內嵌程式碼區塊或HTML實體(`&lt;filename&gt;`)，而非反斜線。

## 認可Markdown變更之前

1. Frontmatter存在，`# Title`會緊接在後面（在空白行之後）。
2. 每個標題前後都有一行空白字；沒有略過的層級。
3. 任何視訊都是`>[!VIDEO](https://video.tv.adobe.com/...)`，不是原始`<video>`標籤。
4. 任何自訂短碼(`>[!NOTE]`、`>[!BEGINTABS]`、`>[!BADGE ...]`)都符合[reference.md](reference.md)中的精確語法 — 包括多行區塊內的空白`>`行。
5. 清單會使用一致的專案符號/編號樣式，整個清單周圍會有空白行。
6. 連結：相對連結解析自&#x200B;*來源*&#x200B;檔案的資料夾；跨存放庫或TOC/徽章連結使用根相對(`/help/...`)表單。
7. 上方的「常見錯誤」區段中的允許清單以外沒有HTML標籤。
