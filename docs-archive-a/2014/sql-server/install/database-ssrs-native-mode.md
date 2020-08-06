---
title: 資料庫 (SSRS 原生模式) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.databasesetup.F1
ms.assetid: 8c9bb3b3-ea77-4a5b-ba35-7451ed11083d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bb8f1841e980279d6051e3393efdf06df238f41f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606623"
---
# <a name="database-ssrs-native-mode"></a>資料庫 (SSRS 原生模式)
  使用 [資料庫] 頁面，即可建立和設定報表伺服器資料庫，以便提供一個或多個報表伺服器執行個體的內部儲存位置。 如果您要設定報表伺服器使用遠端報表伺服器資料庫，您必須使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員建立此資料庫。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]原生模式。  
  
 建立報表伺服器資料庫和設定連接是多重步驟的程序。 此頁面會提供每一種工作類型的精靈，以引導您執行步驟。 將會為您建立或更新權限和登入。 您可以在 [進度] 頁面中監視每一個步驟的狀態。 如果發生錯誤，您可以按一下此錯誤，以取得如何解決它的相關資訊。  
  
 報表伺服器資料庫必須支援特定的伺服器模式。 預設的模式為原生模式，但如果您是在較大的 SharePoint 產品或技術部署中執行報表伺服器，也可以建立使用 SharePoint 整合模式的報表伺服器資料庫。 如需詳細資訊，請參閱[建立原生模式報表伺服器資料庫 &#40;SSRS 設定管理員&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)。  
  
 若要開啟此頁面，請啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員，並按一下導覽窗格中的 **[資料庫]** 。 如需詳細資訊，請參閱 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
## <a name="options"></a>選項  
 **SQL Server 名稱**  
 在目前的報表伺服器資料庫中， **[SQL Server 名稱]** 會指定執行報表伺服器資料庫的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 名稱。 也可以在本機或遠端電腦上使用預設或具名的執行個體。  
  
 **Database Name**  
 指定儲存伺服器資料之報表伺服器資料庫的名稱。  
  
 **報表伺服器模式**  
 指出報表伺服器資料庫是支援原生模式或 SharePoint 整合模式。 如需詳細資訊，請參閱[Reporting Services 報表伺服器](../../../2014/reporting-services/reporting-services-report-server.md)。  
  
 **變更資料庫**  
 啟動精靈，此精靈會引導您建立或選取報表伺服器資料庫所需的所有步驟。  
  
 **認證類型**  
 指定報表伺服器用來連接到報表伺服器資料庫的認證。 您可以指定的認證類型包括服務帳戶、Windows 網域使用者、Windows 本機使用者或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫登入。 如需選取認證的詳細資訊，請參閱[將報表伺服器資料庫連接設定 &#40;SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。  
  
 **使用者名稱**  
 如果您是使用 Windows 認證，請指定網域使用者帳戶；如果您是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認證，請指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 如果您使用 Windows 認證，請以下列格式指定： * \<domain> \\<帳戶 \> *。  
  
 **密碼**  
 指定帳戶的密碼。  
  
 **變更認證**  
 啟動精靈，它將會引導您選取不同帳戶或更新用來連接報表伺服器資料庫之帳戶密碼所需的所有步驟。  
  
## <a name="see-also"></a>另請參閱  
 [建立原生模式報表伺服器資料庫 &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Reporting Services 組態管理員 &#40;SSRS 原生模式的 F1 說明主題&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [&#40;SSRS 原生模式的報表伺服器資料庫&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [設定報表伺服器資料庫連接 &#40;SSRS 組態管理員&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
