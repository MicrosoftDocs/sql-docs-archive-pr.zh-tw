---
title: SQL Server 2014 中 SQL Server Reporting Services 的重大變更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Me.Value references
- Reporting Services, backward compatibility
- breaking changes [Reporting Services]
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c58db038269eae1c023afab18a6e844aa2742d39
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595813"
---
# <a name="breaking-changes-in-sql-server-reporting-services-in-sql-server-2014"></a>SQL Server 2014 中 SQL Server Reporting Services 的重大變更
  本主題描述 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中的重大變更。 這些變更可能會中斷以舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]為根據的應用程式、指令碼或功能。 當您進行升級或是在自訂指令碼或報表內時，可能會遇到這些問題。 如需詳細資訊，請參閱＜ [Use Upgrade Advisor to Prepare for Upgrades](../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)＞。  
  
 **本主題內容：**  
  
-   [SQL Server 2014 Reporting Services 重大變更](#bkmk_sql14)  
  
-   [SQL Server 2012 Reporting Services 的重大變更](#bkmk_rc0)  
  
-   [SQL Server 2008 R2 Reporting Services 的重大變更](#bkmk_kj)  
  
##  <a name="sssql14-reporting-services-breaking-changes"></a><a name="bkmk_sql14"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Reporting Services 的重大變更  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中的 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]沒有任何重大變更。  
  
##  <a name="sssql11-reporting-services-breaking-changes"></a><a name="bkmk_rc0"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]Reporting Services 的重大變更  
  
### <a name="sharepoint-mode-server-references-require-the-sharepoint-site"></a>SharePoint 模式伺服器參考需要 SharePoint 網站  
 您無法在 URL 路徑中直接使用虛擬名稱，瀏覽或參考至報表伺服器。 例如：  
  
 `http://<Server name>/ReportServer`  
  
 因此需要您將 SharePoint 網站納入 URL 路徑。 例如，如果您的網站名稱是 ' `videos` ' 且使用了 ' `sites` ' 前置詞，則 URL 看起來會像下面這樣：  
  
 `http://<Server Name>/sites/videos/_vti_bin/ReportServer`  
  
### <a name="changes-to-sharepoint-mode-command-line-installation"></a>SharePoint 模式命令列安裝的變更  
 輸入設定 **/RSINSTALLMODE** 只能搭配原生模式安裝運作，無法針對 SharePoint 模式安裝運作。 例如，不支援下列各項 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] ： **/RSINSTALLMODE = "DefaultSharePointMode"**。 為取代該輸入設定，請使用 **/RSSHPINSTALLMODE="DefaultSharePointMode"**。  
  
 下列語句是完整安裝命令和參數集的範例： **setup/ACTION = install/FEATURES = SQL，RS/InstanceName = Denali_INST1 .../RSSHPINSTALLMODE = "DefaultSharePointMode"**  
  
 如需命令列安裝的詳細資訊，請參閱[Reporting Services SharePoint 模式和原生模式的命令提示字元安裝](install-windows/install-reporting-services-at-the-command-prompt.md)。  
  
### <a name="the-reporting-services-wmi-provider-no-longer-supports-configuration-of-sharepoint-mode"></a>Reporting Services WMI 提供者不再支援 SharePoint 模式的組態設定  
 您現在可以使用 PowerShell 指令程式和 SharePoint 管理中心完成 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 的組態設定。 新的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式架構會使用 SharePoint 服務架構。 SharePoint 不支援 WMI 介面。  
  
 這些變更會影響下列元件和工作流程：  
  
-   在 SharePoint 模式下使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 之 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] WMI 提供者的自訂應用程式。  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 組態管理員、rskeymgmt.exe 和 rsconfig.exe。 請使用 SharePoint 管理中心和 PowerShell，而非使用這些公用程式進行 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式的組態設定。  
  
-   SQL Server Management Studio：客戶無法使用類似于 <machine_name>/<instance_name> 的語法來參考伺服器。 從 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 版開始，建議的方法是使用 SharePoint 網站 URL。 例如， **HTTP://<sharepoint_server>/<sharePoint_site>**。 從 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]開始，SharePoint 網站 URL 是唯一支援的語法。  
  
### <a name="report-model-designer-is-not-available-in-sql-server-data-tools"></a>SQL Server Data Tools 沒有提供報表模型設計師  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 不再支援報表模型專案。 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]沒有提供報表模型設計師。 您無法在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中建立新的報表模型專案或開啟現有的專案，而且無法建立或更新報表模型。 若要更新報表模型，您可以使用 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 或舊版工具。 在使用報表產生器和報表設計師等 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 工具所撰寫的報表中，您可以繼續使用報表模型做為資料來源。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 將繼續提供查詢設計工具，讓您用來建立查詢，以便從報表模型中擷取報表資料。  
  
##  <a name="sql-server-2008-r2-reporting-services-breaking-changes"></a><a name="bkmk_kj"></a>SQL Server 2008 R2 Reporting Services 重大變更  
 本節描述中的重大變更 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 。  
  
> [!NOTE]  
>  因為 SQL Server 2008 R2 是 SQL Server 2008 的次要版本更新，所以建議您也檢閱 SQL Server 2008 章節中的內容。  
  
### <a name="expanded-csv-data-renderer"></a>擴充的 CSV 資料轉譯器  
 在中 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ，CSV 檔案包含圖表和量測計資料。 相依於舊版 CSV 檔案結構的應用程式會由於圖表和量測計的額外資料行而無法再運作。  
  
 如需詳細資訊，請參閱 [匯出至 CSV 檔案 &#40;報表產生器及 SSRS&#41;](report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md)中使用這項資料。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 中 SQL Server Reporting Services 的行為變更](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [Reporting Services 的新 &#40;&#41;](what-s-new-reporting-services.md)   
 [SQL Server 2014 中 SQL Server Reporting Services 已被取代的功能](deprecated-features-in-sql-server-reporting-services-ssrs.md)   
 [SQL Server 2014 中已中止的 SQL Server Reporting Services 功能](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  
  
  
