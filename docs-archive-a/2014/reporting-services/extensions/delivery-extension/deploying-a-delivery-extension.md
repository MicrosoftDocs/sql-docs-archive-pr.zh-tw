---
title: 部署傳遞延伸模組 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: 4436ce48-397d-42c7-9b5d-2a267e2a1b2c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f4a4e33266c8d3a27ce2a4ab5f568bdee349720f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87607293"
---
# <a name="deploying-a-delivery-extension"></a>部署傳遞延伸模組
  傳遞延伸模組以 XML 組態檔的形式提供其組態資訊。 XML 檔案符合為傳遞延伸模組定義的 XML 結構描述。 傳遞延伸模組提供設定和修改組態檔的基礎結構。  
  
 如果取代或升級傳遞延伸模組，則所有參考傳遞延伸模組的訂閱仍然會有效。  
  
 在您將 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 傳遞延伸模組撰寫和編譯成 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 程式庫之後，必須將延伸模組複製到適當的目錄，並將項目新增至適當的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 設定檔，這樣報表伺服器就可以找到它。  
  
## <a name="configuration-file-extension-element"></a>組態檔延伸模組元素  
 部署到報表伺服器的傳遞延伸模組，需要在組態檔中輸入成 `Extension` 元素。 報表伺服器的組態檔是 RSReportServer.config。  
  
 下表說明傳遞延伸模組之 `Extension` 元素的屬性。  
  
|屬性|描述|  
|---------------|-----------------|  
|`Name`|延伸模組的唯一名稱 (例如，供電子郵件傳遞延伸模組使用的 "Report Server E-Mail"，或是供檔案共用傳遞延伸模組使用的 "Report Server FileShare")。 `Name` 屬性的最大長度為 255 個字元。 該名稱在組態檔之 `Extension` 元素的所有元素中，必須是唯一的。 如果重複的名稱存在，報表伺服器會傳回錯誤。|  
|`Type`|以逗號分隔的清單，包括完整的命名空間以及組件的名稱。|  
|`Visible`|`false` 值指出在使用者介面中應該看不到傳遞延伸模組。 如果沒有包括屬性，預設值是 `true`。|  
  
 如需 RSReportServer.config 或 RSReportDesigner.config 檔的詳細資訊，請參閱 [Reporting Services 設定檔](../../report-server/reporting-services-configuration-files.md)。  
  
## <a name="deploying-the-extension-to-the-report-server"></a>將延伸模組部署到報表伺服器  
 報表伺服器使用傳遞延伸模組來處理和傳遞通知或是報表。 您應該將傳遞延伸模組組件部署到報表伺服器做為私用組件， 也需要在報表伺服器組態檔 RSReportServer.config 中建立項目。  
  
#### <a name="to-deploy-a-deliver-extension-assembly-to-a-report-server"></a>將傳遞延伸模組組件部署到報表伺服器  
  
1.  將組件從執行位置複製到您要在其上使用傳遞延伸模組之報表伺服器的 bin 目錄。 報表伺服器 bin 目錄的預設位置是%ProgramFiles%\Microsoft SQL Server \ MSRS10_50。 \<InstanceName>\Reporting Services\reportserver\bin。  
  
    > [!IMPORTANT]  
    >  如果您嘗試覆寫現有的傳遞延伸模組件，必須先停止報表伺服器服務，再複製更新的組件。 在組件完成複製之後，重新啟動服務。  
  
2.  在複製組件檔之後，開啟 RSReportServer.config 檔。 RSReportServer.config 檔案位於%ProgramFiles%\Microsoft SQL Server \ MSRS10_50。 \<InstanceName>\Reporting Services\ReportServer 目錄。 您需要在傳遞延伸模組組件檔的組態檔中建立項目。 您可以使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 或簡單的文字編輯器（例如 [記事本]）開啟設定檔。  
  
3.  在 RSReportServer.config 檔中，找出 `Delivery` 元素。 應該針對您新建立的傳遞延伸模組，在下列位置建立項目：  
  
    ```  
    <Extensions>  
       <Delivery>  
          <Your extension configuration information goes here>  
       </Delivery>  
    </Extensions>  
    ```  
  
4.  針對您的傳遞延伸模組加入項目。 您的項目應該包含具有 `Extension` 和 `Name` 值的 `Type` 元素，且可能如下所示：  
  
    ```  
    <Extension Name="My Delivery Extension Name" Type="CompanyName.ExtensionName.MyDeliveryExtensionClass, AssemblyName" />  
    ```  
  
     `Name` 的值是傳遞延伸模組的唯一名稱。 `Type` 的值是以逗號分隔的清單，包括實作 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 介面之類別的完整命名空間項目，後面接著組件的名稱 (不包含 .dll 副檔名)。 依預設，傳遞延伸模組是可見的。 若要在使用者介面中隱藏延伸模組 (例如報表管理員)，請將 `Visible` 屬性加入至 `Extension` 元素，並將其設定為 `false`。  
  
