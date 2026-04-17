---
title: 損壞的反向連結機會文件
description: 了解損壞的反向連結機會，以及如何使用它來改進流量贏取。
badgeTrafficAcquisition: label="流量贏取" type="Caution" url="../../opportunity-types/traffic-acquisition.md" tooltip="流量贏取"
source-git-commit: 97e61d3061fb68225eece98ba0f94affb08be9e3
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 30%

---


# 損壞的反向連結機會

<!--![Broken backlinks opportunity](./assets/broken-backlinks/hero.png){align="center"}-->

>[!VIDEO](https://video.tv.adobe.com/v/3483250/?learn=on&enablevpops)

中斷的背景連結機會會識別指向網站上不存(404)頁面的外部連結。 這些連結會導致引薦流量損失和SEO價值減少，因為搜尋引擎會仰賴反向連結來評估相關性和授權。 若沒有適當的重新導向，URL變更、內容移除或頁面就無法再使用時，就會發生這些問題。 AEM Sites Optimizer會識別所有中斷的背景連結、提供特定的AI建議，並啟用一鍵式部署來修正這些建議，所有這些都在單一集中檢視中。

## 自動識別

<!--![Auto-identify broken backlinks](./assets/broken-backlinks/auto-identify.png){align="center"}-->

AEM Sites Optimizer會持續掃描外部資料來源，偵測指向網站上不存404頁面的反向連結。 資料會從多個來源彙總，包括Google搜尋主控台、[作業遙測](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/sites/operational-telemetry-for-aem-as-a-cloud-service)以及協力廠商SEO平台。 自動識別機會會識別連結至失效URL的外部網域，並根據影響（包括網域授權和預期流量及連結權益損失）來排定其優先順序。

此機會列出所有已識別的問題，包括下列詳細資訊：

* **反向連結網域和頁面** — 包含中斷連結的外部頁面或網域。
* **優先順序** — 高、中或低，表示中斷的連結對SEO處理序的影響。
* **目標URL已中斷** — 您的網站上已連結不存在的URL。

## 自動建議

<!--![Auto-suggest broken backlinks](./assets/broken-backlinks/auto-suggest.png){align="center"}-->

對於已識別的每個中斷回連結，AEM Sites Optimizer會建議最適合的目的地，以還原流量和SEO值。 它會透過分析以下專案來決定反向連結的意圖：

* URL結構和權杖
* 錨點文字
* 引用頁面的標題和內容

此意圖會與現有網站內容比對，以識別最相關的目的地頁面。 每個中斷的URL都會對應至精確的取代頁面或最相關的頁面。 如果無法確定合適的目的地，則會出現問題以供手動檢閱。

>[!BEGINTABS]

>[!TAB AI 原理]

<!--![AI rationale on autosuggestion of broken backlinks](./assets/broken-backlinks/auto-suggest-ai-rationale.png){align="center"}-->

選取&#x200B;**資訊**&#x200B;圖示可檢視所建議 URL 的 AI 原理。 該原理會解釋為何 AI 認為所建議的 URL 最適合已損壞的連結使用。 這可以協助您了解 AI 的決策過程，並做出接受或拒絕建議的明智決定。

>[!TAB 編輯目標 URL]

<!--![Edit suggested URL of broken backlinks](./assets/broken-backlinks/edit-target-url.png){align="center"}-->

如果您不同意 AI 生成的建議，則可以透過選取&#x200B;**編輯圖示**&#x200B;來編輯建議的 URL。 您可以利用編輯功能手動輸入您認為最適合無效連結的 URL。 Sites Optimizer 也會列出其認為您網站上可能適合無效連結的任何其他 URL。

>[!TAB 忽略項目]

<!--![Ignore broken backlinks](./assets/broken-backlinks/ignore.png){align="center"}-->

您可以選擇忽略具有損壞目標 URL 的項目。 選取![刪除圖示或忽略圖示](https://spectrum.adobe.com/static/icons/ui_18/CrossSize500.svg)可從機會清單中移除無效的反向連結。 使用機會頁面頂端的「**已忽略**」索引標籤，可以重新啟用已忽略的無效反向連結。

>[!ENDTABS]

## 自動最佳化

<!--[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}-->

在檢閱並核准建議後，您可以按一下&#x200B;**部署最佳化**。 接著AEM Sites Optimizer會根據您實作中管理重新導向的方式，將修正套用至編寫環境。 AEM作者可從內容管理系統(CMS)發佈變更。

根據設定，修正會在現有部署工作流程中套用為內容或程式碼變更。 最佳化程式包含下列步驟：

* **驗證** — 確保變更如預期般運作，且在部署之前不會引入回歸。
* **部署** — 透過現有程式套用變更，例如AEM中的內容更新或透過CI/CD管道部署程式碼。
* **許可權檢查** — 驗證使用者是否擁有部署變更的適當許可權。 如果沒有，則會提供其他輸出，例如可下載的重新導向清單或程式碼修補程式。

此程式可確保重新導向受到精確實作、在發行前經過驗證，並與現有設定和治理程式保持一致。
