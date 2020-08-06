---
title: 具有 AlwaysOn 可用性群組 (SQL Server) 的消費者入門 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], about
ms.assetid: 33f2f2d0-79e0-4107-9902-d67019b826aa
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0dc9fc81fb02f004eb86c1bfef5662460aa4005f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595273"
---
# <a name="getting-started-with-alwayson-availability-groups-sql-server"></a>開始使用 AlwaysOn 可用性群組 (SQL Server)
  本主題介紹設定 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 執行個體，以支援 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 建立、管理及監視可用性群組的步驟。  
  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="recommended-reading"></a><a name="RecommendedReading"></a> 建議閱讀資料  
 在您建立第一個可用性群組之前，建議您先閱讀下列主題：  
  
-   [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
-   [AlwaysOn 可用性群組 &#40;SQL Server 的必要條件、限制和建議&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
  
##  <a name="configuring-an-instance-of-sql-server-to-support-alwayson-availability-groups"></a><a name="ConfigSI"></a>設定 SQL Server 的實例以支援 AlwaysOn 可用性群組  
  
||步驟|連結|  
|------|----------|-----------|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|**啟用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]。** 您必須在要參與可用性群組的每一個 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 執行個體上，啟用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 功能。<br /><br /> **必要條件：** 主機電腦必須是 Windows Server 容錯移轉叢集 (WSFC) 節點。<br /><br /> 如需其他必要條件的相關資訊，請參閱 [AlwaysOn 可用性群組的必要條件、限制和建議 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md) 中的＜SQL Server 執行個體的必要條件和限制＞。|[啟用和停用 AlwaysOn 可用性群組](enable-and-disable-always-on-availability-groups-sql-server.md)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|**建立資料庫鏡像端點 (如果沒有)。** 確定每個伺服器執行個體擁有 [資料庫鏡像端點](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)： 伺服器執行個體使用這個端點，接收其他伺服器執行個體的 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 連接。|若要判斷資料庫鏡像端點是否存在：[sys.database_mirroring_endpoints](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)<br /><br /> **Windows 驗證：** 若要建立資料庫鏡像端點，請使用：<br /><br /> [新增可用性群組精靈](use-the-availability-group-wizard-sql-server-management-studio.md)<br /><br /> [Transact-SQL](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)<br /><br /> [SQL Server PowerShell](database-mirroring-always-on-availability-groups-powershell.md)<br /><br /> **憑證驗證：** 若要建立資料庫鏡像端點，請使用： <br />                    [Transact-SQL](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)|  
  
##  <a name="creating-and-configuring-a-new-availability-group"></a><a name="ConfigAG"></a> Creating and Configuring a New Availability Group  
  
||步驟|連結|  
|------|----------|-----------|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|**建立可用性群組。** 在裝載要加入可用性群組之資料庫的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上，建立可用性群組。<br /><br /> 至少在您建立可用性群組的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上，建立初始主要複本。 您可以指定一到四個次要複本。 如需可用性群組和複本屬性的資訊，請參閱 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql)。<br /><br /> 強烈建議您建立 [可用性群組接聽程式](../../listeners-client-connectivity-application-failover.md)。<br /><br /> **必要條件：** 裝載給定可用性群組之可用性複本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體，必須位於單一 WSFC 叢集的不同節點上。 唯一的例外狀況是在移轉至另一個 WSFC 叢集期間，可用性群組可以暫時跨兩個叢集。<br /><br /> 如需其他必要條件的相關資訊，請參閱 [AlwaysOn 可用性群組的必要條件、限制和建議 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md) 中的＜可用性群組的必要條件和限制＞、＜可用性資料庫的必要條件和限制＞及＜SQL Server 執行個體的必要條件和限制＞。|若要建立可用性群組，您可以使用下列任何一個工具：<br /><br /> [新增可用性群組精靈](use-the-availability-group-wizard-sql-server-management-studio.md)<br /><br /> [Transact-SQL](create-an-availability-group-transact-sql.md)<br /><br /> [SQL Server PowerShell](create-an-availability-group-transact-sql.md)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|**將次要複本聯結至可用性群組。** 連接至裝載次要複本的每個 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 執行個體，然後將本機次要複本聯結至可用性群組。|[將次要複本聯結至可用性群組](join-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> 提示：如果您使用 [新增可用性群組精靈]，則會自動化這個步驟。|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|**準備次要資料庫。** 在裝載次要複本的每一個伺服器執行個體上，使用 RESTORE WITH NORECOVERY 還原主要資料庫的備份。|[手動準備次要資料庫](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)<br /><br /> 提示：[新增可用性群組精靈] 可為您準備次要資料庫。 如需詳細資訊，請參閱[選取初始資料同步處理頁面 &#40;AlwaysOn 可用性群組精靈&#41;](select-initial-data-synchronization-page-always-on-availability-group-wizards.md) 中的＜使用完整初始資料同步處理的必要條件＞。|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|**將次要資料庫聯結至可用性群組。** 在裝載次要複本的每一個伺服器執行個體上，將每個本機次要資料庫聯結至可用性群組。 聯結可用性群組時，給定的次要資料庫會起始與對應主要資料庫的資料同步處理。|[將次要資料庫聯結至可用性群組](join-a-secondary-database-to-an-availability-group-sql-server.md)<br /><br /> 提示：如果每一個次要資料庫都有一個次要複本，則 [新增可用性群組精靈] 會執行這個步驟。|  
||**建立可用性群組接聽程式。**  除非您在建立可用性群組時已經建立可用性群組接聽程式，否則需要進行這個步驟。|[建立或設定可用性群組接聽程式 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|**將接聽程式的 DNS 主機名稱提供給應用程式開發人員。**  開發人員需要在連接字串中指定這個 DNS 名稱，以便將連線要求導向可用性群組接聽程式。 如需詳細資訊，請參閱[可用性群組接聽程式、用戶端連接性及應用程式容錯移轉 &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)。|「後續操作：建立可用性群組接聽程式之後＞(位於[建立或設定可用性群組接聽程式 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md) 中)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|**設定執行備份作業的位置。**  如果您要在次要資料庫上執行備份，則必須建立備份作業指令碼，以便將自動備份喜好設定納入考量。 在裝載可用性群組之可用性複本的每一個伺服器執行個體上，為可用性群組中的每個資料庫建立指令碼。|「後續操作：設定次要複本的備份之後＞(位於[設定可用性複本的備份 &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md) 中)|  
  
##  <a name="managing-availability-groups-replicas-and-databases"></a><a name="ManageAGsEtc"></a> Managing Availability Groups, Replicas, and Databases  
  
> [!NOTE]  
>  如需可用性群組和複本屬性的資訊，請參閱 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql)。  
  
 管理現有的可用性群組包括下列一個或多個工作：  
  
|Task|連結|  
|----------|----------|  
|修改可用性群組的 [彈性容錯移轉原則](flexible-automatic-failover-policy-availability-group.md) ，以便控制造成自動容錯移轉的狀況。 只有在可能發生自動容錯移轉時，這個原則才會相關。|[設定可用性群組的彈性容錯移轉原則](configure-flexible-automatic-failover-policy.md)|  
|執行規劃的手動容錯移轉或強制手動容錯移轉 (可能遺失資料)，後者通常稱為「強制容錯移轉」。 如需詳細資訊，請參閱[容錯移轉及容錯移轉模式 &#40;AlwaysOn 可用性群組&#41;](failover-and-failover-modes-always-on-availability-groups.md)。|[執行已規劃的手動容錯移轉](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)<br /><br /> [執行強制手動容錯移轉](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)|  
|使用一組預先定義的原則，檢視可用性群組及其複本和資料庫的健全狀況。|[使用原則式管理檢視可用性群組健全狀況](use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)<br /><br /> [使用 AlwaysOn 群組儀表板](use-the-always-on-dashboard-sql-server-management-studio.md)|  
|加入或移除次要複本。|[加入次要複本](add-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [移除次要複本](remove-a-secondary-replica-from-an-availability-group-sql-server.md)|  
|暫停或繼續可用性資料庫。 暫停次要資料庫會維持資料庫的目前狀態，直到您繼續為止。|[暫停資料庫](suspend-an-availability-database-sql-server.md)<br /><br /> [繼續資料庫](resume-an-availability-database-sql-server.md)|  
|加入或移除資料庫。|[加入資料庫](availability-group-add-a-database.md)<br /><br /> [移除次要資料庫](remove-a-secondary-database-from-an-availability-group-sql-server.md)<br /><br /> [移除主要資料庫](remove-a-primary-database-from-an-availability-group-sql-server.md)|  
|重新設定或建立可用性群組接聽程式。|[建立或設定可用性群組接聽程式](create-or-configure-an-availability-group-listener-sql-server.md)|  
|刪除可用性群組。|[刪除可用性群組](remove-an-availability-group-sql-server.md)|  
|疑難排解加入檔案作業。 如果主要資料庫和次要資料庫具有不同的檔案路徑，則可能需要這個作業。|[疑難排解失敗的加入檔案作業](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)|  
|在可用性複本屬性之後。|[變更可用性模式](change-the-availability-mode-of-an-availability-replica-sql-server.md)<br /><br /> [變更容錯移轉模式](change-the-failover-mode-of-an-availability-replica-sql-server.md)<br /><br /> [設定備份優先權 (及自動備份喜好設定)](configure-backup-on-availability-replicas-sql-server.md)<br /><br /> [設定唯讀存取](configure-read-only-access-on-an-availability-replica-sql-server.md)<br /><br /> [設定唯讀路由](configure-read-only-routing-for-an-availability-group-sql-server.md)<br /><br /> [變更工作階段逾時期限](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)|  
  
##  <a name="monitoring-availability-groups"></a><a name="MonitorAGsEtc"></a> 監視可用性群組  
 若要監視 AlwaysOn 可用性群組的屬性和狀態，您可以使用以下工具。  
  
|工具|簡短描述|連結|  
|----------|-----------------------|-----------|  
|適用於 SQL Server 的 System Center 監視封包|適用於 SQL Server 的監視封包 (SQLMP) 是建議 IT 管理員用來監視可用性群組、可用性複本和可用性資料庫的解決方案。 特別與 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 相關的監視功能包括以下項目：<br /><br /> 數百部電腦的可用性群組、可用性複本和可用性資料庫的自動探索能力。 如此可讓您輕鬆地持續追蹤 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 存貨。<br /><br /> 功能完整的 System Center Operations Manager (SCOM) 警示和票證功能。 這些功能會提供詳細知識，讓您更快速地解決問題。<br /><br /> 使用原則式管理 (PBM) 之 AlwaysOn 健全狀況監視的自訂延伸模組。<br /><br /> 從可用性資料庫到可用性複本的健全狀況積存。<br /><br /> 從 System Center Operations Manager 主控台管理 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 的自訂工作。|若要下載監視封包 (SQLServerMP.msi) 和＜適用於 System Center Operations Manager 的 SQL Server 管理封包指南＞(SQLServerMPGuide.doc)，請參閱：<br /><br /> [適用於 SQL Server 的 System Center 監視封包](https://www.microsoft.com/download/details.aspx?displaylang=en&id=10631)|  
|[!INCLUDE[tsql](../../../includes/tsql-md.md)]|[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 目錄和動態管理檢視提供有關可用性群組及其複本、資料庫、接聽程式和 WSFC 叢集環境的許多資訊。|[監視可用性群組 &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|**[物件總管詳細資料]** 窗格會顯示您所連接之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上裝載的可用性群組基本資訊。<br /><br /> 提示：使用此窗格選取多個可用性群組、複本或資料庫，並為所選物件執行例行的系統管理工作，例如，從可用性群組移除多個可用性複本或資料庫。|[使用物件總管詳細資料監視可用性群組](use-object-explorer-details-to-monitor-availability-groups.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|**[屬性]** 對話方塊可讓您檢視可用性群組、複本或接聽程式的屬性，並在某些情況下變更其值。|[可用性群組屬性](view-availability-group-properties-sql-server.md)<br /><br /> [可用性複本屬性](view-availability-replica-properties-sql-server.md)<br /><br /> [可用性群組接聽程式屬性](view-availability-group-listener-properties-sql-server.md)|  
|系統監視器|**SQLServer:Availability Replica** 效能物件含有效能計數器，可報告可用性複本的相關資訊。|[SQL Server、可用性複本](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)|  
|系統監視器|**SQLServer:Database Replica** 效能物件含有效能計數器，可報告給定次要複本上次要資料庫的相關資訊。<br /><br /> SQL Server 中的 **SQLServer:Databases** 物件含有效能計數器，可監視交易記錄活動以及其他項目。 下列計數器與監視可用性資料庫上的交易記錄活動特別相關： **Log Flush Write Time (ms)** 、 **Log Flushes/sec**、 **Log Pool Cache Misses/sec**、 **Log Pool Disk Reads/sec**以及 **Log Pool Requests/sec**。|[SQL Server 的 Database Replica](../../../relational-databases/performance-monitor/sql-server-database-replica.md)<br /><br /> [SQL Server, Databases Object](../../../relational-databases/performance-monitor/sql-server-databases-object.md)|  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 相關內容  
  
-   **影片-Alwayson 簡介：**  [Microsoft SQL Server 代碼名稱 "Denali" AlwaysOn 系列，第1部：新一代高可用性解決方案簡介](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
-   **影片-深入探討 alwayson：**  [Microsoft SQL Server 的程式碼名稱 "Denali" AlwaysOn 系列，第2部：使用 Alwayson 建立要徑任務的高可用性解決方案](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **白皮書：**  [Microsoft SQL Server AlwaysOn 高可用性和災害復原方案指南](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   **部落格：**  [SQL Server AlwaysOn 團隊部落格：官方 SQL Server AlwaysOn 團隊部落格](https://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;](always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [設定 AlwaysOn 可用性群組 &#40;SQL Server 的伺服器實例&#41;](configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md)   
 [建立及設定可用性群組 &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [監視可用性群組 &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;的 Transact-sql 語句總覽](transact-sql-statements-for-always-on-availability-groups.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;的 PowerShell Cmdlet 總覽](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
