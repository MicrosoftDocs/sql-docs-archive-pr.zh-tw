---
title: 基數估計 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 11/24/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- cardinality estimator
- CE (cardinality estimator)
- estimating cardinality
ms.assetid: baa8a304-5713-4cfe-a699-345e819ce6df
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: aa56127f649d71bfcc8825322f8bf729175d41df
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606820"
---
# <a name="cardinality-estimation-sql-server"></a><span data-ttu-id="26c30-102">基數估計 (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="26c30-102">Cardinality Estimation (SQL Server)</span></span>
  <span data-ttu-id="26c30-103">基數估計邏輯 (稱為基數估計工具) 在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 中經過重新設計，可改善查詢計劃的品質，從而提升查詢效能。</span><span class="sxs-lookup"><span data-stu-id="26c30-103">The cardinality estimation logic, called the cardinality estimator, is re-designed in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] to improve the quality of query plans, and therefore to improve query performance.</span></span> <span data-ttu-id="26c30-104">新的基數估計工具併入了可搭配新型 OLTP 和資料倉儲工作負載完善運作的假設和演算法。</span><span class="sxs-lookup"><span data-stu-id="26c30-104">The new cardinality estimator incorporates assumptions and algorithms that work well on modern OLTP and data warehousing workloads.</span></span> <span data-ttu-id="26c30-105">這項發展乃是憑藉著我們針對新型工作負載進行深入的基數估計研究，以及過去 15 年來改進 SQL Server 基數估計工具的經驗。</span><span class="sxs-lookup"><span data-stu-id="26c30-105">It is based on in-depth cardinality estimation research on modern workloads, and our learnings over the past 15 years of improving the SQL Server cardinality estimator.</span></span> <span data-ttu-id="26c30-106">由客戶的意見反應得知，儘管無論變更與否都能讓大多數的查詢獲益，但與舊版基數估計工具相比，少數的查詢可能會顯現效能退化。</span><span class="sxs-lookup"><span data-stu-id="26c30-106">Feedback from customers shows that while most queries will benefit from the change or remain unchanged, a small number might show regressions compared to the previous cardinality estimator.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="26c30-107">基數估計值是對查詢結果中的資料列數所做的預測。</span><span class="sxs-lookup"><span data-stu-id="26c30-107">Cardinality estimates are a prediction of the number of rows in the query result.</span></span> <span data-ttu-id="26c30-108">查詢最佳化工具會使用這些估計值選擇執行查詢的計劃。</span><span class="sxs-lookup"><span data-stu-id="26c30-108">The query optimizer uses these estimates to choose a plan for executing the query.</span></span> <span data-ttu-id="26c30-109">查詢計劃的品質對於提升查詢效能有著直接的影響。</span><span class="sxs-lookup"><span data-stu-id="26c30-109">The quality of the query plan has a direct impact on improving query performance.</span></span>  
  
## <a name="performance-testing-and-tuning-recommendations"></a><span data-ttu-id="26c30-110">效能測試與微調建議</span><span class="sxs-lookup"><span data-stu-id="26c30-110">Performance Testing and Tuning Recommendations</span></span>  
 <span data-ttu-id="26c30-111">在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]中建立的所有新資料庫都將啟用新的基數估計工具。</span><span class="sxs-lookup"><span data-stu-id="26c30-111">The new cardinality estimator is enabled for all new databases created in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].</span></span> <span data-ttu-id="26c30-112">不過，升級到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 並不會為現有的資料庫啟用新的基數估計工具。</span><span class="sxs-lookup"><span data-stu-id="26c30-112">However, upgrading to [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] does not enable the new cardinality estimator on existing databases.</span></span>  
  
 <span data-ttu-id="26c30-113">為確保獲得最佳查詢效能，請使用以下建議搭配新的基數估計工具測試您的工作負載，然後再由實際執行系統予以啟用。</span><span class="sxs-lookup"><span data-stu-id="26c30-113">To ensure the best query performance, use these recommendations to test your workload with the new cardinality estimator before enabling it on your production system.</span></span>  
  
