---
title: 資料庫屬性 (查詢存放區頁面) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.querystore.f1
ms.assetid: da47d75e-291a-4305-acef-4b0aaf5215da
author: stevestein
ms.author: sstein
ms.openlocfilehash: bab0d9b697e9ad9ec4b27f320d26b9b9edb5944e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87702957"
---
# <a name="database-properties-query-store-page"></a><span data-ttu-id="3f490-102">資料庫屬性 (查詢存放區頁面)</span><span class="sxs-lookup"><span data-stu-id="3f490-102">Database Properties (Query Store Page)</span></span>
  <span data-ttu-id="3f490-103">請從主體資料庫存取此頁面，並將其用於設定及修改資料庫查詢存放區的屬性。</span><span class="sxs-lookup"><span data-stu-id="3f490-103">Access this page from the principal database, and use it to configure and to modify the properties of the database query store.</span></span> <span data-ttu-id="3f490-104">這些選項也可使用 [ALTER DATABASE SET 選項](/sql/t-sql/statements/alter-database-transact-sql-set-options)加以設定。</span><span class="sxs-lookup"><span data-stu-id="3f490-104">These options can also be configure by using the [ALTER DATABASE SET options](/sql/t-sql/statements/alter-database-transact-sql-set-options).</span></span> <span data-ttu-id="3f490-105">如需查詢存放區的相關資訊，請參閱 [Monitoring Performance By Using the Query Store](../performance/monitoring-performance-by-using-the-query-store.md)</span><span class="sxs-lookup"><span data-stu-id="3f490-105">For information about the query store, see [Monitoring Performance By Using the Query Store](../performance/monitoring-performance-by-using-the-query-store.md).</span></span>  
  
