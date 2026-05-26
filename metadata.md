---
solution: Experience Manager
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
usetq: true
product: adobe experience manager
landing-page-name: experience-manager
landing-page-breadcrumb-title: AEM
type: Documentation
description: AEM Sites Optimizer檔案。
index: true
git-repo: https://github.com/AdobeDocs/experience-manager-sites-optimizer.en
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
recommendations: noDisplay
source-git-commit: b6745249d9a773ce875f421dd16947a1a4d0a245
workflow-type: tm+mt
source-wordcount: 85
ht-degree: 2%

---


# 內部使用的中繼資料

GitHub編寫系統會使用下列相對於前一項的遞增層級，以階層方式組織中繼資料。

1. metadata.md
1. ToC
1. 文章

metadata.md檔案中定義的中繼資料會套用至整個存放庫，但可以在ToC和文章層級覆寫。 中繼資料的任何覆寫都應該儘可能在最低層級進行。

`experience-manager-cloud-service.en`存放庫中的中繼資料是最低要求。

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

ToCs

* `sub-product`
* `user-guide-title`

文章

* `title`
* `description`
* `contentOwner` （僅在`/help/assets`下的核心資產內容上）

