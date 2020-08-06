---
title: 最佳化 SQL 追蹤 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- time [SQL Server], traces
- SQL Trace, performance
- traces [SQL Server], performance
- performance [SQL Server], trace
ms.assetid: 50944218-925f-4576-aec8-4379846d7681
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 831875218423bdb9106d7d84995af1e788da44db
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585784"
---
# <a name="optimize-sql-trace"></a><span data-ttu-id="8f4d4-102">最佳化 SQL 追蹤</span><span class="sxs-lookup"><span data-stu-id="8f4d4-102">Optimize SQL Trace</span></span>
  <span data-ttu-id="8f4d4-103">因為執行 SQL 追蹤會使用系統資源來收集資料，所以會產生效能成本，但是有許多方式可以使成本降至最少。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-103">Although running SQL Trace incurs a performance cost because it uses system resources to gather data, you can do many things to minimize it.</span></span> <span data-ttu-id="8f4d4-104">若要使追蹤導致的效能成本降至最少，請試試下列方法：</span><span class="sxs-lookup"><span data-stu-id="8f4d4-104">To minimize the performance cost incurred by a trace, try the following:</span></span>  
  
-   <span data-ttu-id="8f4d4-105">考慮使用命令提示字元來執行追蹤。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-105">Consider using the command prompt to run traces.</span></span> <span data-ttu-id="8f4d4-106">使用圖形化使用者介面會妨礙效能。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-106">Using a graphical user interface hinders performance.</span></span> <span data-ttu-id="8f4d4-107">如需詳細資訊，請參閱 [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-107">For more information, see [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql).</span></span>  
  
-   <span data-ttu-id="8f4d4-108">避免納入經常發生的事件。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-108">Avoid including events that occur frequently.</span></span> <span data-ttu-id="8f4d4-109">如果可能，利用特定事件類別和篩選來縮小追蹤。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-109">If possible, narrow your trace by means of specific event classes and filters.</span></span> <span data-ttu-id="8f4d4-110">若收集的追蹤事件越少，支援追蹤所需的系統資源也會跟著減少。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-110">If fewer trace events are gathered, fewer system resources are required to support tracing.</span></span>  
  
-   <span data-ttu-id="8f4d4-111">將追蹤集中在只收集可提供相關資料的事件，</span><span class="sxs-lookup"><span data-stu-id="8f4d4-111">Focus the trace to collect only events that provide relevant data.</span></span> <span data-ttu-id="8f4d4-112">例如，如果追蹤是為了要識別死結，則請納入 **Lock:Deadlock** 事件類別，而不要納入 **Lock:Acquired** 事件類別。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-112">For example, if your trace is to identify deadlocks, include the **Lock:Deadlock** event class, but not the **Lock:Acquired** event class.</span></span> <span data-ttu-id="8f4d4-113">如果您同時納入這兩個事件類別，則追蹤必須回應所取得的每一個鎖定，執行成本就會加倍。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-113">If you include both event classes, the trace has to respond to every lock that is acquired, and your execution cost is doubled.</span></span>  
  
-   <span data-ttu-id="8f4d4-114">避免收集重複的資料。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-114">Avoid collecting duplicate data.</span></span> <span data-ttu-id="8f4d4-115">例如，如果您要收集 **SQL:BatchStarted** 和 **SQL:BatchCompleted**，您可以只收集 **SQL:BatchStarted** 事件類別的文字資料，使結果集的大小縮至最小。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-115">For example, if you collect **SQL:BatchStarted** and the **SQL:BatchCompleted**, you can minimize the size of the results set by collecting text data for the **SQL:BatchStarted** event class only.</span></span>  
  
-   <span data-ttu-id="8f4d4-116">在追蹤定義中使用篩選。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-116">Use filters in the trace definition.</span></span> <span data-ttu-id="8f4d4-117">例如，如果您知道某個使用者回報在隨選查詢期間的效能緩慢，則可建立 **LoginName**的篩選，</span><span class="sxs-lookup"><span data-stu-id="8f4d4-117">For example, if you know that a certain user is reporting slow performance during ad hoc queries, create a filter on **LoginName**.</span></span> <span data-ttu-id="8f4d4-118">將篩選設為只納入 **LoginName** 符合使用者名稱的事件。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-118">Set the filter to include only events where the **LoginName** matches that user name.</span></span>  
  
 <span data-ttu-id="8f4d4-119">如果您需要執行的事件追蹤會對效能造成重大影響，請考慮使用下列其中一個方法，來限制此追蹤對伺服器效能的影響：</span><span class="sxs-lookup"><span data-stu-id="8f4d4-119">If you need to run a trace for events that create a significant impact on performance, consider limiting the performance impact on the server by using one of the following methods:</span></span>  
  
-   <span data-ttu-id="8f4d4-120">使執行追蹤的時間變短。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-120">Run traces for shorter periods of time.</span></span> <span data-ttu-id="8f4d4-121">您可以啟用停止時間，來控制追蹤執行的時間長度。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-121">You can control the length of time that a trace runs by enabling a stop time.</span></span> <span data-ttu-id="8f4d4-122">尤其當您無法限制事件類別或篩選事件時，這麼做特別重要。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-122">This is especially important if you cannot limit the event classes or filter an event.</span></span> <span data-ttu-id="8f4d4-123">啟用停止時間可以確定所造成的效能問題，不會無限期地持續下去。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-123">Enabling a stop time ensures that the performance incurred does not last indefinitely.</span></span>  
  
-   <span data-ttu-id="8f4d4-124">限制追蹤結果的大小。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-124">Limit the size of the trace results.</span></span> <span data-ttu-id="8f4d4-125">您可以將追蹤結果的大小限制為檔案大小上限。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-125">You can limit the size of the trace results to a maximum file size.</span></span> <span data-ttu-id="8f4d4-126">此策略可確保在達到檔案大小上限時，效能成本會立即停止 (如果未啟用檔案換用的話)。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-126">This strategy ensures that the performance cost stops when the file-size limit is reached (if file rollover is not enabled).</span></span>  
  
-   <span data-ttu-id="8f4d4-127">限制傳回的事件數目。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-127">Limit the number of events returned.</span></span> <span data-ttu-id="8f4d4-128">利用 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] ，您可以將追蹤儲存至資料表並設定最大資料列數，來限制傳回的事件數目。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-128">With [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] you can limit the number of events returned by saving the trace to a table and setting the maximum number of rows.</span></span> <span data-ttu-id="8f4d4-129">在達到最大資料列數之後，追蹤結果仍會傳回至 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 畫面，但可省去將結果記錄到資料表的成本。</span><span class="sxs-lookup"><span data-stu-id="8f4d4-129">Trace results are still returned to the [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] screen after the maximum number of rows has been reached, but the cost of recording the results to a table is eliminated.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8f4d4-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8f4d4-130">See Also</span></span>  
 [<span data-ttu-id="8f4d4-131">篩選追蹤</span><span class="sxs-lookup"><span data-stu-id="8f4d4-131">Filter a Trace</span></span>](../sql-trace/filter-a-trace.md)  
  
  
