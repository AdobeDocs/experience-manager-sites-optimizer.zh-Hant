---
title: 網站權限機會文件
description: 了解網站權限機會，以及如何使用它來提高網站的安全性。
badgeSecurityPosture: label="安全態勢" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="安全態勢"
source-git-commit: cb64a34b758de8f5dcea298014ddd0ba79a24c17
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 79%

---


# 網站權限機會

![網站權限機會](./assets/website-permissions/hero.png){align="center"}

網站權限機會可將網站權限最佳化，這對於讓 AEM 環境保持安全且易於管理至關重要。此機會可讓您移除範圍過大的權限 (例如 `/` 或 `/content` 等通用路徑上的 `jcr:all` 權限) 並讓使用者存取權與最低權限原則保持一致，藉此來調整存取控制。透過簡化權限和消除冗餘，您可以降低安全風險、提高可維護性並防止日後發生錯誤設定的情況。在AEM安全性許可權控制檯或您的程式碼存放庫中檢閱和更新許可權。 這麼做可確保服務使用者只擁有他們真正需要的存取權。

## 自動識別

![自動識別網站權限](./assets/website-permissions/auto-identify.png){align="center"}

**網站權限機會**&#x200B;功能會自動識別並列出

* **使用者** – 具有可疑權限的使用者帳戶。
* **路徑** — 使用頂端的索引標籤，依狀態組織和篩選商機。
* **許可權** — 懷疑的許可權。
* **問題** - 指出影響權限的問題類型。

## 自動建議

![自動建議網站漏洞](./assets/website-permissions/auto-suggest.png){align="center"}

自動建議會在「**建議的權限**」欄位中提供 AI 生成的建議，以讓您用安全的替代權限取代所標記的權限。

## 自動最佳化

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

![自動最佳化網站權限](./assets/website-permissions/auto-optimize.png){align="center"}

Sites Optimizer Ultimate 新增了針對所發現的漏洞部署自動最佳化功能的能力。

>[!BEGINTABS]

>[!TAB 部署最佳化]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB 請求核准]

{{auto-optimize-request-approval}}

>[!ENDTABS]
