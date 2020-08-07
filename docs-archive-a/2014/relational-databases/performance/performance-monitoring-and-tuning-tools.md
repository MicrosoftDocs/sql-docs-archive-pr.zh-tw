---
title: 效能監視及微調工具 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- tools [SQL Server], monitoring performance
- monitoring server performance [SQL Server], tools
- monitoring performance [SQL Server], tools
- database performance [SQL Server], tools
- tuning databases [SQL Server], tools
- database monitoring [SQL Server], tools
- performance [SQL Server], monitoring tools
- server performance [SQL Server], tools
ms.assetid: 31529dfe-68e7-49f7-b3c2-39fcecf33a95
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c9a1f262493b54c06e2bb9eb3d4d6d44bf60d52f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597789"
---
# <a name="performance-monitoring-and-tuning-tools"></a>效能監視及微調工具
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供一組完整的工具，可用來監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的事件，以及用來微調實體資料庫設計。 要選擇的工具依據要做的監視或微調類型，以及要監視的特殊事件而定。  
  
 下列為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 監視和微調工具：  
  
|工具|說明|  
|----------|-----------------|  
|[sp_trace_setfilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)|[!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 會追蹤引擎處理序事件 (例如批次或交易的開始)，讓您可以監視伺服器和資料庫活動 (例如死結、嚴重錯誤或登入活動)。 您可以將 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 的資料擷取到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表或檔案中以供稍後分析，您也可以逐步重新執行於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 擷取的事件，以查看實際的發生情形。|  
|[SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 可以使用多部電腦重新執行追蹤資料，並模擬關鍵任務的工作負載。|  
|[監視資源使用狀況 &#40;System Monitor&#41;](../performance-monitor/monitor-resource-usage-system-monitor.md)|「系統監視器」主要會追蹤資源使用量 (例如使用中的緩衝區管理員分頁要求的數目)，讓您可以使用預先定義的物件和計數器監視伺服器效能和活動，或使用者定義的計數器來監視事件。 「系統監視器」(Microsoft Windows NT 4.0 中的「效能監視器」) 收集關於事件的計數和比率而非資料 (例如：記憶體使用量、使用中交易的數目、被封鎖的鎖定數目或是 CPU 活動)。 您可以設定特定計數器的臨界值來產生提醒操作員的警示。<br /><br /> 「系統監視器」可在 Microsoft Windows Server 與 Windows 作業系統上運作。 它可以監視 (從遠端或本機) Windows NT 4.0 或更新版本上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。<br /><br /> [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 與「系統監視器」之間最主要的差異在於 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 監視 Database Engine 事件，而「系統監視器」則監視與伺服器處理序關聯的資源使用情形。|  
|[開啟活動監視器 &#40;SQL Server Management Studio&#41;](../performance-monitor/open-activity-monitor-sql-server-management-studio.md)|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的「活動監視器」對於目前活動的特定檢視非常有用，並會以圖形方式顯示以下相關資訊：<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上執行的處理序。<br /><br /> 已封鎖的處理序。<br /><br /> 鎖定。<br /><br /> 使用者活動。|  
|[SQL 追蹤](../sql-trace/sql-trace.md)|[!INCLUDE[tsql](../../../includes/tsql-md.md)] 建立、篩選和定義追蹤的預存程序：<br /><br /> [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)<br /><br /> [sp_trace_generateevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql)<br /><br /> [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)<br /><br /> [sp_trace_setfilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)<br /><br /> [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)|  
|錯誤記錄|Windows 應用程式事件記錄檔針對發生於 Windows Server 和 Windows 作業系統上的事件，以及在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 與全文檢索搜尋中的事件，提供一個概括性的資訊。 記錄檔包含有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中事件的相關資訊，這些資訊無法從別處取得。 您可以使用錯誤記錄檔中的資訊來進行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]相關問題的疑難排解。|  
|[系統預存程序 &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)|下列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統預存程序針對許多監視工作提供了強大的替代方式：<br /><br /> [sp_who &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql)： <br />                    報告目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者與處理序的相關快照資訊，此資訊包括目前正在執行的陳述式以及陳述式是否遭封鎖。<br /><br /> [sp_lock &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-lock-transact-sql)：報告有關鎖定的快照集資訊，包括物件識別碼、索引識別碼、鎖定類型，以及要套用鎖定的類型或資源。<br /><br /> [sp_spaceused &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql)：顯示資料表 (或整個資料庫) 所使用的目前磁碟空間量估計。<br /><br /> [sp_monitor &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-monitor-transact-sql)：顯示統計資料，包括 CPU 使用量、i/o 使用量，以及自上次執行**sp_monitor**以來的閒置時間量。|  
|[DBCC &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-transact-sql)|DBCC (資料庫主控台命令) 陳述式讓您可以檢查效能統計資料和資料庫的邏輯與實體一致性。|  
|[內建函數 &#40;Transact-SQL&#41;](/sql/t-sql/functions/functions)|內建的函數會顯示自伺服器啟動後，關於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 活動的快照統計資料，這些統計資料會儲存在預先定義的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 計數器中。 例如， **@ @CPU_BUSY **包含 CPU 已執行程式碼的時間量 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ;**@@CONNECTIONS**包含連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或嘗試連接的數目，而 **@ @PACKET_ERRORS **包含連線上發生的網路封包數目 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|[追蹤旗標 &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)|追蹤旗標顯示伺服器內部特定活動的相關資訊，並可用來診斷問題或效能問題 (例如死結鏈結)。|  
|[Database Engine Tuning Advisor](database-engine-tuning-advisor.md)|Database Engine Tuning Advisor 會針對您要微調的資料庫，分析執行 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式效能影響。 Database Engine Tuning Advisor 會針對新增、移除，或修改索引、索引檢視和分割提供建議。|  
  
## <a name="choosing-a-monitoring-tool"></a>選擇監視工具  
 監視工具的選擇依據要監視的事件與活動而定。  
  
|事件或活動|SQL Server Profiler|Distributed Replay|系統監視器|活動監視器|Transact-SQL|錯誤記錄|  
|-----------------------|-------------------------|------------------------|--------------------|----------------------|-------------------|----------------|  
|趨勢分析|是||是||||  
|重新執行擷取的事件|是 (從單一電腦)|是 (從多部電腦)|||||  
|特定的監視|是|||是|是|是|  
|產生警示|||是||||  
|圖形化介面|是||是|是||是|  
|在自訂應用程式中使用|是 <sup>1</sup>||||是||  
  
 <sup>1</sup>使用 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 系統預存程式。  
  
## <a name="windows-monitoring-tools"></a>Windows 監視工具  
 Windows 作業系統與 Windows Server 2003 也提供下列監控工具。  
  
|工具|描述|  
|----------|-----------------|  
|工作管理員|顯示執行於系統上的處理序與應用程式概要。|  
|網路監視器代理程式|監視網路流量。|  
  
 如需有關 Windows 作業系統或 Windows Server 工具的詳細資訊，請參閱 Windows 說明文件。  
  
  
