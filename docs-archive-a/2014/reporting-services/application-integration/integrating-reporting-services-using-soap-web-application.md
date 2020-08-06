---
title: 在 Web 應用程式中使用 SOAP API | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], Web applications
- impersonation [Reporting Services]
- user impersonation [Reporting Services]
- report servers [Reporting Services], SOAP
- Web applications [Reporting Services]
ms.assetid: e8ca4455-0dc3-4741-8872-3636114938ad
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e228f01915df633f50b23bf93e892446863c28ad
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687550"
---
# <a name="using-the-soap-api-in-a-web-application"></a>在 Web 應用程式中使用 SOAP API
  您可以透過 Reporting Services SOAP API 存取報表伺服器的完整功能。 因為它是一種 Web 服務，所以可以輕易地存取 SOAP API，以提供企業報表功能給自訂商務應用程式。 您可以從 Web 應用程式存取報表伺服器 Web 服務，這與從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 應用程式存取 SOAP API 非常類似。 使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ，您可以產生 proxy 類別，以公開報表伺服器 Web 服務的屬性和方法，並可讓您使用熟悉的基礎結構和工具來建立技術上的商務應用程式 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表管理功能可以從 Web 應用程式存取，就和從 Windows 應用程式存取一樣簡單。 從 Web 應用程式，您可以從報表伺服器資料庫新增和移除項目、設定項目安全性、修改報表伺服器資料庫項目、管理排程和傳遞等等。  
  
## <a name="enabling-impersonation"></a>啟用模擬  
 設定 Web 應用程式的第一個步驟是從 Web 服務用戶端啟用模擬。 透過模擬，[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 應用程式可以使用它們正在操作的用戶端識別來執行。 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 依賴 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) 驗證使用者並將已驗證的 Token 傳遞給 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 應用程式，或者如果無法驗證使用者，請傳遞未驗證的 Token。 不論是哪一種情況，若有啟用模擬，[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 應用程式不論收到哪一個 Token，都會進行模擬。 您可以透過修改用戶端應用程式的 Web.config 檔案，啟用在用戶端上的模擬：  
  
```  
<!-- Web.config file. -->  
<identity impersonate="true"/>  
```  
  
> [!NOTE]  
>  預設會啟用模擬。  
  
 如需有關模擬的詳細資訊 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] ，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 檔。  
  
## <a name="managing-the-report-server-using-soap-api"></a>使用 SOAP API 管理報表伺服器。  
 您也可以使用 Web 應用程式來管理報表伺服器及其內容。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 隨附的報表管理員，是完全使用 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 與 Reporting Services SOAP API 建立的 Web 應用程式範例。 您可以將報表管理員的報表管理功能加入自訂 Web 應用程式。 例如，您可能會想要傳回報表伺服器資料庫中可用報表的清單，並將其顯示在控制項中， [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] `Listbox` 供您的使用者選擇。 下列程式碼會連接報表伺服器資料庫，並在報表伺服器資料庫中傳回項目的清單。 接著會將可用的報表加入 Listbox 控制項，如此會顯示每個報表的路徑。  
  
```vb  
Private Sub Page_Load(sender As Object, e As System.EventArgs)  
   ' Create a Web service proxy object and set credentials  
   Dim rs As New ReportingService2005()  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
   ' Return a list of catalog items in the report server database  
   Dim items As CatalogItem() = rs.ListChildren("/", True)  
  
   ' For each report, display the path of the report in a Listbox  
   Dim ci As CatalogItem  
   For Each ci In  items  
      If ci.Type = ItemTypeEnum.Report Then  
         catalogListBox.Items.Add(ci.Path)  
      End If  
   Next ci  
End Sub ' Page_Load   
```  
  
```csharp  
private void Page_Load(object sender, System.EventArgs e)  
{  
   // Create a Web service proxy object and set credentials  
   ReportingService2005 rs = new ReportingService2005();  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
  
   // Return a list of catalog items in the report server database  
   CatalogItem[] items = rs.ListChildren("/", true);  
  
   // For each report, display the path of the report in a Listbox  
   foreach(CatalogItem ci in items)  
   {  
      if (ci.Type == ItemTypeEnum.Report)  
         catalogListBox.Items.Add(ci.Path);  
   }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和 .NET Framework 建置應用程式](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [將 Reporting Services 整合至應用程式](../application-integration/integrating-reporting-services-into-applications.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)   
 [在 Windows 應用程式中使用 SOAP API](integrating-reporting-services-using-soap-windows-application.md)  
  
  
