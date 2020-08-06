---
title: 註冊標準的 .NET Framework Data Provider (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], data
- .NET Framework data providers for Reporting Services
- data processing extensions [Reporting Services]
- data providers [Reporting Services]
- data retrieval [Reporting Services]
- Reporting Services, data sources
ms.assetid: d92add64-e93c-4598-8508-55d1bc46acf6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5fd26f9c7fa163d9e6005d42e24c7b1483987f3e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687494"
---
# <a name="register-a-standard-net-framework-data-provider-ssrs"></a>註冊標準的 .NET Framework Data Provider (SSRS)
  若要使用協力廠商的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者來擷取 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表資料集的資料，您必須在兩個位置部署並註冊 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者組件：報表撰寫用戶端與報表伺服器。 在報表撰寫用戶端上，您必須註冊資料提供者做為資料來源類型，並將其與查詢設計工具產生關聯。 然後您可以在建立報表資料集時，選取此資料提供者做為資料來源的類型。 相關聯的查詢設計工具便會開啟，協助您建立此資料來源類型的查詢。 在報表伺服器上，您必須註冊資料提供者，做為資料來源類型。 然後您可以處理使用此資料提供者，從資料來源擷取資料的已發行報表。  
  
 協力廠商的資料提供者不一定會提供適用於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組的所有功能。 如需詳細資訊，請參閱 [Reporting Services &#40;SSRS&#41; 支援的資料來源](../create-deploy-and-manage-mobile-and-paginated-reports.md)。 若要了解有關擴充 .[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]  資料提供者，請參閱[實作資料處理延伸模組](../extensions/data-processing/implementing-a-data-processing-extension.md)。  
  
 您需要管理員認證才能安裝與註冊資料提供者。  
  
## <a name="registering-a-net-framework-data-provider-on-the-report-server"></a>在報表伺服器上註冊 .NET Framework Data Provider  
 若要在報表伺服器上，處理使用此 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者的已發行報表，您必須在報表伺服器上安裝組件。 您必須修改兩個組態檔。 修改 rsreportserver.config 以註冊資料提供者。 修改 rssrvpolicy.config 以授與組件的程式碼存取安全性權限。  
  
#### <a name="to-install-a-data-provider-assembly-on-the-report-server"></a>在報表伺服器上安裝資料提供者組件  
  
1.  在您要使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者的報表伺服器上，巡覽至 bin 目錄的預設位置。 報表伺服器 bin 目錄的預設位置是 *\<drive>* ： \Program Files\Microsoft SQL Server \ MSRS10_50. MSSQLSERVER\Reporting services\reportserver\bin。  
  
2.  將組件從您的臨時位置複製到報表伺服器的 bin 目錄。 或者，您可以將組件載入至全域組件快取 (GAC)。 如需詳細資訊，請參閱 MSDN [SDK 文件集中的＜](https://go.microsoft.com/fwlink/?linkid=63912) 使用組件和全域組件快取 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ＞。  
  
#### <a name="to-register-a-net-data-provider-on-the-report-server"></a>在報表伺服器上註冊 .NET 資料提供者  
  
1.  在 bin 的 ReportServer 上層目錄中，製作 RSReportServer.config 檔的備份。  
  
2.  開啟 RSReportServer.config。您可以利用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 或簡單的文字編輯器 (如 [記事本]) 開啟組態檔。  
  
3.  在 RSReportServer.config 檔中，找出 `Data` 元素。 在下列位置應該就會建立一個 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者的項目：  
  
    ```  
    <Extensions>  
       <Data>  
          <Extension Your data provider configuration information goes here />  
       </Data>  
    </Extensions>  
    ```  
  
4.  加入 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者的項目。  
  
    |屬性|描述|  
    |---------------|-----------------|  
    |`Name`|為資料提供者提供唯一的名稱，例如， **MyNETDataProvider**。 `Name` 屬性的最大長度為 255 個字元。 該名稱在組態檔之 `Extension` 元素的所有元素中，必須是唯一的。 當您建立新的資料來源時，您在此處包含的值會出現在資料來源類型的下拉式清單中。|  
    |`Type`|輸入一個逗號分隔清單，其中包含實作 <xref:System.Data.IDbConnection> 介面之類別的完整命名空間，後面緊接著 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者組件的名稱 (不包含 .dll 副檔名)。|  
  
     例如，若是部署至報表伺服器 bin 目錄的 DLL，該項目可能類似如下：  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="CompanyName.ExtensionName.DataProviderConnectionClass, DataProviderAssembly" />   
    ```  
  
     如果您將組件載入至全域組件快取 (GAC)，您必須提供強式名稱屬性。 例如：  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="CompanyName.ExtensionName.DataProviderConnectionClass, DataProviderAssembly,Version=1.0.0.0, Culture=neutral, PublicKeyToken=MyPublicToken"/>  
    ```  
  
#### <a name="to-set-the-code-group-policy-for-a-net-data-provider"></a>為 .NET 資料提供者設定程式碼群組原則  
  
1.  在 bin 的 ReportServer 上層目錄中，製作 rssrvpolicy.config 檔的備份副本。  
  
2.  開啟 rssrvpolicy.config。您可以使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 或簡單的文字編輯器（如 [記事本]）開啟設定檔。  
  
3.  在 rssrvpolicy.config 檔中，找出 `CodeGroup` 元素。  
  
4.  針對授與 `FullTrust` 權限的資料提供者組件，加入程式碼群組。 您的程式碼群組可能類似如下：  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="ThisDataProviderCodeGroup"  
       Description="Code group for the .NET data provider">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url=  
    "C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\DataProviderAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 URL 成員資格僅是您可以針對資料提供者選取的多個成員資格條件的其中一個。  
  
### <a name="verifying-the-deployment-and-registration"></a>確認部署與註冊  
 您可以確認是否將資料提供者成功部署至報表伺服器，方法是，開啟報表管理員，然後確認該資料提供者包含在可用資料來源的清單中。 如需報表管理員和資料來源的詳細資訊，請參閱[建立、修改及刪除共用資料來源 &#40;SSRS&#41;](create-modify-and-delete-shared-data-sources-ssrs.md)。  
  
## <a name="registering-a-net-framework-data-provider-on-the-report-designer-client"></a>在報表設計師用戶端上註冊 .NET Framework Data Provider  
 若要針對資料來源撰寫使用此 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者的報表，您必須在執行報表設計師的用戶端電腦上安裝該組件。 您必須修改兩個組態檔。 修改 RSReportDesigner.config 以註冊資料提供者做為資料來源，以及使用一般查詢設計工具。 修改 RSPreviewPolicy.config 以授與資料提供者組件的程式碼存取安全性權限。  
  
#### <a name="to-install-a-data-provider-assembly-on-the-report-designer-client"></a>在報表設計師用戶端上安裝資料提供者組件  
  
1.  在您要使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者的報表設計師用戶端上，巡覽至 PrivateAssemblies 目錄的預設位置。 PrivateAssemblies 目錄的預設位置是 *\<drive>* ： \Program Files\Microsoft Visual Studio 9.0 \ common7\ide\privateassemblies。  
  
2.  將組件從您的臨時位置複製到報表設計師用戶端的 PrivateAssemblies 目錄。 或者，您可以將組件載入至全域組件快取 (GAC)。 如需詳細資訊，請參閱 MSDN [SDK 文件集中的＜](https://go.microsoft.com/fwlink/?linkid=63912) 使用組件和全域組件快取 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ＞。  
  
#### <a name="to-register-a-net-data-provider-on-the-report-designer-client"></a>在報表設計師用戶端上註冊 .NET 資料提供者  
  
1.  在 PrivateAssemblies 目錄中，製作 RSReportDesigner.config 檔的備份副本。  
  
2.  利用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 或簡單的文字編輯器 (如 [記事本]) 開啟 RSReportDesigner.config。  
  
3.  在 RSReportDesigner.config 檔中，找出 `Data` 元素。 在下列位置應該就會建立一個資料提供者的項目：  
  
    ```  
    <Extensions>  
       <Data>  
          <Extension Your data provider configuration information goes here />  
       </Data>  
    </Extensions>  
    ```  
  
4.  加入資料提供者的項目。  
  
    |屬性|描述|  
    |---------------|-----------------|  
    |`Name`|為資料提供者提供唯一的名稱，例如， **MyNETDataProvider**。 `Name` 屬性的最大長度為 255 個字元。 該名稱在組態檔之 `Extension` 元素的所有元素中，必須是唯一的。 當您建立新的資料來源時，您在此處包含的值會出現在資料來源類型的下拉式清單中。|  
    |`Type`|輸入一個逗號分隔清單，其中包含實作 <xref:System.Data.IDbConnection> 介面之類別的完整命名空間，後面緊接著 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者組件的名稱 (不包含 .dll 副檔名)。|  
  
     例如，若是部署至 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] PrivateAssemblies 目錄的 DLL，該項目可能類似如下：  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="CompanyName.ExtensionName.DataProviderConnectionClass, DataProviderAssembly" />   
    ```  
  
     如果您將組件載入至 GAC，您必須提供強式名稱屬性。 例如：  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="CompanyName.ExtensionName.DataProviderConnectionClass, DataProviderAssembly, Version=1.0.0.0, Culture=neutral, PublicKeyToken=MyPublicToken"/>  
    ```  
  
5.  在 RSReportDesigner.config 檔中，找出 `Designer` 元素。 在下列位置應該就會建立一個 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者的項目：  
  
    ```  
    <Extensions>  
       <Designer>  
          <Your data provider configuration information goes here>  
       </Designer>  
    </Extensions>  
    ```  
  
6.  將下列項目加入至 RSReportDesigner.config 檔的 `Designer` 元素下。 您僅需要以您在之前項目中提供的名稱，取代 `Name` 屬性。  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="Microsoft.ReportingServices.QueryDesigners.GenericQueryDesigner,Microsoft.ReportingServices.QueryDesigners"/>  
    ```  
  
#### <a name="to-set-the-code-group-policy-for-a-net-data-provider-on-the-report-designer-client"></a>在報表設計師用戶端上設定 .NET 資料提供者的程式碼群組原則  
  
1.  在 PrivateAssemblies 目錄中，製作 RSPreviewPolicy.config 檔的備份副本。  
  
2.  利用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 或簡單的文字編輯器 (如「記事本」) 開啟 RSPreviewPolicy.config。  
  
3.  在 RSPreviewPolicy.config 檔中，找出 `CodeGroup` 元素。  
  
4.  針對授與 `FullTrust` 權限的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者組件，加入程式碼群組。 您的程式碼群組可能類似如下：  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="ThisDataProviderCodeGroup"  
       Description="Code group for the .NET data provider">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url=  
    " C:\Program Files\Microsoft Visual Studio 9\Common7\IDE\PrivateAssemblies\DataProviderAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 URL 成員資格僅是您可以針對資料提供者選取的多個成員資格條件的其中一個。  
  
### <a name="verifying-the-deployment-and-registration-on-the-report-designer-client"></a>在報表設計師用戶端上確認部署與註冊  
 在您可以確認部署之前，必須在本機電腦上，關閉 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 的所有執行個體。 在您已經結束所有目前的工作階段後，您可以確認是否已將您的資料提供者成功部署至報表設計師，方法是，在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]中建立新的報表專案。 當您從報表建立新的資料集時，資料提供者應該會包含在可用資料來源類型的清單中。  
  
## <a name="platform-considerations"></a>平台考量  
 在 64 位元 (x64) 平台上， [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 會以 32 位元 WOW 模式執行。 當您在 x64 平台上撰寫報表時，您需要將 32 位元資料提供者安裝在報表撰寫用戶端上，才能預覽您的報表。 如果您在相同的系統上發行報表，您需要 x64 資料提供者，才能使用報表管理員檢視報表。  
  
 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 不支援以 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]為基礎的平台。  
  
 與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 一起安裝的資料處理延伸模組原始就必須針對每個平台編譯，而且必須安裝在正確的位置。 如果您要註冊自訂的資料提供者或標準的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者，則原始就需要針對適當的平台編譯，而且需要安裝在適當的位置。 如果您是在 32 位元平台上執行，資料提供者必須針對 32 位元平台編譯。 如果您是在 64 位元平台上執行，資料提供者則必須針對 64 位元平台編譯。 您無法在 64 位元平台上，使用以 64 位元介面包裝的 32 位元資料提供者。 如需有關資料提供者是否可以在已安裝的平台上運作的詳細資訊，請查閱您的協力廠商軟體。 如需資料提供者與平台支援的詳細資訊，請參閱 [Reporting Services &#40;SSRS&#41; 支援的資料來源](../create-deploy-and-manage-mobile-and-paginated-reports.md)。  
  
## <a name="see-also"></a>另請參閱  
 [設定和管理報表伺服器 &#40;SSRS 原生模式&#41;](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [執行資料處理延伸模組](../extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 組態檔](../report-server/reporting-services-configuration-files.md)   
 [Reporting Services 中的程式碼存取安全性](../extensions/secure-development/code-access-security-in-reporting-services.md)  
  
  
