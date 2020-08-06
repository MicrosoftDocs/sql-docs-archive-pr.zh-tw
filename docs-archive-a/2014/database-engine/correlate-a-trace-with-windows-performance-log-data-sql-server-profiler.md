---
title: 使追蹤與 Windows 效能記錄資料產生相互關聯 (SQL Server Profiler) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], logs
ms.assetid: e1b3072c-8daf-49a7-9895-c8cccd2adb95
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 34575cf4270d817ecfbb5b2d1824831cc99454fb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596264"
---
# <a name="correlate-a-trace-with-windows-performance-log-data-sql-server-profiler"></a><span data-ttu-id="f82d0-102">使追蹤與 Windows 效能記錄資料產生相互關聯 (SQL Server Profiler)</span><span class="sxs-lookup"><span data-stu-id="f82d0-102">Correlate a Trace with Windows Performance Log Data (SQL Server Profiler)</span></span>
  [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]<span data-ttu-id="f82d0-103">可以讓 Microsoft Windows 系統監視器計數器與 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或事件相互關聯 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="f82d0-103">can correlate Microsoft Windows System Monitor counters with [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] or [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] events.</span></span> <span data-ttu-id="f82d0-104">Windows 系統監視器可將指定計數器的系統活動記錄在效能記錄中。</span><span class="sxs-lookup"><span data-stu-id="f82d0-104">Windows System Monitor logs system activity for specified counters in performance logs.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="f82d0-105">如需有關在不同 Windows 版本之間共用記錄的詳細資訊，請參閱本主題結尾處的程序。</span><span class="sxs-lookup"><span data-stu-id="f82d0-105">For information about sharing logs among different versions of Windows, see the procedure at the end of this topic.</span></span>  
  
### <a name="to-correlate-a-trace-with-performance-log-data"></a><span data-ttu-id="f82d0-106">使追蹤與效能記錄資料產生相互關聯</span><span class="sxs-lookup"><span data-stu-id="f82d0-106">To correlate a trace with performance log data</span></span>  
  
1.  <span data-ttu-id="f82d0-107">在 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]中，開啟儲存的追蹤檔案或追蹤資料表。</span><span class="sxs-lookup"><span data-stu-id="f82d0-107">In [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)], open a saved trace file or trace table.</span></span> <span data-ttu-id="f82d0-108">您無法與仍在收集事件資料的執行中追蹤產生相互關聯。</span><span class="sxs-lookup"><span data-stu-id="f82d0-108">You cannot correlate a running trace that is still collecting event data.</span></span> <span data-ttu-id="f82d0-109">為了與系統監視器資料保持正確的相互關聯，追蹤必須同時包含 [StartTime]\*\*\*\* 與 [EndTime]\*\*\*\* 資料行。</span><span class="sxs-lookup"><span data-stu-id="f82d0-109">For accurate correlation with System Monitor data, the trace must contain both **StartTime** and **EndTime** data columns.</span></span>  
  
2.  <span data-ttu-id="f82d0-110">在  [檔案][!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] \*\*\*\* 功能表上，按一下 [匯入效能資料]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="f82d0-110">On the [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] **File** menu, click **Import Performance Data**.</span></span>  
  
3.  <span data-ttu-id="f82d0-111">在 [開啟]\*\*\*\* 對話方塊中，選取含有效能記錄的檔案。</span><span class="sxs-lookup"><span data-stu-id="f82d0-111">In the **Open** dialog box, select a file that contains a performance log.</span></span> <span data-ttu-id="f82d0-112">擷取效能記錄資料的期間必須與擷取追蹤資料的期間相同。</span><span class="sxs-lookup"><span data-stu-id="f82d0-112">The performance log data must have been captured during the same time period in which the trace data is captured.</span></span>  
  
4.  <span data-ttu-id="f82d0-113">在 [效能計數器限制]\*\*\*\* 對話方塊中，針對要顯示在追蹤旁的系統監視器物件與計數器，選取其對應的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="f82d0-113">In the **Performance Counters Limit** dialog box, select the check boxes that correspond to the System Monitor objects and counters that you want to display alongside the trace.</span></span> <span data-ttu-id="f82d0-114">按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="f82d0-114">Click **OK.**</span></span>  
  
5.  <span data-ttu-id="f82d0-115">選取追蹤事件視窗中的事件，或使用方向鍵來瀏覽追蹤事件視窗中相鄰的幾個資料列。</span><span class="sxs-lookup"><span data-stu-id="f82d0-115">Select an event in the trace events window, or navigate through several adjacent rows in the trace events window by using the arrow keys.</span></span> <span data-ttu-id="f82d0-116">[系統監視器資料]\*\*\*\* 視窗中的紅色直條，代表已與所選追蹤事件產生相互關聯的效能記錄資料。</span><span class="sxs-lookup"><span data-stu-id="f82d0-116">The vertical red bar in the **System Monitor data** window indicates the performance log data that is correlated with the selected trace event.</span></span>  
  
6.  <span data-ttu-id="f82d0-117">在系統監視器圖表中，按一下您所需的時間點。</span><span class="sxs-lookup"><span data-stu-id="f82d0-117">Click a point of interest in the System Monitor graph.</span></span> <span data-ttu-id="f82d0-118">系統會選取時間最接近的對應追蹤資料列。</span><span class="sxs-lookup"><span data-stu-id="f82d0-118">The corresponding trace row that is nearest in time is selected.</span></span> <span data-ttu-id="f82d0-119">若要放大時間範圍，請按住滑鼠指標並在系統監視器圖表中加以拖曳。</span><span class="sxs-lookup"><span data-stu-id="f82d0-119">To zoom in on a time range, press and drag the mouse pointer in the System Monitor graph.</span></span>  
  
