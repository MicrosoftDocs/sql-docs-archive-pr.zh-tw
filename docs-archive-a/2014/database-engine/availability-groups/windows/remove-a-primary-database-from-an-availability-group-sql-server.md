---
title: 將主要資料庫從可用性群組移除 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.removeprimarydb.f1
helpviewer_keywords:
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: 6d4ca31e-ddf0-44bf-be5e-a5da060bf096
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6b6fafaf6464431d68f8cfdf9dc9d8fa844a42a7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593607"
---
# <a name="remove-a-primary-database-from-an-availability-group-sql-server"></a>將主要資料庫從可用性群組移除 (SQL Server)
  此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中的 PowerShell，將主要資料庫和對應的次要資料庫從 AlwaysOn 可用性群組中移除。  
  
-   **開始之前：**  
  
     [必要條件和限制](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目移除可用性資料庫：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **待處理：**  [從可用性群組中移除可用性資料庫之後](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="prerequisites-and-restrictions"></a><a name="Prerequisites"></a> 必要條件和限制  
  
-   只有在主要複本上才支援這個工作。 您必須連接到裝載主要複本的伺服器執行個體。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **若要移除可用性資料庫**  
  
1.  在 [物件總管] 中，連接到裝載要移除資料庫之主要複本的伺服器執行個體，然後展開伺服器樹狀目錄。  
  
2.  依序展開 **[AlwaysOn 高可用性]** 節點和 **[可用性群組]** 節點。  
  
3.  選取可用性群組，然後展開 **[可用性資料庫]** 節點。  
  
4.  此步驟取決於您要移除多個資料庫群組或只要移除一個資料庫，如下所示：  
  
    -   若要移除多個資料庫，請使用 **[物件總管詳細資料]** 窗格檢視及選取您要移除的所有資料庫。 如需詳細資訊，請參閱[使用物件總管詳細資料監視可用性群組 &#40;SQL Server Management Studio&#41;](use-object-explorer-details-to-monitor-availability-groups.md)。  
  
    -   若要移除單一資料庫，請在 **[物件總管]** 窗格或 **[物件總管詳細資料]** 窗格中選取它。  
  
5.  以滑鼠右鍵按一下選取的一或多個資料庫，然後在命令功能表中選取 [從可用性群組移除資料庫]****。  
  
6.  在 **[從可用性群組移除資料庫]** 對話方塊中，若要移除所有列出的資料庫，請按一下 **[確定]**。 如果您不要移除所有列出的資料庫，請按一下 **[取消]**。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要移除可用性資料庫**  
  
1.  連接到裝載主要複本的伺服器執行個體。  
  
2.  使用 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) 陳述式，如下所示：  
  
     ALTER AVAILABILITY GROUP *group_name* REMOVE DATABASE *availability_database_name*  
  
     *group_name* 是可用性群組的名稱，而 *database_name* 是要移除的資料庫名稱。  
  
     下列範例會從 `Db6` 可用性群組中移除名稱為 `MyAG` 的資料庫。  
  
    ```sql
    ALTER AVAILABILITY GROUP MyAG REMOVE DATABASE Db6;  
    ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> 使用 PowerShell  
 **若要移除可用性資料庫**  
  
1.  變更目錄 (`cd`) 為裝載主要複本的伺服器執行個體。  
  
2.  使用 `Remove-SqlAvailabilityDatabase` 指令程式，指定要從可用性群組移除的可用性資料庫名稱。 連接到裝載主要複本的伺服器執行個體時，主要資料庫及其對應的次要資料庫都會從可用性群組中移除。  
  
     例如，下列命令會將 `MyDb9` 可用性資料庫從名為 `MyAg`的可用性群組中移除。 因為此命令是在裝載主要複本的伺服器執行個體上執行，所以系統會從可用性群組中移除主要資料庫及其所有對應的次要資料庫。 系統將不再針對任何次要複本的這個資料庫進行資料同步處理。  
  
    ```powershell
    Remove-SqlAvailabilityDatabase -Path SQLSERVER:\Sql\PrimaryComputer\InstanceName\AvailabilityGroups\MyAg\Databases\MyDb9  
    ```  
  
    > [!NOTE]  
    >  若要檢視指令程式的語法，請在 `Get-Help` PowerShell 環境中使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 指令程式。 如需詳細資訊，請參閱 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
 **若要設定和使用 SQL Server PowerShell 提供者**  
  
-   [SQL Server PowerShell 提供者](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="follow-up-after-removing-an-availability-database-from-an-availability-group"></a><a name="FollowUp"></a> 待處理：從可用性群組中移除可用性資料庫之後  
 從可用性群組中移除可用性資料庫，會結束先前主要資料庫和對應的次要資料庫之間的資料同步處理。 先前主要資料庫會保持上線狀態。 每個對應的次要資料庫處於 RESTORING 狀態。  
  
 此時有替代方法可處理移除的次要資料庫：  
  
-   如果您不再需要給定的次要資料庫，可將它卸除。  
  
     如需詳細資訊，請參閱 [刪除資料庫](../../../relational-databases/databases/delete-a-database.md)。  
  
-   從可用性群組中移除次要資料庫之後，若要存取移除的次要資料庫，可以復原資料庫。 不過，如果復原移除的次要資料庫，線上將會有兩個名稱相同但內容不同的獨立資料庫。 您必須確定用戶端只能存取其中一個資料庫 (通常是最新的主要資料庫)。  
  
     如需詳細資訊，請參閱[復原資料庫而不還原資料 &#40;Transact-SQL&#41;](../../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [將次要資料庫從可用性群組移除 &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
