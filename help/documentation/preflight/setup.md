---
title: 預檢設定
description: 瞭解如何設定AEM Sites Optimizer的Preflight擴充功能。
source-git-commit: 6e177ef6b9d121ac7484ae118037c7e542f981d8
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 96%

---


# 預檢設定

要使用 AEM Sites Optimizer 預檢機會識別，需要先在通用編輯器、文件型預覽或 AEM Cloud Service 中設定預檢擴充功能，以便在頁面發佈前先對其進行預檢稽核。

## 啟用使用者存取

要使用預檢擴充功能，請確認您的使用者在 [Adobe Admin Console](https://adminconsole.adobe.com) 中至少被指派至以下其中一個 AEM Sites Optimizer 產品設定檔：

* AEM Sites Optimizer - 自動建議使用者
* AEM Sites Optimizer - 自動最佳化使用者

## 啟用預檢擴充功能

>[!BEGINTABS]

>[!TAB 通用編輯器]

若要在通用編輯器中設定預檢，請依照以下步驟進行：

1. 在此開啟 **Extension Manager**：
   [https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor?lang=zh-Hant](https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor)
1. 找到 **AEM Sites Optimizer 預檢擴充功能**&#x200B;並提出啟用的請求。
1. **Adobe AEM 團隊**&#x200B;會在審閱後為您的組織啟用此擴充功能。
1. 啟用擴充功能後，在 **通用編輯器**中開啟一個頁面，例如：
   `https://author-p12345-e123456.adobeaemcloud.com/ui#/@org/aem/universal-editor/canvas/author-p12345-e123456.adobeaemcloud.com/content/en/example/home.html`
1. **預檢擴充功能**&#x200B;將出現在&#x200B;**側邊欄中**。
1. 在側邊欄中選取&#x200B;**「預檢擴充功能」**，針對目前頁面開始進行&#x200B;**預檢稽核**。

>[!TAB 文件型製作]

若要設定對文件型製作進行預檢，請依照下列步驟進行：

1. 在 Edge Delivery Services 專案的 GitHub 存放庫中，將以下設定新增至 `/tools/sidekick/config.json`：

   ```json
   {
     "plugins": [
       {
         "id": "preflight",
         "titleI18n": {
           "en": "Preflight"
         },
         "environments": ["preview"],
         "event": "preflight"
       }
     ]
   }
   ```

1. 建立新檔案 `/tools/sidekick/aem-sites-optimizer-preflight.js` 並新增以下內容：

   ```javascript
   (function () {
     let isAEMSitesOptimizerPreflightAppLoaded = false;
     function loadAEMSitesOptimizerPreflightApp() {
       const script = document.createElement('script');
       script.src = 'https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=plugin';
       script.onload = function () {
         isAEMSitesOptimizerPreflightAppLoaded = true;
       };
       script.onerror = function () {
         console.error('Error loading AEMSitesOptimizerPreflightApp.');
       };
       document.head.appendChild(script);
     }
   
     function handlePluginButtonClick() {
       if (!isAEMSitesOptimizerPreflightAppLoaded) {
         loadAEMSitesOptimizerPreflightApp();
       }
     }
   
     // Sidekick V1 extension support
     const sidekick = document.querySelector('helix-sidekick');
     if (sidekick) {
       sidekick.addEventListener('custom:preflight', handlePluginButtonClick);
     } else {
       document.addEventListener('sidekick-ready', () => {
         document.querySelector('helix-sidekick')
           .addEventListener('custom:preflight', handlePluginButtonClick);
       }, { once: true });
     }
   
     // Sidekick V2 extension support
     const sidekickV2 = document.querySelector('aem-sidekick');
     if (sidekickV2) {
       sidekickV2.addEventListener('custom:preflight', handlePluginButtonClick);
     } else {
       document.addEventListener('sidekick-ready', () => {
         document.querySelector('aem-sidekick')
           .addEventListener('custom:preflight', handlePluginButtonClick);
       }, { once: true });
     }
   }());
   ```

1. 更新 `/scripts/scripts.js` 中的函數 `loadLazy()` 以便匯入預覽 URL 的預檢指令碼：

   ```javascript
   if (window.location.href.includes('.aem.page')) {
      import('../tools/sidekick/aem-sites-optimizer-preflight.js');
   }
   ```

1. 開啟要稽核的頁面之預覽 URL (`*.aem.page`)。
1. 在 **Sidekick** 中，按一下&#x200B;**「預檢」**&#x200B;按鈕，開始對目前頁面進行稽核。

>[!TAB AEM Sites 頁面編輯器]

若要在 AEM Sites 頁面編輯器中使用預檢，您可以在網頁瀏覽器中建立書籤小程式。請依照下列步驟操作：

1. 在網頁瀏覽器中顯示您的&#x200B;**書籤列**：

   * 按下 **Ctrl+Shift+B** (Windows) 或 **Cmd+Shift+B** (Mac)。

!. 在瀏覽器中建立新書籤：

* 在書籤列上按一下右鍵，然後選取「**新頁面**」或「**新增書籤**」。
* 在「**位址 (URL)**」欄位中，貼上以下程式碼：

```javascript
javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=aem-cloud-service';document.head.appendChild(script);})();
```

1. 將書籤命名為「**預檢**」(或任何您喜歡的名稱)。
1. 在 **AEM Sites 頁面編輯器**&#x200B;中開啟您要稽核之頁面的預覽 URL (`*.aem.page`)。
1. 在書籤列中按一下「**預檢**」書籤，以便開始稽核目前頁面。

>[!ENDTABS]

## 最佳做法

執行預檢稽核時，請牢記以下準則：

* 在發佈到生產環境前，請務必先在&#x200B;**中繼或預覽頁面**&#x200B;上執行稽核。
* 優先解決&#x200B;**影響重大的問題**，例如連結失效、缺少 H1 標記或不安全的連結。
* 在執行稽核之前，請確保受保護的中繼環境&#x200B;**已啟用驗證**。
* 審閱並套用&#x200B;**後設標記推薦**&#x200B;以提升 SEO 效能。
