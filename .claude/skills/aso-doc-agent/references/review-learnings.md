---
source-git-commit: 2a3a02ea04fac7ce37fdc43e836a4832be224e25
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---
# ASO檔案代理程式 — 檢閱學習內容

從人力公關評論意見中汲取有關這位代理商自身公關的持久課程。 讀取
此檔案位於`pipeline.md`中步驟4 （研究+草稿）的開頭，在起草之前
任何事情 — 重點在於檢閱者一次的更正不應該是
再次於未來的票證上製作。

## 屬於此處的專案

只有&#x200B;**可一般化**的意見反應 — 未來票證將會重複出現的模式，關於
色調、結構、遺漏的部分、錯誤的檔案位置或內容準確度。 範例：

- 「一律提及支援忽略/略過的商機的「已忽略」索引標籤。」
- 「除非票證或現有的同層級頁面確認，否則請勿宣告Ultimate層級閘道 — 將其保持註解狀態，並改為標示為開啟的專案。」
- 「新的商機操作頁面需要一個TOC.md專案，並在其商機型別登陸頁面上加入卡片格線專案，而不只是頁面本身。」

## 什麼不屬於這裡

只適用於單一PR的一次性機械回饋：錯字、中斷連結、PR
遺失逗號，該特定PR中的檔案路徑錯誤。 直接在PR中修正這些錯誤 — 這些錯誤會
不要泛化至未來的草稿，所以持久的專案就是雜訊。

## 專案格式

```markdown
## YYYY-MM-DD — SITES-XXXXX (PR #NN)

**Lesson:** [one or two sentences — the generalizable rule]

**Why:** [what the reviewer actually said, or the specific mistake it corrects]

**Applies to:** [which ticket types / pages this affects — "all opportunity how-to pages", "settings/setup pages", "everything", etc.]
```

頂端的最新專案。 如果稍後的課程取代或縮小較早的課程，請編輯
要注意的先前專案，不要在檔案中留下兩個衝突的規則。

---

尚未輸入任何專案 — 在人類第一次要求變更時，此檔案會取得其第一個專案
代理程式的其中一個PR上。
