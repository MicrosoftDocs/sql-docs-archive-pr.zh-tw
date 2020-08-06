---
title: 適用于 Reporting Services SharePoint 模式的 PowerShell Cmdlet |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 7835bc97-2827-4215-b0dd-52f692ce5e02
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2b20ad870fd8a9cd7f220eebb2b954d7a88a10c3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87710257"
---
# <a name="powershell-cmdlets-for-reporting-services-sharepoint-mode"></a>Reporting Services SharePoint 模式的 PowerShell Cmdlet
  當您安裝 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sharepoint 模式時，系統會安裝 PowerShell Cmdlet，以支援 SharePoint 模式的報表伺服器。 這些指令程式涵蓋三個功能類別。  
  
-   安裝 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 共用服務和 Proxy。  
  
-   佈建和管理 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式和相關聯 Proxy。  
  
-   管理 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 功能，例如擴充功能和加密金鑰。  
  
||  
|-|  
|[!INCLUDE[applies](../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]SharePoint 模式|  
  
 **本主題包含下列內容：**  
  
-   [Cmdlet 摘要](#bkmk_cmdlet_sum)  
  
-   [共用服務和 Proxy Cmdlet](#bkmk_sharedservice_cmdlets)  
  
-   [服務應用程式和 Proxy Cmdlet](#bkmk_serviceapp_cmdlets)  
  
-   [Reporting Services 自訂功能 Cmdlet](#bkmk_ssrsfeatures_cmdlets)  
  
-   [基本範例](#bkmk_basic_samples)  
  
-   [詳細範例](#bkmk_detailedsamples)  
  
    -   [建立 Reporting Services 服務應用程式和 proxy](#bkmk_example_create_service_application)  
  
    -   [檢閱及更新 Reporting Services 傳遞延伸模組](#bkmk_example_delivery_extension)  
  
    -   [取得並設定 Reporting Services 應用程式資料庫的屬性，例如資料庫逾時](#bkmk_example_db_properties)  
  
    -   [列出 reporting services 資料延伸模組-SharePoint 模式](#bkmk_example_list_data_extensions)  
  
    -   [變更並列出訂閱擁有者](#bkmk_change_subscription_owner)  
  
##  <a name="cmdlet-summary"></a><a name="bkmk_cmdlet_sum"></a>Cmdlet 摘要  

 若要執行指令程式，您需要開啟 SharePoint 管理命令介面。 您也可以使用 Microsoft Windows 隨附的圖形化使用者介面編輯器 **Windows PowerShell 整合式指令碼環境 (ISE)**。 如需詳細資訊，請參閱 [Starting Windows PowerShell on Windows Server](https://docs.microsoft.com/powershell/scripting/getting-started/starting-windows-powershell)。 在下列 Cmdlet 摘要中，服務應用程式「資料庫」的參考是指服務應用程式所建立和使用的所有資料庫 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 。 其中包括組態、警示和暫時資料庫。  

  
 當您輸入 PowerShell 範例時，將會看到類似下面的錯誤訊息：  
  
-   Install-SPRSService: 無法辨識 'Install-SPRSService' 詞彙是否為  
    Cmdlet、函數、指令檔或可執行程式的名稱。 請檢查名稱拼字，如果名稱含有路徑，請確認路徑正確，然後再試一次。  
  
 發生以下其中一個問題：  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式未安裝，因此 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 指令程式也未安裝。  
  
-   您已在 Windows PowerShell 或 Windows PowerShell ISE 中執行 PowerShell 命令，而不是在 SharePoint 管理命令介面中執行。 使用 SharePoint 管理命令介面，或是透過以下命令將 SharePoint 嵌入式管理單元加入至 Windows PowerShell 視窗：  
  
    ```powershell
    Add-PSSnapin Microsoft.SharePoint.PowerShell  
    ```  
  
 如需詳細資訊，請參閱[使用 Windows PowerShell 來管理 SharePoint 2013](https://technet.microsoft.com/library/ee806878.aspx) (https://technet.microsoft.com/library/ee806878.aspx) 。  
  
#### <a name="to-open-the-sharepoint-management-shell-and-run-cmdlets"></a>若要開啟 SharePoint 管理命令介面並執行指令程式  
  
1.  按一下 [**開始**] 按鈕  
  
2.  按一下 **[Microsoft SharePoint 產品]** 群組。  
  
3.  按一下 **[SharePoint 管理命令介面]**。  
  
 若要檢視 Cmdlet 的命令列說明，請在 PowerShell 命令提示字元中使用 PowerShell 'Get-Help' 命令。 例如：  
  
 `Get-Help Get-SPRSServiceApplicationServers`  
  
###  <a name="shared-service-and-proxy-cmdlets"></a><a name="bkmk_sharedservice_cmdlets"></a> 共用服務和 Proxy 指令程式  
 下表包含用於 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 共用服務的 PowerShell 指令程式。  
  
|Cmdlet|描述|  
|------------|-----------------|  
|Install-SPRSService|安裝及註冊或是解除安裝 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 共用服務。 只有在安裝了 SharePoint 模式之 SQL Server [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 的電腦上才可以執行這項作業。 針對安裝會進行兩項作業：<br /><br /> 1) [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務已安裝在伺服器陣列中。<br /><br /> 2) 將 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務實例安裝到目前的電腦上。<br /><br /> 針對解除安裝會進行兩項作業：<br />1) [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務會從目前的電腦卸載。<br />2) [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務會從伺服器陣列卸載。<br /><br /> <br /><br /> 注意：如果伺服器陣列中有任何其他電腦已安裝 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務，或者伺服器陣列中仍有執行中的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式，則會顯示警告訊息。|  
|Install-SPRSServiceProxy|在 SharePoint 伺服器陣列中安裝及註冊或是解除安裝 Reporting Services 服務 Proxy。|  
|Get-SPRSProxyUrl|取得存取 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務的 URL。|  
|Get-SPRSServiceApplicationServers|在包含 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 共用服務安裝的本機 SharePoint 伺服器陣列中取得所有伺服器。 這個指令程式對於 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 升級很有用，可判斷哪些伺服器執行共用服務因此需要升級。|  
  
###  <a name="service-application-and-proxy-cmdlets"></a><a name="bkmk_serviceapp_cmdlets"></a> 服務應用程式和 Proxy 指令程式  
 下表包含用於 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式及其相關聯 Proxy 的 PowerShell 指令程式。  
  
|Cmdlet|描述|  
|------------|-----------------|  
|Get-SPRSServiceApplication|取得一或多個 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式物件。|  
|New-SPRSServiceApplication|建立新的 Reporting Services 服務應用程式與相關聯的資料庫。<br /><br /> LogonType 參數：指定報表伺服器會使用 SSRS 應用程式集區帳戶或是 SQL Server 登入來存取報表伺服器資料庫。 可以是下列其中一項：<br /><br /> 0 Windows 驗證<br /><br /> 1 SQL Server<br /><br /> 2 應用程式集區帳戶 (預設)|  
|Remove-SPRSServiceApplication|移除指定的 Reporting Services 服務應用程式。 這項操作也會移除相關聯的資料庫。|  
|Set-SPRSServiceApplication|編輯現有 Reporting Services 服務應用程式的屬性。|  
|New-SPRSServiceApplicationProxy|建立新的 Reporting Services 服務應用程式 Proxy。|  
|Get-SPRSServiceApplicationProxy|取得一個或多個 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式 Proxy。|  
|Dismount-SPRSDatabase|卸載 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式的服務應用程式資料庫。|  
|Remove-SPRSDatabase|移除 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式的服務應用程式資料庫。|  
|Set-SPRSDatabase|設定與 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式相關聯之資料庫的屬性。|  
|Mount-SPRSDatabase|掛接 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式的資料庫。|  
|New-SPRSDatabase|為指定的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式建立新的服務應用程式資料庫。|  
|Get-SPRSDatabaseCreationScript|針對 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式將資料庫建立指令碼輸出到畫面。 然後您就可以在 SQL Server Management Studio 中執行指令碼。|  
|Get-SPRSDatabase|取得一個或多個 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式資料庫。 使用命令來取得服務應用程式資料庫的識別碼，以便使用 Set-SPRSDatabase Cmdlet 來修改屬性，例如 `querytimeout`。 請參閱本主題中的範例，[取得並設定 Reporting Servicea 應用程式資料庫的屬性，例如資料庫超時](#bkmk_example_db_properties)。|  
|Get-SPRSDatabaseRightsScript|針對 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式將資料庫權限指令碼輸出到畫面。 它會提示您提供所需的使用者和資料庫，然後傳回您可執行以修改權限的 Transact SQL。 然後您就可以在 SQL Server Management Studio 中執行這個指令碼。|  
|Get-SPRSDatabaseUpgradeScript|將資料庫升級指令碼輸出至畫面。 指令碼會將 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式資料庫升級至目前 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 安裝的資料庫版本。|  
  
###  <a name="reporting-services-custom-functionality-cmdlets"></a><a name="bkmk_ssrsfeatures_cmdlets"></a> Reporting Services 自訂功能指令程式  
  
|Cmdlet|描述|  
|------------|-----------------|  
|Update-SPRSEncryptionKey|為指定的 Reporting Services 服務應用程式更新加密金鑰，並重新加密其資料。|  
|Restore-SPRSEncryptionKey|為 Reporting Services 服務應用程式還原之前備份的加密金鑰。|  
|Remove-SPRSEncryptedData|為指定的 Reporting Services 服務應用程式刪除加密的資料。|  
|Backup-SPRSEncryptionKey|為指定的 Reporting Services 服務應用程式備份加密金鑰。|  
|New-SPRSExtension|向 Reporting Services 服務應用程式註冊新的延伸模組。|  
|Set-SPRSExtension|設定現有 Reporting Services 延伸模組的屬性。|  
|Remove-SPRSExtension|從 Reporting Services 服務應用程式中移除延伸模組。|  
|Get-SPRSExtension|獲取一個或多個用於 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 延伸模組。<br /><br /> 有效值為：<br /><br /> **傳遞**<br /><br /> **DeliveryUI**<br /><br /> **轉譯**<br /><br /> **Data**<br /><br /> **安全性**<br /><br /> **驗證**<br /><br /> **EventProcessing**<br /><br /> **ReportItems**<br /><br /> **Designer**<br /><br /> **ReportItemDesigner**<br /><br /> **ReportItemConverter**<br /><br /> **ReportDefinitionCustomization**|  
|Get-SPRSSite|根據是否啟用 "ReportingService" 功能取得 SharePoint 網站。 根據預設，將會傳回啟用 "ReportingService" 功能的網站。|  
  
##  <a name="basic-samples"></a><a name="bkmk_basic_samples"></a>基本範例  
 傳回名稱中包含 'SPRS' 的 Cmdlet 清單。 這項操作將傳回完整的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 指令程式清單。  
  
```powershell
Get-command -noun *SPRS*  
```  
  
 或者透過更詳細的資訊，傳送到名為 commandlist.txt 的文字檔  
  
```powershell
Get-Command -Noun *SPRS* | Select name, definition | Format-List | Out-File c:\commandlist.txt  
```  
  
 安裝 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 服務和服務 Proxy。  
  
```powershell
Install-SPRSService  
```  
  
```powershell
Install-SPRSServiceProxy  
```  
  
 啟動 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務  
  
```powershell
Get-SPServiceInstance -all | where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
```  
  
 在 SharePoint 管理命令介面中輸入下列命令，即可從記錄檔傳回已篩選過的資料列清單。 此命令將會篩選包含 "ssrscustomactionerror" 的行。 這個範例會查看安裝 rssharepoint.msi 時建立的記錄檔。  
  
```powershell
Get-Content -Path C:\Users\testuser\AppData\Local\Temp\rs_sp_0.log | Select-String "ssrscustomactionerror"  
```  
  
##  <a name="detailed-samples"></a><a name="bkmk_detailedsamples"></a>詳細範例  
 除了下列範例之外，請參閱[適用于步驟1-4 的 Windows powershell 腳本](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md#bkmk_full_script)主題中的「Windows powershell 腳本」一節。  
  
###  <a name="create-a-reporting-services-service-application-and-proxy"></a><a name="bkmk_example_create_service_application"></a>建立 Reporting Services 服務應用程式和 proxy  
 這個範例指令碼會完成下列工作：  
  
1.  建立 Reporting Services 服務應用程式和 Proxy。 此指令碼會假設應用程式集區 "My App Pool" 已存在。  
  
2.  將 Proxy 加入至預設 Proxy 群組。  
  
3.  將服務應用程式存取權授與連接埠 80 Web 應用程式的內容資料庫。 腳本假設網站 " http://sitename " 已經存在。  
  
```powershell
# Create service application and service application proxy  
$appPool = Get-SPServiceApplicationPool "My App Pool"  
$serviceApp = New-SPRSServiceApplication "My RS Service App" -ApplicationPool $appPool  
$serviceAppProxy = New-SPRSServiceApplicationProxy -Name "My RS Service App Proxy" -ServiceApplication $serviceApp  
  
# Add service application proxy to default proxy group.  Any web application that uses the default proxy group will now be able to use this service application.  
Get-SPServiceApplicationProxyGroup -default | Add-SPServiceApplicationProxyGroupMember -Member $serviceAppProxy  
  
# Grant application pool account access to the port 80 web application's content database.  
$webApp = Get-SPWebApplication "http://sitename"  
$appPoolAccountName = $appPool.ProcessAccount.LookupName()  
$webApp.GrantAccessToProcessIdentity($appPoolAccountName)
```  
  
###  <a name="review-and-update-a-reporting-services-delivery-extension"></a><a name="bkmk_example_delivery_extension"></a>審查和更新 Reporting Services 傳遞延伸模組  
 下列 PowerShell 指令碼範例會更新服務應用程式 `My RS Service App`之報表伺服器電子郵件傳遞延伸模組的組態。 更新 SMTP 伺服器 (`<email server name>`) 和 FROM 電子郵件別名 (`<your FROM email address>`) 的值。  
  
```powershell
$app = Get-SPRSServiceApplication -Name "My RS Service App"  
$emailCfg = Get-SPRSExtension -Identity $app -ExtensionType "Delivery" -Name "Report Server Email" | Select -ExpandProperty ConfigurationXml
$emailXml = [xml]$emailCfg
$emailXml.SelectSingleNode("//SMTPServer").InnerText = "<email server name>"  
$emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
$emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
$emailXml.SelectSingleNode("//From").InnerText = '<your FROM email address>'  
Set-SPRSExtension -Identity $app -ExtensionType "Delivery" -Name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
```  
  
 在上述範例中，如果您不知道服務應用程式的確實名稱，可以重新撰寫第一個陳述式，依據搜尋部分名稱的結果取得服務應用程式。 例如：  
  
```powershell
$app = Get-SPRSServiceApplication | Where {$_.name -like " ssrs_testapp *"}  
```  
  
 下列指令碼將針對服務應用程式「Reporting Services 應用程式」傳回報表伺服器電子郵件傳遞延伸模組的目前設定值。 第一個步驟是將變數 $app 的值設定為名稱為 "My RS Service App" 之服務應用程式的物件。  
  
 第二個陳述式將取得變數 $app 中服務應用程式物件的「報表伺服器電子郵件」傳遞延伸模組，並且選取 configurationXML  
  
```powershell
$app = Get-SPRSServiceapplication -Name "Reporting Services Application"  
Get-SPRSExtension -Identity $app -ExtensionType "Delivery" -Name "Report Server Email" | Select -ExpandProperty ConfigurationXml  
```  
  
 您也可以將上述兩個陳述式重新撰寫成一個：  
  
```powershell
Get-SPRSServiceApplication -Name "Reporting Services Application" | Get-SPRSExtension -ExtensionType "Delivery" -Name "Report Server Email" | Select -ExpandProperty ConfigurationXml  
```  
  
###  <a name="get-and-set-properties-of-the-reporting-servicea-application-database-for-example-database-timeout"></a><a name="bkmk_example_db_properties"></a>取得和設定 Reporting Servicea 應用程式資料庫的屬性，例如資料庫超時  
 下列範例一開始傳回資料庫與屬性的清單，您可以用來決定之後提供給 set 命令的資料庫 GUID (識別碼)。 如需屬性的完整清單，請使用 `Get-SPRSDatabase | format-list`。  
  
```powershell
Get-SPRSDatabase | Select id, querytimeout,connectiontimeout, status, server, ServiceInstance
```  
  
 以下是輸出的範例。 決定您要修改之資料庫的識別碼，並在 SET Cmdlet 中使用該識別碼。  
  
-   `Id                : 56f8d1bc-cb04-44cf-bd41-a873643c5a14`  
  
     `QueryTimeout      : 120`  
  
     `ConnectionTimeout : 15`  
  
     `Status            : Online`  
  
     `Server            : SPServer Name=uetestb01`  
  
     `ServiceInstance   : SPDatabaseServiceInstance`  
  
```powershell
Set-SPRSDatabase -Identity 56f8d1bc-cb04-44cf-bd41-a873643c5a14 -QueryTimeout 300  
```  
  
 若要確認是否已設定值，請再執行一次 GET Cmdlet。  
  
```powershell
Get-SPRSDatabase -Identity 56f8d1bc-cb04-44cf-bd41-a873643c5a14 | Select id, querytimeout,connectiontimeout, status, server, ServiceInstance  
```  
  
###  <a name="list-reporting-services-data-extensions---sharepoint-mode"></a><a name="bkmk_example_list_data_extensions"></a>列出 reporting services 資料延伸模組-SharePoint 模式  
 下列範例會在每一個 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式中執行迴圈，並列出每一個應用程式目前的資料延伸模組。  
  
```powershell
$apps = Get-SPRSServiceApplication  
foreach ($app in $apps)
{  
Write-host -ForegroundColor "yellow" Service App Name $app.Name  
Get-SPRSExtension -identity $app -ExtensionType "Data" | select name, extensiontype | Format-Table -AutoSize  
}  
```  
  
 **範例輸出︰**  
  
-   `Name           ExtensionType`  
  
     `----           -------------`  
  
     `SQL                     Data`  
  
     `SQLAZURE                Data`  
  
     `SQLPDW                  Data`  
  
     `OLEDB                   Data`  
  
     `OLEDB-MD                Data`  
  
     `ORACLE                  Data`  
  
     `ODBC                    Data`  
  
     `XML                     Data`  
  
     `SHAREPOINTLIST          Data`  
  
###  <a name="change-and-list-subscription-owners"></a><a name="bkmk_change_subscription_owner"></a>變更和列出訂用帳戶擁有者  
 請參閱 [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用 PowerShell 來變更和列出 Reporting Services 訂用帳戶擁有者並執行訂用帳戶](subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)   
 [檢查清單：使用 PowerShell 驗證 PowerPivot for SharePoint](https://docs.microsoft.com/analysis-services/instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint)   
 [CodePlex SharePoint Management PowerShell 指令碼](https://sharepointpsscripts.codeplex.com/)   
