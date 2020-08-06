---
title: 重新命名報表伺服器電腦 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- renaming report servers
ms.assetid: 82fc4ba2-291a-4939-a025-271b8d687c54
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fe8f699c17f9e5f1e11406ac6e5c161488767ed1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606635"
---
# <a name="rename-a-report-server-computer"></a>重新命名報表伺服器電腦
  重新命名電腦會使 Web 伺服器和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體 (如果它在同一台電腦上) 發生對應的名稱變更。 在某些情況下，當電腦名稱變更後，可能就無法存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 電腦名稱變更之後，您可以利用本主題提供的步驟來重新設定報表伺服器。  
  
## <a name="renaming-a-sql-server-database-engine"></a>重新命名 SQL Server Database Engine  
 如果您要重新命名執行報表伺服器資料庫的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體，請執行下列步驟：  
  
1.  啟動 Reporting Services 組態工具，然後連接到使用重新命名的伺服器中報表伺服器資料庫的報表伺服器。  
  
2.  開啟 [資料庫安裝] 頁面。  
  
3.  在 **[伺服器名稱]** 中，輸入或選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名稱，然後按一下 **[連接]** 。  
  
4.  按一下 [套用]  。  
  
 如果報表伺服器正使用本機 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，您可以利用 *(local)* 或 *(local)\instancename* 來指定伺服器。 如果您利用 *(local)* 來參考伺服器，您可以重新命名伺服器，如此一來，連接就可以繼續運作。 如果您是使用遠端伺服器，或者 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 是利用伺服器名稱來設定的，則每當伺服器名稱變更時，您都必須更新資料庫連接資訊。  
  
## <a name="renaming-a-report-server-computer"></a>重新命名報表伺服器電腦  
 如果您要重新命名執行報表伺服器的電腦，請執行下列步驟：  
  
1.  在文字編輯器中開啟**RSReportServer.config** ，並修改 `UrlRoot` 設定以反映新的伺服器名稱。 傳遞延伸模組利用 `UrlRoot` 設定來撰寫用於存取儲存在報表伺服器上之項目的 URL。 若要變更報表伺服器 URL 位址，您必須更新 `UrlRoot` 設定，讓訂閱能夠如預期般繼續傳遞報表。  
  
2.  在相同的檔案中，如果已設定名稱，請修改 `ReportServerUrl` 設定來反映新的伺服器名稱。 請注意，並非每一種安裝都使用此設定。 如果它是空的，請不要執行任何動作。  
  
    > [!NOTE]  
    >  如果您在企業網路上使用 Windows 網際網路命名服務 (WINS)，報表伺服器和報表管理員可能還可以在先前的名稱下繼續使用一段時間。 WINS 會將 IP 位址對應到它所提供服務的每台電腦。 WINS 為重新命名的電腦重新整理 IP 位址之後，就無法再利用舊的電腦名稱來存取報表伺服器或報表管理員。  
  
## <a name="see-also"></a>另請參閱  
 [Rsreportserver.config 設定檔](rsreportserver-config-configuration-file.md)   
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Reporting Services 報表伺服器 &#40;原生模式&#41;](reporting-services-report-server-native-mode.md)   
 [啟動與停止 Report Server 服務](start-and-stop-the-report-server-service.md)   
 [rsconfig 公用程式 &#40;SSRS&#41;](../tools/rsconfig-utility-ssrs.md)  
  
  
