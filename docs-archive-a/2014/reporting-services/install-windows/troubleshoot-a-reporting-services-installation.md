---
title: 針對 Reporting Services 安裝進行疑難排解 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: e2536f7f-d90c-4571-9ffd-6bbfe69018d6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 819016a4b6aa08982e787bd1da0af6562f22f677
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598747"
---
# <a name="troubleshoot-a-reporting-services-installation"></a>疑難排解 Reporting Services 安裝
  如果您因為安裝期間發生的錯誤而無法安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，請使用本主題的指示來處理最有可能造成安裝錯誤的狀況。  
  
 如需有關 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]問題的最新資訊，請參閱 [Reporting Services SQL Server 2012 提示、秘訣和疑難排解](https://go.microsoft.com/fwlink/?LinkId=221297)。  
  
 如需有關與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 相關之其他錯誤和問題的詳細資訊，請參閱 [疑難排解 SSRS 問題和錯誤](https://social.technet.microsoft.com/wiki/contents/articles/ssrs-troubleshooting-issues-and-errors.aspx)。  
  
 如果您碰到的問題在版本資訊中有描述，請檢閱 [線上版本資訊](https://go.microsoft.com/fwlink/?linkid=236893) 。  
  
 本主題包含下列資訊：  
  
-   [檢查安裝記錄檔](#bkmk_setuplogs)  
  
-   [檢查必要條件](#bkmk_prereq)  
  
-   [疑難排解 SharePoint 模式安裝的問題](#bkmk_tshoot_sharepoint)  
  
-   [針對原生模式安裝的問題進行疑難排解](#bkmk_tshoot_native)  
  
-   [其他資源](#bkmk_additional)  
  
##  <a name="check-setup-logs"></a><a name="bkmk_setuplogs"></a> 檢查安裝記錄檔  
 安裝錯誤會記錄在**Program FILES\MICROSOFT SQL Server\110\Setup Bootstrap\Log**資料夾的記錄檔中。 每當您執行安裝程式時，都會建立一個子資料夾， 此子資料夾的名稱就是您執行安裝程式的時間和日期。 如需如何檢視安裝記錄檔的指示，請參閱 [檢視與讀取 SQL Server 安裝記錄檔](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)。  
  
-   記錄檔包含檔案的集合。  
  
-   開啟 *_summary.txt 檔，即可檢視產品、元件和執行個體的資訊。  
  
-   開啟 *_errorlog.txt 檔，即可檢視安裝期間所產生的錯誤資訊。  
  
-   開啟 *_RS\_\*_ComponentUpdateSetup.log，即可檢視 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝程式資訊。  
  
##  <a name="check-prerequisites"></a><a name="bkmk_prereq"></a>檢查必要條件  
 安裝程式會自動檢查必要條件。 但是，如果您正在排除安裝問題，知道安裝程式正在檢查哪些需求將會很有協助。  
  
-   執行安裝程式的帳戶需求包括本機管理員群組的成員資格。 安裝程式必須具有加入檔案、登錄設定、建立本機安全性群組及設定權限的權限。 如果您要安裝預設組態，安裝程式必須具有在您進行安裝所在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上建立報表伺服器資料庫的權限。  
  
-   作業系統必須支援 HTTP.SYS 1.1。  
  
-   HTTP 服務必須已啟用且在執行中。  
  
-   如果您也要安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務，則分散式交易協調器 (DTC) 必須在執行中。  
  
-   Authz.dll 必須存在於 System32 資料夾中。  
  
 安裝程式不再檢查 Internet Information Services (IIS) 或 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]需要 MDAC 2.0 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 版本 2.0;安裝程式將會安裝這些（如果尚未安裝）。  
  
##  <a name="troubleshoot-problems-with-sharepoint-mode-installations"></a><a name="bkmk_tshoot_sharepoint"></a> 疑難排解 SharePoint 模式安裝的問題  
  
-   [Reporting Services 組態管理員未啟動](#bkmk_configmanager_notstart)  
  
-   [在 SharePoint 模式下安裝 SQL Server 2012 SSRS 之後，您在 SharePoint 管理中心內看不到 SQL Server Reporting Services 服務](#bkmk_no_ssrs_service)  
  
-   [Reporting Services PowerShell Cmdlet 無法使用，而且無法辨識命令](#bkmk_cmdlets_not_recognized)  
  
-   [您看見一則錯誤訊息，指出 URL 未設定](#bkmk_URL_not_configured)  
  
-   [在已安裝 SharePoint 但尚未設定的電腦上，安裝程式會失敗](#bkmk_sharepoint_not_confiugred)  
  
-   [SharePoint 管理中心頁面是空白的](#bkmk_central_admin_blank)  
  
-   [當您嘗試建立新的報表產生器報表時，會看到一則錯誤訊息](#bkmk_reportbuilder_newreport_error)  
  
-   [您會看到使用 PREPAREIMAGE 時不支援 RS_SHP 的錯誤訊息](#bkmk_RS_SHP_notsupported)  
  
###  <a name="reporting-services-configuration-manager-does-not-start"></a><a name="bkmk_configmanager_notstart"></a>Reporting Services 組態管理員未啟動  
 **描述：** 按 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的設計會出現此情況。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 現在的架構為 SharePoint 服務架構。 在 SharePoint 模式中設定及管理 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 時，不再需要組態管理員。  
  
 **因應措施：** 使用 SharePoint 管理中心，在 SharePoint 模式下設定報表伺服器。 如需詳細資訊，請參閱 [管理 Reporting Services SharePoint 服務應用程式](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)  
  
###  <a name="you-do-not-see-the-sql-server-reporting-services-service-in-sharepoint-central-administration-after-installing-sql-server-2012-ssrs-in-sharepoint-mode"></a><a name="bkmk_no_ssrs_service"></a>在 SharePoint 模式中安裝 SQL Server 2012 SSRS 之後，您在 SharePoint 管理中心內看不到 SQL Server Reporting Services 服務  
 **描述：** 如果成功安裝 sharepoint [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 模式和 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 適用于 sharepoint 2010 的增益集之後，您在下列兩個功能表中看不到 [SQL Server Reporting Services]，表示 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務尚未註冊：  
  
-   SharePoint 2010 管理中心-> 「應用程式管理」-> 「管理伺服器上的服務」頁面  
  
-   SharePoint 2010 管理中心-> "應用程式管理"-> [管理服務應用程式]-> [新增] 功能表  
  
 **因應措施：** 若要註冊並啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint Services，請完成下列步驟：  
  
1.  在執行 SharePoint 2010 管理中心的電腦上  
  
    1.  使用系統管理員權限來開啟 SharePoint 2010 管理命令介面。 以滑鼠右鍵按一下圖示，然後按一下 [以系統管理員身分執行]。 在命令介面中執行下列三個指令程式：  
  
    2.  ```powershell
        Install-SPRSService  
        ```  
  
    3.  ```powershell
        Install-SPRSServiceProxy  
        ```  
  
    4.  ```powershell
        Get-SPServiceInstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
        ```  
  
2.  確認 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務在頁面上將狀態顯示為「**已啟動**」： SharePoint 2010 管理中心-> 「**應用程式管理**」-> 「**管理伺服器上的服務**」  
  
###  <a name="reporting-services-powershell-cmdlets-are-not-available-and-commands-are-not-recognized"></a><a name="bkmk_cmdlets_not_recognized"></a> Reporting Services PowerShell 指令程式無法使用，而且無法辨識命令  
 **描述：** 當您嘗試執行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] PowerShell 指令程式時，看到類似下列的錯誤訊息：  
  
-   **無法辨識** 'Install-SPRSServiceInstall-SPRSService' 詞彙是否為 Cmdlet、函數、指令檔或可執行程式的名稱。 請檢查名稱拼字是否正確，如果包含路徑的話，請確認路徑是否正確，然後再試一次。於行: 1 字元: 39+ Install-SPRSServiceInstall-SPRSService <<<<    + CategoryInfo          : ObjectNotFound: (Install-SPRSServiceInstall-SPRSService:String) [], CommandNotFoundExcep  
  
 **因應措施：** 完成下列其中一項作業：  
  
-   執行適用於 SharePoint 產品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集。 **rssharepoint.msi**。  
  
-   從 SQL Server 安裝媒體安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。  
  
 **注意：** 如果當您完成其中一種因應措施時 **[SharePoint 2013 管理命令介面]** 已開啟，請關閉並重新開啟管理命令介面。  
  
 如需詳細資訊，請參閱下列：  
  
-   [尋找適用於 SharePoint 產品之 Reporting Services 增益集的位置](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
-   [安裝 SharePoint 2010 Reporting Services SharePoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
-   [安裝適用於 SharePoint 2013 的 Reporting Services SharePoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)  
  
###  <a name="you-see-an-error-message-indicating-the-url-is-not-configured"></a><a name="bkmk_URL_not_configured"></a>您會看到錯誤訊息，指出未設定 URL  
 **描述：** 您看見一則類似以下的錯誤訊息：  
  
 系統不支援這項 SQL Server Reporting Services (SSRS) 功能。 請使用管理中心來確認並修正下列一個或多個問題：•報表伺服器 URL 未設定。 請使用 SSRS 整合頁面來設定它。•SSRS 服務應用程式 Proxy 未設定。 請使用 SSRS 服務應用程式頁面來設定 Proxy。•SSRS 服務應用程式並未對應至此 Web 應用程式。 請使用 SSRS 服務應用程式頁面，將 SSRS 服務應用程式 Proxy 關聯至此 Web 應用程式的應用程式 Proxy 群組。  
  
 **因應措施：** 此錯誤訊息包含更正這個問題的三個建議步驟。 「報表伺服器 URL 未設定」訊息中的第一個建議。 是與 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]之前的報表伺服器版本整合時相關。 先前報表伺服器版本的 SharePoint 設定是在 [一般應用程式設定]**** 頁面上，使用 [SQL Server Reporting Services (2008 和 2008 R2)]**** 來完成。  
  
 **詳細資訊：** 當您嘗試使用任何需要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務之連接的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能時，就會看見這則錯誤訊息。 這包括：  
  
-   從 SharePoint 文件庫開啟 SQL Server 報表產生器。  
  
-   管理訂閱。  
  
-   管理服務應用程式。  
  
###  <a name="setup-fails-on-a-computer-with-sharepoint-installed-but-it-is-not-configured"></a><a name="bkmk_sharepoint_not_confiugred"></a> 在已安裝 SharePoint 但尚未進行設定的電腦上，安裝程式會失敗  
 **描述：** 若您在已安裝 SharePoint 但尚未進行設定的電腦上，選擇安裝 Reporting Services SharePoint 模式，將會看到類似下列的訊息，且安裝程式將會停止：  
  
 SQL Server 安裝程式已停止運作  
  
 **因應措施：** 設定 SharePoint，然後執行 SQL Server 安裝。  
  
 **詳細資訊：** 將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝至現有的 SharePoint 安裝時，安裝程式會嘗試安裝並啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 服務。 若尚未設定 SharePoint，服務安裝將會失敗並會導致安裝程式失敗。  
  
###  <a name="sharepoint-central-administration-page-is-blank"></a><a name="bkmk_central_admin_blank"></a>SharePoint 管理中心頁面是空白的  
 **描述：** 您可以順利安裝 SharePoint 2010，且未出現安裝錯誤。 但當您瀏覽至管理中心時，只看到了空白頁面：  
  
 **因應措施：** 此問題不是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 所特有的問題，而是與整體 SharePoint 安裝中的權限組態相關。 下列是建議的清單：  
  
-   請檢閱開發環境上的 SharePoint 主題。 [設定 Windows Vista、Windows 7 及 Windows Server 2008 上 SharePoint 2010 的開發環境](https://msdn.microsoft.com/library/ee554869\(office.14\).aspx)  
  
-   請檢閱論壇文章： [管理中心在 Windows 7 上進行安裝後傳回空白頁面](https://social.technet.microsoft.com/Forums/en/sharepoint2010setup/thread/a422a3c8-39f6-4b9e-988a-4c4d1e745694)  
  
-   為 SharePoint 服務 (如 SharePoint 2010 管理中心服務) 所使用的服務帳戶，應具有本機作業系統中的管理員權限。  
  
###  <a name="you-see-an-error-message-when-you-try-to-create-a-new-report-builder-report"></a><a name="bkmk_reportbuilder_newreport_error"></a> 嘗試建立新的報表產生器報表時看到錯誤訊息  
 **描述：** 嘗試在文件庫中建立報表產生器報表時，會看到類似下列的錯誤訊息：  
  
 尚未支援此功能，因為 SQL Server Reporting Services 服務應用程式不存在，或是未於管理中心設定報表伺服器 URL。  
  
 **因應措施：** 確認您具有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式，且已正確設定。 如需詳細資訊，請參閱[Install Reporting Services Sharepoint Mode For sharepoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)中的「建立 Reporting Services 服務應用程式」一節  
  
###  <a name="you-see-an-error-message-that-rs_shp-is-not-supported-with-prepareimage"></a><a name="bkmk_RS_SHP_notsupported"></a>您會看到 RS_SHP 不支援 PREPAREIMAGE 的錯誤訊息  
 **描述：** 嘗試執行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的 PREPAREIMAGE 時，會看到類似下列的錯誤訊息：  
  
 「執行 PREPAREIMAGE 動作時不支援指定的功能 'RS_SHP'，因為此動作不支援 SysPrep。 請移除與 SysPrep 不相容的功能，然後重新執行安裝程式。」  
  
 **因應措施：** 沒有因應措施。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不支援 SYSPREP (PREPAREIMAGE)。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式支援 SYSPREP。  
  
##  <a name="troubleshoot-problems-with-the-native-mode-installations"></a><a name="bkmk_tshoot_native"></a> 疑難排解原生模式安裝的問題  
  
###  <a name="performance-counters-are-not-visible-after-upgrading-to-windows-vista-or-windows-server-2008"></a><a name="PerfCounters"></a> 升級到 Windows Vista 或 Windows Server 2008 之後，看不到效能計數器  
 如果您在執行 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 的電腦上，將作業系統升級為 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，在升級之後將不會設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 效能計數器。  
  
#### <a name="to-reinstate-reporting-services-performance-counters"></a>若要重新恢復 Reporting Services 效能計數器  
  
1.  刪除下列登錄機碼：  
  
    -   **HKLM\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service**  
  
    -   **HKLM\SYSTEM\CurrentControlSet\Services\MSRS 2011 Windows Service**  
  
2.  開啟命令視窗，然後在命令提示字元下輸入下列命令：  
  
    -   **執行 \<** *.NET 2.0 Framework directory* **>\InstallUtil.exe \<** *Report Server Bin directory* **>\ReportingServicesLibrary.dll**  
  
        > [!NOTE]  
        >  取代 \<*.NET 2.0 Framework directory*> 為 .NET Framework 2.0 檔案的實體路徑，並 \<*Report Server Bin directory*> 以報表伺服器 bin 檔案的實體路徑來取代。  
  
3.  重新啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務。  
  
 若要上述步驟是否有效，請開啟網頁瀏覽器，並導覽至報表管理員 URL 或報表伺服器 URL。 然後，開啟效能監視器來確認計數器是否有在運作。  
  
#### <a name="to-re-add-the-performance-registry-keys-by-using-registry-editor"></a>若要使用登錄編輯程式重新加入效能登錄機碼  
  
1.  開啟登錄編輯程式：  
  
    1.  按一下 **[開始]**，並按一下 **[執行]**。  
  
    2.  在 [**執行**] 對話方塊的 [**開啟**] 方塊中，輸入 `regedit` 。  
  
2.  在 [登錄編輯程式] 中，選取下列登錄機碼： `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service\Performance`  
  
3.  以滑鼠右鍵按一下 [Performance]**** 節點，並指向 [新增]****，然後按一下 [多字串值]****。  
  
4.  輸入 `Counter Names`，然後按 ENTER。  
  
5.  重複上述步驟，在這個節點中加入 `Counter Types` 登錄機碼。  
  
6.  瀏覽到以下的登錄機碼： `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service\Performance`  
  
7.  以滑鼠右鍵按一下 [Performance]  節點，並指向 [新增]  ，然後按一下 [多字串值]  。  
  
8.  輸入 `Counter Names`，然後按 ENTER。  
  
9. 重複上述步驟，在這個節點中加入 `Counter Types` 登錄機碼。  
  
 修復 64 位元執行個體或手動重新加入登錄機碼後，可以使用效能監視器設定您要監視的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 效能物件。  
  
###  <a name="reportserverexternalurl-and-passthroughcookies-configuration-properties-are-not-configured-after-an-upgrade-from-sql-server-2005"></a><a name="ConfigPropsMissing"></a> 從 SQL Server 2005 升級後，ReportServerExternalURL 和 PassThroughCookies 組態屬性未設定  
 當您從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 升級到 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]，升級程序不會設定 `ReportServerExternalURL` 和 `PassThroughCookies` 組態屬性。 `ReportServerExternalURL`是選擇性屬性，只有在您使用 SharePoint 2.0 Web 組件，而且想要讓使用者能夠抓取報表並在新的瀏覽器視窗中開啟時，才應該設定。 如需的詳細資訊 `ReportServerExternalURL` ，請參閱[&#40;SSRS Configuration Manager&#41;的設定檔中的 url ](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)。 `PassThroughCookies`只有在使用自訂驗證方法時才需要。 如需的詳細資訊 `PassThroughCookies` ，請參閱[設定報表管理員以傳遞自訂驗證 cookie](../security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)。  
  
> [!NOTE]  
>  當您使用自訂驗證時，建議您移轉安裝，而不要執行升級。 如需移轉 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的詳細資訊，請參閱[移轉 Reporting Services 安裝 &#40;原生模式&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)。  
  
 根據預設，這些屬性不存在 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 組態中。 如果您在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中設定了這些屬性，而且仍然需要這些屬性的功能，就必須在升級程序之後將這些屬性手動加入至 **RSReportServer.config** 檔案。 如需詳細資訊，請參閱[修改 Reporting Services 組態檔 &#40;RSreportserver.config&#41;](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
###  <a name="installation-fails-for-a-default-instance-of-sql-server-2005-reporting-services-on-a-computer-that-runs-sql-server-2012reporting-services"></a><a name="Default2005InstallBreaks2008"></a>在執行 SQL Server 2012Reporting Services 的電腦上，SQL Server 2005 Reporting Services 的預設實例安裝失敗  
 如果您嘗試 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 在已經執行實例的電腦上安裝的預設實例 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] ， [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 實例將無法安裝，並出現下列錯誤訊息：  
  
 「具有相同名稱的執行個體已安裝在這部電腦上。 若要繼續 SQL Server 安裝程式，請提供唯一的執行個體名稱。」  
  
 不論 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 執行個體是預設或具名執行個體，也不論電腦上是否已存在相同名稱的 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 執行個體，都會發生這個問題。  
  
 若要解決這個問題，請使用下列其中一個選項：  
  
-   如果您必須 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 在電腦上以預設實例的形式執行，您必須在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 實例之前安裝實例 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 。  
  
-   如果 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 實例不需要是預設實例，您可以在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝實例之後，將實例安裝為已命名的實例 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 。  
  
###  <a name="401-unauthorized-error-when-using-windows-authentication-after-an-upgrade-from-sql-server-2005-to-sql-server-2012"></a><a name="WindowsAuthBreaksAfterUpgrade"></a>401-從 SQL Server 2005 升級至 SQL Server 2012 之後，使用 Windows 驗證時發生未經授權的錯誤  
 如果您從升級 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 到 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] ，而且對報表伺服器服務帳戶使用 NTLM 驗證與內建帳戶，當您在升級後存取報表伺服器或報表管理員時，可能會遇到 401-未經授權的錯誤。  
  
 之所以發生這個錯誤，是因為 Windows 驗證的預設 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 組態中出現變更。 當報表伺服器服務帳戶是 Network Service 或 Local System 時，會設定交涉。 如果報表伺服器服務帳戶不是上述其中一個內建帳戶時，則會設定 NTLM。 若要在升級後修正這個問題，您可以編輯 RSReportServer.config 檔案，並將 `AuthenticationType` 設為 `RSWindowsNTLM`。 如需詳細資訊，請參閱 [Configure Windows Authentication on the Report Server](../security/configure-windows-authentication-on-the-report-server.md) (在報表伺服器上設定 Windows 驗證)。  
  
###  <a name="uninstalling-32-bit-instance-of-sql-server-2012-reporting-services-in-side-by-side-deployment-with-a-64-bit-instance-breaks-the-64-bit-instance"></a><a name="Uninstall32BitBreaks64Bit"></a>在具有64位實例的並存部署中，卸載 SQL Server 2012 Reporting Services 的32位實例會中斷64位實例  
 當您在電腦上並存安裝 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 的 32 位元執行個體與 64 位元執行個體後，如果解除安裝 32 位元執行個體，就會移除四個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 登錄機碼。 這會中斷 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的 64 位元執行個體。 當您解除安裝 32 位元執行個體時，會移除的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 登錄機碼如下：  
  
 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service\Performance:Counter Names` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Windows Service\Performance:Counter Names` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service\Performance:Counter Types` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Windows Service\Performance:Counter Types`  
  
 若要修正這個問題，您可以修復 64 位元執行個體。 雖然建議您使用修復，不過您也可以使用登錄編輯程式以手動方式重新加入登錄機碼。  
  
> [!CAUTION]  
>  不當編輯登錄可能會造成系統嚴重受損。 變更登錄之前，您應該先備份電腦所有的重要資料。  
  
##  <a name="additional-resources"></a><a name="bkmk_additional"></a> 其他資源  
 下列為您可檢閱以協助您進行問題疑難排解的其他資源：  
  
-   TechNet Wiki：疑難排解主題 [疑難排解 SharePoint 整合模式的 SQL Server Reporting Services (SSRS)](https://social.technet.microsoft.com/wiki/contents/articles/troubleshoot-sql-server-reporting-services-ssrs-in-sharepoint-integrated-mode.aspx)  
  
-   [論壇：SQL Server Reporting Services](https://social.msdn.microsoft.com/Forums/sqlreportingservices/threads)  
  
