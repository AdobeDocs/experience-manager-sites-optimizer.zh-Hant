---
title: 損壞的內部連結機會文件
description: 了解損壞的連結機會，以及如何使用它來提高您網站上的參與度。
badgeEngagement: label="參與度" type="Caution" url="../../opportunity-types/engagement.md" tooltip="參與度"
source-git-commit: c2bd3f7dc998b103ecdd02c239b1ea0312db20f1
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 99%

---


# 中斷的內部連結機會

![損壞的內部連結機會](./assets/broken-internal-links/hero.png){align="center"}

損壞的內部連結會影響搜尋引擎為您的網站建立索引的能力，並對使用者體驗和搜尋引擎最佳化產生負面影響。為了協助解決這個問題，損壞的內部連結機會會指出損壞的 URL，並提供有效連結更新的建議。解決這些問題會提高使用者參與度，並確保導覽和協助工具順暢運作。

損壞的內部連結機會會在頁面頂端顯示摘要，內含問題的概要及其對您網站和業務的影響。

* **預計流量損失** - 預計會因內部連結損壞而損失的流量。
* **預計流量值** – 預計的損失流量值。

## 自動識別

<!---![Auto-identify broken internal links](./assets/missing-or-invalid-metadata/auto-identify.png){align="center"}-->

損壞的內部連結機會會自動識別並列出您頁面上所有損壞的內部連結，內容包括：

* **反向連結頁面** – 包含損壞連結的頁面。
* **損壞的目標 URL** – 損壞的內部連結。
* **建議** – 關於如何更新損壞連結的 AI 生成建議。如需詳細資訊，請參閱自動建議區段。

## 自動建議

<!--![Auto-suggest broken internal links](./assets/broken-internal-links/auto-suggest.png){align="center"}-->

損壞的內部連結機會會提供有關如何更新損壞連結的 AI 生成建議。其會根據損壞的目標 URL 來提供這些建議，且建議中會提供合適的替代值。選取&#x200B;**資訊圖示**&#x200B;可提供所建議更新的 AI 生成原理。


>[!BEGINTABS]

>[!TAB AI 原理]

<!--[AI rationale of broken internal links](./assets/broken-internal-links/auto-suggest-ai-rationale.png) -->

選取&#x200B;**資訊**&#x200B;圖示可檢視所建議 URL 的 AI 原理。該原理會解釋為何 AI 認為所建議的 URL 最適合已損壞的連結使用。這可以協助您了解 AI 的決策過程，並做出是要接受還是拒絕建議的明智決定。

>[!TAB 編輯目標 URL]

<!--![Edit suggested URL of broken internal links](./assets/broken-internal-links/edit-target-url.png){align="center"}-->

如果您不同意 AI 生成的建議，則可以透過選取&#x200B;**編輯圖示**&#x200B;來編輯建議的連結值。這可讓您手動輸入所需的連結。編輯視窗中會包含連結的&#x200B;**損壞目標路徑**、可供您手動編輯連結的&#x200B;**所需目標路徑**，以及含有 AI 生成建議的欄位。編輯完成後，請按一下「**儲存**」以更新損壞的連結項目。輸入欄位中會出現一個黃點，以指出該連結已經過編輯。

>[!TAB 忽略項目]

<!--![Ignore broken links](./assets/broken-internal-links/ignore.png){align="center"}-->

您可以選擇忽略具有損壞目標 URL 的項目。選取&#x200B;**忽略圖示**&#x200B;便會從機會清單中移除該項目。若要重新啟用已忽略的項目，可從機會頁面頂端的「**已忽略**」索引標籤進行。

>[!ENDTABS]


## 自動最佳化

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

<!---![Auto-optimize suggested invalid or missing metadata](./assets/broken-internal-links/auto-optimize.png){align="center"}-->

Sites Optimizer Ultimate 新增了針對機會所發現的損壞連結部署自動最佳化功能的能力。<!--- TBD-need more in-depth and opportunity specific information here. What does the auto-optimization do?-->


>[!BEGINTABS]

>[!TAB 部署最佳化]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB 請求核准]

{{auto-optimize-request-approval}}

>[!ENDTABS]

