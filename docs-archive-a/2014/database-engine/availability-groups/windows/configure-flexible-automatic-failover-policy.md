---
title: 設定彈性容錯移轉原則，以控制 Always On 可用性群組的自動容錯移轉 (的條件) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], flexible failover policy
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 1ed564b4-9835-4245-ae35-9ba67419a4ce
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c938624a3ed39fe2d41f21a21af5231aa76a8c17
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707913"
---
# <a name="configure-the-flexible-failover-policy-to-control-conditions-for-automatic-failover-always-on-availability-groups"></a>設定彈性容錯移轉原則以控制自動容錯移轉的條件 (AlwaysOn 可用性群組)
  本主題描述如何使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]或 PowerShell 來設定 AlwaysOn 可用性群組的彈性容錯移轉原則。 彈性容錯移轉原則可讓您更精確地控制造成可用性群組之自動容錯移轉的狀況。 透過變更觸發自動容錯移轉的失敗狀況和健全狀況檢查的頻率，您可以提高或降低自動容錯移轉的可能性，以便支援高可用性的 SLA。  
  
  
  
    > [!NOTE]  
    >  The flexible failover policy of an availability group cannot be configured by using [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-on-automatic-failovers"></a><a name="Limitations"></a>自動容錯移轉的限制  
  
-   若要進行自動容錯移轉，目前的主要複本和一個次要複本必須設定為具有自動容錯移轉的同步認可可用性模式，而且次要複本必須與主要複本同步處理。  
  
-   如果可用性群組超過其 WSFC 失敗臨界值，WSFC 叢集將不會嘗試進行可用性群組的自動容錯移轉。 此外，可用性群組的 WSFC 資源群組會維持失敗狀態，直到叢集管理員手動讓失敗的資源群組上線，或者資料庫管理員執行可用性群組的手動容錯移轉為止。 *「WSFC 失敗臨界值」* (WSFC Failure Threshold) 定義為可用性群組在給定的時間週期內支援的失敗次數上限。 預設的時間週期為六小時，而且在這段時間內失敗次數上限的預設值為 *n*-1，其中 *n* 是 WSFC 節點的數目。 若要變更給定可用性群組得失敗臨界值，請使用 WSFC 容錯移轉管理員主控台。  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
  
-   您必須連接到裝載主要複本的伺服器執行個體。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
  
|Task|權限|  
|----------|-----------------|  
|若要設定新可用性群組的彈性容錯移轉原則|需要 **系統管理員 (sysadmin)** 固定伺服器角色的成員資格，以及 CREATE AVAILABILITY GROUP 伺服器權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。|  
|若要修改現有可用性群組的原則|需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。|  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要設定彈性容錯移轉原則**  
  
1.  連接到裝載主要複本的伺服器執行個體。  
  
2.  若為新的可用性群組，請使用[CREATE AVAILABILITY group](/sql/t-sql/statements/create-availability-group-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] 語句。 如果您要修改現有的可用性群組，請使用[ALTER AVAILABILITY group](/sql/t-sql/statements/alter-availability-group-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] 語句。  
  
    -   若要設定容錯移轉狀況層級，請使用 FAILURE_CONDITION_LEVEL = *n* 選項，其中 *n* 是介於 1 到 5 之間的整數。  
  
         例如，下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式會將現有可用性群組 `AG1`的失敗狀況層級變更為層級一：  
  
        ```sql
        ALTER AVAILABILITY GROUP AG1 SET (FAILURE_CONDITION_LEVEL = 1);  
        ```  
  
         這些整數值與失敗狀況層級的關聯性如下所示：  
  
        |[!INCLUDE[tsql](../../../includes/tsql-md.md)] 值|層級|起始自動容錯移轉的狀況|  
        |------------------------------|-----------|-------------------------------------------|  
        |1|一個|伺服器關閉時。 SQL Server 服務由於容錯移轉或重新啟動而停止。|  
        |2|兩個|伺服器沒有回應時。 滿足任何狀況的較低值，而且 SQL Server 服務連接到叢集且超過健全狀況檢查逾時臨界值，或者目前主要複本處於失敗狀態。|  
        |3|三|發生嚴重伺服器錯誤時。 滿足任何狀況的較低值，或者發生內部嚴重伺服器錯誤。<br /><br /> 這是預設層級。|  
        |4|四|發生一般伺服器錯誤時。 滿足任何狀況的較低值，或者發生一般伺服器錯誤。|  
        |5|五|發生任何限定的失敗狀況時。 滿足任何狀況的較低值，或者發生限定失敗狀況。|  
  
         如需容錯移轉條件層級的詳細資訊，請參閱[可用性群組自動容錯移轉的彈性容錯移轉原則 &#40;SQL Server&#41;](flexible-automatic-failover-policy-availability-group.md)。  
  
    -   若要設定健全狀況檢查逾時臨界值，請使用 HEALTH_CHECK_TIMEOUT = *n* 選項，其中 *n* 是介於 15000 毫秒 (15 秒) 到 4294967295 毫秒之間的整數。 預設值為 30000 毫秒 (30 秒)。  
  
         例如，下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式會將現有可用性群組 `AG1`的健全狀況檢查逾時臨界值變更為 60,000 毫秒 (一分鐘)。  
  
        ```sql
        ALTER AVAILABILITY GROUP AG1 SET (HEALTH_CHECK_TIMEOUT = 60000);  
        ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> 使用 PowerShell  

### <a name="to-configure-the-flexible-failover-policy"></a>若要設定彈性容錯移轉原則 * *  
  
1.  將預設值 (`cd`) 設定為裝載主要複本的伺服器執行個體。  
  
2.  將可用性複本加入至可用性群組時，請使用 `New-SqlAvailabilityGroup` 指令程式。 修改現有的可用性複本時，請使用 `Set-SqlAvailabilityGroup` 指令程式。  
  
    -   若要設定容錯移轉狀況層級，請使用 `FailureConditionLevel` *level*參數，其中*level*是下列其中一個值：  
  
        |值|層級|起始自動容錯移轉的狀況|  
        |-----------|-----------|-------------------------------------------|  
        |`OnServerDown`|一個|伺服器關閉時。 SQL Server 服務由於容錯移轉或重新啟動而停止。|  
        |`OnServerUnresponsive`|兩個|伺服器沒有回應時。 滿足任何狀況的較低值，而且 SQL Server 服務連接到叢集且超過健全狀況檢查逾時臨界值，或者目前主要複本處於失敗狀態。|  
        |`OnCriticalServerError`|三|發生嚴重伺服器錯誤時。 滿足任何狀況的較低值，或者發生內部嚴重伺服器錯誤。<br /><br /> 這是預設層級。|  
        |`OnModerateServerError`|四|發生一般伺服器錯誤時。 滿足任何狀況的較低值，或者發生一般伺服器錯誤。|  
        |`OnAnyQualifiedFailureConditions`|五|發生任何限定的失敗狀況時。 滿足任何狀況的較低值，或者發生限定失敗狀況。|  
  
         如需容錯移轉條件層級的詳細資訊，請參閱[可用性群組自動容錯移轉的彈性容錯移轉原則 &#40;SQL Server&#41;](flexible-automatic-failover-policy-availability-group.md)。  
  
         例如，下列命令會將現有可用性群組 `AG1`的失敗狀況層級變更為層級一。  
  
        ```powershell
        Set-SqlAvailabilityGroup `
         -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg `
         -FailureConditionLevel OnServerDown  
        ```  
  
    -   若要設定健全狀況檢查超時閾值，請使用 `HealthCheckTimeout` *n*參數，其中*n*是15000毫秒的整數， (15 秒) 到4294967295毫秒。 預設值為 30000 毫秒 (30 秒)。  
  
         例如，下列命令會將現有可用性群組 `AG1`的健全狀況檢查逾時臨界值變更為 120,000 毫秒 (兩分鐘)。  
  
        ```powershell
        Set-SqlAvailabilityGroup `
         -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAG `
         -HealthCheckTimeout 120000  
        ```  
  
> [!NOTE]  
>  若要檢視指令程式的語法，請在 `Get-Help` PowerShell 環境中使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 指令程式。 如需詳細資訊，請參閱 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
 **若要設定和使用 SQL Server PowerShell 提供者**  
  
-   [SQL Server PowerShell 提供者](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性模式 (AlwaysOn 可用性群組) ](availability-modes-always-on-availability-groups.md)   
 [容錯移轉和容錯移轉模式 &#40;AlwaysOn 可用性群組&#41;](failover-and-failover-modes-always-on-availability-groups.md)   
 [SQL Server 的 Windows Server 容錯移轉叢集 &#40;WSFC&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [容錯移轉叢集執行個體的容錯移轉原則](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)   
 [sp_server_diagnostics &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql)  
