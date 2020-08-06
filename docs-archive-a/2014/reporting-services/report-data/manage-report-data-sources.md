---
title: 管理報表資料來源 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], data
- published reports [Reporting Services], data source connections
- shared data sources [Reporting Services]
- data sources [Reporting Services], managing
ms.assetid: 0475aded-c8fe-4337-a2b5-4df0ec4c46af
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 30c5c3b762267fb2e0d5cea978598d18e5f31ecd
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706254"
---
# <a name="manage-report-data-sources"></a>管理報表資料來源
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，報表、報表模型和資料驅動訂閱都會從外部資料來源擷取資料。 為了連接到外部資料來源，報表伺服器會使用在報表、模型或訂閱中定義，或者從其中參考的資料來源連接資訊。 資料來源連接屬性一定會在建立報表或模型時，使用報表或模型來定義，但是當報表或模型發行到報表伺服器之後，可以獨立管理這些屬性。  
  
 若要管理報表資料來源，您可以針對原生模式報表伺服器使用報表管理員，或是使用 SharePoint 網站上的應用程式頁面 (如果將報表伺服器部署為 SharePoint 整合模式)。  
  
 資料來源連接的管理是以本主題的下列工作來說明其特性：  
  
-   變更連接字串。  
  
-   變更認證。  
  
-   在報表伺服器上建立及使用共用資料來源，包括切換共用資料來源的內嵌資料來源。  
  
-   控制資料來源屬性的存取，其方式是設定您所使用之報表、模型或任何共用資料來源的權限。  
  
 請注意，修改查詢不是資料來源連接管理的一部分。 若要針對報表或模型修改查詢，您必須使用撰寫工具，並在報表或模型定義內進行變更。  
  
## <a name="managed-properties-data-source-type-connection-strings-and-credentials"></a>Managed 屬性：資料來源類型、連接字串和認證  
 您可以在報表伺服器上管理的資料來源屬性如下：  
  
|屬性|描述|如何管理|  
|--------------|-----------------|----------------------|  
|資料來源類型|決定外部資料上要使用哪一個報表伺服器資料處理延伸模組。 資料處理器的範例包括 SQL Server、Analysis Services 和 Oracle。|資料來源類型是一種 Managed 屬性，因為它可以設定。 但是，只有當您建立新的共用資料來源時，才應該設定資料來源類型。<br /><br /> 請勿在已發行之報表或模型的屬性頁中變更資料來源類型，因為這樣做幾乎會讓連接失效。 在不同資料平台上，報表或模型所需的資料結構不可能會相同。|  
|連接字串|建立與外部資料來源的初始連接。 報表可以使用靜態或動態的連接設定。<br /><br /> *「靜態連接字串」* (Static Connection String) 是一組值，每當報表執行時，一定會使用這一組值來連接相同的資料來源。<br /><br /> *「動態連接字串」* (Dynamic Connection String) 是一個內建到報表中的運算式，可讓使用者選取執行階段所要使用的資料來源。 當您在報表設計師中建立報表時，您必須將此運算式和資料來源選擇清單內建到報表中。|如果您要將資料來源移到另一部電腦，或是您已經使用測試資料建立報表，但是想要使用實際資料庫來部署報表，則變更連接字串會很有幫助。<br /><br /> 若要管理靜態連接字串，可使用另一個連接字串取代原始的字串。<br /><br /> 若要在報表管理員或 SharePoint 網站上管理動態連接字串，您受限於只能使用靜態連接字串取代這個字串。 您無法編輯運算式本身，也無法變更資料來源選擇清單。 若要變更運算式或有效的值清單，您必須編輯報表定義，然後將它重新發行到報表伺服器。 如需詳細資訊，請參閱 [Reporting Services 中的資料連接、資料來源及連接字串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)。|  
|認證|提供有權讀取資料來源資料之使用者的名稱和密碼。<br /><br /> 如果資料來源不支援驗證 (例如，如果資料來源是檔案系統上的 XML 檔案)，您可以設定自動執行帳戶，好讓報表伺服器連接外部資料來源，而不需傳遞認證。|若要管理認證，可以更新使用者帳戶或密碼 (如果過期的話)。<br /><br /> 您也可以變更認證的取得方式 (例如，在執行階段提示使用者輸入認證)。<br /><br /> 如果您希望使用者能夠訂閱報表，您就必須設定報表使用預存認證。|  
  
