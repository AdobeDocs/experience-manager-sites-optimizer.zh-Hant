---
title: 準備程式碼修補程式檔案
description: 瞭解AEM Sites Optimizer如何為Core Web Vitals修正準備程式碼修補程式，以及如何後續追蹤。
product_v2: id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: a86d83ee226055e6401b13fd421b40d449b96fa8
workflow-type: tm+mt
source-wordcount: 248
ht-degree: 2%

---

# 準備程式碼修補程式檔案

<!--![Preparing code patches](./assets/preparing-code-patches/hero.png){align="center"}-->

針對[核心網站機會](/help/documentation/opportunities/core-web-vitals.md)，AEM Sites Optimizer會產生已識別效能問題的程式碼層級修正。 您可以檢閱並準備這些修正程式作為程式碼修補程式，而非直接部署。

## 準備程式碼修補程式

從Core Web Vitals清單中選取一或多個問題，然後按一下&#x200B;**準備程式碼修補程式**&#x200B;以準備您的選擇，或&#x200B;**準備所有程式碼修補程式**&#x200B;一次準備每個可用的修補程式。 AEM Sites Optimizer會為每個修正建立貼標籤的GitHub問題，並自動開啟包含程式碼變更的連結提取請求，供您的團隊檢閱、測試和合併。

如果您沒有準備程式碼修補程式的許可權，或網站未針對此進行完整設定（例如，未連執行緒式碼儲存區域，或仍在產生修補程式），此動作會停用。 在各種情況下，Sites Optimizer都會在「停用」按鈕旁邊說明原因。

## 追蹤已準備的程式碼修補程式

準備好程式碼修補程式後，您可以從Core Web Vitals詳細資料頁面上的「**已部署**」標籤、「**目前**」和「**已忽略**」標籤旁邊管理這些修補程式，並採取後續步驟。 修補程式的狀態反映其提取要求是否已合併，而不僅僅是產生 — 問題只有在修正程式實際合併至程式碼基底後，才會移至&#x200B;**已部署**。

## 另請參閱

* [核心網頁指標機會](/help/documentation/opportunities/core-web-vitals.md#auto-optimize)
* [部署至作者檔案](/help/documentation/opportunities/deploying-to-author.md)
