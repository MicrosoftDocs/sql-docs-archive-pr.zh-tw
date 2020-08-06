---
title: 監視 Analysis Services 實例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- monitoring [Analysis Services - multidimensional data]
- multidimensional data [Analysis Services], monitoring
- monitoring performance [SQL Server], SQL Server Profiler
- performance [SQL Server], monitoring tools
ms.assetid: 2f0ab717-05f3-427e-b8cd-a8bdca374add
author: minewiskan
ms.author: owend
ms.openlocfilehash: b98037ea9f26c339cdf7aba22c37e2cfb3dfbb97
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598040"
---
# <a name="monitor-an-analysis-services-instance"></a><span data-ttu-id="f0ea0-102">監視 Analysis Services 執行個體</span><span class="sxs-lookup"><span data-stu-id="f0ea0-102">Monitor an Analysis Services Instance</span></span>
  <span data-ttu-id="f0ea0-103">您可使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或效能監視器 (此應用程式有時稱為 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] PerfMon **) 來監視**的效能。</span><span class="sxs-lookup"><span data-stu-id="f0ea0-103">You can monitor the performance of [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] by using [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] or Performance Monitor, an application sometimes referred to as **PerfMon**.</span></span> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] <span data-ttu-id="f0ea0-104">可讓您建立和管理追蹤，並分析和重新執行追蹤結果。</span><span class="sxs-lookup"><span data-stu-id="f0ea0-104">lets you create and manage traces and analyze and replay trace results.</span></span> <span data-ttu-id="f0ea0-105">效能監視器會報告伺服器狀態 (透過某些計數器來建立索引)，這些將在下節中討論。</span><span class="sxs-lookup"><span data-stu-id="f0ea0-105">Performance Monitor reports on server status, as indexed through certain counters, which are discussed in the next section.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="f0ea0-106">如需監視的詳細資訊，請參閱 [SQL Server 2008 R2 操作指南](https://go.microsoft.com/fwlink/?LinkID=225539)。</span><span class="sxs-lookup"><span data-stu-id="f0ea0-106">For more information about monitoring, see the [SQL Server 2008 R2 Operations Guide](https://go.microsoft.com/fwlink/?LinkID=225539).</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="f0ea0-107">本節內容</span><span class="sxs-lookup"><span data-stu-id="f0ea0-107">In This Section</span></span>  
 <span data-ttu-id="f0ea0-108">請追蹤這些連結來深入了解監視。</span><span class="sxs-lookup"><span data-stu-id="f0ea0-108">Follow these links to learn more about monitoring.</span></span>  
  
 [<span data-ttu-id="f0ea0-109">Analysis Services 追蹤事件</span><span class="sxs-lookup"><span data-stu-id="f0ea0-109">Analysis Services Trace Events</span></span>](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)  
  
 [<span data-ttu-id="f0ea0-110">使用 SQL Server Profiler 監視 Analysis Services</span><span class="sxs-lookup"><span data-stu-id="f0ea0-110">Use SQL Server Profiler to Monitor Analysis Services</span></span>](use-sql-server-profiler-to-monitor-analysis-services.md)  
  
 [<span data-ttu-id="f0ea0-111">使用 SQL Server 擴充事件 &#40;XEvents&#41; 監視 Analysis Services</span><span class="sxs-lookup"><span data-stu-id="f0ea0-111">Use SQL Server Extended Events &#40;XEvents&#41; to Monitor Analysis Services</span></span>](../instances/monitor-analysis-services-with-sql-server-extended-events.md)  
  
 [<span data-ttu-id="f0ea0-112">使用動態管理檢視 &#40;DMV&#41; 監視 Analysis Services</span><span class="sxs-lookup"><span data-stu-id="f0ea0-112">Use Dynamic Management Views &#40;DMVs&#41; to Monitor Analysis Services</span></span>](use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
 [<span data-ttu-id="f0ea0-113">效能計數器 &#40;SSAS&#41;</span><span class="sxs-lookup"><span data-stu-id="f0ea0-113">Performance Counters &#40;SSAS&#41;</span></span>](performance-counters-ssas.md)  
  
  
