---
source-git-commit: 14f10c231373992c49a8bb93c043556305b6280d
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 0%

---
# Experience League Markdown — 完整語法參考資料

摘自https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/markdown-syntax （最後針對「上次更新日期：2026年6月17日」頁面確認）。 如果此處有些內容似乎已過期，請重新擷取即時頁面。

## 前置內容與標題

```markdown
---
title: Title for search optimization
description: This is the article description used for search optimization.
---
# Article title
```

緊接在結束`---`之後的行（以及一個空白行）必須是`# Title` — 而且它應該在前置內容中符合`title:`。

## 基本文字格式

- 粗體： `**bold**`
- 斜體： `*italic*`
- 粗體+斜體： `***both***`
- 逸出格式化字元： `\*not italic\*`
- 段落不需要特殊語法 — 只需要在它們之間加上空白行。

## 標題

```markdown
# This is level 1 (article title)
## This is level 2 (mini-TOC entry)
### This is level 3
```

- `#` (H1) =文章標題，必須符合frontmatter `title`。
- `##` (H2) =預設出現在mini-TOC中（`mini-toc-levels: 3`顯示更多層級）。
- 永不略過層級（`##`→`####`無效）。
- 每個標題後面的&#x200B;**和**&#x200B;前需要空白行。
- 最大標題長度：69個字元(EN)、120 （本地化）。
- 標題ID /錨點： `## Creating processing rules {#processing-rules}` — 小寫，斷字。 如果標題文字以數字（例如年）開頭，則此為必填欄位。 若沒有明確的ID，預設錨點是自動視覺化的標題文字。

## 附註/警告

標準型別： `NOTE`、`TIP`、`IMPORTANT`、`WARNING`。 較新的EXL專用型別： `ADMIN`、`AVAILABILITY`、`PREREQUISITES`、`INFO`、`ERROR`、`SUCCESS`。

```markdown
>[!NOTE]
>
>This is a standard NOTE block.
>
>It can include multiple paragraphs.
```

區塊的每一行都以`>`開頭。 在型別標籤後面包含空的`>`行。

## 索引標籤

```markdown
>[!BEGINTABS]

>[!TAB iOS]

Content for the iOS tab.

>[!TAB Android]

Content for the Android tab.

>[!ENDTABS]
```

- 無法在索引標籤集合內巢狀內嵌索引標籤集合，或在清單內巢狀內嵌索引標籤集合。
- 索引標籤標題會逐字轉譯 — `>[!TAB ...]`中沒有標籤格式。
- 在一個頁面上可以有多個定位點集。

## 影片

```markdown
>[!VIDEO](https://video.tv.adobe.com/v/27069/?learn=on&enablevpops)
```

- 視訊必須已託管於`video.tv.adobe.com` (Adobe TV/MPC) — 不支援原始視訊檔案連結或`<video>`標籤。
- 建議的查詢引數： `?learn=on&enablevpops` （此存放庫中每個內嵌使用的標準格式）。 新增`&autoplay=true`以自動播放。
- 成績單：將`{transcript=true}`新增到短碼，或在`TOC.md`/`metadata.md`中設定整個指南/存放庫的`auto-video-transcripts: true`。

## 徽章

內嵌徽章（在放置處轉譯）：

```markdown
[!BADGE Beta]{type=Informative url="https://www.example.com" tooltip="Go to example.com"}
```

中繼資料徽章（呈現於H1上方） — 在frontmatter中：

```yaml
badgePremium: label="Premium" type="Positive" url="https://www.premium-product.com" tooltip="Download Premium"
```

- `type` （不區分大小寫）： `Informative` （預設/藍色）、`Positive` （綠色）、`Negative` （紅色）、`Neutral` （深灰色）、`Caution` （黃色）。
- 只需要標籤；`type`/`url`/`tooltip`是選用專案。
- 每篇文章最多&#x200B;**兩個**&#x200B;中繼資料徽章（可設定，但需先詢問，才能依賴例外狀況）。
- 中繼資料徽章值必須加上引號。 內嵌徽章`url`/`tooltip`必須加上引號。
- 從`TOC.md`使用的徽章URL必須是根相對(`/help/guide/article.md`)，而非相對 — TOC專案套用至各資料夾。
- `before-title="false"`將中繼資料徽章移動到H1下方。
- 新增`newtab=true`以在新的索引標籤中開啟徽章URL。

## 影像

```markdown
![alt text](assets/logo.png "Hover text"){width="300" align="center"}
```

- `align`：僅`center`或`right` — 無`left`，無`valign`。
- `width`：畫素(`"300"`)或檢視區域百分比(`"50%"`)。
- `zoomable="yes"`使影像按一下放大（不要與也是連結的影像結合 — 連結獲勝）。
- 共用影像的根相對路徑： `/help/assets/imagename.png`。
- 上限： 100 MB硬性上限(GitHub)、5 MB在開始關注前限制，20 MB會觸發驗證錯誤。 每篇文章最多100個影像（EDS演算限制）。

## 連結和交叉引用

- 外部： `[Adobe](https://www.adobe.com)`
- 作為連結的裸URL： `<https://www.adobe.com>` — 未包裝的裸URL **不**&#x200B;自動連結。
- 相對互動參照： `[Overview](collaborative-doc-instructions/overview.md)` — 從&#x200B;*來源*&#x200B;檔案的位置解析；支援`./`、`../`、`../../`。
- 根相對互動參照： `[Overview](/help/using/docile-rules/introduction.md)` — 可從存放庫中的任何檔案運作，不論來源位置為何。
- 前往標題的深層連結：目標需要`{#heading-id}`；連結至`[Text](file.md#heading-id)` （或同一頁面只有`#heading-id`）。
- 在新標籤中開啟： `[See What's new](whats-new.md){target="_blank"}`。

