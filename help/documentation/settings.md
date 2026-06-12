---
title: Sites Optimizer 設定
description: 了解如何設定 Sites Optimizer 設定並與其他工具整合。
TQID: https://experienceleague.adobe.com/eznjSHZgAmCh-ek-XE-lLtuoGJxC0yY4UVrmPjc0KYo
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 84a1ae98d67bc02ab272131194511efbeccab492
workflow-type: tm+mt
source-wordcount: 749
ht-degree: 100%

---

# Sites Optimizer 設定

![Sites Optimizer 設定](./assets/settings/hero.png){align="center"}

Sites Optimizer 設定是您設定 Sites Optimizer 體驗的中樞。

## Google Search Console

![Google Search Console 的 Sites Optimizer 設定](./assets/settings/google-search-console.png){align="center"}

AEM Sites Optimizer 中的 Google Search Console 設定連接器可讓您分析關鍵 SEO 量度，例如搜尋排名、點按率和核心網頁指標。 透過讓 Google Search Console 保持連接，您可以利用 JSON 分析來發現最佳化機會並提高網站績效。

若要設定此連接器，您必須擁有能以系統管理員身分存取該網域之 Google Search Console 的認證。

## 連線至 AEM Sites

以下指南將說明如何將您現有的 Edge Delivery Services (EDS) 網站連結至 AEM Sites Optimizer。 開始之前，請確定您的 EDS 網站已設定且正常運作，此連線專供 AEM Sites Optimizer 存取您的內容。

此連線需要兩個步驟：

1. 提供您的程式碼存放庫 URL 以及內容來源 URL。
2. 授予 AEM Sites Optimizer 權利存取您的內容來源。

### 步驟 1：將您的程式碼存放庫連結至您的內容來源

在 AEM Sites Optimizer 中，導覽至&#x200B;**「設定」→「連線至 AEM Sites」**&#x200B;並輸入下列資料：

- **程式碼存放庫 URL**：您 EDS 網站的 GitHub URL，例如：
  `https://github.com/owner/repo`

- **內容來源 URL**：支援您 EDS 網站的 SharePoint 資料夾或 Google 雲端硬碟資料夾的 URL，例如：
  `https://drive.google.com/drive/folders/...` 或 `https://myorg.sharepoint.com/...`

輸入內容來源 URL 後，AEM Sites Optimizer 會偵測您的內容來源類型，並顯示下列相關存取指示。

### 步驟 2：授予內容來源的存取權

請依照符合您內容來源的區段完成此步驟。

#### SharePoint：Adobe 網域

![顯示「Adobe SharePoint 網域無須任何動作」的「連線至 AEM Sites」對話框](./assets/settings/connect-content-and-drive.png){align="center"}

如果您的內容來源 URL 使用 Adobe SharePoint 網域，則無須進一步動作。 已設定存取權。 按下「**儲存**」以完成連線。

#### SharePoint：自訂網域

如果內容來源 URL 使用您組織的 SharePoint 網域，您需要註冊 Azure 應用程式並提供其憑證給 AEM Sites Optimizer。

##### 您將需要的內容

- 在 Azure 入口網站註冊應用程式的權限，或可代為註冊應用程式的連絡人。
- 授予 API 同意的租用戶管理員權限，或可代為核准 API 同意的管理員。

##### 步驟 2a：在 Azure 中註冊應用程式

1. 導覽至 **「Azure 入口網站」→「Microsoft Entra ID」→「應用程式註冊」→「新註冊」**。
2. 為應用程式命名，例如：`AEM Sites Optimizer`。
3. 保留其他所有預設值，按下「**註冊**」。
4. 在「**概觀**」頁面上，記下以下內容：
   - **應用程式 (用戶端) 識別碼**
   - **目錄 (租用戶) 識別碼**

##### 步驟 2b：新增 API 權限

1. 導覽至&#x200B;**「API 權限」→「新增權限」→「Microsoft Graph」→「應用程式權限」**。
2. 新增下列兩項：
   - `Sites.Selected`：特定 SharePoint 網站集合的限定範圍存取權。
   - `Files.SelectedOperations.Selected`：無須登入使用者的檔案存取權。
3. 以上兩項皆要按下「**授予管理員同意**」。

![Azure API 權限顯示 Sites.Selected 和 Files.SelectedOperations.Selected 已授予存取權](./assets/settings/app-permissions.png){align="center"}

>[!NOTE]
>
>授予管理員同意需要租用戶管理員權限。 如果您沒有此權限，請先要求 IT 或 Azure 管理員完成此步驟，再繼續進行。

##### 步驟 2c：建立用戶端密碼

應用程式註冊的![「Azure 憑證與密碼」頁面](./assets/settings/create-credentials.png){align="center"}

1. 導覽至&#x200B;**「憑證與密碼」→「新增用戶端密碼」**。
2. 設定說明和到期日後，按下「**新增**」。
3. 立即複製密碼值，此值僅顯示一次。

##### 步驟 2d：授予應用程式存取 SharePoint 網站的存取權

您可以使用 Microsoft Graph Explorer、PowerShell 或直接透過 Graph API 呼叫，授予應用程式存取權。

導覽至「[Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)」，使用您的 Microsoft 帳戶登入，並執行以下請求：

1. 尋找您的網站識別碼：

```
GET https://graph.microsoft.com/v1.0/sites/{tenant}.sharepoint.com:/sites/{site-name}
```

1. 從回應中複製 `id` 後，授予網站層級的存取權：

```
POST https://graph.microsoft.com/v1.0/sites/{siteId}/permissions
```

請求內容：

```json
{
  "roles": ["write"],
  "grantedToIdentities": [{
    "application": {
      "id": "{your-client-id}",
      "displayName": "{Your app name}"
    }
  }]
}
```

##### 步驟 2e：在 AEM Sites Optimizer 中輸入認證

![顯示「SharePoint 認證」欄位的「連線至 AEM Sites」對話框](./assets/settings/add-sharepoint-credentials.png){align="center"}

在「**連線至 AEM Sites**」對話框中，透過「**SharePoint 連線內容存放庫**」輸入下列內容：

- **租用戶識別碼 (Azure AD)**：來自「應用程式註冊」→「概觀」。
- **用戶端識別碼 (應用程式註冊)**：來自「應用程式註冊」→「概觀」。
- **用戶端密碼**：已在步驟 2c 建立。

按下「**驗證連線**」以確認存取，接著按下「**儲存**」。

#### Google 雲端硬碟

![「連線至 AEM Sites」對話框，顯示共用存取權的 Google 雲端硬碟服務帳戶](./assets/settings/validate-eds-google.png){align="center"}

1. 在 Google 雲端硬碟中，用滑鼠右鍵按下支援您 EDS 網站的資料夾，並選取「**共用**」。
2. 在「**新增人員和群組**」欄位中，輸入「**連線至 AEM Sites**」對話框中顯示的服務帳戶電子郵件：
   `experience-success-studio@helix-225321.iam.gserviceaccount.com`
3. 將權限等級設定為「**編輯者**」。
4. 取消勾選「**通知共用對象**」，接著按下「**共用**」。

共用完成後，在對話框中按下「**驗證連線**」，接著按下「**儲存**」。
