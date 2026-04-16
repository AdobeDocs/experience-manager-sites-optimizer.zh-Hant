---
title: 缺少替代文字文件
description: 了解缺少替代文字機會，以及如何使用它來提高您網站上的參與度。
badgeEngagement: label="參與度" type="Caution" url="../../opportunity-types/engagement.md" tooltip="參與度"
source-git-commit: 8052c94f778829012f023fe470411dfe77ef46b9
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 36%

---


# 缺少替代文字機會

![缺少替代文字機會](./assets/missing-alt-text/hero.png){align="center"}

遺失的替代文字機會可識別網站上沒有描述性替代文字的影像。 如果沒有替代文字，依賴熒幕助讀程式的使用者將無法解譯視覺內容，造成協助工具障礙。 這也會限制搜尋引擎理解和索引影像的方式，降低內容發現和搜尋效能。 AEM Sites Optimizer會識別遺失的替代文字問題、提供特定的AI建議，並啟用一鍵式部署來修正這些問題，所有這些都在單一集中檢視中。

## 自動識別

![自動識別缺少替代文字](./assets/missing-alt-text/auto-identify.png){align="center"}

AEM Sites Optimizer使用多步驟稽核來掃描您的網站，該稽核結合網站抓取、真實使用者流量資料和AI分析，以識別需要替代文字但未定義該文字的影像。 它也會評估頁面上的影像，以判斷是否需要替代文字，根據網頁內容可及性指引(WCAG)排除裝飾性或非資訊性影像。 系統會根據影像在頁面中的角色和相關性，排定對協助工具和SEO影響最大的修正專案，藉此分析影像。

此機會提供已識別問題的清單，包括：

* **頁面** – 包含缺少替代文字之頁面的路徑。
* **影像** – 缺少描述性替代文字的影像。

## 自動建議

![自動建議缺少替代文字](./assets/missing-alt-text/auto-suggest.png){align="center"}

AEM Sites Optimizer會針對每個已識別的問題，建議影像使用描述性替代文字。 它會使用AI視覺模型來分析影像，並產生可反映其在頁面中內容和角色的說明。 Recommendations內容簡潔、相關，並符合協助工具的最佳實務。 每個建議都可以在套用前進行檢閱和編輯。

>[!BEGINTABS]

>[!TAB 編輯缺少的替代文字]

![編輯缺少的替代文字](./assets/missing-alt-text/edit-alt-text-value.png){align="center"}

如果您不同意 AI 生成的建議，則可以透過選取&#x200B;**編輯圖示**&#x200B;來編輯建議的替代文字。 您可以利用這個功能來手動調整您認為最適合影像的文字說明。 編輯視窗包含以下內容：

* **頁面路徑** – 此為唯讀欄位，會顯示缺少替代文字問題發生所在頁面的路徑。 按一下路徑旁的箭頭，即可開啟對應的頁面。
* **影像** – 需要替代文字之影像的唯讀預覽。
* **目標替代文字** – 此為可編輯的欄位，可供您手動輸入影像的描述性替代文字。 請確保替代文字簡潔明瞭地傳達影像的內容和目的。 如有相關的關鍵字，自然可以納入其中，但數量不要過多。

>[!TAB 忽略項目]

您可以選擇忽略機會清單中的項目。 選取![刪除圖示](https://spectrum.adobe.com/static/icons/ui_18/CrossSize500.svg)，即可從清單中移除此項目。 使用機會頁面頂端的「**已忽略**」索引標籤，可以重新啟用已忽略的項目。

>[!ENDTABS]

## 自動最佳化

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

>[!VIDEO](https://video.tv.adobe.com/v/3483275/?captions=chi_hant&learn=on&enablevpops)

在檢閱並核准建議後，您可以按一下&#x200B;**部署最佳化**。 AEM Sites Optimizer接著會根據您實作中管理替代文字的方式，將修正套用至編寫環境。 AEM作者可從內容管理系統(CMS)發佈變更。

視設定而定，可能會將更新直接套用至頁面內容、資產中繼資料或支援的內容模型。 最佳化程式包含下列步驟：

* **驗證** — 確保安全套用更新而不影響現有功能。
* **部署** — 透過現有程式（例如AEM中的內容更新或與內容API的整合）套用更新。
* **許可權檢查** — 驗證使用者是否擁有套用變更的適當許可權。 如果沒有，則可以使用替代輸出（例如可下載的更新）進行移交。

更新會在支援的地方建立版本，提供可視性和回覆容量。 這可確保準確地套用替代文字更新，與現有實作保持一致，並與治理和協助工具標準一致。

AEM Sites Optimizer會根據您的設定，自動套用替代文字更新，如下所示：

>[!BEGINTABS]

>[!TAB Edge Delivery Services]

更新來原始檔（例如，Google Docs或SharePoint）。

>[!TAB AEM as a Cloud Service]

透過內容API直接寫入更新，具有版本設定和遞補支援。

>[!TAB 數位資產管理（選擇性）]

在適用的地方更新資產層級替代文字。

>[!ENDTABS]
