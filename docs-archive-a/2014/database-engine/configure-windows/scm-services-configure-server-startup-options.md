---
title: 設定伺服器啟動選項 (SQL Server 組態管理員) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- parameters [SQL Server], startup options
- SQL Server, startup options
- single-user mode [SQL Server], starting in
- startup options [SQL Server]
- SQL Server services, setting startup options
ms.assetid: 7a94643c-6460-4baf-bb31-0cb99eaf970d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 405a96208c774a6326a69cf9826a14ca3552eae1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688198"
---
# <a name="configure-server-startup-options-sql-server-configuration-manager"></a>設定伺服器啟動選項 (SQL Server 組態管理員)
  本主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager，設定每次 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 於 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中啟動時要使用的啟動選項。 如需啟動選項的清單，請參閱 [Database Engine 服務啟動選項](database-engine-service-startup-options.md)。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
### <a name="limitations-and-restrictions"></a>限制事項  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員會將啟動參數寫入登錄中。 下次啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)]時，這些參數就會生效。  
  
 在叢集中，您必須在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上線時在使用中伺服器上進行變更；當 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 重新啟動時，這些變更就會生效。 下次容錯移轉時則會在另一個節點上進行啟動選項的登錄更新。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 設定伺服器啟動選項僅限於能夠在登錄中變更相關項目的使用者， 包括下列使用者。  
  
-   本機 Administrators 群組的成員。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所使用的網域帳戶 (如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 設定為使用網域帳戶來執行的話)。  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> 使用 SQL Server 組態管理員  
  
#### <a name="to-configure-startup-options"></a>若要設定啟動選項  
  
1.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員中，按一下 **[SQL Server 服務]** 。  
  
    > [!NOTE]  
    >  因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理主控台程式的嵌入式管理單元，而不是獨立的程式，所以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員在較新版本的 Windows 中不會作為應用程式出現。  
    >   
    >  -   **Windows 10**：  
    >          若要開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager，請在 [**開始] 頁面**上，輸入適用于) 的 sqlservermanager12.msc (。 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 針對先前版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，以較小的數字取代 12。 按一下 SQLServerManager12.msc 即可開啟 Configuration Manager。 若要將 Configuration Manager 釘選到起始頁或工作列，請在 [Sqlservermanager12.msc] 上按一下滑鼠右鍵，然後按一下 [**開啟檔案位置**]。 在 Windows 檔案瀏覽器中，以滑鼠右鍵按一下 [Sqlservermanager12.msc]，然後按一下 [**釘選到開始**] 或 [**釘選到工作列**]。  
    > -   **Windows 8**：  
    >          若要開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager，請在 [**搜尋**] 快速鍵的 [**應用程式**] 底下，輸入**SQLServerManager \<version> ** （例如 `SQLServerManager12.msc` ），然後按**enter**。  
  
2.  在右窗格中，以滑鼠右鍵按一下 [ **SQL Server (***<instance_name>***) **]，然後按一下 [**屬性**]。  
  
3.  在 **[啟動參數]** 索引標籤的 **[指定啟動參數]** 方塊中輸入參數，然後按一下 **[加入]** 。  
  
     例如，若要在單一使用者模式中啟動，請 `-m` 在 [**指定啟動參數**] 方塊中輸入，然後按一下 [**新增**]。 (當您以單一使用者模式重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，請先停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent。 否則， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 可能會先進行連接，您就無法以另一個使用者的身分進行連接)。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  重新啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
    > [!WARNING]  
    >  當您完成使用單一使用者模式之後，請在 [啟動參數] 方塊的 `-m` [**現有參數**] 方塊中選取參數，然後按一下 [**移除**]。 重新啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 還原為一般多使用者模式。  
  
## <a name="see-also"></a>另請參閱  
 [以單一使用者模式啟動 SQL Server](start-sql-server-in-single-user-mode.md)   
 [當系統管理員遭到鎖定時連接到 SQL Server](connect-to-sql-server-when-system-administrators-are-locked-out.md)   
 [啟動、停止或暫停 SQL Server Agent 服務](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  