1.  <span data-ttu-id="26c30-114">升級所有現有的資料庫以使用新的基數估計工具。</span><span class="sxs-lookup"><span data-stu-id="26c30-114">Upgrade all existing databases to use the new cardinality estimator.</span></span> <span data-ttu-id="26c30-115">若要這麼做，請使用[ALTER Database 相容性層級 &#40;transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) ，將資料庫相容性層級設定為120。</span><span class="sxs-lookup"><span data-stu-id="26c30-115">To do this, use [ALTER DATABASE Compatibility Level &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) to set the database compatibility level to 120.</span></span>  
  
2.  <span data-ttu-id="26c30-116">搭配新的基數估計工具執行您的測試工作負載，然後依照您目前疑難排解效能問題的相同方式，疑難排解任何新的效能問題。</span><span class="sxs-lookup"><span data-stu-id="26c30-116">Run your test workload with the new cardinality estimator, and then troubleshoot any new performance issues in the same manner you currently troubleshoot performance issues.</span></span>  
  
3.  <span data-ttu-id="26c30-117">在您搭配新的基數估計工具 (資料庫相容性層級 120 (SQL Server 2014)) 執行工作負載之後，若有特定的查詢顯現效能退化，請用追蹤旗標 9481 執行查詢，即可使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更早版本所用的基數估計工具版本。</span><span class="sxs-lookup"><span data-stu-id="26c30-117">Once your workload is running with the new cardinality estimator (database compatibility level 120 (SQL Server 2014)), and a specific query has regressed, you can run the query with trace flag 9481 to use the version of the cardinality estimator used in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] and earlier.</span></span> <span data-ttu-id="26c30-118">若要使用追蹤旗標執行查詢，請參閱知識庫文件＜ [啟用會影響計劃而可在特定的查詢層級透過不同的追蹤旗標加以控制的 SQL Server 查詢最佳化工具行為](https://support.microsoft.com/kb/2801413)＞(機器翻譯)。</span><span class="sxs-lookup"><span data-stu-id="26c30-118">To run a query with a trace flag, see the KB article [Enable plan-affecting SQL Server query optimizer behavior that can be controlled by different trace flags on a specific-query level](https://support.microsoft.com/kb/2801413).</span></span>  
  
4.  <span data-ttu-id="26c30-119">如果您無法一次變更所有資料庫以使用新的基數估計工具，您可以使用[ALTER DATABASE 相容性層級 &#40;transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) ，將先前的基數估計工具用於所有資料庫，將資料庫相容性層級設定為110。</span><span class="sxs-lookup"><span data-stu-id="26c30-119">If you cannot change all of the databases at once to use the new cardinality estimator, you can use the former cardinality estimator for all databases by using [ALTER DATABASE Compatibility Level &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) to set the database compatibility level to 110.</span></span>  
  
5.  <span data-ttu-id="26c30-120">如果您是以資料庫相容性層級 110 執行工作負載，而想要搭配新的基數估計工具來測試或執行特定的查詢，請用追蹤旗標 2312 執行查詢，即可使用 SQL Server 2014 版本的基數估計工具。</span><span class="sxs-lookup"><span data-stu-id="26c30-120">If your workload is running with database compatibility level 110 and you want to test or run a specific query with the new cardinality estimator, you can run the query with trace flag 2312 to use the SQL Server 2014 version of the cardinality estimator.</span></span>  <span data-ttu-id="26c30-121">若要使用追蹤旗標執行查詢，請參閱知識庫文件＜ [啟用會影響計劃而可在特定的查詢層級透過不同的追蹤旗標加以控制的 SQL Server 查詢最佳化工具行為](https://support.microsoft.com/kb/2801413)＞(機器翻譯)。</span><span class="sxs-lookup"><span data-stu-id="26c30-121">To run a query with a trace flag, see the KB article [Enable plan-affecting SQL Server query optimizer behavior that can be controlled by different trace flags on a specific-query level](https://support.microsoft.com/kb/2801413).</span></span>  
  
## <a name="new-xevents"></a><span data-ttu-id="26c30-122">新的 XEvents</span><span class="sxs-lookup"><span data-stu-id="26c30-122">New XEvents</span></span>  
 <span data-ttu-id="26c30-123">現已有兩個新的 query_optimizer_estimate_cardinality XEvents 支援新的查詢計劃。</span><span class="sxs-lookup"><span data-stu-id="26c30-123">There are two new query_optimizer_estimate_cardinality XEvents to support the new query plans.</span></span>  
  
-   <span data-ttu-id="26c30-124">*query_optimizer_estimate_cardinality* 會在查詢最佳化工具估計關聯運算式的基數時發生。</span><span class="sxs-lookup"><span data-stu-id="26c30-124">*query_optimizer_estimate_cardinality* occurs when the query optimizer estimates the cardinality on a relational expression.</span></span>  
  
-   <span data-ttu-id="26c30-125">*query_optimizer_force_both_cardinality_estimation*_behaviors 會在一併啟用追蹤旗標 2312 和 9481 而嘗試同時強制新舊兩版的基數估計行為時發生。</span><span class="sxs-lookup"><span data-stu-id="26c30-125">*query_optimizer_force_both_cardinality_estimation*_behaviors occurs when both traceflags 2312 and 9481 are enabled, attempting to force both old and new cardinality estimation behavior at the same time.</span></span>  
  
## <a name="examples"></a><span data-ttu-id="26c30-126">範例</span><span class="sxs-lookup"><span data-stu-id="26c30-126">Examples</span></span>  
 <span data-ttu-id="26c30-127">下列範例示範新的基數估計值的部分變更。</span><span class="sxs-lookup"><span data-stu-id="26c30-127">The following examples show some of the changes in the new cardinality estimates.</span></span> <span data-ttu-id="26c30-128">估計基數的程式碼已經改寫。</span><span class="sxs-lookup"><span data-stu-id="26c30-128">The code for estimating cardinality has been rewritten.</span></span> <span data-ttu-id="26c30-129">其邏輯相當複雜，因此無法提供所有變更的詳盡清單。</span><span class="sxs-lookup"><span data-stu-id="26c30-129">The logic is complex and it is not possible to provide an exhaustive list of all changes.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="26c30-130">這些範例的用意是提供概念性資訊。</span><span class="sxs-lookup"><span data-stu-id="26c30-130">These examples are provided as conceptual information.</span></span> <span data-ttu-id="26c30-131">您不需要採取任何動作變更資料庫和查詢的設計方式。</span><span class="sxs-lookup"><span data-stu-id="26c30-131">No action is required on your part to change the way you design databases and queries.</span></span>  
  
### <a name="example-a-new-cardinality-estimates-use-an-average-cardinality-for-recently-added-ascending-data"></a><span data-ttu-id="26c30-132">範例 A：新的基數估計值會針對最近加入的遞增資料使用平均基數</span><span class="sxs-lookup"><span data-stu-id="26c30-132">Example A. New cardinality estimates use an average cardinality for recently added ascending data</span></span>  
 <span data-ttu-id="26c30-133">此範例示範新的基數估計工具如何針對在最近更新統計資料期間超出資料表最大值的遞增資料，改善基數估計值。</span><span class="sxs-lookup"><span data-stu-id="26c30-133">This example demonstrates how the new cardinality estimator can improve cardinality estimates for ascending data that exceeds the maximum value in the table during the most recent statistics update.</span></span>  
  
```  
SELECT item, category, amount FROM dbo.Sales AS s WHERE Date = '2013-12-19';  
```  
  
 <span data-ttu-id="26c30-134">在此範例中，Sales 資料表每天都會加入新的資料列，而查詢則要求 12/19/2013 當天的銷售額，且統計資料上次更新的日期是 12/18/2013。</span><span class="sxs-lookup"><span data-stu-id="26c30-134">In this example, new rows are added to the Sales table each day, the query asks for sales that occurred on 12/19/2013, and statistics were last updated on 12/18/2013.</span></span> <span data-ttu-id="26c30-135">舊版基數估計工具會假設 12/19/2013 的值不存在，因為該日期並未超過最大日期，而且統計資料尚未更新成包含 12/19/2013 的值。</span><span class="sxs-lookup"><span data-stu-id="26c30-135">The previous cardinality estimator assumes the 12/19/2013 values do not exist since the date exceeds the maximum date and statistics have not been updated to include the 12/19/2013 values.</span></span> <span data-ttu-id="26c30-136">如果您是載入當天的資料，然後對統計資料更新之前的資料執行查詢，就會發生這種情況，又稱為遞增索引鍵問題。</span><span class="sxs-lookup"><span data-stu-id="26c30-136">This situation, known as the ascending key problem, will occur if you load data during the day, and then run queries against the data before statistics are updated.</span></span>  
  
 <span data-ttu-id="26c30-137">此行為已經變更。</span><span class="sxs-lookup"><span data-stu-id="26c30-137">This behavior has changed.</span></span> <span data-ttu-id="26c30-138">現在，即使統計資料尚未更新到自從統計資料上次更新後最近加入的遞增資料，新的基數估計工具也將假設其值存在，並且使用資料行內每個值的平均基數做為基數估計值。</span><span class="sxs-lookup"><span data-stu-id="26c30-138">Now, even if statistics have not been updated for the most recent ascending data that is added since the last statistics update, the new cardinality estimator assumes the values exist and uses the average cardinality for each value in the column as the cardinality estimate.</span></span>  
  
### <a name="example-b-new-cardinality-estimates-assume-filtered-predicates-on-the-same-table-have-some-correlation"></a><span data-ttu-id="26c30-139">範例 B：新的基數估計值會假設相同資料表上的篩選述詞具有若干相互關聯性</span><span class="sxs-lookup"><span data-stu-id="26c30-139">Example B. New cardinality estimates assume filtered predicates on the same table have some correlation</span></span>  
 <span data-ttu-id="26c30-140">此範例假設 Cars 資料表有 1000 個資料列，其中 Make (品牌) 符合 'Honda' 者為 200 列，Model (車款) 符合 'Civic' 者為 50 列，而且所有的 Civic 車款都是 Honda 品牌。</span><span class="sxs-lookup"><span data-stu-id="26c30-140">For this example, assume the table Cars as 1000 rows, Make has 200 matches for 'Honda', Model has 50 matches for 'Civic', and that all of the Civics are Hondas.</span></span> <span data-ttu-id="26c30-141">因此，Make 資料行的值有 20% 為 'Honda'，Model 資料行的值有 5% 為 'Civic'，而且 Honda Civic 的實際數目是 50。</span><span class="sxs-lookup"><span data-stu-id="26c30-141">Therefore, 20% of the values in the Make column are 'Honda', 5% of the values in the Model column are 'Civic', and the actual number of Honda Civics is 50.</span></span> <span data-ttu-id="26c30-142">原本的基數估計值假設 Make 和 Model 資料行的值彼此獨立。</span><span class="sxs-lookup"><span data-stu-id="26c30-142">The previous cardinality estimates assume the values in the Make and the Model columns are independent of each other.</span></span> <span data-ttu-id="26c30-143">先前的查詢最佳化工具估計有10個 Honda Civic ( .05 \* .20 \* 1000 資料列 = 10 個數據列) 。</span><span class="sxs-lookup"><span data-stu-id="26c30-143">The previous query optimizer estimates there are 10 Honda Civics (.05 \* .20 \* 1000 rows = 10 rows).</span></span>  
  
```  
SELECT year, purchase_price FROM dbo.Cars WHERE Make = 'Honda' AND Model = 'Civic';  
```  
  
 <span data-ttu-id="26c30-144">此行為已經變更。</span><span class="sxs-lookup"><span data-stu-id="26c30-144">This behavior has changed.</span></span> <span data-ttu-id="26c30-145">現在，新的基數估計值會假設 Make 和 Model 資料行具有「若干」 \*\* 相互關聯性。</span><span class="sxs-lookup"><span data-stu-id="26c30-145">Now, the new cardinality estimates assume the Make and Model columns have *some* correlation.</span></span> <span data-ttu-id="26c30-146">查詢最佳化工具會為估計方程式加入指數元件，以估計出較高的基數。</span><span class="sxs-lookup"><span data-stu-id="26c30-146">The query optimizer estimates a higher cardinality by adding an exponential component to the estimation equation.</span></span> <span data-ttu-id="26c30-147">查詢最佳化工具現在會估計22.36 個數據列 ( .05 \* SQRT ( .20) \* 1000 rows = 22.36 資料列 ) 符合述詞。</span><span class="sxs-lookup"><span data-stu-id="26c30-147">The query optimizer now estimates that 22.36 rows ( .05 \* SQRT(.20) \* 1000 rows = 22.36 rows ) match the predicate.</span></span> <span data-ttu-id="26c30-148">就此案例和具體資料分佈來看，22.36 個資料列更趨近於查詢將會傳回的實際數目 50 個資料列。</span><span class="sxs-lookup"><span data-stu-id="26c30-148">For this scenario and specific data distribution, 22.36 rows is closer to the actual 50 rows that the query will return.</span></span>  
  
 <span data-ttu-id="26c30-149">請注意，新的基數估計工具邏輯會對述詞選擇性排序並增加指數乘冪。</span><span class="sxs-lookup"><span data-stu-id="26c30-149">Note, the new cardinality estimator logic sorts the predicate selectivities and increases the exponent.</span></span> <span data-ttu-id="26c30-150">例如，如果述詞選擇性是 .05、.20 和 .25，基數估計值會是 ( .05 \* SQRT ( .20) \* sqrt (SQRT ( .25) # A6 ) 。</span><span class="sxs-lookup"><span data-stu-id="26c30-150">For example, if the predicate selectivities were .05, .20, and .25, the cardinality estimate would be (.05 \* SQRT(.20) \* SQRT(SQRT(.25)) ).</span></span>  
  
### <a name="example-c-new-cardinality-estimates-assume-filtered-predicates-on-different-tables-are-independent"></a><span data-ttu-id="26c30-151">範例 C：新的基數估計值會假設不同資料表上的篩選述詞彼此無關</span><span class="sxs-lookup"><span data-stu-id="26c30-151">Example C. New cardinality estimates assume filtered predicates on different tables are independent</span></span>  
 <span data-ttu-id="26c30-152">就此範例而言，舊版基數估計工具假設述詞篩選 s.type 和 r.date 相互關聯。</span><span class="sxs-lookup"><span data-stu-id="26c30-152">For this example, the previous cardinality estimator assumes that the predicate filters s.type and r.date are correlated.</span></span> <span data-ttu-id="26c30-153">不過，對新型工作負載測試的結果顯示，不同資料表中各資料行的述詞篩選通常並非彼此相互關聯。</span><span class="sxs-lookup"><span data-stu-id="26c30-153">However, test results on modern workloads showed that predicate filters on columns in different tables are usually not correlated with each other.</span></span>  
  
```  
SELECT s.ticket, s.customer, r.store FROM dbo.Sales AS s CROSS JOIN dbo.Returns AS r  
WHERE s.ticket = r.ticket AND s.type = 'toy' AND r.date = '2013-12-19';  
```  
  
 <span data-ttu-id="26c30-154">此行為已經變更。</span><span class="sxs-lookup"><span data-stu-id="26c30-154">This behavior has changed.</span></span> <span data-ttu-id="26c30-155">現在，新的基數估計工具邏輯會假設 s.type 並未與 r.date 相互關聯。</span><span class="sxs-lookup"><span data-stu-id="26c30-155">Now, the new cardinality estimator logic assumes that s.type is not correlated with r.date.</span></span> <span data-ttu-id="26c30-156">實際的講法就是，其假設每天都會有玩具退貨，而非只限特定的哪一天。</span><span class="sxs-lookup"><span data-stu-id="26c30-156">In practical terms, the assumption is that toys are returned every day and not only on a specific day.</span></span> <span data-ttu-id="26c30-157">在此情況下，新的基數估計值將小於原本的基數估計值。</span><span class="sxs-lookup"><span data-stu-id="26c30-157">In this case, the new cardinality estimates will be a smaller number than the previous cardinality estimates.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="26c30-158">另請參閱</span><span class="sxs-lookup"><span data-stu-id="26c30-158">See Also</span></span>  
 [<span data-ttu-id="26c30-159">效能的監視與微調</span><span class="sxs-lookup"><span data-stu-id="26c30-159">Monitor and Tune for Performance</span></span>](monitor-and-tune-for-performance.md)  
  
  