5.  最後，針對為傳遞延伸模組授與 `FullTrust` 權限的自訂組件，加入程式碼群組。 若要這麼做，您可以將程式碼群組加入至預設位於%ProgramFiles%\Microsoft SQL Server \ MSRS10_50 中的 rssrvpolicy.config 檔案。 \<InstanceName>\Reporting Services\reportserver。 您的程式碼群組可能如下所示：  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my delivery extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.<InstanceName>\Reporting Services\ReportServer\bin\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
     URL 成員資格僅是您可以針對傳遞延伸模組所選擇的許多成員資格條件的其中一個。 如需 [!INCLUDE[ssRS](../../../includes/ssrs.md)] 程式碼存取安全性的詳細資訊，請參閱[安全開發 &#40;Reporting Services&#41;](../secure-development/secure-development-reporting-services.md)  
  
## <a name="deploying-the-extension-to-report-manager"></a>將延伸模組部署到報表管理員  
 如果您的傳遞延伸模組實作 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 介面，就可以將傳遞延伸模組與報表管理員的 [訂閱] 頁面搭配使用。 若要讓訂閱使用者介面可供使用，需要將延伸模組部署到報表管理員。  
  
#### <a name="to-deploy-a-deliver-extension-assembly-to-report-manager"></a>將傳遞延伸模組組件部署到報表管理員  
  
1.  將組件從您的執行位置複製到報表管理員的 bin 目錄。 報表管理員 bin 目錄的預設位置是%ProgramFiles%\Microsoft SQL Server \ MSRS10_50。 \<InstanceName>\Reporting Services\reportmanager\bin。  
  
2.  在複製組件檔之後，開啟 RSReportServer.config 檔。 RSReportServer.config 檔案位於%ProgramFiles%\Microsoft SQL Server \ MSRS10_50。 \<InstanceName>\Reporting Services\ReportServer 目錄。 您需要在傳遞延伸模組組件檔的組態檔中建立項目。 您可以使用 Visual Studio .NET 或簡單的文字編輯器 (如 [記事本]) 開啟組態檔。  
  
3.  在 RSReportServer.config 檔中，找出 `DeliveryUI` 元素。 應該針對您新建立的傳遞延伸模組，在下列位置建立項目：  
  
    ```  
    <Extensions>  
       <DeliveryUI>  
          <Your extension configuration information goes here>  
       </DeliveryUI>  
    </Extensions>  
    ```  
  
4.  針對您的傳遞延伸模組加入項目。 您的項目應該包含具有 `Extension` 和 `Name` 值的 `Type` 元素，且看起來可能與下列項目類似：  
  
    ```  
    <Extension Name="My Delivery Extension Name" Type="CompanyName.ExtensionName.MyDeliveryUIExtensionClass, AssemblyName" />  
    ```  
  
     `Name` 的值是傳遞延伸模組的唯一名稱。 `Type` 的值是以逗號分隔的清單，包括實作 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 介面之類別的完整命名空間項目，後面接著組件的名稱 (不包含 .dll 副檔名)。  
  
    > [!IMPORTANT]  
    >  報表伺服器與報表管理員組態檔項目的 `Name` 屬性值必須相同。 如果它們不同，您的伺服器組態將無效。  
  
     最後，針對為傳遞延伸模組授與 `FullTrust` 權限的自訂組件，加入程式碼群組。 若要這麼做，您可以將程式碼群組加入至預設位於 C:\Program Files\Microsoft SQL Server \ MSRS10_50 中的 RSmgrpolicy.config 檔案。 \<InstanceName>\Reporting Services\reportmanager。 您的程式碼群組可能如下所示：  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my delivery UI extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.<InstanceName>\Reporting Services\ReportManager\bin\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
     URL 成員資格僅是您可以針對傳遞延伸模組所選擇的許多成員資格條件的其中一個。 如需中代碼啟用安全性的詳細資訊 [!INCLUDE[ssRS](../../../includes/ssrs.md)] ，請參閱[安全開發 &#40;Reporting Services&#41;](../secure-development/secure-development-reporting-services.md)  
  
## <a name="verifying-the-deployment"></a>確認部署  
 您可以使用 Web 服務 <xref:ReportService2010.ReportingService2010.ListExtensions%2A> 方法來確認傳遞延伸模組是否已成功部署到報表伺服器。 您也可以開啟報表管理員，然後確認延伸模組是否包含在訂閱的可用傳遞延伸模組清單。 如需報表管理員和訂閱的詳細資訊，請參閱[Reporting Services&#41;的訂閱和傳遞 &#40;](../../subscriptions/subscriptions-and-delivery-reporting-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [執行傳遞延伸模組](implementing-a-delivery-extension.md)   
 [Reporting Services 延伸模組程式庫](../reporting-services-extension-library.md)  
  
  
