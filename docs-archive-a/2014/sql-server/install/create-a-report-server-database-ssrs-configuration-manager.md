---
title: 建立報表伺服器資料庫 (SSRS 設定管理員) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], databases
- report server database
- databases [Reporting Services], creating
ms.assetid: 8a3a6ffe-4001-46be-8548-94532550f6a5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d899d0585eda7c9cd2b12147732b23c01872128b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593776"
---
# <a name="create-a-report-server-database--ssrs-configuration-manager"></a>建立報表伺服器資料庫 (SSRS 組態管理員)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**原生模式**會使用兩個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 關係資料庫來儲存報表伺服器中繼資料和物件。 一個資料庫做為主要儲存體，而另一個用來儲存暫存資料。 兩個資料庫會一起建立，並依名稱繫結。 使用預設的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，資料庫會命名為 `reportserver` 和 `reportservertempdb`。 這兩個資料庫統稱為「報表伺服器資料庫」或「報表伺服器目錄」。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **SharePoint 模式** 包括用於資料警示中繼資料的第三個資料庫。 這三個資料庫是針對每個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式所建立，而資料庫名稱預設會包含代表服務應用程式的 GUID。 以下是這三個 SharePoint 模式資料庫的範例名稱：  
  
-   ReportingService_90a9f37075544f22953c4a62e4a9f370  
  
-   ReportingService_90a9f37075544f22953c4a62e4a9f370TempDB  
  
-   ReportingService_90a9f37075544f22953c4a62e4a9f370_Alerting  
  
> [!IMPORTANT]  
>  請勿撰寫針對報表伺服器資料庫執行查詢的應用程式。 報表伺服器資料庫並非公用結構描述。 前後版次的資料表結構可能會變更。 如果您寫入的應用程式需要存取報表伺服器資料庫，請一定要利用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] API 來存取報表伺服器資料庫。  
>   
>  這種情況的例外狀況為執行記錄檢視。 如需詳細資訊，請參閱 [報表伺服器執行記錄和 ExecutionLog3 視圖](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)  
  
## <a name="ways-to-create-the-report-server-database"></a>建立報表伺服器資料庫的方法  
 **原生模式：** 您可以利用下列方式建立原生模式報表伺服器資料庫：  
  
-   自動：如果選擇預設組態安裝選項，則會使用 SQL Server 安裝精靈。 在 [SQL Server 安裝精靈] 中，這是 [報表伺服器安裝選項] 頁面中的 [安裝和設定]****。 如果您選擇了 [Install only]  (只安裝)**** 選項，就必須使用 Reporting Services 設定管理員建立資料庫。  
  
-   手動：使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員。 如果您要使用遠端 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 來主控報表伺服器資料庫，您必須手動建立此資料庫。 如需詳細資訊，請參閱[建立原生模式報表伺服器資料庫 &#40;SSRS 設定管理員&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)。  
  
 **SharePoint 模式：**[報表伺服器安裝選項] 頁面只有一個用於 SharePoint 模式的選項 [只安裝]****。 此選項會安裝所有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 檔案和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共用服務。 下一步是透過下列其中一種方式建立至少一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式：  
  
-   使用 SharePoint 管理中心建立 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。 如需詳細資訊，請參閱 [步驟3：建立 Reporting Services 服務應用程式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md#bkmk_create_serrviceapplication)的「服務應用程式」一節。  
  
-   使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] PowerShell 指令程式建立服務應用程式和報表伺服器資料庫。 如需詳細資訊，請參閱 [Reporting Services SharePoint 模式的 PowerShell Cmdlet](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)主題中的建立服務應用程式範例。  
  
## <a name="database-server-version-requirements"></a>資料庫伺服器版本需求  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可用來主控報表伺服器資料庫。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體可以是本機或遠端執行個體。 以下是支援的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 版本，可用來裝載報表伺服器資料庫：  
  
- SQL Server 2014
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
 在遠端電腦上建立報表伺服器資料庫時，您必須設定連接以使用網域使用者帳戶，或是擁有網路存取權的服務帳戶。 如果您決定使用遠端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，請仔細考慮報表伺服器要用來連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的認證。 如需詳細資訊，請參閱 [&#40;SSRS 設定報表伺服器資料庫連接 Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。  
  
> [!IMPORTANT]  
>  報表伺服器與主控報表伺服器資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，可以在不同的網域中。 針對網際網路部署，常會使用位於防火牆後方的伺服器。 如果您要設定供網際網路存取的報表伺服器，請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認證，以連接到位於防火牆後方之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，並使用 IPSEC 來保護連接的安全。  
  
## <a name="database-server-edition-requirements"></a>資料庫伺服器版本需求  
 當您建立報表伺服器資料庫時，請注意，並非所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本都可以用來主控資料庫。 如需詳細資訊，請參閱 [SQL Server 2014 版本所支援之功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)的「報表伺服器資料庫伺服器版本需求」一節。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態管理員 &#40;del&#41;](https://docs.microsoft.com/sql/sql-server/install/reporting-services-configuration-manager-native-mode)  
  
  
