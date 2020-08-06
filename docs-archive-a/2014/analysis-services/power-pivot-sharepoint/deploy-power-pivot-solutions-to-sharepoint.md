---
title: 將 PowerPivot 方案部署到 SharePoint |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f202a2b7-34e0-43aa-90d5-c9a085a37c32
author: minewiskan
ms.author: owend
ms.openlocfilehash: 043647988598f932b70cc06e6bb5492d66864372
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598014"
---
# <a name="deploy-powerpivot-solutions-to-sharepoint"></a>將 PowerPivot 方案部署到 SharePoint
  利用下列指示手動部署兩個方案套件，將 PowerPivot 功能加入至 SharePoint Server 2010 環境。 部署方案是在 SharePoint 2010 伺服器上設定 PowerPivot for SharePoint 的必要步驟。 若要查看必要步驟的完整清單，請參閱[管理中心的 PowerPivot 服務器管理和](power-pivot-server-administration-and-configuration-in-central-administration.md)設定。  
  
 或者，您可以使用 PowerPivot 組態工具部署方案。 使用組態工具對於單一伺服器安裝來說，是較簡單且更有效率的方式，不過，如果您習慣使用熟悉的工具或是要同時設定多項功能，則建議您使用管理中心和 PowerShell。 如需使用設定工具的詳細資訊，請參閱[PowerPivot 組態工具](power-pivot-configuration-tools.md)。  
  
 在部署方案之前，必須先使用 SQL Server 2012 安裝媒體安裝 PowerPivot for SharePoint。 SQL Server 安裝程式會安裝您將要部署的方案套件。  
  
 本主題包含下列幾節：  
  
 [必要條件：確認 Web 應用程式使用傳統模式驗證](#bkmk_classic)  
  
 [步驟 1：部署伺服器陣列方案](#bkmk_farm)  
  
 [步驟 2：將 PowerPivot Web 應用程式方案部署到管理中心](#deployCA)  
  
 [步驟 3：將 PowerPivot Web 應用程式方案部署到其他 Web 應用程式](#deployUI)  
  
 [重新部署或撤銷方案](#retract)  
  
 [關於 PowerPivot 方案](#intro)  
  
##  <a name="prerequisite-verify-the-web-application-uses-classic-mode-authentication"></a><a name="bkmk_classic"></a> 必要條件：驗證 Web 應用程式是否使用傳統模式驗證  
 使用 Windows 傳統模式驗證的 Web 應用程式才支援 PowerPivot for SharePoint。 若要檢查應用程式是否使用傳統模式，請從**sharepoint 2010 管理命令**介面執行下列 PowerShell Cmdlet， `http://<top-level site name>` 並將取代為您的 sharepoint 網站名稱：  
  
```powershell
Get-SPWebApplication http://<top-level site name> | Format-List UseClaimsAuthentication  
```  
  
 傳回值應為 **false**。 若為**true**，則無法使用此 web 應用程式來存取 PowerPivot 資料。  
  
##  <a name="step-1-deploy-the-farm-solution"></a><a name="bkmk_farm"></a>步驟1：部署伺服器陣列方案  
 本節示範如何使用 PowerShell 部署方案，但是您也可以使用 PowerPivot 組態工具完成此工作。 如需詳細資訊，請參閱[設定或修復 PowerPivot for SharePoint 2010 &#40;PowerPivot 設定工具&#41;](../configure-repair-powerpivot-sharepoint-2010.md)。  
  
 此工作只需要在安裝 PowerPivot for SharePoint 之後執行一次。  
  
1.  在安裝 PowerPivot for SharePoint 的伺服器上，使用 [以**系統管理員身分執行**] 選項開啟 SharePoint 2010 管理命令介面。  
  
2.  執行下列指令程式加入伺服器陣列方案。  
  
    ```powershell
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp"  
    ```  
  
     此指令程式會傳回方案的名稱、方案識別碼及 Deployed=False。 在下個步驟中，您將部署方案。  
  
3.  執行下一個指令程式來部署伺服器陣列方案：  
  
    ```powershell
    Install-SPSolution -Identity PowerPivotFarm.wsp -GACDeployment -Force  
    ```  
  
##  <a name="step-2-deploy-the-powerpivot-web-application-solution-to-central-administration"></a><a name="deployCA"></a>步驟2：將 PowerPivot Web 應用程式方案部署到管理中心  
 部署伺服器陣列方案之後，您必須將 Web 應用程式方案部署到管理中心。 此步驟會將 PowerPivot 管理儀表板加入至管理中心。  
  
1.  使用 **[以系統管理員身分執行]** 選項，開啟 SharePoint 2010 管理命令介面。  
  
2.  執行下列指令程式建立管理中心的參考：  
  
    ```powershell
    $centralAdmin = $(Get-SPWebApplication -IncludeCentralAdministration | Where { $_.IsAdministrationWebApplication -eq $TRUE})  
    ```  
  
3.  執行下列指令程式加入伺服器陣列方案。  
  
    ```powershell
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotWebApp.wsp"  
    ```  
  
     此指令程式會傳回方案的名稱、方案識別碼及 Deployed=False。 在下個步驟中，您將部署方案。  
  
4.  執行下一個指令程式，將 Web 應用程式方案安裝到管理中心。  
  
    ```powershell
    Install-SPSolution -Identity PowerPivotWebApp.wsp -GACDeployment -Force -WebApplication $centralAdmin  
    ```  
  
 現在 Web 應用程式方案已部署到管理中心，您可以使用管理中心完成所有其餘組態步驟。  
  
##  <a name="step-3-deploy-the-powerpivot-web-application-solution-to-other-web-applications"></a><a name="deployUI"></a>步驟3：將 PowerPivot Web 應用程式方案部署到其他 Web 應用程式  
 在上一個工作中，您已經將 Powerpivotwebapp.wsp 部署到管理中心。 在本節中，您會在支援 PowerPivot 資料存取的每個現有 Web 應用程式上部署 powerpivotwebapp.wsp。 如果您之後加入更多 Web 應用程式，務必針對其他 Web 應用程式重複此步驟。  
  
1.  在管理中心的 [系統設定] 中，按一下 **[管理伺服器陣列方案]**。  
  
2.  按一下 [ **powerpivotwebapp.wsp**]。  
  
3.  按一下 **[部署方案]**。  
  
4.  在 [**部署至？**] 中，選取您要加入 PowerPivot 功能支援的 SharePoint web 應用程式。  
  
5.  按一下 [確定]  。  
  
6.  針對其他也支援 PowerPivot 資料存取的 SharePoint Web 應用程式重複以上步驟。  
  
##  <a name="redeploy-or-retract-the-solution"></a><a name="retract"></a>重新部署或撤銷方案  
 雖然 SharePoint 管理中心會提供方案撤銷，但是除非您有系統地排除安裝或修補程式的部署問題，否則不需要撤銷 powerpivotwebapp.wsp 檔。  
  
1.  在 SharePoint 2010 管理中心的 [系統設定] 中，按一下 **[管理伺服陣列方案]**。  
  
2.  按一下 **[Powerpivotwebapp.wsp]**。  
  
3.  按一下 **[撤銷方案]**。  
  
 如果您遇到伺服器部署問題，而您追蹤至伺服器陣列方案，您可以在 PowerPivot 設定工具中執行 [**修復**] 選項來重新部署它。 透過此工具的修復作業是慣用的方式，因為您需要執行的步驟比較少。 如需詳細資訊，請參閱[設定或修復 PowerPivot for SharePoint 2010 &#40;PowerPivot 設定工具&#41;](../configure-repair-powerpivot-sharepoint-2010.md)。  
  
 如果您仍然要重新部署所有方案，請務必以下列順序進行：  
  
1.  從使用 PowerPivot Web 應用程式方案的所有 SharePoint Web 應用程式撤銷它。  
  
2.  撤銷 PowerPivot 伺服陣列方案。  
  
3.  重新部署 PowerPivot 伺服陣列方案。  
  
4.  將 PowerPivot Web 應用程式方案重新部署至所有 SharePoint Web 應用程式。  
  
##  <a name="about-the-powerpivot-solutions"></a><a name="intro"></a>關於 PowerPivot 方案  
 PowerPivot for SharePoint 會使用兩個方案套件，將它的應用程式頁面和程式檔案從伺服陣列部署到個別 Web 應用程式。  
  
-   伺服器陣列方案為全域所通用， 這個方案會部署一次，然後自動提供給您之後加入至伺服器陣列的任何新 PowerPivot for SharePoint 伺服器使用。  
  
-   此 Web 應用程式方案是應用程式所特有，而且必須部署到伺服器陣列中的每一個 Web 應用程式，包括管理中心 Web 應用程式。  
  
 每一個方案都會以不同方式部署。  伺服器陣列方案會在安裝第一個 PowerPivot for SharePoint 執行個體之後部署一次。 若要部署伺服器陣列方案，您必須使用 PowerPivot 組態工具或 PowerShell 指令程式。  
  
 此 Web 應用程式方案一開始會部署到管理中心，隨後會將後續方案部署到支援 PowerPivot 資料要求的其他任何 Web 應用程式。 若要將 Web 應用程式方案部署到管理中心，您必須使用 PowerPivot 組態工具或 PowerShell 指令程式。 如果是所有其他 Web 應用程式，您可以使用管理中心或 PowerShell 來手動部署 Web 應用程式方案。  
  
|解決方法|描述|  
|--------------|-----------------|  
|Powerpivotfarm.wsp|將 Microsoft.AnalysisServices.SharePoint.Integration.dll 加入至全域組件。<br /><br /> 將 Microsoft.AnalysisServices.ChannelTransport.dll 加入至全域組件。<br /><br /> 安裝功能和資源檔，並註冊內容類型。<br /><br /> 加入 PowerPivot 圖庫和資料摘要庫的文件庫範本。<br /><br /> 為服務應用程式組態、PowerPivot 管理儀表板、資料重新整理及 PowerPivot 圖庫加入應用程式頁面。|  
|[powerpivotwebapp.wsp]|將 Microsoft.AnalysisServices.SharePoint.Integration.dll 資源檔加入至 Web 前端的 Web Server Extensions 資料夾。<br /><br /> 將 PowerPivot Web 服務加入至 Web 前端。<br /><br /> 加入 PowerPivot 圖庫產生的縮圖影像。|  
  
## <a name="see-also"></a>另請參閱  
 [升級 PowerPivot for SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [管理中心的 PowerPivot 服務器管理和設定](power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [使用 Windows PowerShell 的 PowerPivot 設定](power-pivot-configuration-using-windows-powershell.md)  
