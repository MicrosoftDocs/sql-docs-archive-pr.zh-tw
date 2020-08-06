---
title: 使用測試伺服器的考量 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- overhead [Database Engine Tuning Advisor]
- tuning overhead [SQL Server]
- reducing production server tuning load
- Database Engine Tuning Advisor [SQL Server], test servers
- xp_msver
- test servers [Database Engine Tuning Advisor]
- production servers [SQL Server]
- offload tuning overhead [SQL Server]
ms.assetid: 94e6c3e5-1f09-4616-9da2-4e44d066d494
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3fe835c1e92b382e3e2fadd7e80d4b2984929cc5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87697996"
---
# <a name="considerations-for-using-test-servers"></a><span data-ttu-id="be03e-102">使用測試伺服器的考量</span><span class="sxs-lookup"><span data-stu-id="be03e-102">Considerations for Using Test Servers</span></span>
  <span data-ttu-id="be03e-103">使用測試伺服器微調實際伺服器上的資料庫，是 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 的重要優點。</span><span class="sxs-lookup"><span data-stu-id="be03e-103">Using a test server to tune a database on a production server is an important benefit of [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor.</span></span> <span data-ttu-id="be03e-104">您可利用這項功能，在不需將實際資料從實際伺服器複製到測試伺服器的情況下，將微調負擔卸載到測試伺服器上。</span><span class="sxs-lookup"><span data-stu-id="be03e-104">Using this feature, you can offload tuning overhead to a test server without copying the actual data over to the test server from the production server.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="be03e-105">[!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 圖形化使用者介面 (GUI) 不支援測試伺服器微調功能。</span><span class="sxs-lookup"><span data-stu-id="be03e-105">The test server tuning feature is not supported in the [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor graphical user interface (GUI).</span></span>  
  
 <span data-ttu-id="be03e-106">若要順利使用這項功能，請檢閱下列章節列出的考量事項。</span><span class="sxs-lookup"><span data-stu-id="be03e-106">To use this feature successfully, review the considerations listed in the following sections.</span></span>  
  
## <a name="setting-up-the-test-serverproduction-server-environment"></a><span data-ttu-id="be03e-107">設定測試伺服器/實際伺服器環境</span><span class="sxs-lookup"><span data-stu-id="be03e-107">Setting Up the Test Server/Production Server Environment</span></span>  
  
-   <span data-ttu-id="be03e-108">要使用測試伺服器對實際伺服器上的資料庫進行微調的使用者，必須同時位於兩部伺服器上，否則此案例將會失敗。</span><span class="sxs-lookup"><span data-stu-id="be03e-108">The user who wants to use a test server to tune a database on a production server must exist on both servers, or this scenario will not work.</span></span>  
  
-   <span data-ttu-id="be03e-109">必須啟用擴充預存程序 **xp_msver**，才能使用測試伺服器/實際伺服器案例。</span><span class="sxs-lookup"><span data-stu-id="be03e-109">The extended stored procedure, **xp_msver**, must be enabled to use the test server/production server scenario.</span></span> [!INCLUDE[ssDE](../../includes/ssde-md.md)] <span data-ttu-id="be03e-110">Tuning Advisor 會使用此擴充預存程序來提取在微調測試伺服器時實際伺服器上可使用的處理器數量與記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="be03e-110">Tuning Advisor uses this extended stored procedure to fetch the number of processors and the available memory of the production server to use while tuning the test server.</span></span> <span data-ttu-id="be03e-111">若未啟用 **xp_msver** ， [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 即會採用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 執行所在電腦的硬體特性。</span><span class="sxs-lookup"><span data-stu-id="be03e-111">If **xp_msver** is not enabled, [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor assumes the hardware characteristics of the computer where [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor is running.</span></span> <span data-ttu-id="be03e-112">如果無法取得執行 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 所在電腦的硬體特性，將會假設 1 個處理器和 1024 MB 的記憶體。</span><span class="sxs-lookup"><span data-stu-id="be03e-112">If the hardware characteristics of the computer where [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor is running are not available, one processor and 1024 megabytes (MBs) of memory are assumed.</span></span> <span data-ttu-id="be03e-113">安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，預設會開啟擴充預存程序。</span><span class="sxs-lookup"><span data-stu-id="be03e-113">This extended stored procedure is turned on by default when you install [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="be03e-114">如需詳細資訊，請參閱[介面區組態](../security/surface-area-configuration.md)和 [xp_msver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/xp-msver-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="be03e-114">For more information, see [Surface Area Configuration](../security/surface-area-configuration.md) and [xp_msver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/xp-msver-transact-sql).</span></span>  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] <span data-ttu-id="be03e-115">Tuning Advisor 預期測試伺服器和實際伺服器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本必須相同。</span><span class="sxs-lookup"><span data-stu-id="be03e-115">Tuning Advisor expects the editions of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] to be the same on both the test server and the production server.</span></span> <span data-ttu-id="be03e-116">如果有兩種不同的版本，將優先採用測試伺服器上的版本。</span><span class="sxs-lookup"><span data-stu-id="be03e-116">If there are two different editions, the edition on the test server takes precedence.</span></span> <span data-ttu-id="be03e-117">例如，如果測試伺服器執行的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard，即使實際伺服器執行的是 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Enterprise， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tuning Advisor 也不會在其建議中包含索引檢視表、資料分割和線上作業。</span><span class="sxs-lookup"><span data-stu-id="be03e-117">For example, if the test server is running [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard, [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor will not include indexed views, partitioning, and online operations in its recommendations even if the production server is running [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise.</span></span>  
  
## <a name="about-test-serverproduction-server-behavior"></a><span data-ttu-id="be03e-118">關於測試伺服器/實際伺服器的行為</span><span class="sxs-lookup"><span data-stu-id="be03e-118">About Test Server/Production Server Behavior</span></span>  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] <span data-ttu-id="be03e-119">Tuning Advisor 在做出建議時，會將實際伺服器與測試伺服器之間的硬體差異列入考量。</span><span class="sxs-lookup"><span data-stu-id="be03e-119">Tuning Advisor takes into account hardware differences between the production and the test server when creating recommendations.</span></span> <span data-ttu-id="be03e-120">這些建議就像是在單獨對實際伺服器完成微調的情況下所做的建議。</span><span class="sxs-lookup"><span data-stu-id="be03e-120">The recommendation is the same as though the tuning was done on the production server alone.</span></span>  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] <span data-ttu-id="be03e-121">Tuning Advisor 在收集中繼資料及建立必要的微調統計資料時，可能會對實際伺服器造成一些負荷。</span><span class="sxs-lookup"><span data-stu-id="be03e-121">Tuning Advisor may impose some load on the production server for gathering metadata as well as creation of statistics necessary for tuning.</span></span>  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] <span data-ttu-id="be03e-122">Tuning Advisor 不會從實際伺服器將實際資料複製到測試伺服器。</span><span class="sxs-lookup"><span data-stu-id="be03e-122">Tuning Advisor does not copy actual data from the production server to the test server.</span></span> <span data-ttu-id="be03e-123">它只會複製資料庫的中繼資料與必要的統計資料。</span><span class="sxs-lookup"><span data-stu-id="be03e-123">It only copies the metadata of the databases and the necessary statistics.</span></span>  
  
-   <span data-ttu-id="be03e-124">所有工作階段資訊都會儲存在實際伺服器的 **msdb** 中。</span><span class="sxs-lookup"><span data-stu-id="be03e-124">All session information is stored in **msdb** on the production server.</span></span> <span data-ttu-id="be03e-125">如此可讓您充分利用可進行微調的所有測試伺服器，且所有工作階段的相關資訊都會存放在同一個位置 (實際伺服器) 上。</span><span class="sxs-lookup"><span data-stu-id="be03e-125">This allows you to exploit any available test server for tuning, and information about all sessions is available in one place (the production server).</span></span>  
  
## <a name="issues-related-to-the-shell-database"></a><span data-ttu-id="be03e-126">Shell 資料庫的相關問題</span><span class="sxs-lookup"><span data-stu-id="be03e-126">Issues Related to the Shell Database</span></span>  
  
-   <span data-ttu-id="be03e-127">在微調完成後， [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 會移除它在微調處理過程中於測試伺服器上建立的任何中繼資料。</span><span class="sxs-lookup"><span data-stu-id="be03e-127">After tuning, [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor should remove any metadata that it created on the test server during the tuning process.</span></span> <span data-ttu-id="be03e-128">其中包括 Shell 資料庫。</span><span class="sxs-lookup"><span data-stu-id="be03e-128">This includes the shell database.</span></span> <span data-ttu-id="be03e-129">若您要以相同的實際伺服器與測試伺服器執行一系列的微調工作階段，您可以保留此 Shell 資料庫以節省時間。</span><span class="sxs-lookup"><span data-stu-id="be03e-129">If you are performing a series of tuning sessions with the same production and test servers, you may want to retain this shell database to save time.</span></span> <span data-ttu-id="be03e-130">請在 XML 輸入檔中，指定 **RetainShellDB** 子元素以及 **TuningOptions** 父元素下的其他子元素。</span><span class="sxs-lookup"><span data-stu-id="be03e-130">In the XML input file, specify the **RetainShellDB** subelement with the other sub elements under the **TuningOptions** parent element.</span></span> <span data-ttu-id="be03e-131">利用這些選項， [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 就會保留 Shell 資料庫。</span><span class="sxs-lookup"><span data-stu-id="be03e-131">Using these options causes [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor to retain the shell database.</span></span> <span data-ttu-id="be03e-132">如需詳細資訊，請參閱 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](database-engine-tuning-advisor.md)。</span><span class="sxs-lookup"><span data-stu-id="be03e-132">For more information, see [XML Input File Reference &#40;Database Engine Tuning Advisor&#41;](database-engine-tuning-advisor.md).</span></span>  
  
-   <span data-ttu-id="be03e-133">在順利完成測試伺服器/實際伺服器微調工作階段之後，即使您尚未指定 **RetainShellDB** 子元素，Shell 資料庫可能還是會留在測試伺服器上。</span><span class="sxs-lookup"><span data-stu-id="be03e-133">Shell databases may be left behind on the test server after a successful test server/production server tuning session even if you have not specified the **RetainShellDB** subelement.</span></span> <span data-ttu-id="be03e-134">這些不需要的 Shell 資料庫可能會干擾後續的微調工作階段，因此應該在執行其他測試伺服器/實際伺服器微調工作階段之前加以卸除。</span><span class="sxs-lookup"><span data-stu-id="be03e-134">These unwanted shell databases may interfere with subsequent tuning sessions and should be dropped before performing another test server/production server tuning session.</span></span> <span data-ttu-id="be03e-135">此外，如果有未預期的微調工作階段存在，測試伺服器上的 Shell 資料庫及這些資料庫中的物件都可能留在測試伺服器上。</span><span class="sxs-lookup"><span data-stu-id="be03e-135">In addition, if a tuning session exits unexpectedly, the shell databases on the test server and the objects within those databases may be left behind on the test server.</span></span> <span data-ttu-id="be03e-136">啟動新的測試伺服器/實際伺服器微調工作階段之前，您也應該刪除這些資料庫和物件。</span><span class="sxs-lookup"><span data-stu-id="be03e-136">You should also delete these databases and objects before starting a new test server/production server tuning session.</span></span>  
  
## <a name="issues-related-to-the-tuning-process"></a><span data-ttu-id="be03e-137">微調程序的相關問題</span><span class="sxs-lookup"><span data-stu-id="be03e-137">Issues Related to the Tuning Process</span></span>  
  
-   <span data-ttu-id="be03e-138">使用者必須檢查微調記錄中，是否有因實際伺服器與測試伺服器之間的差異所導致的微調錯誤，以及因為從實際伺服器複製中繼資料到測試伺服器所導致的錯誤。</span><span class="sxs-lookup"><span data-stu-id="be03e-138">The user must check the tuning log for tuning errors that result from differences between the production and test servers, and for errors that result from copying metadata from the production to the test server.</span></span> <span data-ttu-id="be03e-139">例如，測試伺服器上可能沒有使用者登入存在。</span><span class="sxs-lookup"><span data-stu-id="be03e-139">For example, a user login may not exist on the test server.</span></span> <span data-ttu-id="be03e-140">若測試伺服器上沒有使用者登入存在，則工作負載中這些由該使用者登入所發出的事件，將無法進行微調。</span><span class="sxs-lookup"><span data-stu-id="be03e-140">If a user login does not exist on the test server, those events in the workload that are issued by that user login may not be tunable.</span></span> <span data-ttu-id="be03e-141">請使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor GUI 來檢視微調記錄。</span><span class="sxs-lookup"><span data-stu-id="be03e-141">Use the [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor GUI to view the tuning log.</span></span> <span data-ttu-id="be03e-142">如需詳細資訊，請參閱 [檢視及處理 Database Engine Tuning Advisor 的輸出](view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="be03e-142">For more information, see [View and Work with the Output from the Database Engine Tuning Advisor](view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)</span></span>  
  
-   <span data-ttu-id="be03e-143">如果因為在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 建立於測試伺服器中的 Shell 資料庫中有物件遺漏，而使 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 無法微調多項事件，使用者必須檢查微調記錄。</span><span class="sxs-lookup"><span data-stu-id="be03e-143">If [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor cannot tune many events because objects are missing in the shell database that [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor creates on the test server, the user must check the tuning log.</span></span> <span data-ttu-id="be03e-144">無法微調的事件都會列在記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="be03e-144">Events that cannot be tuned are listed in the log.</span></span> <span data-ttu-id="be03e-145">若要順利微調測試伺服器上的資料庫，使用者必須在 Shell 資料庫中建立遺漏的物件，然後啟動新的微調工作階段。</span><span class="sxs-lookup"><span data-stu-id="be03e-145">To successfully tune the database on the test server, the user must create the missing objects in the shell database, and then start a new tuning session.</span></span>  
  
-   <span data-ttu-id="be03e-146">若測試伺服器上已有同名的資料庫存在，則 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 不會複製中繼資料，但會繼續依需要進行微調並收集統計資料。</span><span class="sxs-lookup"><span data-stu-id="be03e-146">If a database with the same name already exists on the test server, [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor does not copy metadata, but continues tuning and gathers statistics as necessary.</span></span> <span data-ttu-id="be03e-147">若使用者已在測試伺服器上建立資料庫，並在叫用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 之前複製了適當的中繼資料，就適用於這種情況。</span><span class="sxs-lookup"><span data-stu-id="be03e-147">This is useful if the user has already created a database on the test server and has copied the appropriate metadata before invoking [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor.</span></span>  
  
-   <span data-ttu-id="be03e-148">若實際伺服器上資料庫的 DATE_CORRELATION_OPTIMIZATION 選項已開啟，在微調測試伺服器時，與此選項關聯的中繼資料與資料不會完全指令碼化。</span><span class="sxs-lookup"><span data-stu-id="be03e-148">If the DATE_CORRELATION_OPTIMIZATION option is turned on for a database on the production server, metadata and the data associated with this option are not completely scripted while tuning the test server.</span></span> <span data-ttu-id="be03e-149">在測試伺服器/實際伺服器案例中執行微調時，可能會有下列問題：</span><span class="sxs-lookup"><span data-stu-id="be03e-149">When tuning is performed for a test server/production server scenario, the following issues may apply:</span></span>  
  
    -   <span data-ttu-id="be03e-150">對於使用 DATE_CORRELATION_OPTIMIZATION 選項的查詢，使用者可以在伺服器上擁有不同的查詢計畫。</span><span class="sxs-lookup"><span data-stu-id="be03e-150">Users can have different query plans on the servers for queries that use the DATE_CORRELATION_OPTIMIZATION option.</span></span>  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)] <span data-ttu-id="be03e-151">Tuning Advisor 可能會建議卸除在建議指令碼中強制使用 DATE_CORRELATION_OPTIMIZATION 選項的索引檢視表。</span><span class="sxs-lookup"><span data-stu-id="be03e-151">Tuning Advisor may suggest dropping indexed views that enforce the DATE_CORRELATION_OPTIMIZATION option in the recommendation script.</span></span>  
  
     <span data-ttu-id="be03e-152">因此，您可以忽略 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 對保存交互關聯統計資料之索引檢視所做的任何相關建議，因為 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 對它們的成本有所認知，對其利益則否。</span><span class="sxs-lookup"><span data-stu-id="be03e-152">Therefore, you may want to ignore any recommendations that [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor makes about the indexed views that hold correlation statistics because [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor knows their costs but not their benefits.</span></span> [!INCLUDE[ssDE](../../includes/ssde-md.md)] <span data-ttu-id="be03e-153">Tuning Advisor 可能不會建議使用者選取特定的索引，例如 **datetime** 資料行中的叢集索引，而此索引在 DATE_CORRELATION_OPTIMIZATION 啟用的情況下應該會有益處。</span><span class="sxs-lookup"><span data-stu-id="be03e-153">Tuning Advisor may not recommend selection of certain indexes such as clustered indexes on **datetime** columns, which could be beneficial when DATE_CORRELATION_OPTIMIZATION is enabled.</span></span>  
  
     <span data-ttu-id="be03e-154">若要判斷檢視是否以相互關聯統計資料為基礎，請選取 **sys.views** 目錄檢視的 [is_date_correlation_view](/sql/relational-databases/system-catalog-views/sys-views-transact-sql) 資料行。</span><span class="sxs-lookup"><span data-stu-id="be03e-154">To determine if a view is based on correlation statistics, select the **is_date_correlation_view** column of the [sys.views](/sql/relational-databases/system-catalog-views/sys-views-transact-sql) catalog view.</span></span>  
  
  