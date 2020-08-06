---
title: 判斷哪些查詢持有鎖定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], extended events
- queries [SQL Server], holding locks
- xe
- extended events [SQL Server], locks
- extended events [SQL Server], holding locks
ms.assetid: bdfce092-3cf1-4b5e-99d5-fd8c6f9ad560
author: rothja
ms.author: jroth
ms.openlocfilehash: 1ecbee10f53ca2a45513bc3386940d96b7e82dce
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598400"
---
# <a name="determine-which-queries-are-holding-locks"></a><span data-ttu-id="3ec8e-102">判斷哪些查詢持有鎖定</span><span class="sxs-lookup"><span data-stu-id="3ec8e-102">Determine Which Queries Are Holding Locks</span></span>
  <span data-ttu-id="3ec8e-103">資料庫管理員經常需要識別阻礙資料庫效能的鎖定來源。</span><span class="sxs-lookup"><span data-stu-id="3ec8e-103">Database administrators often need to identify the source of locks that are hindering database performance.</span></span>  
  
 <span data-ttu-id="3ec8e-104">例如，您懷疑伺服器上的效能問題可能是由鎖定造成。</span><span class="sxs-lookup"><span data-stu-id="3ec8e-104">For example, you suspect that a performance issue on your server could be caused by blocking.</span></span> <span data-ttu-id="3ec8e-105">當您查詢 sys.dm_exec_requests 時，您發現有數個工作階段處於已暫停模式，而且其等候類型指示鎖定是正在等候的資源。</span><span class="sxs-lookup"><span data-stu-id="3ec8e-105">When you query the sys.dm_exec_requests, you find several sessions in a suspended mode with a wait type indicating that a lock is the resource being waited on.</span></span>  
  
 <span data-ttu-id="3ec8e-106">您查詢 sys.dm_tran_locks，而結果顯示有許多鎖定尚未處理，但是被授與鎖定的工作階段並沒有任何使用中的要求顯示在 sys.dm_exec_requests 中。</span><span class="sxs-lookup"><span data-stu-id="3ec8e-106">You query sys.dm_tran_locks and the results show that there are many locks outstanding, but the sessions that were granted the locks do not have any active requests showing in sys.dm_exec_requests.</span></span>  
  
 <span data-ttu-id="3ec8e-107">這個範例會示範一個方法來決定哪一個查詢取得鎖定、查詢的計劃，以及取得鎖定時的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 堆疊。</span><span class="sxs-lookup"><span data-stu-id="3ec8e-107">This example demonstrates a method of determining what query took the lock, the plan of the query, and the [!INCLUDE[tsql](../../includes/tsql-md.md)] stack at the time the lock was taken.</span></span> <span data-ttu-id="3ec8e-108">這個範例也會示範如何將配對目標用於擴充的事件工作階段中。</span><span class="sxs-lookup"><span data-stu-id="3ec8e-108">This example also illustrates how the pairing target is used in an Extended Events session.</span></span>  
  
 <span data-ttu-id="3ec8e-109">完成這項工作需要在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中使用查詢編輯器來進行以下程序。</span><span class="sxs-lookup"><span data-stu-id="3ec8e-109">Accomplishing this task involves using Query Editor in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] to carry out the following procedure.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="3ec8e-110">這個範例會使用 AdventureWorks 資料庫。</span><span class="sxs-lookup"><span data-stu-id="3ec8e-110">This example uses the AdventureWorks database.</span></span>  
  
### <a name="to-determine-which-queries-are-holding-locks"></a><span data-ttu-id="3ec8e-111">判斷哪些查詢持有鎖定</span><span class="sxs-lookup"><span data-stu-id="3ec8e-111">To determine which queries are holding locks</span></span>  
  
1.  <span data-ttu-id="3ec8e-112">在查詢編輯器中，發出下列陳述式。</span><span class="sxs-lookup"><span data-stu-id="3ec8e-112">In Query Editor, issue the following statements.</span></span>  
  
    ```  
    -- Perform cleanup.   
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='FindBlockers')  
        DROP EVENT SESSION FindBlockers ON SERVER  
    GO  
    -- Use dynamic SQL to create the event session and allow creating a -- predicate on the AdventureWorks database id.  
    --  
    DECLARE @dbid int  
  
    SELECT @dbid = db_id('AdventureWorks')  
  
    IF @dbid IS NULL  
    BEGIN  
        RAISERROR('AdventureWorks is not installed. Install AdventureWorks before proceeding', 17, 1)  
        RETURN  
    END  
  
    DECLARE @sql nvarchar(1024)  
    SET @sql = '  
    CREATE EVENT SESSION FindBlockers ON SERVER  
    ADD EVENT sqlserver.lock_acquired   
        (action   
            ( sqlserver.sql_text, sqlserver.database_id, sqlserver.tsql_stack,  
             sqlserver.plan_handle, sqlserver.session_id)  
        WHERE ( database_id=' + cast(@dbid as nvarchar) + ' AND resource_0!=0)   
        ),  
    ADD EVENT sqlserver.lock_released   
        (WHERE ( database_id=' + cast(@dbid as nvarchar) + ' AND resource_0!=0 ))  
    ADD TARGET package0.pair_matching   
        ( SET begin_event=''sqlserver.lock_acquired'',   
                begin_matching_columns=''database_id, resource_0, resource_1, resource_2, transaction_id, mode'',   
                end_event=''sqlserver.lock_released'',   
                end_matching_columns=''database_id, resource_0, resource_1, resource_2, transaction_id, mode'',  
        respond_to_memory_pressure=1)  
    WITH (max_dispatch_latency = 1 seconds)'  
  
    EXEC (@sql)  
    --   
    -- Create the metadata for the event session  
    -- Start the event session  
    --  
    ALTER EVENT SESSION FindBlockers ON SERVER  
    STATE = START  
  
    ```  
  
