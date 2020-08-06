---
title: 驗證 Reporting Services 安裝 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- checking report server installations
- verifying report server installations
- Report Designer [Reporting Services], verifying installations
- installing Reporting Services, verifying installations
- Report Manager [Reporting Services], verifying installations
- report servers [Reporting Services], verifying installations
- Setup [Reporting Services], verifying installations
ms.assetid: 82a51a99-66f0-4b0c-b05b-07d22387adb0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5b90f997f99cfc9d3f8625eb4e08d193af52d7f6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585130"
---
# <a name="verify-a-reporting-services-installation"></a>Verify a Reporting Services Installation
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器：原生或 SharePoint。 確認安裝所應遵循的步驟會視報表伺服器模式而定。  
  
 本主題包含下列資訊：  
  
-   [確認 SharePoint 模式安裝](#bkmk_sharepointmode)  
  
-   [確認原生模式安裝](#bkmk_nativemode)  
  
##  <a name="verify-sharepoint-mode-installation"></a><a name="bkmk_sharepointmode"></a> 確認 SharePoint 模式安裝  
  
#### <a name="to-verify-the-reporting-services-service"></a>確認 Reporting Services 服務  
  
1.  從 SharePoint 管理中心，按一下 **[系統設定]** 群組中的 **[管理伺服器上的服務]** 。  
  
2.  確認已安裝 **[SQL Server Reporting Services 服務]** ，且該服務處於 **[執行中]** 狀態。  
  
     如果您在清單中未看到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務，請確認是否已安裝此服務。 如需詳細資訊，請參閱[安裝適用于 sharepoint 2010 的 Reporting Services Sharepoint 模式](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)中的「安裝並啟動 Reporting Services SharePoint 服務」一節。  
  
#### <a name="to-verify-the-service-application"></a>確認服務應用程式  
  
1.  若要從管理中心確認您至少具有一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式，請按一下 **[應用程式管理]** 群組中的 **[管理服務應用程式]** 。  
  
2.  確認 **[SQL Server Reporting Services 服務應用程式]** 類型的服務應用程式確實存在，而且有對應的應用程式 Proxy。  
  
3.  在服務應用程式名稱 **附近** 按一下，然後在 SharePoint 工具列中按一下 **[屬性]** 。  如果您按一下服務應用程式的名稱，即會開啟服務應用程式的 [管理] 頁面，而不是屬性頁面。  
  
4.  確認 **[Web 應用程式關聯]** 設定為指向所需的 Web 應用程式。  
  
#### <a name="to-verify-the-site-collection-feature"></a>確認網站集合功能  
  
1.  在網站設定中，按一下 **[網站集合管理]** 群組中的 **[網站集合功能]** 。  
  
2.  確認已啟用 **[報表伺服器整合功能]** 。  
  
#### <a name="to-verify-reporting-server-content-types"></a>確認報表伺服器內容類型  
  
1.  若要確認或加入 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器內容類型，請參閱[將報表伺服器內容類型加入至程式庫 &#40;Reporting Services SharePoint 整合模式中的&#41;](../add-reporting-services-content-types-to-a-sharepoint-library.md)。  
  
#### <a name="to-verify-you-can-launch-report-builder"></a>確認您可以啟動報表產生器  
  
1.  從文件庫中，按一下 SharePoint 功能區中的 **[文件]** 。  
  
2.  按一下 **[新增文件]** ，然後再按一下 **[報表產生器報表]**。 如果您看不到這個選項，請檢閱有關將報表伺服器內容類型加入文件庫的先前程序。  
  
#### <a name="create-a-basic-report"></a>建立基本報告  
  
1.  在 SharePoint 文件庫中，建立只包含一個文字方塊 (例如標題) 的基本 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表。 此報表不包含任何資料來源或資料集。 其目的是要確認您可以開啟報表產生器，而且基本報表將會進行預覽。  
  
2.  將報表儲存至文件庫，然後從文件庫中執行報表。 如需使用報表產生器建立報表的詳細資訊，請參閱 [啟動報表產生器 (報表產生器)](https://technet.microsoft.com/library/ms159221.aspx)。  
  
#### <a name="reporting-services-samples"></a>Reporting Services 範例  
  
1.  完成其中一個 Reporting Services 教學課程。 如需詳細資訊，請參閱 [Reporting Services 教學課程 &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)。  
  
2.  從 CodePlex 下載 Adventure Works 範例資料庫和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 範例報表。 如需詳細資訊，請參閱＜ [AdventureWorks 報表範例](https://msftrsprodsamples.codeplex.com/wikipage?title=SS2012!AdventureWorks2012%20Report%20Samples&referringTitle=Home)＞。  
  
##  <a name="verify-a-native-mode-installation"></a><a name="bkmk_nativemode"></a> 驗證原生模式安裝  
 當您使用預設組態安裝原生模式報表伺服器時，安裝程式會安裝和部署該伺服器。 您可以執行一些簡單的測試，來確認安裝程式是否部署報表伺服器。 您必須是本機管理員才能執行這些步驟。 若要讓其他使用者能夠執行測試，您必須為那些使用者設定報表伺服器存取權。  
  
#### <a name="to-verify-that-the-report-server-is-installed-and-running"></a>確認報表伺服器已安裝及執行  
  
1.  執行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並連接到您剛安裝的報表伺服器執行個體。 [Web 服務 URL] 頁面包含報表伺服器 Web 服務的連結。 請按一下此連結，確認您可以存取伺服器。 如果報表伺服器資料庫並未設定，請在按一下連結之前先行設定。  
  
2.  開啟 [服務] 主控台應用程式，並確認報表伺服器服務正在執行中。 若要檢視報表伺服器服務的狀態，請按一下 [開始]****，指向 [控制台]****，並按兩下 [系統管理工具]****，然後按兩下 [服務]****。 當服務清單出現時，請捲動至 [報表伺服器 (MSSQLSERVER)]****。 其狀態應該是 **[已啟動]**。  
  
3.  開啟瀏覽器，並在位址列輸入報表伺服器 URL。 位址是由您在安裝期間對報表伺服器指定的伺服器名稱和虛擬目錄名稱所組成。 報表伺服器虛擬目錄的預設名稱為 **ReportServer**。 您可以使用下列 URL 來確認報表伺服器的安裝： HTTP:// *\<computer name>* /ReportServer *\<_instance name>* 。 如果您將報表伺服器安裝成具名執行個體，則需使用不同的 URL。 如需 URL 格式的詳細資訊，請參閱[設定報表伺服器 URL &#40;SSRS 設定管理員&#41;](configure-report-server-urls-ssrs-configuration-manager.md)。 如果您是 Windows Vista 或 Windows Server 2008 的本機系統管理員，請參閱[設定原生模式報表伺服器進行本機管理 &#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
4.  執行報表來測試報表伺服器作業。 在此步驟中，您可以根據教學課程建立範例報表。 如需詳細資訊，請參閱[建立基本資料表報表 &#40;SSRS 教學課程&#41;](../create-a-basic-table-report-ssrs-tutorial.md)。  
  
#### <a name="to-verify-that-report-manager-is-installed-and-running"></a>確認報表管理員已安裝及執行  
  
1.  開啟瀏覽器，並在位址列輸入報表管理員 URL。 此位址是由伺服器名稱和虛擬目錄名稱所組成，此目錄名稱是安裝期間針對報表管理員所指定，或是在 Reporting Services 組態工具的 [報表管理員 URL] 頁面中指定。 依預設，報表管理員虛擬目錄的名稱為 **Reports**。 您可以使用下列 URL 確認報表管理員的安裝：  
  
     HTTP:// *\<computer name>* /Reports *\<_instance name>* 。  
  
2.  使用報表管理員來建立新資料夾，或上傳檔案來測試定義是否傳回至報表伺服器資料庫。 如果這些作業都成功，表示連接可運作。  
  
     如需詳細資訊，請參閱[報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)。  
  
#### <a name="to-verify-that-report-designer-is-installed-and-running"></a>確認報表設計師已安裝及執行  
  
1.  開啟 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，並根據報表伺服器專案類型來建立新的專案。 如需使用 [報表伺服器專案精靈] 的詳細資訊，請參閱《SQL Server 線上叢書》中的 [SQL Server 資料工具中的 Reporting Services &#40;SSDT&#41;](../tools/reporting-services-in-sql-server-data-tools-ssdt.md)。  
  
2.  如果您已安裝報表範例，請開啟範例報表專案檔，並將報表發行至報表伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [針對 Reporting Services 安裝進行疑難排解](troubleshoot-a-reporting-services-installation.md)   
 [Reporting Services 錯誤的原因和解決方案](../troubleshooting/cause-and-resolution-of-reporting-services-errors.md)  
  
  
