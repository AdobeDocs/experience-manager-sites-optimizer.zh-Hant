---
title: Sites Optimizer 設定
description: 了解如何設定 Sites Optimizer 設定並與其他工具整合。
TQID: https://experienceleague.adobe.com/eznjSHZgAmCh-ek-XE-lLtuoGJxC0yY4UVrmPjc0KYo
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
source-git-commit: 37d90154e6868ee392bf1b779b2bf3697112b7ce
workflow-type: tm+mt
source-wordcount: '1960'
ht-degree: 39%
---
# Sites Optimizer 設定

![Sites Optimizer 設定](./assets/settings/hero.png){align="center"}

Sites Optimizer 設定是您設定 Sites Optimizer 體驗的中樞。

## Google Search Console

![Google Search Console 的 Sites Optimizer 設定](./assets/settings/google-search-console.png){align="center"}

AEM Sites Optimizer 中的 Google Search Console 設定連接器可讓您分析關鍵 SEO 量度，例如搜尋排名、點按率和核心網頁指標。 透過讓 Google Search Console 保持連接，您可以利用 JSON 分析來發現最佳化機會並提高網站效能。

若要設定此連接器，您必須擁有能以系統管理員身分存取該網域之 Google Search Console 的認證。

## 連線至 AEM Sites

以下指南將說明如何將您現有的 Edge Delivery Services (EDS) 網站連結至 AEM Sites Optimizer。 開始之前，請確定您的 EDS 網站已設定且正常運作，此連線專供 AEM Sites Optimizer 存取您的內容。

此連線需要兩個步驟：

1. 提供您的程式碼存放庫 URL 以及內容來源 URL。
2. 授予 AEM Sites Optimizer 存取您的內容來源的權限。

### 步驟 1：連結您的程式碼存放庫和內容來源

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
3. 立即複製秘密值，此值僅顯示一次。

##### 步驟 2d：授予應用程式 SharePoint 網站的存取權

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
   `aem-sites-optimizer@adbe-gcp0843.iam.gserviceaccount.com`
3. 將權限等級設定為「**編輯者**」。
4. 取消勾選「**通知共用對象**」，接著按下「**共用**」。

共用完成後，在對話框中按下「**驗證連線**」，接著按下「**儲存**」。

## 管理使用者許可權

控制誰可以存取Sites Optimizer中的網站，以及他們可以使用網站做什麼。 存取權是由您授予每個人的一組小型獨立&#x200B;*功能* （檢視、編輯、部署、設定及管理使用者）所建置。

存取權是&#x200B;**累加**：人員的許可權是已授予他們所有許可權的總和。 沒有「拒絕」，因此授與內容不會相互衝突或取消。 若要減少某人的存取權，請移除授權而非嘗試覆寫授權。

### 存取權的授與方式

使用者有兩種存取許可權方式，而且這兩種方式可搭配使用：

