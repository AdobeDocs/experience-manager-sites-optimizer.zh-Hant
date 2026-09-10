---
title: Sites Optimizer 試用版
description: 現有 AEM Sites 客戶可開始使用 AEM Sites Optimizer 試用版。
source-git-commit: 5bd55dcc380f0721fb9818413207c22e21e8299b
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 59%

---


# Sites Optimizer 試用版

使用針對現有&#x200B;**Sites Optimizer客戶（Edge Delivery Services、Cloud Services和Managed Services）**&#x200B;的此試用版，開始使用AEM Sites。 您的網域資料已預先上線，可立即開始最佳化。 以下影片逐步說明試用版體驗，並示範如何開始使用。

>[!IMPORTANT]
>
>開始之前，請確認您的網站符合下列需求：
>
>* 這是以AEM Sites （Edge Delivery Services、Cloud Service或Managed Services）為基礎所建置。
>* 這是一個生產網站，而不是開發、QA、測試、作者或預覽環境。
>* 可供公開存取，且不會位於登入後面。
>* 它使用AEM Sites前端傳送。 目前不支援Headless傳送。

>[!VIDEO](https://video.tv.adobe.com/v/3483298/?captions=chi_hant&learn=on&enablevpops)

>[!TIP]
>
> 若有任何問題或需求，請連絡 [siteoptimizer-now@adobe.com](mailto:siteoptimizer-now@adobe.com)。

## 立即開始試用！

請依照下列步驟開始使用您的試用版：

1. 使用您的 AEM Sites IMS 組織識別碼登入 [www.sitesoptimizer.live](http://www.sitesoptimizer.live/)。
2. 檢視關鍵量度，例如頁面瀏覽量、網頁載入時間與參與度，以及根據影響程度優先順序排序的熱門最佳化機會。
3. 探索三種現有的機會類型：[損壞的反向連結](./opportunities/broken-backlinks.md)、[Core Web Vitals](./opportunities/core-web-vitals.md) 以及[缺少替代文字](./opportunities/missing-alt-text.md)。
4. 每個機會可審閱最多三個已識別的問題。 您可使用 AI 生成的建議，準備好後直接將最佳化的內容部署至您的 AEM 環境。
5. 隨時可升級至完整授權版，解鎖更多機會。

## 試用版所提供的功能

試用版包含下列內容：

* 三種機會類型：[損壞的反向連結](./opportunities/broken-backlinks.md)、[Core Web Vitals](./opportunities/core-web-vitals.md) 以及[缺少替代文字](./opportunities/missing-alt-text.md)。
* 每個機會每月最多三個問題。
* 每個問題的完整工作流程：自動識別、自動建議以及自動最佳化。
  * **自動識別**：使用多個資料來源偵測您網站上的問題。
  * **自動建議**：針對每個問題，提供規範性、AI 生成的建議。
  * **自動最佳化**：核准後，將修正內容直接部署至您的製作環境。 更新會遵循您現有的工作流程，讓您的團隊可透過 AEM 順利審閱並發佈。

## 為Edge Delivery試用網站啟用自動修正

了解試用版客戶如何啟用在Google Drive或SharePoint中撰寫的Edge Delivery Services (EDS)網站上，針對自動修正建議的&#x200B;**部署至作者**&#x200B;動作。

>[!NOTE]
>
>這項要求僅適用於網站是使用Google Drive或SharePoint編寫的試用組織。 付費客戶以及在「行人穿越道」或「黑暗巷」中編寫的網站不受影響。

試用客戶必須屬於&#x200B;**ASO-EDS-Autofix-Users** IMS群組。 如果群組不存在，則組織的管理員可以建立群組並新增您。

1. 登入[Adobe Admin Console](https://adminconsole.adobe.com/)。
1. 選取&#x200B;**使用者** > **使用者群組**。
1. 選取&#x200B;**新增使用者群組**。
1. 針對&#x200B;**使用者群組名稱**，請完全輸入：

   ```
   ASO-EDS-Autofix-Users
   ```

   >[!IMPORTANT]
   >
   > 群組名稱必須完全相符，包括大小寫。 它區分大小寫相符，因此不同的拼字或大小寫（例如，`ASO-EDS-Autofix-users`）無法運作。 建立群組後，請勿重新命名群組。

1. 選取「**儲存**」。

   ![在Adobe Admin Console中建立新的使用者群組對話方塊，使用者群組名稱欄位設為ASO-EDS-Autofix-Users](./assets/trial/create-user-group.png){align="center"}

1. 開啟新群組並選取&#x200B;**新增使用者**。
1. 輸入每個應該能夠部署自動修正的人員的電子郵件地址或使用者名稱，然後選取&#x200B;**儲存**。

   ![在Adobe Admin Console中將使用者新增至此使用者群組對話方塊](./assets/trial/add-users-to-group.png){align="center"}

如果您是群組的成員，則會啟用&#x200B;**部署到作者**&#x200B;按鈕。 如果您尚未成為成員，**部署至作者**&#x200B;已停用，工具提示會要求您連絡系統管理員，以將您新增至群組。 管理員將您新增至群組後，請先登出再重新登入Sites Optimizer，這樣您的工作階段就會選取新的群組成員資格。

## 常見問題

請閱讀下列內容，了解有關 AEM Sites Optimizer 試用版的常見問題解答。

+++什麼是 AEM Sites Optimizer?

[AEM Sites Optimizer](/help/home.md) 是 AI 優先的應用程式，可識別您網站上的問題、提供規範性建議，並協助您修正問題，以提高流量贏取、參與度與轉換率。

+++
+++誰可以使用此試用版?

AEM Sites 現有客戶 (Edge Delivery Services、Cloud Services 及 Managed Services 客戶)。

+++
+++要如何存取試用版?

前往 [www.sitesoptimizer.live](http://www.sitesoptimizer.live/) 並使用您的 AEM Sites IMS 組織識別碼登入。

+++
+++此試用版是否需要付費?

否。 現有 AEM Sites 客戶可免費使用此試用版。

+++
+++試用版是否有授權使用期限?

否。 此試用版不以時間為限制。 此試用版的使用期限則基於可用的機會類型以及問題的數量。
+++
+++修正所有問題後會發生什麼事?

Sites Optimizer 會持續識別影響績效的問題。 免費試用版每月僅新增問題一次。 升級版本以持續稽核並最佳化。

+++
+++要如何存取更多機會?

您可透過產品體驗提供的升級功能或連絡銷售 CTA，或寄送電子郵件至 [siteoptimizer-now@adobe.com](mailto:siteoptimizer-now@adobe.com)。

+++
+++我在ASO-EDS-Autofix-Users群組中，但是仍然停用部署到作者。 我應檢查哪些專案？

登出並重新登入 — 當您登入時，會讀取群組成員資格。 同時確認群組名稱的拼字與大寫剛好是`ASO-EDS-Autofix-Users`，而且是在網站所屬的相同組織中建立的。

+++
+++ASO-EDS-Autofix-Users群組要求是否適用於所有Edge Delivery Services網站？

否。 它僅適用於在&#x200B;**Google Drive**&#x200B;或&#x200B;**SharePoint**&#x200B;中編寫的試用網站。 在&#x200B;**Crossswalk**&#x200B;或&#x200B;**暗巷**&#x200B;中編寫的網站以及所有&#x200B;**付費**&#x200B;網站不受影響。

+++

<!--
CARDS
* ./opportunities/core-web-vitals.md
  {title=Core web vitals}
  {image=../assets/common/card-performance.png}
* ./opportunities/missing-alt-text.md
  {title=Missing alt text}
  {image=../assets/common/card-arrows.png}
* ./opportunities/broken-backlinks.md
  {title=Broken backlinks}
  {image=../assets/common/card-arrows.png}
-->

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Core web vitals">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./opportunities/core-web-vitals.md" title="核心網頁指標" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-performance.png" alt="核心網頁指標"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./opportunities/core-web-vitals.md" target="_blank" rel="referrer" title="核心網站指標">核心網頁指標</a>
                    </p>
                    <p class="is-size-6">了解核心網頁指標機會，以及如何使用此機會來改進流量贏取。</p>
                </div>
                <a href="./opportunities/core-web-vitals.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解更多</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Missing alt text">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./opportunities/missing-alt-text.md" title="缺少替代文字" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-arrows.png" alt="缺少替代文字"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./opportunities/missing-alt-text.md" target="_blank" rel="referrer" title="缺少替代文字">缺少替代文字</a>
                    </p>
                    <p class="is-size-6">了解缺少替代文字機會，以及如何使用此機會來提高您網站上的參與度。</p>
                </div>
                <a href="./opportunities/missing-alt-text.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解更多</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Broken backlinks">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./opportunities/broken-backlinks.md" title="損壞的反向連結" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-arrows.png" alt="損壞的反向連結"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./opportunities/broken-backlinks.md" target="_blank" rel="referrer" title="損壞的反向連結">損壞的反向連結</a>
                    </p>
                    <p class="is-size-6">了解損壞的反向連結機會，以及如何使用此機會來改進流量贏取。</p>
                </div>
                <a href="./opportunities/broken-backlinks.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解更多</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->
