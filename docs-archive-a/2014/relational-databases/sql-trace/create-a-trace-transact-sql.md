---
title: 建立追蹤 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], example
- traces [SQL Server], creating
ms.assetid: 79dd4254-e3c6-467a-bb6f-f99e51757e99
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 35644891b2dca8359d6dc68fbddb67288d241cb4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597051"
---
# <a name="create-a-trace-transact-sql"></a><span data-ttu-id="509eb-102">建立追蹤 (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="509eb-102">Create a Trace (Transact-SQL)</span></span>
  <span data-ttu-id="509eb-103">此主題描述如何使用預存程序來建立追蹤。</span><span class="sxs-lookup"><span data-stu-id="509eb-103">This topic describes how to use stored procedures to create a trace.</span></span>  
  
### <a name="to-create-a-trace"></a><span data-ttu-id="509eb-104">若要建立追蹤</span><span class="sxs-lookup"><span data-stu-id="509eb-104">To create a trace</span></span>  
  
1.  <span data-ttu-id="509eb-105">執行 **sp_trace_create** 並加上必要的參數，以建立新的追蹤。</span><span class="sxs-lookup"><span data-stu-id="509eb-105">Execute **sp_trace_create** with the required parameters to create a new trace.</span></span> <span data-ttu-id="509eb-106">新的追蹤會處於停止狀態 (*status* 為 **0**)。</span><span class="sxs-lookup"><span data-stu-id="509eb-106">The new trace will be in a stopped state (*status* is **0**).</span></span>  
  
2.  <span data-ttu-id="509eb-107">執行 **sp_trace_setevent** 並加上必要的參數，以選取要追蹤的事件和資料行。</span><span class="sxs-lookup"><span data-stu-id="509eb-107">Execute **sp_trace_setevent** with the required parameters to select the events and columns to trace.</span></span>  
  
3.  <span data-ttu-id="509eb-108">(選擇性) 執行 **sp_trace_setfilter** 以設定任何篩選或篩選組合。</span><span class="sxs-lookup"><span data-stu-id="509eb-108">Optionally, execute **sp_trace_setfilter** to set any or a combination of filters.</span></span>  
  
     <span data-ttu-id="509eb-109">**sp_trace_setevent** 和 **sp_trace_setfilter** 只能在已停止的現有追蹤上執行。</span><span class="sxs-lookup"><span data-stu-id="509eb-109">**sp_trace_setevent** and **sp_trace_setfilter** can be executed only on existing traces that are stopped.</span></span>  
  
    > [!IMPORTANT]  
    >  <span data-ttu-id="509eb-110">與一般的預存程序不同，所有 SQL Server Profiler 預存程序 (<strong>sp_trace_*xx*</strong>) 的參數均嚴格區分類型，且不支援自動資料類型轉換。</span><span class="sxs-lookup"><span data-stu-id="509eb-110">Unlike regular stored procedures, parameters of all SQL Server Profiler stored procedures (<strong>sp_trace_*xx*</strong>) are strictly typed and do not support automatic data type conversion.</span></span> <span data-ttu-id="509eb-111">如果沒有依照引數描述所指定，以正確的輸入參數資料類型來呼叫這些參數，預存程序會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="509eb-111">If these parameters are not called with the correct input parameter data types, as specified in the argument description, the stored procedure returns an error.</span></span>  
  
## <a name="example"></a><span data-ttu-id="509eb-112">範例</span><span class="sxs-lookup"><span data-stu-id="509eb-112">Example</span></span>  
 <span data-ttu-id="509eb-113">下列程式碼將示範如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]來建立追蹤。</span><span class="sxs-lookup"><span data-stu-id="509eb-113">The following code demonstrates creating a trace using [!INCLUDE[tsql](../../includes/tsql-md.md)].</span></span> <span data-ttu-id="509eb-114">這個程式碼含有三個區段：建立追蹤、擴展追蹤檔案以及停止追蹤。</span><span class="sxs-lookup"><span data-stu-id="509eb-114">It is in three sections: creating the trace, populating the trace file, and stopping the trace.</span></span> <span data-ttu-id="509eb-115">您可以透過加入想要追蹤的事件，自訂追蹤。</span><span class="sxs-lookup"><span data-stu-id="509eb-115">Customize the trace by adding the events that you want to trace.</span></span> <span data-ttu-id="509eb-116">如需事件和資料行的清單，請參閱 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)來建立追蹤。</span><span class="sxs-lookup"><span data-stu-id="509eb-116">For the list of events and columns, see [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql).</span></span>  
  
 <span data-ttu-id="509eb-117">下列程式碼會建立追蹤、將事件加入至追蹤，然後啟動追蹤：</span><span class="sxs-lookup"><span data-stu-id="509eb-117">The following code creates a trace, adds events to the trace, and then starts the trace:</span></span>  
  
