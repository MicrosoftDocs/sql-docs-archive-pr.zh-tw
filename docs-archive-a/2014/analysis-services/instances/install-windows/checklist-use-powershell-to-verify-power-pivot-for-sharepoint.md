---
title: 檢查清單：使用 PowerShell 驗證 PowerPivot for SharePoint |Microsoft Docs
ms.custom: ''
ms.date: 07/20/2020
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 73a13f05-3450-411f-95f9-4b6167cc7607
author: minewiskan
ms.author: owend
ms.openlocfilehash: 001b3fae82851b9ec08b0383bb3db9e6d011ae32
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688361"
---
# <a name="checklist-use-powershell-to-verify-powerpivot-for-sharepoint"></a>檢查清單：使用 PowerShell 驗證 PowerPivot for SharePoint
  一定要通過穩固的驗證測試來確認您的服務和資料可運作， [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 安裝或復原作業才會是完整的。 在本文中，我們會示範如何使用 Windows PowerShell 執行這些步驟。 我們將每個步驟放在各自的章節中，好讓您可以直接前往特定工作。 例如，請執行本主題＜ [資料庫](#bkmk_databases) ＞一節中的指令碼來驗證服務應用程式和內容資料庫的名稱，以便排程這些應用程式或資料庫進行維護或備份。

|||
|-|-|
|![PowerShell 相關內容](../../../reporting-services/media/rs-powershellicon.jpg "PowerShell 相關內容")|本主題的底部包含了完整的 PowerShell 指令碼。 請使用完整指令碼做為起點來建立自訂指令碼，以便稽核完整的 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 部署。|

||
|-|
|**[!INCLUDE[applies](../../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|

 **本主題內容**：以下目錄中的字母項目對應到圖表的區域。 此圖表將說明

|||
|-|-|
|[準備您的 PowerShell 環境](#bkmk_prerequisites)<br /><br /> [徵兆和建議的動作](#bkmk_symptoms)<br /><br /> **(A)** [Analysis Services Windows 服務](#bkmk_windows_service)<br /><br /> ** (B) ** [PowerPivotSystemService 和 PowerPivotEngineService](#bkmk_engine_and_system_service)<br /><br /> **(C)** [PowerPivot 服務應用程式與 Proxy](#bkmk_powerpivot_service_application)<br /><br /> **(D)** [資料庫](#bkmk_databases)<br /><br /> [SharePoint 功能](#bkmk_features)<br /><br /> [計時器工作](#bkmk_timer_jobs)<br /><br /> [健全狀況規則](#bkmk_health_rules)<br /><br /> **(E)** [Windows 和 ULS 記錄](#bkmk_logs)<br /><br /> [MSOLAP 提供者](#bkmk_msolap)<br /><br /> [ADOMD.Net 用戶端程式庫](#bkmk_adomd)<br /><br /> [健全狀況資料收集規則](#bkmk_health_collection)<br /><br /> [方案](#bkmk_solutions)<br /><br /> [手動驗證步驟](#bkmk_manual)<br /><br /> [其他資源](#bkmk_more_resources)<br /><br /> [完整 PowerShell 指令碼](#bkmk_full_script)|![powershell 的 powerpivot 驗證](../../../sql-server/install/media/ssas-powershell-component-verification.png "powershell 的 powerpivot 驗證")|

##  <a name="prepare-your-powershell-environment"></a><a name="bkmk_prerequisites"></a>準備您的 PowerShell 環境
 本節的步驟會準備您的 PowerShell 環境。 根據目前設定指令碼環境的方式，可能不需要這些步驟。

 **PowerShell 權限**

 使用 **系統管理權限**開啟 PowerShell 視窗或 PowerShell ISE (整合式指令碼環境)。 如果當您執行命令時沒有系統管理權限，您將會看到類似下面的錯誤訊息：

 Get-SPLogEvent：您必須擁有電腦的 **系統管理員權限** 才能執行此指令程式。

 **SharePoint 和 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)]** 模組

 如果當您執行 SharePoint 相關的指令程式時看到類似下面的錯誤訊息，請執行 Add-PSSnapin 命令：

 **無法辨識**'Get-PowerPivotSystemService' 詞彙是否為 Cmdlet、函數、指令檔或可執行程式的名稱。 請檢查名稱拼字，如果名稱含有路徑，請確認路徑正確，然後再試一次。

```
Add-PSSnapin Microsoft.Sharepoint.Powershell -EA 0
```

 **Windows PowerShell**

 如需有關 PowerShell ISE 的詳細資訊，請參閱＜ [Windows PowerShell ISE 簡介](https://technet.microsoft.com/library/dd315244.aspx) ＞和＜ [使用 Windows Powershell 管理 SharePoint 2013](https://technet.microsoft.com/library/ee806878\(v=office.15\).aspx)＞。

|||
|-|-|
|![sharepoint 一般應用程式設定中的 powerpivot](../../../sql-server/install/media/ssas-powerpivot-logo.png "sharepoint 一般應用程式設定中的 powerpivot")|您可以選擇使用 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 管理儀表板來驗證管理中心的大多數元件。 若要在管理中心開啟儀表板，請按一下 **[一般應用程式設定]**，然後按一下 **[PowerPivot]** 中的 **[管理儀表板]**。 如需有關儀表板的詳細資訊，請參閱＜ [PowerPivot Management Dashboard and Usage Data](../../power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)＞。|

##  <a name="symptoms-and-recommended-actions"></a><a name="bkmk_symptoms"></a>徵兆和建議的動作
 下表是徵兆或問題清單以及這個主題的建議章節，您可參考這些章節來幫助您解決問題。

|徵狀|請參閱章節|
|-------------|-----------------|
|資料重新整理並未執行|請參閱＜ [Timer Jobs](#bkmk_timer_jobs) ＞一節，並確認 **線上 PowerPivot 資料重新整理計時器工作** 在線上。|
|管理儀表板資料是舊的|請參閱＜ [計時器工作](#bkmk_timer_jobs) ＞一節，並確認 **管理儀表板處理計時器工作** 在線上。|
|管理儀表板的某些部分|如果您將 PowerPivot for SharePoint 安裝到具有管理中心拓撲的伺服陣列中，但沒有 Excel Services 或 PowerPivot for SharePoint，如果您想要完整存取 PowerPivot 管理儀表板中的內建報表，您必須下載及安裝 Microsoft ADOMD.NET 用戶端程式庫。 儀表板中的某些報表會使用 ADOMD.NET 來存取內部資料，這些資料會提供關於在伺服陣列中 PowerPivot 查詢處理和伺服器健全狀況的報告資料。 請參閱 [ADOMD.Net 用戶端程式庫](#bkmk_adomd) 一節和 [在執行管理中心的 Web 前端伺服器上安裝 ADOMD.NET](../../../sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md)主題。|
|\<future content>||

##  <a name="analysis-services-windows-service"></a><a name="bkmk_windows_service"></a>Analysis Services Windows 服務
 本節的指令碼會在 SharePoint 模式下驗證 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的執行個體。 確認**服務正在執行。**

```powershell
Get-Service | Select name, displayname, status | Where {$_.Name -eq "msolap`$powerpivot"} | Format-Table -Property * -AutoSize | Out-Default
```

```Output
Name              DisplayName                                Status
----              -----------                                ------
MSOLAP$POWERPIVOT SQL Server Analysis Services (POWERPIVOT) Running
```

##  <a name="powerpivotsystemservice-and-powerpivotengineservice"></a><a name="bkmk_engine_and_system_service"></a>PowerPivotSystemService 和 PowerPivotEngineService
 本節的指令碼會驗證 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 系統服務。 有一個適用於 SharePoint 2013 部署的系統服務以及適用於 SharePoint 2010 部署的兩個服務。

 **PowerPivotSystemService**

 確認狀態為**線上**。

```powershell
Get-PowerPivotSystemService | Select typename, status, applications, farm | Format-Table -Property * -AutoSize | Out-Default
```

```Output
TypeName                                  Status Applications                             Farm
--------                                  ------ ------------                             ----
SQL Server PowerPivot Service Application Online {Default PowerPivot Service Application} SPFarm Name=SharePoint_Config_77d8ab0744a34e8aa27c806a2b8c760c
```

 **PowerPivotEngineService**

> [!NOTE]
>  如果您正在使用 SharePoint 2013，請**略過這個指令碼** 。 PowerPivotEngineService 不是 SharePoint 2013 部署的一部分。 如果您在 SharePoint 2013 上執行 Get-PowerPivot**Engine**Service 指令程式，您將會看到類似下面的錯誤訊息。 即使您已經執行本主題的＜必要條件＞一節所描述的 Add-PSSnapin 命令，還是會傳回這個錯誤訊息。
> 
>  'Get-PowerPivotEngineService' 詞彙無法辨識為指令程式名稱

 在 SharePoint 2010 部署中，確認狀態為 **線上**。

```powershell
Get-PowerPivotEngineService | Select typename, status, name, instances, farm | Format-Table -Property * -AutoSize | Out-Default
```

```Output
TypeName  : SQL Server Analysis Services
Status    : Online
Name      : MSOLAP$POWERPIVOT
Instances : {POWERPIVOT}
Farm      : SPFarm Name=SharePoint_Config
```

##  <a name="powerpivot-service-applications-and-proxies"></a><a name="bkmk_powerpivot_service_application"></a>PowerPivot 服務應用程式 (s) 和 proxy
 確認狀態為 **線上**。 Excel Services 應用程式不會使用服務應用程式資料庫，因此指令程式不會傳回資料庫名稱。 請記下 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服務應用程式所使用的資料庫，好讓您能夠在本主題稍後的＜資料庫＞一節中確認資料庫為線上狀態。

 **PowerPivot 和 Excel 服務應用程式**

 針對 SharePoint 2010 部署，確認狀態為 **線上**。

```powershell
Get-PowerPivotServiceApplication | Select typename,name, status, unattendedaccount, applicationpool, farm, database
Get-SPExcelServiceApplication | Select typename, DisplayName, status
```

```Output
TypeName          : PowerPivot Service Application
Name              : PowerPivotServiceApplication1
Status            : Online
UnattendedAccount : PowerPivotUnattendedAccount
ApplicationPool   : SPIisWebServiceApplicationPool Name=sqlbi_serviceapp
Farm              : SPFarm Name=SharePoint_Config
Database          : GeminiServiceDatabase Name=PowerPivotServiceApplication1_19648f3f2c944e27acdc6c20aab8487a

TypeName    : Excel Services Application Web Service Application
DisplayName : Excel Services Application
Status      : Online
```

 **服務應用程式集區**

> [!NOTE]
>  下列程式碼範例會先傳回預設 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 服務應用程式的 applicationpool 屬性。 從名稱會從字串剖析並用來取得應用程式集區物件的狀態。
> 
>  確認狀態為**線上**。 如果狀態不是線上，或當您流覽網站時看到「HTTP 錯誤」 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] ，請確認 IIS 應用程式集區中的身分識別認證仍然正確。 IIS 集區名稱將會是 Get-SPServiceApplicationPool 命令所傳回之 ID 屬性的值。

```powershell
$poolname = [string](Get-PowerPivotServiceApplication | Select -Property applicationpool)
$position = $poolname.lastindexof("=")
$poolname = $poolname.substring($position+1)
$poolname = $poolname.substring(0,$poolname.length-1)

Get-SPServiceApplicationPool | Select name, status, processaccountname, id | Where {$_.Name -eq $poolname} | Format-Table -Property * -AutoSize | Out-Default
```

```Output
Name                           Status ProcessAccountName Id
----                           ------ ------------------ ------- 
SharePoint Web Services System Online DOMAIN\account     89b50ec3-49e3-4de7-881a-2cec4b8b73ea
```

 ![注意](../../../reporting-services/media/rs-fyinote.png "注意")應用程式集區也可以在管理中心的 [**管理服務應用程式**] 頁面上進行驗證。 按一下服務應用程式的名稱，然後按一下功能區中的 **[屬性]** 。

 **PowerPivot 和 Excel 服務應用程式 Proxy**

 確認狀態為**線上**。

```powershell
Get-SPServiceApplicationProxy | Select typename, status, unattendedaccount, displayname | Where {$_.TypeName -Like "*powerpivot*" -Or $_.TypeName -Like "*excel services*"} | Format-Table -Property * -AutoSize | Out-Default
```

```Output
TypeName                                                 Status UnattendedAccount           DisplayName
--------                                                 ------ -----------------           -----------
PowerPivot Service Application Proxy                     Online PowerPivotUnattendedAccount PowerPivotServiceApplication1
Excel Services Application Web Service Application Proxy Online                             Excel Services Application
```

##  <a name="databases"></a><a name="bkmk_databases"></a>資料庫
 下列指令碼會傳回服務應用程式資料庫及所有內容資料庫的狀態。 確認狀態為 **線上**。

```powershell
Get-SPDatabase | Select name, status, server, typename | Where {$_.TypeName -eq "content database" -Or $_.TypeName -Like "*Gemini*"} | Format-Table -Property * -AutoSize | Out-Default
```

```Output
Name                                                                       Status Server                  TypeName 
----                                                                       ------ ------                  -------- 
DefaultPowerPivotServiceApplicationDB-38422181-2b68-4ab2-b2bb-9c00c39e5a5e Online SPServer Name=TESTSERVER Microsoft.AnalysisServices.SPAddin.GeminiServiceDatabase
DefaultWebApplicationDB-f0db1a8e-4c22-408c-b9b9-153bd74b0312               Online TESTSERVER\POWERPIVOT    Content Database 
SharePoint_Admin_3cadf0b098bf49e0bb15abd487f5c684                          Online TESTSERVER\POWERPIVOT    Content Database
```

##  <a name="sharepoint-features"></a><a name="bkmk_features"></a>SharePoint 功能
 確認網站、Web 和伺服器陣列功能都在線上。

```powershell
Get-SPFeature | Select displayname, status, scope, farm | Where {$_.displayName -Like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default
```

```Output
DisplayName     Status Scope Farm                         
-----------     ------ ----- ----                         
PowerPivotSite  Online  Site SPFarm Name=SharePoint_Config
PowerPivotAdmin Online   Web SPFarm Name=SharePoint_Config
PowerPivot      Online  Farm SPFarm Name=SharePoint_Config
```

##  <a name="timer-jobs"></a><a name="bkmk_timer_jobs"></a>計時器工作
 確認計時器工作在 **線上**。 SharePoint 2013 上並未安裝 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] EngineService，因此指令碼將不會在 SharePoint 2013 部署中列出 EngineService 計時器工作。

```powershell
Get-SPTimerJob | Where {$_.service -Like "*power*" -Or $_.service -Like "*mid*"} | Select status, displayname, LastRunTime, service | Format-Table -Property * -AutoSize | Out-Default
```

```Output
      Status DisplayName                                                                          LastRunTime          Service                             
------ -----------                                                                          -----------          -------                             
Online Health Analysis Job (Daily, SQL Server Analysis Services, All Servers)               4/9/2014 12:00:01 AM EngineService Name=MSOLAP$POWERPIVOT
Online Health Analysis Job (Hourly, SQL Server Analysis Services, All Servers)              4/9/2014 1:00:01 PM  EngineService Name=MSOLAP$POWERPIVOT
Online Health Analysis Job (Weekly, SQL Server Analysis Services, All Servers)              4/6/2014 12:00:10 AM EngineService Name=MSOLAP$POWERPIVOT
Online PowerPivot Management Dashboard Processing Timer Job                                 4/8/2014 3:45:38 AM  MidTierService
Online PowerPivot Health Statistics Collector Timer Job                                     4/9/2014 1:00:12 PM  MidTierService
Online PowerPivot Data Refresh Timer Job                                                    4/9/2014 1:09:36 PM  MidTierService
Online Health Analysis Job (Daily, SQL Server PowerPivot Service Application, All Servers)  4/9/2014 12:00:00 AM MidTierService
Online Health Analysis Job (Daily, SQL Server PowerPivot Service Application, Any Server)   4/9/2014 12:00:00 AM MidTierService
Online Health Analysis Job (Weekly, SQL Server PowerPivot Service Application, All Servers) 4/6/2014 12:00:03 AM MidTierService
Online Health Analysis Job (Weekly, SQL Server PowerPivot Service Application, Any Server)  4/6/2014 12:00:03 AM MidTierService
Online PowerPivot Setup Extension Timer Job                                                 4/1/2014 1:40:31 AM  MidTierService
```

##  <a name="health-rules"></a><a name="bkmk_health_rules"></a>健全狀況規則
 SharePoint 2013 部署中的規則較少。 如需每個 SharePoint 環境的完整規則清單以及如何使用規則的說明，請參閱[PowerPivot 健全狀況規則-設定](../../power-pivot-sharepoint/configure-power-pivot-health-rules.md)。

```powershell
Get-SPHealthAnalysisRule | Select name, enabled, summary | Where {$_.summary -Like "*power*"}  | Format-Table -Property * -AutoSize | Out-Default
```

```Output
Name                          Enabled Summary
----                          ------- -------         
SecondaryLogonHealthRule         True PowerPivot:  Secondary Logon service (seclogon) is disabled
DataRefreshTimerJobHealthRule    True PowerPivot: The PowerPivot Data Refresh timer job is disabled.
ASUsageLoadHealthRule            True PowerPivot: The ratio of load events to connections is too high.
ASMiniDumpHealthRule             True PowerPivot: One or more minidump files were found in the Logs directory, indicating a program crash
ASUsageCubeRule                  True PowerPivot: Usage data is not getting updated at the expected frequency.
ASADOMDNETHealthRule             True PowerPivot: ADOMD.NET is not installed on a standalone WFE that is configured for central admin
MidTierAcctReadPermissionRule    True PowerPivot: MidTier process account should have 'Full Read' permission on all associated SPWebApplications.
```

##  <a name="windows-and-uls-logs"></a><a name="bkmk_logs"></a>Windows 和 ULS 記錄檔
 **Windows 事件記錄檔**

 下列命令將會搜尋 Windows 事件記錄檔，以便找出 SharePoint 模式下與 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體有關的事件。 如需停用事件或變更事件層級的詳細資訊，請參閱[設定及查看 SharePoint 記錄檔和診斷記錄 &#40;PowerPivot for SharePoint&#41;](../../power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md)。

 **服務名稱** ：MSOLAP$POWERPIVOT

 **Windows 服務中的顯示名稱** ：SQL Server Analysis Services (POWERPIVOT)

```powershell
Get-EventLog "application" | Where-Object {$_.source -Like "msolap`$powerpivot*"}  | Select timegenerated, entrytype , source, message | Format-Table -property * -AutoSize | Out-Default
```

```Output
TimeGenerated           EntryType Source            Message
-------------           --------- ------            -------
4/16/2014 1:45:19 PM  Information MSOLAP$POWERPIVOT Software usage metrics are disabled.
4/16/2014 1:45:19 PM  Information MSOLAP$POWERPIVOT Service started. Microsoft SQL Server Analysis Services 64 Bit Evaluation (x64) RTM 12.0.1997.5.
4/16/2014 1:45:18 PM  Information MSOLAP$POWERPIVOT The flight recorder was started.
4/14/2014 6:45:37 PM  Information MSOLAP$POWERPIVOT Software usage metrics are disabled.
```

 **SharePoint ULS 記錄 (過去 48 個小時)**

 下列命令將會從過去 48 小時內建立的 ULS 記錄傳回 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 訊息。 針對您的需要調整 addhours 參數。

```powershell
Get-SPLogEvent -StartTime(Get-Date).AddHours(-48) | Where-Object {$_.Area -eq "powerpivot service" -and $_.level -eq "high"} | Select timestamp, area, category, eventid,level, message | Format-Table -Property * -AutoSize | Out-Default
```

 以下的命令變化只會傳回 **資料重新整理** 類別目錄的記錄事件。

```powershell
Get-SPLogEvent -starttime(Get-Date).addhours(-48) | Where-Object {$_.category -eq "data refresh" -and $_.level -eq "high"} | Select timestamp, area, category, eventid, level, correlation, message
```

```Output
Timestamp   : 4/14/2014 7:15:01 PM
Area        : PowerPivot Service
Category    : Data Refresh
EventID     : 43
Level       : High
Correlation : 5755879c-7cab-e097-8f80-f27895d44a77
Message     : The following error occurred when working with the service application, Default PowerPivot Service Application. Skipping the service application..

Timestamp   : 4/14/2014 7:15:02 PM
Area        : PowerPivot Service
Category    : Data Refresh
EventID     : 99
Level       : High
Correlation : 5755879c-7cab-e097-8f80-f27895d44a77
Message     : EXCEPTION: System.TimeoutException: The request channel timed out while waiting for a reply after 00:00:47.0625313. Increase the timeout value passed to 
              the call to Request or increase the SendTimeout value on the Binding. The time allotted to this operation may have been a portion of a longer timeout. 
              ---> System.TimeoutException: The HTTP request to 'http://localhost:32843/SecurityTokenServiceApplication/securitytoken.svc/actas' has exceeded the 
              allotted timeout of 00:00:54.5930000. The time allotted to this operation may have been a portion of a longer timeout. ---> System.Net.WebException: The 
              operation has timed out     at System.Net.HttpWebRequest.GetResponse()     at 
              System.ServiceModel.Channels.HttpChannelFactory`1.HttpRequestChannel.HttpChannelRequest.WaitForReply(TimeSpan timeout...
```

##  <a name="msolap-provider"></a><a name="bkmk_msolap"></a>MSOLAP 提供者
 驗證 MSOLAP 提供者。 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]和 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 需要 MSOLAP. 5。

```powershell
$excelApp = Get-SPExcelServiceApplication
Get-SPExcelDataProvider -ExcelServiceApplication $excelApp | Select providerid, providertype, description | Where {$_.providerid -like "msolap*" } | Format-Table -Property * -AutoSize | Out-Default
```

```Output
ProviderId ProviderType Description
---------- ------------ -----------
MSOLAP     Oledb        Microsoft OLE DB Provider for OLAP Services     
MSOLAP.3   Oledb        Microsoft OLE DB Provider for OLAP Services 9.0 
MSOLAP.4   Oledb        Microsoft OLE DB Provider for OLAP Services 10.0
MSOLAP.5   Oledb        Microsoft OLE DB Provider for OLAP Services 11.0
```

 如需詳細資訊，請參閱 [在 SharePoint 伺服器上安裝 Analysis Services OLE DB 提供者](../../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md) 和 [加入 MSOLAP.5 做為 Excel Services 中受信任的資料提供者](https://technet.microsoft.com/library/hh758436.aspx)。

##  <a name="adomdnet-client-library"></a><a name="bkmk_adomd"></a>ADOMD.Net 用戶端程式庫

```powershell
Get-WMIObject -Class win32_product | Where-Object {$_.name -Like "*ado*"} | Select name, version, vendor | Format-Table -Property * -AutoSize | out-default
```

```Output
name                                                  version      vendor
----                                                  -------      ------
Microsoft SQL Server 2008 Analysis Services ADOMD.NET 10.1.2531.0  Microsoft Corporation
Microsoft SQL Server 2005 Analysis Services ADOMD.NET 9.00.1399.06 Microsoft Corporation
```

 如需詳細資訊，請參閱 [在執行管理中心的 Web 前端伺服器上安裝 ADOMD.NET](../../../sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md)。

##  <a name="health-data-collection-rules"></a><a name="bkmk_health_collection"></a>健全狀況資料收集規則
 確認 **[狀態]** 為線上，而且 **[已啟用]** 成立。

```powershell
Get-SPUsageDefinition | Select name, status, enabled, tablename, DaysToKeepDetailedData | Where {$_.name -Like "powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default
```

```Output
Name                         Status Enabled TableName                   DaysToKeepDetailedData
----                         ------ ------- ---------                   ----------------------
PowerPivot Connections       OnlineTrue AnalysisServicesConnections  14
PowerPivot Load Data Usage   Online    True AnalysisServicesLoads                           14
PowerPivot Query Usage       Online    True AnalysisServicesRequests                        14
PowerPivot Unload Data Usage Online    True AnalysisServicesUnloads                         14
```

 如需詳細資訊，請參閱 [PowerPivot Usage Data Collection](../../power-pivot-sharepoint/power-pivot-usage-data-collection.md)。

##  <a name="solutions"></a><a name="bkmk_solutions"></a>適用
 如果其他元件在線上，您可以略過方案的驗證。 不過，如果遺漏了健全狀況規則，請確認這兩個方案都存在，並確認兩個 PowerPivot 方案為 **線上** 和 **已部署**狀態。

```powershell
Get-SPSolution | Select name, status, deployed, DeploymentState, DeployedServers | Where {$_.Name -Like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default
```

SharePoint 2013：

```Output
Name                                 Status Deployed        DeploymentState DeployedServers
----                                 ------ --------        --------------- ---------------
powerpivotfarm14solution.wsp         Online     True         GlobalDeployed {UETESTA00}
powerpivotfarmsolution.wsp           Online     True         GlobalDeployed {UETESTA00}
powerpivotwebapplicationsolution.wsp Online     True WebApplicationDeployed {UETESTA00}
```

SharePoint 2010：

```Output
Name                 Status Deployed        DeploymentState DeployedServers 
----                 ------ --------        --------------- --------------- 
powerpivotfarm.wsp   Online     True         GlobalDeployed {uesql11spoint2}
powerpivotwebapp.wsp Online     True WebApplicationDeployed {uesql11spoint2}
```

 如需如何部署 SharePoint 方案的詳細資訊，請參閱 [部署方案套件 (SharePoint Server 2010)](https://technet.microsoft.com/library/cc262995\(v=office.14\).aspx)。

##  <a name="manual-verification-steps"></a><a name="bkmk_manual"></a>手動驗證步驟
 本節描述無法使用 PowerShell 指令程式完成的步驟。

 **排定的資料重新整理** ：將重新整理活頁簿排程設定為 **[並且盡快重新整理]**。  如需詳細資訊，請參閱[排程資料重新整理和不支援 Windows 驗證的資料來源 &#40;PowerPivot for SharePoint&#41;](../../power-pivot-sharepoint/schedule-data-refresh-and-data-sources-no-windows-authentication.md)中的「確認資料重新整理」一節。

##  <a name="more-resources"></a><a name="bkmk_more_resources"></a>其他資源
 [Windows PowerShell 中的 Web 伺服器 (IIS) 管理指令程式](https://technet.microsoft.com/library/ee790599.aspx)。

 [要在 SharePoint 中檢查服務、IIS 網站和應用程式集區狀態的 PowerShell](https://gallery.technet.microsoft.com/office/PowerShell-to-check-a6ed72a0)。

 [SharePoint Server 2013 的 Windows PowerShell 參考](https://technet.microsoft.com/library/ee890108\(v=office.15\).aspx)

 [SharePoint Foundation 2010 的 Windows PowerShell 參考](https://technet.microsoft.com/library/ee890105\(v=office.14\).aspx)

 [使用 Windows PowerShell 管理 Excel Services (SharePoint Server 2010)](https://technet.microsoft.com/library/ff191201\(v=office.14\).aspx)

 [檢視與讀取 SQL Server 安裝程式記錄檔](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)

 [使用 Get-EvenLog 指令程式](https://technet.microsoft.com/library/ee176846.aspx)

##  <a name="full-powershell-script"></a><a name="bkmk_full_script"></a>完整的 PowerShell 腳本
 下列指令碼包含之前章節中的所有命令。 此指令碼會依照命令出現在本主題的相同順序來執行命令。 此指令碼包含本主題所註明的一些選擇性命令變化，以免您需要額外的篩選。 這些變化會以註解字元 (#) 停用。 此指令碼也包含用來驗證 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint 模式的一些陳述式。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 陳述式會以註解字元 (#) 停用。

```powershell
# This script audits services related to PowerPivot for SharePoint
$starttime = Get-Date
write-host -foregroundcolor DarkGray StartTime $starttime

Write-Host  "Import the SharePoint PowerShell snappin"
Add-PSSnapin Microsoft.Sharepoint.Powershell -EA 0

Write-Host -ForegroundColor Green "Analysis Services Windows Service"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-Service | Select name, displayname, status | Where {$_.Name -eq "msolap`$powerpivot"} | Format-Table -Property * -AutoSize | Out-Default

Write-Host -ForegroundColor Green "PowerPivotEngineService and PowerPivotSystemService"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"

Get-PowerPivotSystemService | Select typename, status, applications, farm | Format-Table -property * -AutoSize | Out-Default
# If needed, you can run the following to compare job definitions specific to the service against the results of the timer job definition section
#Get-PowerPivotSystemService | select -ExpandProperty jobdefinitions | select displayname, schedule, service | format-table -property * -autosize | out-default

Get-PowerPivotEngineService | Select typename, status, name, instances, farm | Format-Table -property * -AutoSize | Out-Default
# If needed, you can run the following to compare job definitions specific to the service against the results of the timer job definition section
#Get-PowerPivotEngineService | select -ExpandProperty jobdefinitions | select displayname, schedule, service | format-table -property * -autosize | out-default

#Write-Host -ForegroundColor Green "Service Instances - optional if you want to associate services with the server"
#Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
#Get-SPServiceInstance | select typename, status, server, service, instance | where {$_.TypeName -like "*powerpivot*" -or $_.TypeName -like "*excel*" -or $_.TypeName -like "*Analysis Services*"} | format-table -property * -autosize | out-default
#Get-PowerPivotEngineServiceInstance  | select typename, ASServername, status, server, service, instance
#Get-PowerPivotSystemServiceInstance  | select typename, ASSServerName, status, server, service, instance

Write-Host -ForegroundColor Green "PowerPivot And Excel Service Applications"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-PowerPivotServiceApplication | Select typename,name, status, unattendedaccount, applicationpool, farm, database
Get-SPExcelServiceApplication | Select typename,  DisplayName, status

#Write-Host ""
Write-Host -ForegroundColor Green "PowerPivot Service Application pool"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
# the following assumes there is only 1 PowerPivot Service Application, and returns that application's pool name.  if you have more than one, use the 2nd version
$poolname = [string](Get-PowerPivotServiceApplication | Select -Property applicationpool)
$position = $poolname.lastindexof("=")
$poolname = $poolname.substring($position+1)
$poolname = $poolname.substring(0,$poolname.length-1)
Get-SPServiceApplicationPool | Select name, status, processaccountname, id | Where {$_.Name -eq $poolname} | Format-Table -Property * -AutoSize | Out-Default

#Write-Host ""
Write-Host -ForegroundColor Green "PowerPivot and Excel Service Application Proxy"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPServiceApplicationProxy |  Select typename, status, unattendedaccount, displayname | Where {$_.TypeName -like "*powerpivot*" -or $_.TypeName -like "*excel services*"} | Format-Table -Property * -AutoSize | Out-Default
#Get-SPServiceApplicationProxy |  select typename, status, unattendedaccount, displayname | where {$_.TypeName -like "*powerpivot*" -or $_.TypeName -like "*Reporting Services*" -or $_.TypeName -like "*excel services*"} | format-table -property * -autosize | out-default

Write-Host -ForegroundColor Green "DATABASES"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPDatabase | Select name, status, server, typename | Where {$_.TypeName -eq "content database" -or $_.TypeName -like "*Gemini*"} | Format-Table -Property * -AutoSize | Out-Default
#Get-SPDatabase | select name, status, server, typename | where {$_.TypeName -eq "content database" -or $_.TypeName -like "*Gemini*" -or $_.TypeName -like "*ReportingServices*"}

Write-Host -ForegroundColor Green "features"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPFeature | Select displayname, status, scope, farm | Where {$_.displayName -like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default
#Get-SPFeature | select displayname, status, scope, farm | where {$_.displayName -like "*powerpivot*" -or $_.displayName -like "*ReportServer*"}  | format-table -property * -autosize | out-default

Write-Host -ForegroundColor Green "Timer Jobs (Job Definitions) -- list is the same as seen in the 'Review timer job definitions' section of the management dashboard"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPTimerJob | Where {$_.service -like "*power*" -or $_.service -like "*mid*"} | Select status, displayname, LastRunTime, service | Format-Table -Property * -AutoSize | Out-Default

Write-Host -ForegroundColor Green "health rules"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPHealthAnalysisRule | Select name, enabled, summary | Where {$_.summary -Like "*power*"}  | Format-Table -Property * -AutoSize | Out-Default

$time = Get-Date
Write-Host -ForegroundColor DarkGray StartTime $starttime
Write-Host -ForegroundColor DarkGray EndTime $time

Write-Host -ForegroundColor Green "Windows Event Log data MSSQL$POWERPIVOT and "
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-EventLog "application" | Where-Object {$_.source -like "msolap`$powerpivot*"}  | Select timegenerated, entrytype , source, message | Format-Table -Property * -autosize | Out-Default
#The following is the same command but with the Inforamtion events filtered out.
#Get-EventLog "application" | Where-Object {$_.source -like "msolap`$powerpivot*" -and ($_.entrytype -match "error" -or $_.entrytype -match "critical" -or $_.entrytype -match "warning")}  |select timegenerated, entrytype , source, message | format-table -property * -autosize | out-default

#Write-Host ""
Write-Host -ForegroundColor Green "ULS Log data"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPLogEvent -StartTime(Get-Date).AddHours(-48) | Where-Object {$_.Area -eq "powerpivot service" -and $_.level -eq "high"} | Select timestamp, area, category, eventid, level, correlation, message | Format-Table -Property * -AutoSize | Out-Default
#the following example filters for the category 'data refresh'
#Get-SPLogEvent -starttime(get-date).addhours(-48) | Where-Object {$_.category -eq "data refresh" -and $_.level -eq "high"} | select timestamp, area, category, eventid, level, correlation, message

$time = Get-Date
Write-Host -ForegroundColor DarkGray StartTime $starttime
Write-Host -ForegroundColor DarkGray EndTime $time

Write-Host -ForegroundColor Green "MSOLAP data provider for Excel Servivces, service application"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
$excelApp = Get-SPExcelServiceApplication
Get-SPExcelDataProvider -ExcelServiceApplication $excelApp | Select providerid, providertype, description | Where {$_.providerid -like "msolap*" } | Format-Table -Property * -AutoSize | Out-Default

Write-Host -ForegroundColor Green "ADOMD.net client library"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-WMIObject -Class win32_product | Where-Object {$_.name -like "*ado*"} | Select name, version, vendor | Format-Table -Property * -AutoSize | Out-Default

Write-Host -ForegroundColor Green "Usage Data Rules"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPUsageDefinition | Select name, status, enabled, tablename, DaysToKeepDetailedData | Where {$_.name -like "powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default

Write-Host -ForegroundColor Green "Solutions"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPSolution | Select name, status, deployed, DeploymentState, DeployedServers | Where {$_.Name -like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default

$time = Get-Date
Write-Host -ForegroundColor DarkGray StartTime $starttime
Write-Host -ForegroundColor DarkGray EndTime $time
```
