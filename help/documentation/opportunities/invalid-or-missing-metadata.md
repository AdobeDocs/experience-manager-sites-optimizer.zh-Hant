---
title: 無效或缺少中繼資料機會文件
description: 了解無效或缺少中繼資料機會，以及如何使用它來改進流量贏取。
badgeTrafficAcquisition: label="流量贏取" type="Caution" url="../../opportunity-types/traffic-acquisition.md" tooltip="流量贏取"
source-git-commit: cb64a34b758de8f5dcea298014ddd0ba79a24c17
workflow-type: ht
source-wordcount: '521'
ht-degree: 100%

---


# 無效或缺少中繼資料機會

![無效或缺少中繼資料機會](./assets/missing-or-invalid-metadata/hero.png){align="center"}

無效或缺少中繼資料機會可識別您網頁上缺少或錯誤的中繼資料。修正中繼資料問題可提升內容可見度、搜尋排名和使用者參與，從而增強 SEO。這類問題可能起因於標記缺少或無效、說明太長或太短等因素。

無效或缺少中繼資料機會會在頁面頂端顯示摘要，內含問題的概要及其對您網站和業務的影響。

* **預計流量損失** - 預計會因中繼資料錯誤而損失的流量。
* **預計流量值** - 預計的損失流量值。

## 自動識別

![自動識別無效或缺少中繼資料](./assets/missing-or-invalid-metadata/auto-identify.png){align="center"}

無效或缺少中繼資料機會會列出頁面上所有的錯誤中繼資料，內容包括：

* **頁面** - 包含無效或缺少中繼資料的頁面。
* **問題** - 指出影響中繼資料標記的問題類型。這類問題可能包括缺少標題以及 H1 重複等等。
* **值** - 目前需要變更的中繼資料標記值。
* **建議** - 用於進行合適標記更新的 AI 生成建議。如需詳細資訊，請參閱下一節。

## 自動建議

![自動建議無效或缺少中繼資料](./assets/missing-or-invalid-metadata/auto-suggest.png){align="center"}

無效或缺少中繼資料機會還會提供有關如何變更或更新中繼資料標記的 AI 生成建議。其會根據包含錯誤中繼資料的初始標記以及所建議更新的內容來提供這些建議。

>[!BEGINTABS]

>[!TAB AI 原理]

選取![資訊圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_InfoOutline_18_N.svg)可檢視 AI 針對所建議更新提供的理由。

>[!TAB  編輯建議的中繼資料值]

![編輯建議的無效或缺少中繼資料](./assets/missing-or-invalid-metadata/edit-suggested-metadata-value.png){align="center"}

如果您不同意 AI 產生的建議，則可以選取![刪除圖示](https://spectrum.adobe.com/static/icons/ui_18/CrossSize500.svg)來編輯建議的後設資料值。您可以利用此功能手動輸入您認為最適合的後設資料值。編輯視窗包含以下內容：

* **路徑** - 包含中繼資料 (或缺少) 之頁面的路徑。
* **問題說明** - 指出影響中繼資料標記的問題類型和簡短說明。
* **標記值建議** - 關於如何變更或更新中繼資料標記的 AI 生成建議。例如，標記更新應該包含多少個字元等等。
* **原始標記內容** - 原始標記值。
* **目標標記值** - 編輯此欄位並手動新增所需的標記值。當您選取「**儲存**」時，此值便會套用至所建議的更新。
* **建議** - 關於如何變更值的 AI 生成建議。
* **儲存** - 儲存並套用「**目標標記值**」欄位中的值。

>[!TAB 忽略項目]

您可以選擇忽略具有已損毀或無效目標中繼資料的項目。選取![刪除圖示](https://spectrum.adobe.com/static/icons/ui_18/CrossSize500.svg)會從機會清單中移除此項目。使用機會頁面頂端的「**已忽略**」索引標籤，可以重新啟用已忽略的項目。

>[!ENDTABS]

## 自動最佳化

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

![自動最佳化所建議的無效或缺少中繼資料](./assets/missing-or-invalid-metadata/auto-optimize.png){align="center"}

Sites Optimizer Ultimate 新增了針對無效或缺少中繼資料機會所發現的問題部署自動最佳化功能的能力。 <!--- TBD-need more in-depth and opportunity specific information here. What does the auto-optimization do?-->

>[!BEGINTABS]

>[!TAB 部署最佳化]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB 請求核准]

{{auto-optimize-request-approval}}

>[!ENDTABS]
