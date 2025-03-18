---
title: Sitemap問題機會檔案
description: 瞭解Sitemap問題商機，以及如何使用它來改善流量贏取。
badgeTrafficAcquisition: label="流量贏取" type="Caution" url="../../opportunity-types/traffic-acquisition.md" tooltip="流量贏取"
source-git-commit: d812a49e4b49d329717586b9f3c7a235aff3e69a
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---


# Sitemap問題機會

![網站地圖問題商機](./assets/sitemap-issues/hero.png){align="center"}

完整且精確的Sitemap可協助搜尋引擎有效率地編目網站頁面並編制索引，確保搜尋結果更具可見性。 此網站地圖機會可識別您的網站地圖的潛在問題。 修正這些問題可大幅改善搜尋引擎索引以及您網站上的內容可發現性。

頁面頂端會顯示摘要，包括問題及其對網站和業務影響的摘要。

* **專案流量損失** — 網站地圖問題造成的預估流量損失。
* **預計流量值** — 遺失流量的預估值。

## 自動識別

可使用下列條件篩選Sitemap問題：

* **有問題的Sitemap** — 分析過的Sitemap URL包含潛在問題。
* **問題型別** — 網站地圖中識別的問題型別：
   * **使用者端錯誤** — 未傳回`200 Success`回應的專案。
   * **重新導向** — 錯誤或設定錯誤的重新導向。

>[!BEGINTABS]

>[!TAB 使用者端錯誤]

![自動識別Sitemap使用者端錯誤](./assets/sitemap-issues/auto-identify-client-errors.png){align="center"}

如果您的網站地圖中的URL傳回這些專案，搜尋引擎可能會假設您的網站地圖已過期，或頁面遭到錯誤移除。 使用者端指出來自使用者端（瀏覽器或編目程式）的要求無效。 常見問題包括：

* **404找不到** — 要求的頁面不存在。
* **403禁止存取** — 伺服器拒絕存取要求的頁面。
* **410不存在** — 此頁面已被刻意移除，將不會傳回。
* **401未獲授權** — 需要驗證，但未提供。

這些錯誤可能會損害SEO，尤其是當重要頁面傳回&#x200B;**404或410**&#x200B;時，因為搜尋引擎可能會將它們取消索引。

每個問題都會顯示在表格中，**Page**&#x200B;欄會識別受影響的Sitemap專案：

* **頁面** — 有問題的Sitemap專案的URL。

>[!TAB 重新導向]

![自動識別Sitemap使用者端錯誤](./assets/sitemap-issues/auto-identify-redirects.png){align="center"}

Sitemap應僅包含最終目的地URL，而非重新導向的URL。 重新導向旨在引導使用者和編目程式到正確的位置，但如果設定錯誤，則可能會導致問題：

* **302已找到（暫時重新導向）** — 若誤用而非&#x200B;**301**，可能會導致SEO問題。
* **307暫時重新導向** — 類似於302，但保留HTTP方法。
* **重新導向回圈** — 頁面重新導向回本身或建立無限回圈時。
* **中斷的重新導向** — 當重新導嚮導向導致不存在的或4xx頁面。

每個問題都會顯示在表格中，**Page**&#x200B;欄會識別受影響的Sitemap專案：

* **頁面** — 有問題的Sitemap專案的URL。

>[!ENDTABS]

## 自動建議

每個符合篩選條件](#auto-identify)的Sitemap問題[都會列在含有下列資料行的表格中：

* **頁面** — 有問題的Sitemap專案的URL。
* **建議** — 此問題的建議修正。

建議通常會包括更新的網站路徑，以更正網站地圖專案。 在某些情況下，它們可能也會提供更詳細的指示，例如指定正確的重新導向目標。

## 自動最佳化[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}


![自動最佳化Sitemap問題](./assets/sitemap-issues/auto-optimize.png){align="center"}

Sites Optimizer Ultimate新增了部署Sitemap自動最佳化的功能。

>[!BEGINTABS]

>[!TAB 部署最佳化]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB 要求核准]

{{auto-optimize-request-approval}}

>[!ENDTABS]