### <a name="to-create-performance-logs-that-can-be-shared-among-different-versions-of-windows"></a><span data-ttu-id="f82d0-120">若要建立可在不同的 Windows 版本間共用的效能記錄</span><span class="sxs-lookup"><span data-stu-id="f82d0-120">To create performance logs that can be shared among different versions of Windows</span></span>  
  
1.  <span data-ttu-id="f82d0-121">在 [控制台] 中，開啟 [系統管理工具]\*\*\*\*，然後按兩下 [效能]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="f82d0-121">In Control Panel, open **Administrative Tools**, and then double click **Performance**.</span></span>  
  
2.  <span data-ttu-id="f82d0-122">在 [效能] 對話方塊中，展開 [效能記錄檔及警示]，以滑鼠右鍵按一下 [計數器記錄檔]，然後按一下 [新記錄檔設定]。</span><span class="sxs-lookup"><span data-stu-id="f82d0-122">In the **Performance** dialog box, expand **Performance Logs and Alerts**, right-click **Counter Logs**, and then click **New Log Settings**.</span></span>  
  
3.  <span data-ttu-id="f82d0-123">輸入計數器記錄檔的名稱，再按一下 [確定]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="f82d0-123">Type a name for the counter log, and then click **OK**.</span></span>  
  
4.  <span data-ttu-id="f82d0-124">在 [一般]\*\*\*\* 索引標籤上，按一下 [新增計數器]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="f82d0-124">On the **General** tab, click **Add Counters**.</span></span>  
  
5.  <span data-ttu-id="f82d0-125">在 [效能物件]\*\*\*\* 清單中，選取您要監視的效能物件。</span><span class="sxs-lookup"><span data-stu-id="f82d0-125">In the **Performance object** list, select a performance object you want to monitor.</span></span> <span data-ttu-id="f82d0-126">[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 預設執行個體的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 效能物件名稱會以 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 作為開頭，而具名執行個體則會以 MSSQL$*instanceName*作為開頭。</span><span class="sxs-lookup"><span data-stu-id="f82d0-126">The names of [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] performance objects for default instances of [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] start with [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] and named instances start with MSSQL$*instanceName*.</span></span>  
  
6.  <span data-ttu-id="f82d0-127">盡可能為您的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體加入所需的計數器以及其他重要的值，如處理器時間與磁碟時間。</span><span class="sxs-lookup"><span data-stu-id="f82d0-127">Add as many counters as necessary for your [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instance and other important values, such as processor time and disk time.</span></span>  
  
7.  <span data-ttu-id="f82d0-128">完成新增計數器後，請按一下 [關閉]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="f82d0-128">When you have finished adding counters, click **Close**.</span></span>  
  
8.  <span data-ttu-id="f82d0-129">設定 [Sample data every (依下列週期進行資料取樣)]\*\*\*\* 的間隔值。</span><span class="sxs-lookup"><span data-stu-id="f82d0-129">Set values for the **Sample data every** interval.</span></span> <span data-ttu-id="f82d0-130">一開始請使用適度的抽樣間隔，例如 5 分鐘，然後再視需要調整間隔。</span><span class="sxs-lookup"><span data-stu-id="f82d0-130">Start with a modest sampling interval, such as 5 minutes, and then adjust the interval if necessary.</span></span>  
  
9. <span data-ttu-id="f82d0-131">在 [記錄檔]\*\*\*\* 索引標籤上，從 [記錄檔案類型]\*\*\*\* 清單中選擇 [TextFile (Comma delimited) (文字檔案 (以逗號分隔))]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="f82d0-131">On the **Log Files** tab, choose **TextFile (Comma delimited)** from the **Log file type** list.</span></span> <span data-ttu-id="f82d0-132">以逗號分隔的文字記錄檔可在不同的 Windows 版本間共用，並且稍後可在諸如 Microsoft Excel 的報告工具中加以檢視。</span><span class="sxs-lookup"><span data-stu-id="f82d0-132">Comma-delimited text log files can be shared among different versions of Windows and can be viewed later in reporting tools such as Microsoft Excel.</span></span>  
  
10. <span data-ttu-id="f82d0-133">在 [排程]\*\*\*\* 索引標籤上，指定監視排程。</span><span class="sxs-lookup"><span data-stu-id="f82d0-133">On the **Schedule** tab, specify a monitoring schedule.</span></span>  
  
11. <span data-ttu-id="f82d0-134">按一下 [確定]\*\*\*\* 建立效能記錄。</span><span class="sxs-lookup"><span data-stu-id="f82d0-134">Click **OK** to create the performance log.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f82d0-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f82d0-135">See Also</span></span>  
 <span data-ttu-id="f82d0-136">[SQL Server Profiler 範本和權限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md) </span><span class="sxs-lookup"><span data-stu-id="f82d0-136">[SQL Server Profiler Templates and Permissions](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md) </span></span>  
 [<span data-ttu-id="f82d0-137">啟動 SQL Server Profiler</span><span class="sxs-lookup"><span data-stu-id="f82d0-137">Start SQL Server Profiler</span></span>](../tools/sql-server-profiler/start-sql-server-profiler.md)  
  
  
