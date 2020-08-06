---
title: RSReportDesigner 設定檔 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], configuration file
- RSReportDesigner configuration file
ms.assetid: fdcc9c58-3bad-45b3-ba8e-c7816d64f14c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 563c5ea602eef3af2400057f3da41a5850a31cec
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596487"
---
# <a name="rsreportdesigner-configuration-file"></a>RSReportDesigner 組態檔
  RSReportDesigner.config 檔會儲存有關 [報表設計師] 可用之轉譯和資料處理延伸模組的設定。 資料處理延伸模組資訊儲存在 `Data` 元素中。 轉譯延伸模組資訊儲存在 `Render` 元素中。 `Designer` 元素列舉報表設計師中所使用的查詢產生器。  
  
 報表設計師使用內嵌的報表伺服器功能來預覽報表。 可以指定伺服器相關的設定，以支援預覽作業的本機伺服器端處理。 如需有關報表伺服器設定的詳細資訊，請參閱[Rsreportserver.config Configuration File](rsreportserver-config-configuration-file.md)。  
  
## <a name="file-location"></a>檔案位置  
 此檔案位於 \Program Files\Microsoft Visual Studio 8\Common7\IDE\PrivateAssemblies。  
  
## <a name="editing-guidelines"></a>編輯指導方針  
 除非您要部署或移除自訂延伸模組、在預覽期間停用快取，或是在 Service Pack 升級之後登錄新的資料處理延伸模組，否則請勿修改這個檔案中的設定。  
  
 如果您要自訂轉譯延伸模組設定，請使用編輯組態檔的特定指示。 如需詳細資訊，請參閱 [在 RSReportServer.Config 中自訂轉譯延伸模組參數](../customize-rendering-extension-parameters-in-rsreportserver-config.md)。  
  
 如需如何編輯設定檔的一般指示，請參閱[修改 Reporting Services 設定檔 &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
## <a name="example-configuration-file"></a>範例組態檔  
 下列範例說明 RSReportDesigner.config 檔案的格式。  
  
```  
<Configuration>  
  <Add Key="SecureConnectionLevel" Value="0" />  
  <Add Key="InstanceName" Value="Microsoft.ReportingServices.PreviewServer" />  
  <Add Key="SessionCookies" Value="true" />  
  <Add Key="SessionTimeoutMinutes" Value="3" />  
  <Add Key="PolicyLevel" Value="rspreviewpolicy.config" />  
  <Add Key="CacheDataForPreview" Value="true" />  
  <Extensions>  
    <Render> . . . </Render>  
    <Data> . . . </Data>  
    <Designer> . . . </Designer>  
```  
  
## <a name="configuration-settings"></a>組態設定  
  
|設定|描述|  
|-------------|-----------------|  
|`SecureConnectionLevel`|指定 Web 服務連接的安全性程度。 有效值範圍是從 0 到 3，其中 0 表示最不安全。 如需詳細資訊，請參閱 [使用安全的 Web 服務方法](../report-server-web-service/net-framework/using-secure-web-service-methods.md)。|  
|`InstanceName`|預覽伺服器的識別碼。 請勿修改此值。|  
|`SessionCookies`|指定報表伺服器是否使用瀏覽器 Cookie 來維護工作階段資訊。 有效值包括 `true` 和 `false`。 預設為 `true`。 如果將此值設定為 [False]，工作階段資料就會儲存在 **reportservertempdb** 資料庫中。|  
|`SessionTimeoutMinutes`|指定工作階段 Cookie 有效的期間。 預設值是 3 分鐘。|  
|`PolicyLevel`|指定安全性原則組態檔。 有效的值為 Rspreviewpolicy.config。如需詳細資訊，請參閱[使用 Reporting Services 安全性原則](../extensions/secure-development/using-reporting-services-security-policy-files.md)檔案。|  
|`CacheDataForPreview`|設定為 `True` 時，報表設計師會將資料儲存在本機電腦上的快取檔案內。 有效值為 `True` (預設值) 和 `False`。 如需詳細資訊，請參閱 [預覽報表](../reports/previewing-reports.md)。|  
|`Render`|列舉報表設計師可用於預覽的轉譯延伸模組。 用來預覽的轉譯延伸模組集，應該要和安裝在報表伺服器中的轉譯延伸模組相同。<br /><br /> `Name` 指定轉譯延伸模組。 如果您透過程式碼叫用轉譯延伸模組，請使用此值以呼叫特定延伸模組。<br /><br /> `Type` 指定延伸模組類別的完整類別名稱加上程式庫名稱，並以逗號分隔。<br /><br /> `Visible` 指定是否在任何使用者介面中顯示名稱。 此值可以是 `True` (預設值) 或 `False`。 如果為 `True`，則會在使用者介面中顯示。|  
|`Data`|列舉報表設計師可用於連接到提供報表資料之資料來源的資料處理延伸模組。 使用於報表設計師中的資料處理延伸模組集，應該要和安裝在報表伺服器中的資料處理延伸模組相同。 如果您要加入或移除自訂延伸模組，請參閱 [部署資料處理延伸模組](../extensions/data-processing/deploying-a-data-processing-extension.md)。<br /><br /> `Name` 指定資料處理延伸模組。<br /><br /> `Type` 指定延伸模組類別的完整類別名稱加上程式庫名稱，並以逗號分隔。|  
|`Designer`|列舉報表設計師可以使用的查詢產生器。 查詢產生器會提供建構查詢的使用者介面，以擷取報表所使用的資料。 不同的資料處理延伸模組可能有不同的查詢產生器。 依預設，Reporting Services 會對產品內所包括的所有資料處理延伸模組，提供一個視覺化資料工具使用者介面。 然而，如果您建立或使用協力廠商的資料處理延伸模組，則可套用其他查詢產生器介面。|  
|`PreviewProcessingServiceStartupTimeoutSeconds`|指定在顯示錯誤訊息之前，等待預覽處理服務啟動的週期。 預設為 15 秒。|  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態檔](reporting-services-configuration-files.md)   
 [報表設計師 SQL Server Data Tools &#40;SSRS&#41;中的查詢設計工具](../report-data/query-design-tools-ssrs.md)  
  
  
