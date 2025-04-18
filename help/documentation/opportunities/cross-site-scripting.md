---
title: 跨網站指令碼機會文件
description: 了解跨網站指令碼機會並識別和解決網站安全性漏洞。
badgeSecurityPosture: label="安全態勢" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="安全態勢"
source-git-commit: c99bd0ab418c1eb0693f39ea16ee41f8a1263099
workflow-type: ht
source-wordcount: '132'
ht-degree: 100%

---


# 跨網站指令碼機會

![跨網站機會](./assets/cross-site-scripting/hero.png){align="center"}

跨網站指令碼機會可識別並修復網站程式碼中的漏洞，攻擊者可能會利用這些漏洞將惡意指令碼注入到其他使用者檢視的網頁中。這些指令碼可以竊取敏感資訊 (例如工作階段 Cookie)，或代表使用者執行操作 (例如變更使用者的密碼)。

## 自動識別

![自動識別跨網站機會](./assets/cross-site-scripting/auto-identify.png){align="center"}

* **有漏洞的程式碼** - 任何有漏洞而會遭到跨網站指令碼攻擊的程式碼。
* **重現連結** - 漏洞發現所在頁面的連結。

## 自動建議

![自動建議跨網站機會](./assets/cross-site-scripting/auto-suggest.png){align="center"}

* **建議的修正** - 關於如何修正漏洞的 AI 生成建議。

## 自動最佳化

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

>[!BEGINTABS]

>[!TAB 部署最佳化]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB 請求核准]

{{auto-optimize-request-approval}}

>[!ENDTABS]
