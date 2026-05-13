---
title: 核心網頁指標機會文件
description: 了解核心網頁指標機會，以及如何使用它來改進流量贏取。
badgeSiteHealth: label="網站健康情況" type="Caution" url="../../opportunity-types/site-health.md" tooltip="網站健康情況"
TQID: https://experienceleague.adobe.com/3h-Xas767zUk-Sod7JEr9Lh767r5S3LKpbwJZFZU2kg
product_v2: id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 84a1ae98d67bc02ab272131194511efbeccab492
workflow-type: tm+mt
source-wordcount: 533
ht-degree: 100%

---

# 核心網頁指標機會

<!--![core web vitals opportunity](./assets/core-web-vitals/hero.png){align="center"}-->

>[!VIDEO](https://video.tv.adobe.com/v/3483371/?learn=on&enablevpops)

Core Web Vitals 機會將識別您網站上表現不佳且影響使用者體驗以及自然搜尋效能的頁面。 這些問題可能源自多種因素，如自訂字型、未最佳化的 JavaScript 相依性以及第三方指令碼等。 Core Web Vitals 將測量內容載入的速度、頁面配置的穩定性以及頁面對使用者互動的回應程度。

AEM Sites Optimizer 將偵測受這些問題影響的頁面、在程式碼層級提供特定的 AI 建議，並將修正套用於您現有的開發工作流程。 請注意，只有瀏覽量為 1000 次以上的頁面才能進行分析。

## 自動識別

<!--![Auto-identify core web vitals](./assets/core-web-vitals/auto-identify.png){align="center"}-->

AEM Sites Optimizer 將使用 [Operational Telemetry](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/sites/operational-telemetry-for-aem-as-a-cloud-service) 來持續監視網站效能，以偵測 Core Web Vitals 量度如最大內容繪製 (LCP)、累積版面配置位移 (CLS) 及互動到下一次繪製 (INP) 中的回歸。 此功能利用真實的使用者資料來識別效能回歸，並根據問題對使用者體驗的影響，指定問題的優先順序。

AEM Sites Optimizer 將顯示所有當前問題的清單，並依行動裝置與桌面裝置提供詳細資訊。 「**頁面**」欄指出受影響的頁面項目及，其對應問題將依 LCP、INP 及 CLS 進行分類。

## 自動建議

<!--![Auto-suggest core web vitals opportunity](./assets/core-web-vitals/auto-suggest.png){align="center"}-->

AEM Sites Optimizer 將針對每個已識別的問題，產生規範性程式碼層級建議，以改善 Core Web Vitals 效能。 此功能透過存取您的程式碼存放庫，評估基礎實施。 這使系統能分析元件、指令碼及樣式的實施方式，並找出效能問題的根本原因。 根據此分析，系統將提供針對性的建議，並產生修補程式，指定能以改善效能的變更。 每個建議都可在套用前進行稽核。

按下「建議」按鈕後，將出現一個新視窗，內含效能量度 LCP、INP 和 CLS 等三種類別。 您可以在這些類別之間切換以查看特定問題的清單。 每個類別可能會包含多個問題，因此請務必向下捲動以查看問題和建議的完整清單。 此外，每個量度都有適用於行動裝置和桌面裝置的兩個績效指標。

## 自動最佳化

<!--[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}-->

審閱並核准建議後，您可以按下「**部署最佳化**」。 AEM Sites Optimizer 將根據已識別的問題產生修補程式，並透過版本控制流程供使用。 最佳化流程包含下列步驟：

* **建立問題**：為每個修正建立帶標籤的 GitHub 問題，內含清楚的說明與受影響的 URL，以提升能見度。
* **提取要求傳遞**：自動開啟連結的提取要求，內含完整的程式碼修正，並可直接審閱、測試並合併。
* **狀態追蹤**：追蹤每項修正的完成進度，並標記部分完成或失敗，以便後續處理。

在提供這些更新之前，AEM Sites Optimizer 將執行驗證，確保修正可解決基礎問題且不會引入回歸。 所有更新都遵循標準開發做法，在合併到生產環境之前必須先稽核並核准。

這能確保效能最佳化是準確的、經過驗證，並能整合到現有的開發與治理流程中。
