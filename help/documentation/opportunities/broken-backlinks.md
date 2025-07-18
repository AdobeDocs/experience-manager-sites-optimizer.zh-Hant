---
title: 損壞的反向連結機會文件
description: 了解損壞的反向連結機會，以及如何使用它來改進流量贏取。
badgeTrafficAcquisition: label="流量贏取" type="Caution" url="../../opportunity-types/traffic-acquisition.md" tooltip="流量贏取"
source-git-commit: cb64a34b758de8f5dcea298014ddd0ba79a24c17
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 71%

---


# 損壞的反向連結機會

![損壞的反向連結機會](./assets/broken-backlinks/hero.png){align="center"}

損壞的反向連結機會可識別其他網站與您的網站之間會導致 404 錯誤的連結。由於搜尋引擎使用反向連結來確定搜尋相關性，因此損壞的連結可能會對您網站的 SEO 和可發現性產生負面影響。這些問題可能起因於 URL 變更或所連結的頁面已移除等因素。

損壞的反向連結機會會在頁面頂端顯示摘要，內含問題的概要及其對您網站和業務的影響。

* **預計流量損失** - 預計會因反向連結損壞而損失的流量。
* **預計流量值** - 預計的損失流量值。

## 自動識別

![自動識別損壞的反向連結](./assets/broken-backlinks/auto-identify.png){align="center"}

損壞的反向連結機會會列出您網站上所有損壞的反向連結，其中包括：

* **反向連結頁面** - 包含損壞連結的網站網域。
* **優先順序** - 高、中、低，會根據 TODO 指出損壞的連結對 SEO 的影響。
* **損壞的目標 URL** - 連結到之網站上的不存在 URL。

## 自動建議

![自動建議損壞的反向連結](./assets/broken-backlinks/auto-suggest.png){align="center"}

損壞的反向連結機會也會提供 AI 生成的建議，以指出損壞的 URL 應重新導向到您網站上的哪個頁面。系統會根據包含已損壞 URL 的文字以及建議頁面的內容來提出這些建議。


>[!BEGINTABS]

>[!TAB AI 原理]

![關於已損壞反向連結之自動建議的 AI 原理](./assets/broken-backlinks/auto-suggest-ai-rationale.png){align="center"}

選取&#x200B;**資訊**&#x200B;圖示可檢視所建議 URL 的 AI 原理。該原理會解釋為何 AI 認為所建議的 URL 最適合已損壞的連結使用。它有助於您瞭解AI的決策流程，並做出是否接受或拒絕建議的明智決定。

>[!TAB 編輯目標 URL]

![編輯已損壞反向連結的建議 URL](./assets/broken-backlinks/edit-target-url.png){align="center"}

如果您不同意 AI 生成的建議，則可以透過選取&#x200B;**編輯圖示**&#x200B;來編輯建議的 URL。編輯可讓您手動輸入您認為最適合中斷連結的URL。 Sites Optimizer也會列出您網站上其認為可能適合中斷連結的任何其他URL。

>[!TAB 忽略項目]

![忽略損壞的反向連結](./assets/broken-backlinks/ignore.png){align="center"}

您可以選擇忽略具有已損壞目標 URL 的項目。選取![刪除圖示或忽略圖示](https://spectrum.adobe.com/static/icons/ui_18/CrossSize500.svg)會從機會清單中移除中斷的背景連結。 若要重新啟用已忽略的損壞反向連結，可從機會頁面頂端的「**已忽略**」索引標籤進行。

>[!ENDTABS]

## 自動最佳化

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

![自動最佳化損壞的反向連結](./assets/broken-backlinks/auto-optimize.png){align="center"}

Sites Optimizer Ultimate 新增了為損壞的反向連結部署自動最佳化功能的能力。選取「**自動最佳化**」按鈕會自動更新 AEM 網站的重新導向規則，以將&#x200B;**損壞的目標 URL** 對應到&#x200B;**建議的 URL**。此功能可確保&#x200B;**反向連結頁面**&#x200B;上連結中斷後的網站訪客和搜尋機器人重新導向至您網站上的正確頁面，進而改善SEO和使用者體驗。

>[!BEGINTABS]

>[!TAB 部署最佳化]

![部署已損壞反向連結的最佳化](./assets/broken-backlinks/deploy-optimization.png){align="center"}

選取&#x200B;**部署最佳化**&#x200B;會更新AEM網站的重新導向規則，以便將&#x200B;**中斷的目標URL**&#x200B;對應到&#x200B;**建議的URL**。 此功能可確保&#x200B;**反向連結頁面**&#x200B;上連結中斷後的網站訪客和搜尋機器人重新導向至您網站上的正確頁面，進而改善SEO和使用者體驗。

>[!TAB 請求核准]

![已損壞反向連結的請求核准](./assets/broken-backlinks/request-approval.png){align="center"}

{{auto-optimize-request-approval}}

>[!ENDTABS]