2.  <span data-ttu-id="3ec8e-113">在伺服器上執行工作負載之後，請在查詢編輯器中發出下列陳述式，以尋找仍然持有鎖定的查詢。</span><span class="sxs-lookup"><span data-stu-id="3ec8e-113">After execution of a workload on the server, issue the following statements in Query Editor to find queries still holding locks.</span></span>  
  
    ```  
    --  
    -- The pair matching targets report current unpaired events using   
    -- the sys.dm_xe_session_targets dynamic management view (DMV)  
    -- in XML format.  
    -- The following query retrieves the data from the DMV and stores  
    -- key data in a temporary table to speed subsequent access and  
    -- retrieval.  
    --  
    SELECT   
    objlocks.value('(action[@name="session_id"]/value)[1]', 'int')  
            AS session_id,  
        objlocks.value('(data[@name="database_id"]/value)[1]', 'int')   
            AS database_id,  
        objlocks.value('(data[@name="resource_type"]/text)[1]', 'nvarchar(50)' )   
            AS resource_type,  
        objlocks.value('(data[@name="resource_0"]/value)[1]', 'bigint')   
            AS resource_0,  
        objlocks.value('(data[@name="resource_1"]/value)[1]', 'bigint')   
            AS resource_1,  
        objlocks.value('(data[@name="resource_2"]/value)[1]', 'bigint')   
            AS resource_2,  
        objlocks.value('(data[@name="mode"]/text)[1]', 'nvarchar(50)')   
            AS mode,  
        objlocks.value('(action[@name="sql_text"]/value)[1]', 'varchar(MAX)')   
            AS sql_text,  
        CAST(objlocks.value('(action[@name="plan_handle"]/value)[1]', 'varchar(MAX)') AS xml)   
            AS plan_handle,      
        CAST(objlocks.value('(action[@name="tsql_stack"]/value)[1]', 'varchar(MAX)') AS xml)   
            AS tsql_stack  
    INTO #unmatched_locks  
    FROM (  
        SELECT CAST(xest.target_data as xml)   
            lockinfo  
        FROM sys.dm_xe_session_targets xest  
        JOIN sys.dm_xe_sessions xes ON xes.address = xest.event_session_address  
        WHERE xest.target_name = 'pair_matching' AND xes.name = 'FindBlockers'  
    ) heldlocks  
    CROSS APPLY lockinfo.nodes('//event[@name="lock_acquired"]') AS T(objlocks)  
  
    --  
    -- Join the data acquired from the pairing target with other   
    -- DMVs to return provide additional information about blockers  
    --  
    SELECT ul.*  
        FROM #unmatched_locks ul  
        INNER JOIN sys.dm_tran_locks tl ON ul.database_id = tl.resource_database_id AND ul.resource_type = tl.resource_type  
        WHERE resource_0 IS NOT NULL  
        AND session_id IN   
            (SELECT blocking_session_id FROM sys.dm_exec_requests WHERE blocking_session_id != 0)  
        AND tl.request_status='wait'  
        AND REPLACE(ul.mode, 'LCK_M_', '' ) = tl.request_mode  
  
    ```  
  
3.  <span data-ttu-id="3ec8e-114">在識別問題之後，請卸除任何暫存資料表和事件工作階段。</span><span class="sxs-lookup"><span data-stu-id="3ec8e-114">After identifying the issues, drop any temporary tables and the event session.</span></span>  
  
    ```  
    DROP TABLE #unmatched_locks  
    DROP EVENT SESSION FindBlockers ON SERVER  
    ```  
  
## <a name="see-also"></a><span data-ttu-id="3ec8e-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3ec8e-115">See Also</span></span>  
 <span data-ttu-id="3ec8e-116">[CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="3ec8e-116">[CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql) </span></span>  
 <span data-ttu-id="3ec8e-117">[ALTER EVENT SESSION &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-event-session-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="3ec8e-117">[ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql) </span></span>  
 <span data-ttu-id="3ec8e-118">[DROP EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-event-session-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="3ec8e-118">[DROP EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-event-session-transact-sql) </span></span>  
 <span data-ttu-id="3ec8e-119">[sys.dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="3ec8e-119">[sys.dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql) </span></span>  
 [<span data-ttu-id="3ec8e-120">sys.dm_xe_sessions &#40;Transact-SQL&#41;</span><span class="sxs-lookup"><span data-stu-id="3ec8e-120">sys.dm_xe_sessions &#40;Transact-SQL&#41;</span></span>](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql)  
  
  