## <a name="creating-and-using-shared-data-sources"></a>建立及使用共用資料來源  
 如果您要發行在報表中有內嵌資料來源屬性的報表，請考慮切換成共用資料來源屬性。 共用資料來源比較容易管理，因為您可以在一個頁面中更新認證和連接字串。 所有使用該資料來源的報表、模型和資料驅動訂閱都會立即收取變更。 您也可以讓共用資料來源離線，有效地暫停報表或訂閱讓它不要執行，同時針對發生的任何問題進行調查或疑難排解。  
  
## <a name="controlling-access-data-source-properties"></a>控制存取資料來源屬性  
 根據預設，任何有權管理報表的人都可以在報表上設定任何屬性，其中包括決定資料來源類型的屬性、連接字串、認證，以及此報表是要從內嵌還是共用資料來源取得連接資訊。 如需哪一個工作和權限可控制原生模式報表伺服器上資料來源屬性之存取的詳細資訊，請參閱 [保護共用資料來源項目的安全](../security/secure-shared-data-source-items.md) 和 [保護報表和資源的安全](../security/secure-reports-and-resources.md)。  
  
 檢視及編輯 SharePoint 文件庫內項目屬性的權限是由網站管理員所決定。 如需哪一個權限可控制資料來源連接屬性之存取的詳細資訊，請參閱 [報表伺服器項目的 SharePoint 網站和清單權限參考](../security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)。  
  
## <a name="how-to-work-with-data-source-properties-on-a-report-server"></a>如何在報表伺服器上處理資料來源屬性  
 您可以使用各種工具來建立及修改資料來源屬性。 下表摘要列出方法和工具，並提供其他指示的連結。  
  
|Task|工具|連結|  
|----------|----------|----------|  
|檢視連接字串的範例。||[Data Connections, Data Sources, and Connection Strings in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)|  
|選擇取得認證以連接資料來源的方法。||[指定報表資料來源的認證及連線資訊](specify-credential-and-connection-information-for-report-data-sources.md)|  
|將資料來源連接屬性加入到報表定義 (.rdl) 檔案。|報表設計師|[建立內嵌或共用資料來源 &#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md)|  
|在報表專案中加入共用資料來源 (.rds) 檔案的連結。|報表設計師|[建立、修改和刪除共用資料來源 &#40;SSRS&#41;](create-modify-and-delete-shared-data-sources-ssrs.md)|  
|建立資料來源的預先定義清單，供使用者在執行階段選取。 當使用者要求報表時，此報表會提供資料來源的清單。 使用者在執行此報表之前，必須先選取所要使用的資料來源。 若要在報表中加入資料來源選擇清單，您可使用運算式。<br /><br /> 這稱之為動態資料來源連接。|報表設計師|[Data Connections, Data Sources, and Connection Strings in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)|  
|在報表伺服器上建立共用資料來源項目。|報表管理員|[建立、刪除或修改共用資料來源 &#40;報表管理員&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)|  
|將認證儲存為建立訂閱或報表快照集的必要元件。|報表管理員|[Store Credentials in a Reporting Services Data Source](store-credentials-in-a-reporting-services-data-source.md)|  
|在已發行的報表上編輯資料來源連接屬性。|報表管理員|[設定報表的資料來源屬性 &#40;報表管理員&#41;](configure-data-source-properties-for-a-report-report-manager.md)|  
|在報表伺服器上建立共用資料來源項目。|SharePoint 網站|[建立和管理共用資料來源 &#40;SharePoint 整合模式的 Reporting Services&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)|  
|搭配報表使用現有的 .odc 連接資訊。|SharePoint 網站|[搭配報表使用 Office 資料連接 &#40;.odc&#41; &#40;SharePoint 整合模式的 Reporting Services&#41;](use-an-office-data-connection-odc-with-reports.md)|  
  
> [!NOTE]  
>  管理報表資料來源的資料來源連接，和管理報表伺服器資料庫的報表伺服器連接不同。 如需報表伺服器連線與其內部資料存放區的詳細資訊，請參閱[設定報表伺服器資料庫連線 &#40;SSRS 設定管理員&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。  
  
## <a name="see-also"></a>另請參閱  
 [將報表或模型系結至 &#40;SSRS&#41;的共用資料來源](bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [建立、刪除或修改共用資料來源 &#40;報表管理員&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [將認證儲存在 Reporting Services 資料來源中](store-credentials-in-a-reporting-services-data-source.md)   
 [Reporting Services 中的資料連線、資料來源及連接字串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Reporting Services &#40;SSRS 支援的資料來源&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [報表伺服器內容管理 &#40;SSRS 原生模式&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
