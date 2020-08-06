---
title: 建立或自訂資料摘要庫 (PowerPivot for SharePoint) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data feed library
- data feeds [Analysis Services with SharePoint]
ms.assetid: 699fbeb9-42ab-436b-beba-214db51ea3dd
author: minewiskan
ms.author: owend
ms.openlocfilehash: b86f63c1af094ea9e8a2a1149debeac387bccbf0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87698581"
---
# <a name="create-or-customize-a-data-feed-library-powerpivot-for-sharepoint"></a>建立或自訂資料摘要庫 (PowerPivot for SharePoint)
  *「資料摘要庫」* (Data Feed Library) 是一種特殊用途的 SharePoint 文件庫，可讓您註冊與共用 Atom 資料服務文件 (.atomsvc)。 這些文件會提供 XML 資料摘要給支援 Atom 資料摘要格式的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿或其他用戶端應用程式。 資料摘要庫與其他 SharePoint 文件庫不同，因為它讓您能夠：

-   建立或編輯 *「資料服務文件」*(Data service document)，用來指定特定摘要的 HTTP 連接。

-   在中央位置共用及管理資料服務文件。

-   以圖示以視覺化方式識別資料服務檔，讓您可以輕鬆地區別服務檔與儲存在相同文件庫中的其他檔： ![GMNI_IconDataFeed](../media/gmni-icondatafeed.gif "GMNI_IconDataFeed")

 資料摘要庫一直都是包含資料服務文件 (.atomsvc) 檔案，而從來都不包含資料摘要本身。 資料服務文件與包含靜態 XML 資料的資料摘要不同，它會指定 URL 給接到要求時會產生摘要的服務或應用程式，為可重複的匯入作業提供可重複使用的連接資訊。

 本主題包含下列幾節：

 [先決條件](#prereq)

 [建立新的資料摘要庫](#createlib)

 [將資料摘要庫內容類型加入至任何文件庫](#addtolib)

##  <a name="prerequisites"></a><a name="prereq"></a> 必要條件
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 功能整合必須針對您要建立其資料摘要庫的網站啟用。 如果無法使用資料摘要庫範本類型，最可能的原因是不符合這項先決條件。 如需詳細資訊，請參閱為[管理中心的網站集合啟用 PowerPivot 功能整合](activate-power-pivot-integration-for-site-collections-in-ca.md)。

 您必須是網站擁有者，才能建立該文件庫。

##  <a name="create-a-new-data-feed-library"></a><a name="createlib"></a>建立新的資料摘要庫
 建立資料摘要庫是為 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿啟用資料摘要的第一個步驟。 資料摘要庫會提供資料服務文件的應用程式和管理頁面，因此您必須先將此摘要庫準備就緒，才能建立新文件。

 資料摘要庫的根據是內建範本與預先設定的 *「資料服務文件內容類型」* (Data service document content type)，此類型定義資料服務文件的屬性和行為。

1.  按一下頁面左上角的 [網站動作]****。

2.  按一下 [**更多選項**]

3.  按一下文件庫之下的 [資料摘要庫]****。

4.  輸入名稱、描述、啟動及版本喜好設定。 加入描述性資訊，以協助使用者將這個文件庫識別為資料服務文件的儲存位置。

5.  按一下 [建立]。

 資料摘要庫的連結會出現在目前網站的導覽 [快速啟動] 窗格中。

 建立文件庫之後，您可以使用它來建立資料服務文件。 如需詳細資訊，請參閱[使用資料摘要 &#40;PowerPivot for SharePoint&#41;](use-data-feeds-power-pivot-for-sharepoint.md)。

##  <a name="add-the-data-feed-content-type-to-any-library"></a><a name="addtolib"></a>將資料摘要內容類型新增至任何程式庫
 如果您不要建立專用的資料摘要庫，但仍要從 SharePoint 網站建立及管理資料服務文件，則可以手動方式為要用來共用資料服務文件 (.atomsvc) 檔案的任何文件庫，加入並設定資料服務文件內容類型。

 您必須至少有「管理清單」權限，才能加入並設定內容類型。 此權限內建在「設計」權限等級以上 (含)。

 您必須為要建立或編輯資料摘要註冊文件的每個文件庫重複執行下列步驟。

#### <a name="step-1-enable-content-type-management"></a>步驟 1：啟用內容類型管理

1.  開啟要啟用多個內容類型的文件庫。

2.  在 SharePoint 功能區的 [文件庫工具] 中，按一下 **[文件庫]**。

3.  按一下 [設定]。

4.  按一下 **[文件庫設定]**。

5.  按一下 [一般設定] 中的 **[進階設定]**。

6.  在 [內容類型] 的 [是否允許內容類型的管理?] 區段中按一下 **[是]**。

7.  按一下 [確定]  。

#### <a name="step-2-add-the-data-service-document-content-type"></a>步驟 2：加入資料服務文件內容類型

1.  在 [內容類型] 區段中，按一下 **[從現有的網站內容類型新增]**。 如果您看不到此頁面，請回到網站中，按一下文件庫工具中的 **[文件庫]** ，然後按一下 **[文件庫設定]**。

2.  在 [內容類型] 中，按一下 **[從現有的網站內容類型新增]**。

3.  在 [從下列位置選取網站內容類型:] 中，選取 **[商業智慧]**。

4.  在 [可用的網站內容類型] 中，按一下 [資料服務文件]****，然後按一下 [加入]****，將所選取的內容類型移到 [要新增的內容類型] 清單中。

5.  按一下 [確定]  。

#### <a name="step-3-verify-data-service-document-configuration"></a>步驟 3：確認資料服務文件設定

1.  開啟網站首頁。

2.  開啟文件庫。

3.  在 SharePoint 功能區上，按一下 [文件]****。

4.  按一下 [新文件] 上的向下箭號，然後選取 [資料服務文件]****。 [新資料服務文件] 頁面應該會出現。

## <a name="see-also"></a>另請參閱
 [使用資料摘要 &#40;PowerPivot for SharePoint&#41;](use-data-feeds-power-pivot-for-sharepoint.md)在管理中心[powerpivot 資料](power-pivot-data-feeds.md)摘要中[刪除 Powerpivot 資料摘要庫](delete-a-power-pivot-data-feed-library.md) [powerpivot 伺服器管理和](power-pivot-server-administration-and-configuration-in-central-administration.md)設定


