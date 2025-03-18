---
title: CORS設定機會檔案
description: 瞭解CORS設定機會，以及識別和修正網站安全漏洞。
badgeSecurityPosture: label="安全態勢" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="安全態勢"
source-git-commit: ab2d75b1d986d83e3303e29a25d2babd1598394a
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 2%

---


# CORS設定機會

![CORS設定機會](./assets/cors-configuration/hero.png){align="center"}

正確設定跨原始資源共用(CORS)對於保護Web應用程式免受未經授權的資料存取至關重要。 當`Access-Control-Allow-Origin`標頭設為`*`時，任何網域都可以要求及接收回應，可能會將敏感資訊暴露給攻擊者。 這可藉由實作受信任網域的受控允許清單或在不需要時停用CORS來加強安全性。 確保安全的CORS設定，有助於保護私人內容，同時維持授權使用者的順暢存取。

## 自動識別

![自動識別CORS設定機會](./assets/cors-configuration/auto-identify.png){align="center"}

自動識別會掃描您的網站以找出CORS錯誤設定，並偵測容易受到未授權存取影響的URL。 這些URL以及下列詳細資料列於頂端表格中：

* **頁面前置詞** — 易受CORS錯誤設定影響的URL路徑前置詞。
* **頁面範例** — 有可能未經授權存取的範例URL。

## 自動建議

![自動建議CORS設定機會](./assets/cors-configuration/auto-suggest.png){align="center"}

自動建議提供&#x200B;**應用程式程式碼檔案**&#x200B;及其&#x200B;**行**，以供檢閱可能設定鬆散CORS原則。


## 自動最佳化[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}



>[!BEGINTABS]

>[!TAB 部署最佳化]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB 要求核准]

{{auto-optimize-request-approval}}

>[!ENDTABS]