- **全組織存取權** — 由您的Adobe組織管理員在[Adobe Admin Console](https://adminconsole.adobe.com/)中指派。 它適用於您組織中的每個網站。 適合所有地方都需要相同存取許可權的使用者。
- **網站層級存取** — 已在Sites Optimizer中指派給&#x200B;**設定→許可權**&#x200B;頁面。 它適用於單一網站，可依需求隨意擴大或縮小。 不需要Admin Console存取權。

>[!NOTE]
>
>兩個圖層相加。 擁有組織範圍檢視存取許可權，且在一個網站上被授予編輯許可權的人可以檢視每個網站並編輯該網站。 若要將人員限制在單一網站，請確定他們不會同時擁有全組織的角色。

#### 組織範圍角色(Admin Console)

全組織存取權來自[AEM Sites Optimizer](https://adminconsole.adobe.com/)中指派的兩個&#x200B;**Adobe Admin Console**&#x200B;產品角色之一：

- **ASO管理員** — 每個網站的完整存取權，包括&#x200B;**管理使用者**。 管理員可以開啟任何網站的&#x200B;**許可權**&#x200B;頁面，並指派存取權給其他網站。
- **ASO使用者** — 每個網站的僅檢視存取權。 沒有變更，也沒有使用者管理。

若要指派角色，您必須是組織的&#x200B;**系統管理員**，或AEM Sites Optimizer的&#x200B;**產品管理員**。

1. 登入[Adobe Admin Console](https://adminconsole.adobe.com/)。
1. 移至&#x200B;**產品**&#x200B;並選取&#x200B;**AEM Sites Optimizer**。
1. 開啟&#x200B;**使用者**&#x200B;索引標籤，並透過電子郵件新增使用者（或選取現有使用者）。
1. 按一下&#x200B;**+** （新增）圖示以新增產品設定檔，然後選擇產品設定檔。

   ![在Adobe Admin Console中為使用者選擇產品設定檔](./assets/settings/permissions-admin-console-product-profile.png){align="center"}

1. 按一下「**下一步**」。
1. 選擇角色 — **ASO管理員**&#x200B;以取得完整存取權，或&#x200B;**ASO使用者**&#x200B;以取得僅供檢視的存取權 — 然後按一下&#x200B;**套用**。

   ![在Adobe Admin Console中選取ASO管理員角色](./assets/settings/permissions-admin-console-aso-manager-role.png){align="center"}

   ![在Adobe Admin Console中選取ASO使用者角色](./assets/settings/permissions-admin-console-aso-user-role.png){align="center"}

如需新增使用者的詳細資訊，請參閱[內建使用者](setup/onboard-users.md)。

>[!IMPORTANT]
>
>只有組織管理員可以授與整個組織的&#x200B;**管理使用者**。 在網站上具有&#x200B;**管理使用者**&#x200B;的成員可以指派該網站的存取權，但無法建立全組織的&#x200B;**ASO管理員**。

### 功能層級

每項功能都可控制一種動作。 它們是獨立的 — 例如，您可以授與部署而不使用編輯。

| 功能 | 它允許 | 不允許的內容 |
|---|---|---|
| 檢視 | 檢視網站資料 — 商機、建議、修正、報告和設定 — 而不變更任何專案。 | 任何變更。 |
| 編輯 | 建立並變更機會和建議（應該變更的內容）。 | 發佈變更、變更設定或管理使用者。 |
| 部署 | 將修正發佈到網站，然後復原這些修正。 | 管理使用者。 |
| 設定 | 變更網站的設定和連線。 | 發佈修正或管理使用者。 |
| 管理使用者 | 授予或撤銷其他成員對網站的存取權。 | 管理該人員尚無法存取的網站。 |

>[!NOTE]
>
>**檢視一律包括在內。** 每個授權都會自動包含檢視 — 您無法管理、設定、編輯或部署您無法看到的內容。 因此，無法自行移除檢視。 若要完全移除某人的存取權，請移除成員（請參閱下方的[編輯或移除成員](#edit-or-remove-a-member)），而非取消勾選每個權能。

### 機會型別的存取範圍

您可以在單一網站上授予&#x200B;**特定機會型別** （例如，Core Web Vitals或中斷的內部連結）的檢視、編輯和部署許可權，而非整個網站。 如此一來，使用者就能在編輯Core Web Vitals時只檢視其他專案。

- **檢視**、**編輯**&#x200B;和&#x200B;**部署**&#x200B;的範圍可以是一或多個機會型別，或是&#x200B;**所有**&#x200B;機會型別。
- **設定**&#x200B;和&#x200B;**管理使用者**&#x200B;一律套用至整個網站 — 他們不能僅限於機會型別。

每個範圍授權都會顯示為該成員自己的資料列，其中&#x200B;**套用至**&#x200B;欄會顯示機會型別、**全部**&#x200B;或&#x200B;**全網站**。

>[!CAUTION]
>
>範圍設定只會限制&#x200B;*授與的*&#x200B;內容 — 它永遠不會移除其他授與所提供的存取權。 如果個人也擁有組織範圍的存取權或&#x200B;**所有**&#x200B;型別的授權，則較廣泛的存取權仍適用。 因此，若要將某人真正限製為特定機會型別，請確定他們也沒有擁有更廣泛的角色或&#x200B;**所有**&#x200B;型別授權。

### 新增成員

1. 移至&#x200B;**設定→許可權**&#x200B;並選取網站。
1. 按一下&#x200B;**新增成員**。
1. 依名稱或電子郵件搜尋，並選取一或多個人員。
1. 選擇存取權套用的&#x200B;**機會型別** （或&#x200B;**全部**），然後選取要授與的功能。
1. 按一下&#x200B;**「新增」**。

<!-- MEDIA PENDING: Site Manager / Site User walkthrough videos are being re-recorded with demo data to remove PII, then re-uploaded to video.tv.adobe.com and embedded here with >[!VIDEO]. The earlier uploads v/3503767 and v/3503768 (KT-22672 / KT-22673) contain PII and must not be used. -->

### 編輯或移除成員

在&#x200B;**成員**&#x200B;資料表中：

- 按一下成員列上的&#x200B;**編輯權能**&#x200B;以變更其功能。 編輯現有授權時，其機會型別會維持固定 — 您只會變更權能，而且至少必須維持選取一個權能。
- 按一下&#x200B;**移除**&#x200B;以完全撤銷該成員對網站的存取權。

>[!NOTE]
>
>變更權能和移除成員是不同的動作。 若要移除所有存取權，請使用&#x200B;**移除** — 您不可以取消核取權能來執行此操作，因為授權必須保留至少一個權能（且檢視一律保留）。

### 誰可以管理許可權

網站的&#x200B;**許可權**&#x200B;頁面可用於：

- 在該網站上具有&#x200B;**管理使用者**&#x200B;權能的成員，以及
- 組織管理員（ASO管理員）。

沒有&#x200B;**管理使用者**&#x200B;的成員會看到一則訊息，指出他們無權管理該網站的存取權。

### 開啟使用者和存取管理

使用者和存取權管理是由您組織的設定所控制。 您可以在開啟之前指派存取權，但設定開啟後只有&#x200B;**強制執行**。

如果尚未啟用，**許可權**&#x200B;頁面會顯示橫幅，要求您連絡帳戶團隊。 請聯絡您的Sites Optimizer客戶團隊以將其開啟。

>[!NOTE]
>
>開啟使用者與存取權管理之前，您指派的許可權會儲存但不強制執行。

### 常見問題

**網站層級成員是否需要Admin Console角色？**

否。 在&#x200B;**許可權**&#x200B;頁面上，網站層級存取權完全在Sites Optimizer中授予。 在Admin Console中只會指派組織範圍內的角色。

**如果有人同時擁有整個組織和網站層級的存取權，會發生什麼情況？**

兩者皆適用。 其有效存取權是兩者的組合。 授予不會發生衝突，因為沒有授予可以拒絕存取。

**為什麼具有「管理」使用者的成員無法建立全組織經理？**

建立組織範圍角色是Admin Console動作。 具有&#x200B;**管理使用者**&#x200B;的成員可以在自己的網站上指派存取權，但只有組織管理員可以授與整個組織的角色。

**我如何撤銷使用者對網站的存取權？**

在&#x200B;**許可權**&#x200B;頁面上移除其授權。 這與編輯功能不同，編輯功能必須一律留下至少一個功能。

**我可以限制人員使用特定機會型別嗎？**

是 — 將「檢視」、「編輯」或「部署」範圍授與特定機會型別，而非&#x200B;**全部**。 由於存取權是可附加的，因此只有在使用者沒有全組織的存取權或&#x200B;**所有**&#x200B;型別的授權時，這才會生效。
