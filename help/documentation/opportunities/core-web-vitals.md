---
title: 核心網頁指標機會文件
description: 了解核心網頁指標機會，以及如何使用它來改進流量贏取。
badgeSiteHealth: label="網站健康情況" type="Caution" url="../../opportunity-types/site-health.md" tooltip="網站健康情況"
source-git-commit: cb64a34b758de8f5dcea298014ddd0ba79a24c17
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 86%

---


# 核心網頁指標機會

![核心網頁指標機會](./assets/core-web-vitals/hero.png){align="center"}

核心網頁指標機會可識別會降低網頁使用者體驗和有機搜尋績效的問題。這些問題源自於廣泛的因素，例如：自訂字型、未最佳化的JavaScript相依性、第三方指令碼等。 核心網頁指標機會會指出這些錯誤元素，並建議可以提高網頁績效的解決方式。請注意，只有瀏覽量至少為 1000 次的頁面才能進行分析。

首先，核心網頁指標機會會在頁面頂端顯示摘要，內含問題的概要及其對您網站和業務的影響。

* **預計流量損失** – 預計會因核心網頁指標低於績效臨界值而損失的流量。
* **預計流量值** – 預計的損失流量值。

## 自動識別

![自動識別核心網頁指標](./assets/core-web-vitals/auto-identify.png){align="center"}

頁面下方有所有當前問題的清單，並分組如下：

* **行動裝置問題** – 影響頁面行動裝置版本的問題清單。
* **桌面問題** – 影響頁面桌面版本的問題清單。

以上各個問題會顯示在一張表格中，內有「**頁面**」欄可供您識別受影響的頁面項目。

系統會按照「核心Web重要資訊」報表中的標準效能度量來分組這些問題：

* 最大內容繪製&#x200B;**LCP**
* 下一個繪圖&#x200B;**INP**&#x200B;的互動
* 累積配置位移&#x200B;**CLS**

## 自動建議

![自動建議核心網頁指標機會](./assets/core-web-vitals/auto-suggest.png){align="center"}

核心網頁指標機會會提供 AI 生成的解決建議。按一下建議按鈕時會出現一個新視窗，內含效能指標 **LCP**、**INP** 和 **CLS** 這三個類別。您可以在這些類別之間切換以查看特定問題的清單。

每個類別可能會包含多個問題，因此請務必向下捲動以查看問題和建議的完整清單。此外，每個量度都有適用於行動裝置和桌面的兩個績效指標。

## 自動最佳化

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

![自動最佳化核心網頁指標機會](./assets/core-web-vitals/auto-optimize.png){align="center"}

Sites Optimizer Ultimate 新增了針對核心網頁指標機會所發現的問題部署自動最佳化功能的能力。 <!--- TBD-need more in-depth and opportunity specific information here. What does the auto-optimization do?-->

>[!BEGINTABS]

>[!TAB 部署最佳化]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB 請求核准]

{{auto-optimize-request-approval}}

>[!ENDTABS]

