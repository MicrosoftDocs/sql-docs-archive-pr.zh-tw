---
title: SQL Server 2014 中已停止的管理工具功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 6e58acd0-73c5-4161-9fbc-8ea531bc681c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3ae7d4a708816c1b30a0b208bb422e0920b4c76c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87701638"
---
# <a name="discontinued-management-tools-features-in-sql-server-2014"></a>在 SQL Server 2014 中已停止的管理工具功能
  此主題描述 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中無法再使用的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]管理工具功能。  
  
## <a name="features-removed-in-sscurrent"></a>[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中移除的功能  
 無  
  
## <a name="features-removed-in-sssql11"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中移除的功能  
  
### <a name="sql-server-compact-edition"></a>SQL Server Compact Edition  
 已從 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]移除 SQL Server Compact Edition 程式碼編輯器。 此外，亦從 [物件總管]、[方案總管] 及 [範本總管] 中移除了 SQL Server Compact Edition 支援。 請改用 Microsoft Visual Studio 2010 Service Pack 1 或 Webmatrix 的 Transact-SQL 編輯器。  
  
### <a name="activex-subsystem-for-sql-server-agent"></a>SQL Server Agent 的 ActiveX 子系統  
 此版本中已移除 SQL Server Agent 的 ActiveX 子系統。 沒有取代功能。  
  
### <a name="sp_addtask-sp_deletetask-sp_updatetask"></a>sp_addtask、sp_deletetask、sp_updatetask  
 此版本中已移除 Sp_addtask、sp_deletetask 及 sp_updatetask。 請勿在新的或更新的應用程式中使用此功能。  
  
### <a name="net-send-and-pager-notification"></a>Net Send 和呼叫器通知  
 此版本中已移除 Net Send 和呼叫器通知。 請勿在新的或更新的應用程式中使用此功能。  
  
### <a name="data-tier-applications"></a>資料層應用程式  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 中的部分資料層應用程式 (DAC) 功能在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]中已經移除。 但是，隨 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 發行的資料層應用程式架構 (DACfx 3.0 版) 透過 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 和 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 與 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] 相容。 舊版的 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 不支援 DAC 3.0 版，包括 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 中的 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]。 Visual Studio 2010 資料庫專案不支援使用 DACfx 3.0 版或更新版本產生的 DAC 3.0 DACPAC 封裝或 DAC 匯出 (BACPAC) 封裝。  
  
 Microsoft 建議使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 資料庫專案的最新可用版本。  
  
 DACfx 3.0 API 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工具確實支援讀取以舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工具和 DACfx 版本所建立的 DACPAC 和 BACPAC 檔案：將資料庫擷取至這些版本的 DACPAC 檔案，以及透過 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] Data Tools 將資料庫部署至支援的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。  
  
## <a name="see-also"></a>另請參閱  
 [回溯相容性](../../2014/getting-started/backward-compatibility.md)  
  
  