```  
DECLARE @RC int, @TraceID int, @on BIT  
EXEC @rc = sp_trace_create @TraceID output, 0, N'C:\SampleTrace'  
  
-- Select the return code to see if the trace creation was successful.  
SELECT RC = @RC, TraceID = @TraceID  
  
-- Set the events and data columns you need to capture.  
SELECT @on = 1  
  
-- 10 is RPC:Completed event. 1 is TextData column.   
EXEC sp_trace_setevent @TraceID, 10, 1, @on   
-- 13 is SQL:BatchStarting, 11 is LoginName  
EXEC sp_trace_setevent @TraceID, 13, 11, @on   
-- 13 is SQL:BatchStarting, 14 is StartTime  
EXEC sp_trace_setevent @TraceID, 13, 14, @on   
-- 12 is SQL:BatchCompleted, 15 is EndTime  
EXEC sp_trace_setevent @TraceID, 12, 15, @on   
-- 13 is SQL:BatchStarting, 1 is TextData  
EXEC sp_trace_setevent @TraceID, 13, 1, @on   
  
-- Set any filter. Not provided in this example  
--EXEC sp_trace_setfilter 1, 10, 0, 6, N'%Profiler%'  
  
-- Start Trace (status 1 = start)  
EXEC @RC = sp_trace_setstatus @TraceID, 1  
GO  
  
```  
  
## <a name="example"></a><span data-ttu-id="509eb-118">範例</span><span class="sxs-lookup"><span data-stu-id="509eb-118">Example</span></span>  
 <span data-ttu-id="509eb-119">此時您已經建立並啟動追蹤，請執行下列程式碼，使用活動來擴展追蹤。</span><span class="sxs-lookup"><span data-stu-id="509eb-119">Now that the trace has been created and started, execute the following code to populate the trace with activity.</span></span>  
  
```  
SELECT * FROM master.sys.databases  
GO  
SELECT * FROM ::fn_trace_getinfo(default)  
GO  
  
```  
  
## <a name="example"></a><span data-ttu-id="509eb-120">範例</span><span class="sxs-lookup"><span data-stu-id="509eb-120">Example</span></span>  
 <span data-ttu-id="509eb-121">您可以隨時停止並重新啟動追蹤。</span><span class="sxs-lookup"><span data-stu-id="509eb-121">The trace can be stopped and restarted at any time.</span></span> <span data-ttu-id="509eb-122">在這個範例中，請執行下列程式碼來停止追蹤、關閉追蹤，然後刪除追蹤定義。</span><span class="sxs-lookup"><span data-stu-id="509eb-122">In this example, execute the following code to stop the trace, close the trace, and delete the trace definition.</span></span>  
  
```  
DECLARE @TraceID int  
-- Populate a variable with the trace_id of the current trace  
SELECT  @TraceID = TraceID FROM ::fn_trace_getinfo(default) WHERE VALUE = N'C:\SampleTrace.trc'  
  
-- First stop the trace.   
EXEC sp_trace_setstatus @TraceID, 0  
  
-- Close and then delete its definition from SQL Server.   
EXEC sp_trace_setstatus @TraceID, 2  
  
```  
  
## <a name="example"></a><span data-ttu-id="509eb-123">範例</span><span class="sxs-lookup"><span data-stu-id="509eb-123">Example</span></span>  
 <span data-ttu-id="509eb-124">若要檢查追蹤檔案，請使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]來開啟 SampleTrace.trc 檔案。</span><span class="sxs-lookup"><span data-stu-id="509eb-124">To examine the trace file, open the SampleTrace.trc file using [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="509eb-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="509eb-125">See Also</span></span>  
 <span data-ttu-id="509eb-126">[SQL Server Profiler 預存程序 &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="509eb-126">[SQL Server Profiler Stored Procedures &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql) </span></span>  
 <span data-ttu-id="509eb-127">[sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="509eb-127">[sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql) </span></span>  
 <span data-ttu-id="509eb-128">[sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="509eb-128">[sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql) </span></span>  
 [<span data-ttu-id="509eb-129">sp_trace_setfilter &#40;Transact-SQL&#41;</span><span class="sxs-lookup"><span data-stu-id="509eb-129">sp_trace_setfilter &#40;Transact-SQL&#41;</span></span>](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)  
  
  