||  
|-|  
|<span data-ttu-id="3f490-106">**適用於**： [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。</span><span class="sxs-lookup"><span data-stu-id="3f490-106">**Applies to**: [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].</span></span>|  
  
## <a name="options"></a><span data-ttu-id="3f490-107">選項</span><span class="sxs-lookup"><span data-stu-id="3f490-107">Options</span></span>  
 <span data-ttu-id="3f490-108">啟用</span><span class="sxs-lookup"><span data-stu-id="3f490-108">Enable</span></span>  
 <span data-ttu-id="3f490-109">啟用及停用查詢存放區。</span><span class="sxs-lookup"><span data-stu-id="3f490-109">Enables and disables the query store.</span></span>  
  
 <span data-ttu-id="3f490-110">作業模式</span><span class="sxs-lookup"><span data-stu-id="3f490-110">Operation Mode</span></span>  
 <span data-ttu-id="3f490-111">有效值為 READ_ONLY 和 READ_WRITE。</span><span class="sxs-lookup"><span data-stu-id="3f490-111">Valid values are READ_ONLY and READ_WRITE.</span></span> <span data-ttu-id="3f490-112">在 READ_WRITE 模式中，查詢存放區會收集並保存查詢計劃和執行階段執行統計資料資訊。</span><span class="sxs-lookup"><span data-stu-id="3f490-112">In READ_WRITE mode, the query store collects and persists query plan and runtime execution statistics information.</span></span> <span data-ttu-id="3f490-113">在 READ_ONLY 模式中，可以從查詢存放區讀取資訊，但不會加入新資訊。</span><span class="sxs-lookup"><span data-stu-id="3f490-113">In READ_ONLY mode, information can be read from the query store, but new information is not added.</span></span> <span data-ttu-id="3f490-114">如果已用到了查詢存放區的配置空間上限，查詢存放區就會將其作業模式變更為 READ_ONLY。</span><span class="sxs-lookup"><span data-stu-id="3f490-114">If the maximum allocated space of the query store has been exhausted, the query store will change its operation mode to READ_ONLY.</span></span>  
  
 <span data-ttu-id="3f490-115">作業模式 (實際)</span><span class="sxs-lookup"><span data-stu-id="3f490-115">Operation Mode (Actual)</span></span>  
 <span data-ttu-id="3f490-116">取得查詢存放區的實際作業模式。</span><span class="sxs-lookup"><span data-stu-id="3f490-116">Gets the actual operation mode of the query store.</span></span>  
  
 <span data-ttu-id="3f490-117">作業模式 (要求的)</span><span class="sxs-lookup"><span data-stu-id="3f490-117">Operation Mode (Requested)</span></span>  
 <span data-ttu-id="3f490-118">取得及設定查詢存放區所需的作業模式。</span><span class="sxs-lookup"><span data-stu-id="3f490-118">Gets and sets the desired operation mode of the query store.</span></span>  
  
 <span data-ttu-id="3f490-119">資料排清間隔 (分鐘)</span><span class="sxs-lookup"><span data-stu-id="3f490-119">Data Flush Interval (Minutes)</span></span>  
 <span data-ttu-id="3f490-120">決定將寫入查詢存放區的資料保存到磁碟的頻率。</span><span class="sxs-lookup"><span data-stu-id="3f490-120">Determines the frequency at which data written to the query store is persisted to disk.</span></span> <span data-ttu-id="3f490-121">為了獲得最佳效能，查詢存放區所收集的資料會以非同步方式寫入磁碟。</span><span class="sxs-lookup"><span data-stu-id="3f490-121">To optimize for performance, data collected by the query store is asynchronously written to the disk.</span></span> <span data-ttu-id="3f490-122">已設定進行此非同步傳輸的頻率。</span><span class="sxs-lookup"><span data-stu-id="3f490-122">The frequency at which this asynchronous transfer occurs is configured.</span></span>  
  
 <span data-ttu-id="3f490-123">統計資料收集間隔</span><span class="sxs-lookup"><span data-stu-id="3f490-123">Statistics Collection Interval</span></span>  
 <span data-ttu-id="3f490-124">取得及設定統計資料收集間隔值。</span><span class="sxs-lookup"><span data-stu-id="3f490-124">Gets and sets the statistics collection interval value.</span></span>  
  
 <span data-ttu-id="3f490-125">大小上限 (MB)</span><span class="sxs-lookup"><span data-stu-id="3f490-125">Max Size (MB)</span></span>  
 <span data-ttu-id="3f490-126">取得及設定配置給查詢存放區的總空間。</span><span class="sxs-lookup"><span data-stu-id="3f490-126">Gets and sets the total space allocated to the query store.</span></span>  
  
 <span data-ttu-id="3f490-127">過時查詢臨界值 (天)</span><span class="sxs-lookup"><span data-stu-id="3f490-127">Stale Query Threshold (Days)</span></span>  
 <span data-ttu-id="3f490-128">取得及設定過時查詢臨界值。</span><span class="sxs-lookup"><span data-stu-id="3f490-128">Gets and sets the stale query threshold.</span></span> <span data-ttu-id="3f490-129">設定 STALE_QUERY_THRESHOLD_DAYS 引數，可指定在查詢存放區中保留資料的天數。</span><span class="sxs-lookup"><span data-stu-id="3f490-129">Configure the STALE_QUERY_THRESHOLD_DAYS argument to specify the number of days to retain data in the query store.</span></span>  
  
 <span data-ttu-id="3f490-130">清除查詢資料</span><span class="sxs-lookup"><span data-stu-id="3f490-130">Purge Query Data</span></span>  
 <span data-ttu-id="3f490-131">移除查詢存放區的內容。</span><span class="sxs-lookup"><span data-stu-id="3f490-131">Removes the contents of the query store.</span></span>  
  
 <span data-ttu-id="3f490-132">圓形圖</span><span class="sxs-lookup"><span data-stu-id="3f490-132">Pie Charts</span></span>  
 <span data-ttu-id="3f490-133">左圖顯示在磁碟上耗用總資料庫檔案，以及填有查詢存放區資料的檔案比率。</span><span class="sxs-lookup"><span data-stu-id="3f490-133">The left chart shows the total database file consumption on the disk, and the portion of the file which is filled with the query store data.</span></span>  
  
 <span data-ttu-id="3f490-134">右圖顯示目前用完的查詢存放區配額比率。</span><span class="sxs-lookup"><span data-stu-id="3f490-134">The right chart shows the portion of the query store quota which is currently used up.</span></span> <span data-ttu-id="3f490-135">請注意，配額不會顯示在左圖中。</span><span class="sxs-lookup"><span data-stu-id="3f490-135">Note that the quota is not shown in the left chart.</span></span> <span data-ttu-id="3f490-136">配額可能超過目前資料庫的大小。</span><span class="sxs-lookup"><span data-stu-id="3f490-136">The quota may exceed the current size of the database.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="3f490-137">備註</span><span class="sxs-lookup"><span data-stu-id="3f490-137">Remarks</span></span>  
 <span data-ttu-id="3f490-138">查詢存放區功能為 DBA 提供查詢計劃選擇及效能的深入了解。</span><span class="sxs-lookup"><span data-stu-id="3f490-138">The query store feature provides DBAs with insight on query plan choice and performance.</span></span> <span data-ttu-id="3f490-139">它能讓您快速找出因為查詢計劃中的變更所導致的效能差異，以簡化效能疑難排解。</span><span class="sxs-lookup"><span data-stu-id="3f490-139">It simplifies performance troubleshooting by enabling you to quickly find performance differences caused by changes in query plans.</span></span> <span data-ttu-id="3f490-140">該功能會自動擷取查詢、計劃及執行階段統計資料的記錄，並會保留這些記錄供您檢閱。</span><span class="sxs-lookup"><span data-stu-id="3f490-140">The feature automatically captures a history of queries, plans, and runtime statistics, and retains these for your review.</span></span> <span data-ttu-id="3f490-141">其會以時段來區分資料、供您查看資料庫使用模式，並了解何時在伺服器上發生查詢計劃變更。</span><span class="sxs-lookup"><span data-stu-id="3f490-141">It separates data by time windows, allowing you to see database usage patterns and understand when query plan changes happened on the server.</span></span> <span data-ttu-id="3f490-142">可藉由使用這個查詢存放區資料庫屬性頁面，或是使用 [ALTER DATABASE SET](/sql/t-sql/statements/alter-database-transact-sql-set-options) 選項，設定查詢存放區。</span><span class="sxs-lookup"><span data-stu-id="3f490-142">The query store can be configured by using this query store database property page, or by using the [ALTER DATABASE SET](/sql/t-sql/statements/alter-database-transact-sql-set-options) option.</span></span> <span data-ttu-id="3f490-143">使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 對話方塊，查詢存放區即可呈現資訊。</span><span class="sxs-lookup"><span data-stu-id="3f490-143">The query store presents information by using a [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] dialog box.</span></span> <span data-ttu-id="3f490-144">如需查詢存放區的詳細資訊，請參閱 [Monitoring Performance By Using the Query Store](../performance/monitoring-performance-by-using-the-query-store.md)。</span><span class="sxs-lookup"><span data-stu-id="3f490-144">For more information about query store, see [Monitoring Performance By Using the Query Store](../performance/monitoring-performance-by-using-the-query-store.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3f490-145">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3f490-145">See Also</span></span>  
 <span data-ttu-id="3f490-146">[查詢存放區預存程序 &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="3f490-146">[Query Store Stored Procedures &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql) </span></span>  
 [<span data-ttu-id="3f490-147">查詢存放區目錄檢視 &#40;Transact-SQL&#41;</span><span class="sxs-lookup"><span data-stu-id="3f490-147">Query Store Catalog Views &#40;Transact-SQL&#41;</span></span>](/sql/relational-databases/system-catalog-views/query-store-catalog-views-transact-sql)  
  
  