## 清單

```markdown
1. This is step 1.
1. This is the next step.
   1. Sub-step (indent 3 spaces for numbered lists)
   1. Sub-step
```

```markdown
* First item.
* Second item.
```

- 編號清單：一律寫入`1.` （或一律寫入`1)`） — GitHub呈現實際順序。 挑選一種樣式（`.`與`)`），並在文章中保持一致。
- 專案符號清單：從`*`、`-`、`+`中選擇一個，並保持一致 — 將它們混合在同一篇文章中是驗證錯誤。 大部分存放庫中的慣例： `*`。
- 任何清單前後都必須有空白行。
- 清單專案（影像、表格、附註）之間的內容必須縮排至文字開頭（編號清單為3個空格，專案符號清單為2個），否則會中斷清單。 過度縮排（6個空格）會改為將其轉換為程式碼區塊。

## 程式碼區塊

內嵌： `` `code` `` — 如果您需要在內有常值反勾號，請以內嵌的三重反勾號換行。

包圍型：

````markdown
```javascript
var x = 1;
```
````

- 一律指定語法醒目提示的語言+複製按鈕。
- 包圍區塊的上方和下方需要空白行。
- 行號： `` ```html {line-numbers="true"} ``
- 從其他位置開始編號： `` ```html {line-numbers="true" start-line="7"} ``
- 反白顯示行： `` ```html {line-numbers="true" start-line="7" highlight="11-13, 16"} ``
- 程式碼區塊內容絕不會本地化（除了`!UICONTROL`/`!DNL`標籤，這些標籤會在發佈時移除）。
- 程式碼區塊內部沒有Markdown/HTML格式（例如`<i>`）可供使用 — 請使用角括弧或純文字作為預留位置。

## 表格

- 標準GFM管路表適用於簡單的情況。
- HTML表格可用於特殊情況（例如沒有標題列的表格） — 否則偏好使用Markdown 。
- Markdown資料表儲存格內允許有限的HTML： `<p>`、`<br>`、`<ul>`、`<ol>`。
- 您可以將表格設定為自動或固定轉譯 — 如果您需要該層級的控制，請參閱語法指南中的「表格」文章。

## 可摺疊區段

```markdown
+++See details

This is text inside a collapsible section.

* Bullet one
* Bullet two

+++
```

- 請勿巢狀內嵌可摺疊的區段 — 這些區段將無法正確呈現（且驗證不會失敗，因此錯誤會以無訊息方式發出）。
- 區段內的內部清單/程式碼區塊周圍需要空白行，與其他位置相同。

## 文字反白顯示

```markdown
This sentence is normal. <span class="preview">This text is highlighted.</span>
```

使用`<span class="preview">`進行內嵌/段落反白顯示，`<div class="preview">`用於多個段落/元件。

## 代碼片段及

- 從存放庫的`help/snippets.md`共用H2錨點：與`{{anchor-id}}`的參考。
- 來自`help/_includes/*.md`的共用包含檔案：參考`{{$include /help/_includes/filename.md}}`。

## 評論

```markdown
<!-- standard comment code -->
```

- 絕不使用`<!--> bad comment syntax <-->` （缺少破折號） — 它可顯示而非隱藏文字。
- 已轉譯的檔案不會顯示註解，但&#x200B;**任何檢視GitHub上原始.md的人皆可見** — 沒有機密或機密資訊。
- 避免專案符號清單內的評論（可能會破壞清單轉譯）。 在`TOC.md`中，只註解檔案結尾的行，不會註解清單中間的行。

## 空白行因應措施

轉譯器會收合來源中的額外空白行。 若要強制可見的垂直間距，請將`<br>&nbsp;`放置在您想要間隙的位置上。

## 逸出字元

- 可逸出反斜線的字元： `` # { } [ ] * + - . ! `` — 例如`\# not a heading`。
- 對於角括弧(`<placeholder>`)，反斜線無法運作 — 請使用內嵌程式碼區塊(`` `<placeholder>` ``)或HTML實體(`&lt;placeholder&gt;`)。
- 程式碼區塊內的HTML實體&#x200B;**不是**&#x200B;轉換回字元 — `&gt;`在此保留常值文字。
- 中繼資料(YAML frontmatter)有自己的逸出規則 — 如果值以特殊字元（如`:`或`[`）開頭，請引述整個值： `title: "Processing rules: A new beginning"`。

## 受限制的HTML允許清單

Markdown中的任何地方都只允許使用這些HTML標籤；其他任何地方都是驗證錯誤：

```
table  tbody  td  tfoot  thead  th  tr  col  colgroup
p  ul  ol  li  br
b  i  strong  u  s  em  sub  sup  span
caption  a  img  div
pre  code  codeblock
```

偏好使用Markdown語法，而不偏好使用HTML能執行工作的任何位置 — HTML實際上僅適用於邊緣案例，例如無標題表格。

## 明確不支援（即使本機預覽轉譯，也請勿使用）

- 水準規則(`***`， `<hr>`)
- Emoji短碼(`:bowtie:`)
- 工作清單(`- [x] done`)
- 區塊引號&#x200B;*元件*&#x200B;超出note/tab/video短碼（一般`>`區塊引號呈現為引號，而非樣式元件）
- Markdown定義清單語法（請改用手動粗體+破折號格式： `**Frog** - An amphibious green creature.`）
- 影像上的`valign`

## 值得瞭解的檔案大小/計數限制

| 物件 | 限制 |
|---|---|
| 影像/下載檔案大小 | 5 MB的驗證警告、20 MB的錯誤、硬體GitHub上限100 MB |
| 每篇文章的影像數 | 100 （EDS轉譯限制） |
| 每篇文章的中繼資料徽章 | 2 （預設） |
