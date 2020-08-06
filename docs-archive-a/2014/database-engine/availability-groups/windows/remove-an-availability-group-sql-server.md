---
title: 移除可用性群組 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.deleteag.f1
helpviewer_keywords:
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], dropping
ms.assetid: 4b7f7f62-43a3-49db-a72e-22d4d7c2ddbb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c17b7d5b362d8b4030d66ebf7ba0e425495410e7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593600"
---
# <a name="remove-an-availability-group-sql-server"></a>移除可用性群組 (SQL Server)
  此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中的 PowerShell，刪除 (卸除) AlwaysOn 可用性群組。 如果當您刪除可用性群組時，裝載其中一個可用性複本的伺服器執行個體離線，則在回到線上之後此伺服器執行個體將會卸除本機可用性複本。 卸除可用性群組，會刪除任何關聯的可用性群組接聽程式。  
  
 請注意，必要時您可以從任何擁有可用性群組之正確安全性認證的 Windows Server 容錯移轉叢集 (WSFC) 節點中卸除可用性群組。 如此一來，當可用性群組沒有任何可用性複本存在時，就可以刪除此可用性群組。  
  
> [!IMPORTANT]  
>  如果可能的話，只在連接主控主要複本的伺服器執行個體時移除可用性群組。 從主要複本卸除可用性群組時，就可以在舊的主要資料庫中進行變更 (沒有高可用性保護)。 從次要複本刪除可用性群組會讓主要複本處於 RESTORING 狀態，而且不允許對資料庫進行變更。  
  
-   **開始之前：**  
  
     [限制與建議](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用下列方法刪除可用性群組：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [相關內容](#RelatedContent)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-recommendations"></a><a name="Restrictions"></a>限制與建議  
  
-   當可用性群組已上線時，從次要複本刪除它會導致主要複本轉換為 RESTORING 狀態。 因此，如果可能的話，只能從裝載主要複本的伺服器執行個體中移除可用性群組。  
  
-   如果您要刪除可用性群組的電腦已經從 WSFC 容錯移轉叢集中移除或逐出，則只會在本機刪除此可用性群組。  
  
-   避免在 Windows Server 容錯移轉叢集 (WSFC) 叢集沒有仲裁時卸除可用性群組。 如果您必須在叢集缺少仲裁時卸除可用性群組，儲存在叢集中的中繼資料可用性群組並不會移除。 在叢集重新取得仲裁之後，您將需要再次卸除可用性群組，以便從 WSFC 叢集中將它移除。  
  
-   在次要複本上，只有在緊急狀況下才可使用 DROP AVAILABILITY GROUP。 這是因為卸除可用性群組會讓可用性群組離線。 如果您從次要複本卸除可用性群組，主要複本就無法判斷 OFFLINE 狀態是因為遺失仲裁、強制容錯移轉或 DROP AVAILABILITY GROUP 命令而發生。 主要複本會轉換成 RESTORING 狀態，以防止可能的裂腦情況發生。 如需詳細資訊，請參閱 [How It Works: DROP AVAILABILITY GROUP Behaviors](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (運作方式：DROP AVAILABILITY GROUP 行為) (CSS SQL Server 工程師部落格)。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。 若要卸除本機伺服器執行個體所未裝載的可用性群組，您需要該可用性群組的 CONTROL SERVER 權限或 CONTROL 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **若要刪除可用性群組**  
  
1.  在 [物件總管] 中，連接到裝載主要複本的伺服器執行個體，可能的話，連接到擁有可用性群組之正確安全性認證的 WSFC 節點上已啟用 AlwaysOn 可用性群組的另一個伺服器執行個體。 展開伺服器樹狀目錄。  
  
2.  依序展開 **[AlwaysOn 高可用性]** 節點和 **[可用性群組]** 節點。  
  
3.  此步驟取決於您要刪除多個可用性群組或只要刪除一個可用性群組，如下所示：  
  
    -   若要刪除多個可用性群組 (其主要複本位於連接的伺服器執行個體上)，請使用 [物件總管詳細資料]**** 窗格，檢視及選取要刪除的所有可用性群組。 如需詳細資訊，請參閱[使用物件總管詳細資料監視可用性群組 &#40;SQL Server Management Studio&#41;](use-object-explorer-details-to-monitor-availability-groups.md)。  
  
    -   若要刪除單一可用性群組，請在 **[物件總管]** 窗格或 **[物件總管詳細資料]** 窗格中選取它。  
  
4.  以滑鼠右鍵按一下一或多個選取的可用性群組，然後選取 [刪除]**** 命令。  
  
5.  在 **[移除可用性群組]** 對話方塊中，刪除所有列出的可用性群組，按一下 **[確定]**。 如果您不要移除所有列出的可用性群組，請按一下 **[取消]**。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要刪除可用性群組**  
  
1.  連接到裝載主要複本的伺服器執行個體，可能的話，連接到擁有可用性群組之正確安全性認證的 WSFC 節點上已啟用 AlwaysOn 可用性群組的另一個伺服器執行個體。  
  
2.  使用 [DROP AVAILABILITY GROUP](/sql/t-sql/statements/drop-availability-group-transact-sql) 陳述式，如下所示。  
  
     DROP AVAILABILITY GROUP *group_name*  
  
     其中 *group_name* 是要卸除的可用性群組名稱。  
  
     下列範例會刪除 `MyAG` 可用性群組。  
  
    ```sql
    DROP AVAILABILITY GROUP MyAG;  
    ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> 使用 PowerShell  
 **若要刪除可用性群組**  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 提供者內：  
  
1.  將目錄切換到 (`cd`) 裝載主要複本的伺服器執行個體，可能的話，連接到擁有可用性群組之正確安全性認證的 WSFC 節點上已啟用 AlwaysOn 可用性群組的另一個伺服器執行個體。  
  
2.  使用 **Remove-SqlAvailabilityGroup** Cmdlet。  
  
     例如，下列命令會移除名為 `MyAg`的可用性群組。 此命令可以在裝載可用性群組之可用性複本的任何伺服器執行個體上執行。  
  
    ```powershell
    Remove-SqlAvailabilityGroup -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg  
    ```  
  
    > [!NOTE]  
    >  若要檢視指令程式的語法，請在 `Get-Help` PowerShell 環境中使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 指令程式。 如需詳細資訊，請參閱 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
 **若要設定和使用 SQL Server PowerShell 提供者**  
  
-   [SQL Server PowerShell 提供者](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 相關內容  
  
-   [How It Works: DROP AVAILABILITY GROUP Behaviors](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (運作方式：DROP AVAILABILITY GROUP 行為) (CSS SQL Server 工程師部落格)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [建立及設定可用性群組 &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)  
