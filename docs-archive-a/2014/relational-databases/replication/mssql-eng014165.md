---
title: MSSQL_ENG014165 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014165 error
ms.assetid: 7bb07672-310c-4f51-ae76-c55e7c8d51ea
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8ac0d9c0bad79b13676296e4a041f0141d134c75
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87702814"
---
# <a name="mssql_eng014165"></a><span data-ttu-id="366ee-102">MSSQL_ENG014165</span><span class="sxs-lookup"><span data-stu-id="366ee-102">MSSQL_ENG014165</span></span>
    
## <a name="message-details"></a><span data-ttu-id="366ee-103">訊息詳細資料</span><span class="sxs-lookup"><span data-stu-id="366ee-103">Message Details</span></span>  
  
|||  
|-|-|  
|<span data-ttu-id="366ee-104">產品名稱</span><span class="sxs-lookup"><span data-stu-id="366ee-104">Product Name</span></span>|<span data-ttu-id="366ee-105">SQL Server</span><span class="sxs-lookup"><span data-stu-id="366ee-105">SQL Server</span></span>|  
|<span data-ttu-id="366ee-106">事件識別碼</span><span class="sxs-lookup"><span data-stu-id="366ee-106">Event ID</span></span>|<span data-ttu-id="366ee-107">14165</span><span class="sxs-lookup"><span data-stu-id="366ee-107">14165</span></span>|  
|<span data-ttu-id="366ee-108">事件來源</span><span class="sxs-lookup"><span data-stu-id="366ee-108">Event Source</span></span>|<span data-ttu-id="366ee-109">MSSQLSERVER</span><span class="sxs-lookup"><span data-stu-id="366ee-109">MSSQLSERVER</span></span>|  
|<span data-ttu-id="366ee-110">元件</span><span class="sxs-lookup"><span data-stu-id="366ee-110">Component</span></span>|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|<span data-ttu-id="366ee-111">符號名稱</span><span class="sxs-lookup"><span data-stu-id="366ee-111">Symbolic Name</span></span>||  
|<span data-ttu-id="366ee-112">訊息文字</span><span class="sxs-lookup"><span data-stu-id="366ee-112">Message Text</span></span>|<span data-ttu-id="366ee-113">已設定針對發行集[%s]的臨界值[%s:%s]</span><span class="sxs-lookup"><span data-stu-id="366ee-113">The threshold [%s:%s] for the publication [%s] has been set.</span></span> <span data-ttu-id="366ee-114">請確定合併代理程式正在執行，而且符合預期需求。</span><span class="sxs-lookup"><span data-stu-id="366ee-114">Please make sure that the merge agent is running and can match the expected requirement.</span></span>|  
  
## <a name="explanation"></a><span data-ttu-id="366ee-115">說明</span><span class="sxs-lookup"><span data-stu-id="366ee-115">Explanation</span></span>  
 <span data-ttu-id="366ee-116">複寫可讓您啟用多個條件的警告。</span><span class="sxs-lookup"><span data-stu-id="366ee-116">Replication lets you enable warnings for several conditions.</span></span> <span data-ttu-id="366ee-117">這包括在同步處理合併發行者與訂閱者之間的變更時，無法處理足夠數量的資料列的情況。</span><span class="sxs-lookup"><span data-stu-id="366ee-117">This includes failure to process a sufficient number of rows when synchronizing changes between a merge Publisher and Subscriber.</span></span> <span data-ttu-id="366ee-118">您可以為 LAN 連接和撥號連接指定不同的時間。</span><span class="sxs-lookup"><span data-stu-id="366ee-118">Different times can be specified for LAN connections and dial-up connections.</span></span>  
  
 <span data-ttu-id="366ee-119">使用複寫監視器或 [sp_replmonitorchangepublicationthreshold](/sql/relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql)啟用警告時，您會指定決定何時觸發警告的臨界值。</span><span class="sxs-lookup"><span data-stu-id="366ee-119">When you enable a warning by using Replication Monitor or [sp_replmonitorchangepublicationthreshold](/sql/relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql), you specify a threshold that determines when a warning is triggered.</span></span> <span data-ttu-id="366ee-120">當達到或超過臨界值時，複寫監視器中會顯示警告，而且會有事件寫入 Windows 事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="366ee-120">When that threshold is met or exceeded, a warning is displayed in Replication Monitor, and an event is written to the Windows event log.</span></span> <span data-ttu-id="366ee-121">達到臨界值也會觸發 SQL Server Agent 警示。</span><span class="sxs-lookup"><span data-stu-id="366ee-121">Reaching a threshold can also trigger a SQL Server Agent alert.</span></span> <span data-ttu-id="366ee-122">如需詳細資訊，請參閱[在複寫監視器中設定臨界值和警告](monitor/set-thresholds-and-warnings-in-replication-monitor.md)和[以程式設計方式監視複寫](monitoring-replication.md)。</span><span class="sxs-lookup"><span data-stu-id="366ee-122">For more information, see [Set Thresholds and Warnings in Replication Monitor](monitor/set-thresholds-and-warnings-in-replication-monitor.md) and [Programmatically Monitor Replication](monitoring-replication.md).</span></span>  
  
## <a name="user-action"></a><span data-ttu-id="366ee-123">使用者動作</span><span class="sxs-lookup"><span data-stu-id="366ee-123">User Action</span></span>  
 <span data-ttu-id="366ee-124">如果訂閱不符合資料列處理臨界值，則必須判斷是否發生系統效能問題，或者應該調整臨界值。</span><span class="sxs-lookup"><span data-stu-id="366ee-124">If a subscription is not meeting a row processing threshold, you must determine whether there is a performance issue with the system or whether the threshold should be adjusted.</span></span> <span data-ttu-id="366ee-125">在設定複寫後，請開發效能基準線，以便決定複寫對應用程式及拓撲一般工作負載的操作方式。</span><span class="sxs-lookup"><span data-stu-id="366ee-125">After you configure replication, develop a performance baseline that will let you determine how replication behaves with a workload that is typical for your applications and topology.</span></span> <span data-ttu-id="366ee-126">請將已處理的資料列數包含在此基準線中，以便設定適當的臨界值。</span><span class="sxs-lookup"><span data-stu-id="366ee-126">Include number of rows processed in this baseline so that you can set an appropriate value for the threshold.</span></span>  
  
 <span data-ttu-id="366ee-127">如果臨界值適當，但是即將超過，您就必須判斷系統的效能瓶頸何在。</span><span class="sxs-lookup"><span data-stu-id="366ee-127">If the threshold value is appropriate, but it is being exceeded, you must determine where the performance bottleneck is in the system.</span></span> <span data-ttu-id="366ee-128">如需有關如何監視與疑難排解複寫效能的詳細資訊，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="366ee-128">For more information about how to monitor and troubleshoot replication performance, see the following topics:</span></span>  
  
-   <span data-ttu-id="366ee-129">[使用複寫監視器監視效能](monitor/monitor-performance-with-replication-monitor.md) (特別是＜檢視合併式複寫的詳細同步處理效能＞一節)</span><span class="sxs-lookup"><span data-stu-id="366ee-129">[Monitor Performance with Replication Monitor](monitor/monitor-performance-with-replication-monitor.md) (especially the section "Viewing Detailed Synchronization Performance for Merge Replication")</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="366ee-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="366ee-130">See Also</span></span>  
 [<span data-ttu-id="366ee-131">錯誤和事件參考 &#40;複寫&#41;</span><span class="sxs-lookup"><span data-stu-id="366ee-131">Errors and Events Reference &#40;Replication&#41;</span></span>](errors-and-events-reference-replication.md)  
  
  