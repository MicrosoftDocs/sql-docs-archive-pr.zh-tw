---
title: 資源管理員 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, overview
- Resource Governor
ms.assetid: 2bc89b66-e801-45ba-b30d-8ed197052212
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7660446a176b9535883a001318c8f8fc981f99c1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87699364"
---
# <a name="resource-governor"></a><span data-ttu-id="1235e-102">資源管理員</span><span class="sxs-lookup"><span data-stu-id="1235e-102">Resource Governor</span></span>
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] <span data-ttu-id="1235e-103">資源管理員是一項功能，可讓您用於管理 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 工作負載和系統資源耗用量。</span><span class="sxs-lookup"><span data-stu-id="1235e-103">Resource Governor is a feature than you can use to manage [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] workload and system resource consumption.</span></span> <span data-ttu-id="1235e-104">Resource Governor 可讓您指定內送應用程式要求所能使用的 CPU、實體 IO 和記憶體數量限制。</span><span class="sxs-lookup"><span data-stu-id="1235e-104">Resource Governor enables you to specify limits on the amount of CPU, physical IO, and memory that incoming application requests can use.</span></span>  
  
## <a name="benefits-of-resource-governor"></a><span data-ttu-id="1235e-105">資源管理員的優點</span><span class="sxs-lookup"><span data-stu-id="1235e-105">Benefits of Resource Governor</span></span>  
 <span data-ttu-id="1235e-106">資源管理員可讓您藉由指定內送要求的資源耗用量限制來管理 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 工作負載和資源。</span><span class="sxs-lookup"><span data-stu-id="1235e-106">Resource Governor enables you to manage [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] workloads and resources by specifying limits on resource consumption by incoming requests.</span></span> <span data-ttu-id="1235e-107">在「資源管理員」環境中，工作負載是一組大小類似的查詢或要求，可以也應該將其視為單一實體。</span><span class="sxs-lookup"><span data-stu-id="1235e-107">In the Resource Governor context, workload is a set of similarly sized queries or requests that can, and should be, treated as a single entity.</span></span> <span data-ttu-id="1235e-108">這不是一項規定，但是當工作負載的資源使用模式越一致時，您就可以從「資源管理員」得到更多的好處。</span><span class="sxs-lookup"><span data-stu-id="1235e-108">This is not a requirement, but the more uniform the resource usage pattern of a workload is, the more benefit you are likely to derive from Resource Governor.</span></span> <span data-ttu-id="1235e-109">可以即時重新設定資源限制，對正在執行的工作負載造成最低的影響。</span><span class="sxs-lookup"><span data-stu-id="1235e-109">Resource limits can be reconfigured in real time with minimal impact on workloads that are executing.</span></span>  
  
 <span data-ttu-id="1235e-110">在相同伺服器上有多個相異工作負載的環境中，資源管理員可讓您區分這些工作負載，並根據您指定的限制在要求的情況下配置共用資源。</span><span class="sxs-lookup"><span data-stu-id="1235e-110">In an environment where multiple distinct workloads are present on the same server, Resource Governor enables you to differentiate these workloads and allocate shared resources as they are requested, based on the limits that you specify.</span></span> <span data-ttu-id="1235e-111">這些資源是 CPU、實體 IO 和記憶體。</span><span class="sxs-lookup"><span data-stu-id="1235e-111">These resources are CPU, physical IO, and memory.</span></span>  
  
 <span data-ttu-id="1235e-112">使用資源管理員，您可以：</span><span class="sxs-lookup"><span data-stu-id="1235e-112">By using Resource Governor, you can:</span></span>  
  
-   <span data-ttu-id="1235e-113">在服務多個用戶端工作負載的 SQL Server 單一執行個體上，提供多組織用戶管理和資源隔離。</span><span class="sxs-lookup"><span data-stu-id="1235e-113">Provide multitenancy and resource isolation on single instances of SQL Server that serve multiple client workloads.</span></span> <span data-ttu-id="1235e-114">也就是說，您可以將伺服器上的可用資源分割給各工作負載，將工作負載競爭資源時所發生的問題減到最少。</span><span class="sxs-lookup"><span data-stu-id="1235e-114">That is, you can divide the available resources on a server among the workloads and minimize the problems that can occur when workloads compete for resources.</span></span>  
  
-   <span data-ttu-id="1235e-115">為多工作負載和多使用者環境中的工作負載租用戶提供可預測的效能及支援 SLA。</span><span class="sxs-lookup"><span data-stu-id="1235e-115">Provide predictable performance and support SLAs for workload tenants in a multi-workload and multi-user environment.</span></span>  
  
-   <span data-ttu-id="1235e-116">針對 DBCC CHECKDB 等會使 IO 子系統飽和以及對其他工作負載產生負面影響的作業，隔離並限制失控查詢或對 IO 資源進行節流。</span><span class="sxs-lookup"><span data-stu-id="1235e-116">Isolate and limit runaway queries or throttle IO resources for operations such as DBCC CHECKDB that can saturate the IO subsystem and negatively impact other workloads.</span></span>  
  
-   <span data-ttu-id="1235e-117">針對資源使用量交易糾紛，加入細部鎖定資源追蹤，並且為伺服器資源的取用者提供預測帳單。</span><span class="sxs-lookup"><span data-stu-id="1235e-117">Add fine-grained resource tracking for resource usage chargebacks and provide predictable billing to the consumers of the server resources.</span></span>  
  
## <a name="resource-governor-constraints"></a><span data-ttu-id="1235e-118">資源管理員條件約束</span><span class="sxs-lookup"><span data-stu-id="1235e-118">Resource Governor Constraints</span></span>  
 <span data-ttu-id="1235e-119">這一版的資源管理員有以下條件約束：</span><span class="sxs-lookup"><span data-stu-id="1235e-119">This release of Resource Governor has the following constraints:</span></span>  
  
-   <span data-ttu-id="1235e-120">資源管理受限於 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。</span><span class="sxs-lookup"><span data-stu-id="1235e-120">Resource management is limited to the [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].</span></span> <span data-ttu-id="1235e-121">「資源管理員」無法用於 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。</span><span class="sxs-lookup"><span data-stu-id="1235e-121">Resource Governor can not be used for [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], and [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].</span></span>  
  
-   <span data-ttu-id="1235e-122">在 SQL Server 執行個體之間，沒有任何工作負載監視或工作負載管理。</span><span class="sxs-lookup"><span data-stu-id="1235e-122">There is no workload monitoring or workload management between SQL Server instances.</span></span>  
  
-   <span data-ttu-id="1235e-123">資源管理員可以管理 OLTP 工作負載，但是這些類型的查詢 (通常持續時間會很短) 在 CPU 上的時間不一定都夠長而足以套用頻寬控制。</span><span class="sxs-lookup"><span data-stu-id="1235e-123">Resource Governor can manage OLTP workloads but these types of queries, which are typically very short in duration, are not always on the CPU long enough to apply bandwidth controls.</span></span> <span data-ttu-id="1235e-124">這樣可能會扭曲針對 CPU 使用量百分比傳回的統計資料。</span><span class="sxs-lookup"><span data-stu-id="1235e-124">This may skew in the statistics returned for CPU usage %.</span></span>  
  
-   <span data-ttu-id="1235e-125">管理實體 IO 的能力只適用於使用者作業，而非系統工作。</span><span class="sxs-lookup"><span data-stu-id="1235e-125">The ability to govern physical IO only applies to user operations and not system tasks.</span></span> <span data-ttu-id="1235e-126">系統工作包含交易記錄的寫入作業及延遲寫入器 IO 作業。</span><span class="sxs-lookup"><span data-stu-id="1235e-126">System tasks include write operations to the transaction log and Lazy Writer IO operations.</span></span> <span data-ttu-id="1235e-127">由於大部分寫入作業通常是由系統工作來執行，因此資源管理員主要適用於使用者讀取作業。</span><span class="sxs-lookup"><span data-stu-id="1235e-127">The Resource Govenor applies primarily to user read operations because most write operations are typically performed by system tasks.</span></span>  
  
-   <span data-ttu-id="1235e-128">您無法設定內部資源集區的 IO 臨界值。</span><span class="sxs-lookup"><span data-stu-id="1235e-128">You cannot set IO thresholds on the internal resource pool.</span></span>  
  
## <a name="resource-concepts"></a><span data-ttu-id="1235e-129">資源概念</span><span class="sxs-lookup"><span data-stu-id="1235e-129">Resource Concepts</span></span>  
 <span data-ttu-id="1235e-130">下列三個概念是了解和使用資源管理員的基礎：</span><span class="sxs-lookup"><span data-stu-id="1235e-130">The following three concepts are fundamental to understanding and using Resource Governor:</span></span>  
  
-   <span data-ttu-id="1235e-131">**資源集區。**</span><span class="sxs-lookup"><span data-stu-id="1235e-131">**Resource pools.**</span></span> <span data-ttu-id="1235e-132">資源集區代表伺服器的實體資源。</span><span class="sxs-lookup"><span data-stu-id="1235e-132">A resource pool, represents the physical resources of the server.</span></span> <span data-ttu-id="1235e-133">您可以將集區視為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體內部的虛擬 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體。</span><span class="sxs-lookup"><span data-stu-id="1235e-133">You can think of a pool as a virtual [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instance inside of a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instance.</span></span> <span data-ttu-id="1235e-134">安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時，系統會建立兩個資源集區 (內部和預設)。</span><span class="sxs-lookup"><span data-stu-id="1235e-134">Two resource pools (internal and default) are created when [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] is installed.</span></span> <span data-ttu-id="1235e-135">資源管理員也可支援使用者定義的資源集區。</span><span class="sxs-lookup"><span data-stu-id="1235e-135">Resource Governor also supports user-defined resource pools.</span></span> <span data-ttu-id="1235e-136">如需詳細資訊，請參閱 [Resource Governor Resource Pool](resource-governor-resource-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="1235e-136">For more information, see [Resource Governor Resource Pool](resource-governor-resource-pool.md).</span></span>  
  
-   <span data-ttu-id="1235e-137">**工作負載群組。**</span><span class="sxs-lookup"><span data-stu-id="1235e-137">**Workload groups.**</span></span> <span data-ttu-id="1235e-138">工作負載群組可做為有類似分類準則之工作階段要求的容器。</span><span class="sxs-lookup"><span data-stu-id="1235e-138">A workload group serves as a container for session requests that have similar classification criteria.</span></span> <span data-ttu-id="1235e-139">工作負載允許對工作階段進行彙總監視，並定義工作階段的原則。</span><span class="sxs-lookup"><span data-stu-id="1235e-139">A workload allows for aggregate monitoring of the sessions, and defines policies for the sessions.</span></span> <span data-ttu-id="1235e-140">每個工作負載群組各在一個資源集區中。</span><span class="sxs-lookup"><span data-stu-id="1235e-140">Each workload group is in a resource pool.</span></span> <span data-ttu-id="1235e-141">安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時，系統會建立兩個工作負載群組 (內部和預設)，並將其對應至相對應的資源集區。</span><span class="sxs-lookup"><span data-stu-id="1235e-141">Two workload groups (internal and default) are created and mapped to their corresponding resource pools when [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] is installed.</span></span> <span data-ttu-id="1235e-142">資源管理員也可支援使用者定義的工作負載群組。</span><span class="sxs-lookup"><span data-stu-id="1235e-142">Resource Governor also supports user-defined workload groups.</span></span> <span data-ttu-id="1235e-143">如需相關資訊，請參閱 [Resource Governor Workload Group](resource-governor-workload-group.md)。</span><span class="sxs-lookup"><span data-stu-id="1235e-143">For more information see, [Resource Governor Workload Group](resource-governor-workload-group.md).</span></span>  
  
-   <span data-ttu-id="1235e-144">**分類。**</span><span class="sxs-lookup"><span data-stu-id="1235e-144">**Classification.**</span></span> <span data-ttu-id="1235e-145">分類程序會根據工作階段的特性，將工作階段指派給工作負載群組。</span><span class="sxs-lookup"><span data-stu-id="1235e-145">The Classification process assigns incoming sessions to a workload group based on the characteristics of the session.</span></span> <span data-ttu-id="1235e-146">您可以透過撰寫使用者定義函數 (稱為分類函數) 來自訂分類邏輯。</span><span class="sxs-lookup"><span data-stu-id="1235e-146">You can tailor the classification logic by writing a user-defined function, called a classifier function.</span></span> <span data-ttu-id="1235e-147">資源管理員也可支援實作分類規則的使用者定義分類函數。</span><span class="sxs-lookup"><span data-stu-id="1235e-147">Resource Governor also supports a classifier user-defined function for implementing classification rules.</span></span> <span data-ttu-id="1235e-148">如需詳細資訊，請參閱 [Resource Governor Classifier Function](resource-governor-classifier-function.md)。</span><span class="sxs-lookup"><span data-stu-id="1235e-148">For more information, see [Resource Governor Classifier Function](resource-governor-classifier-function.md).</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="1235e-149">資源管理員不會對專用管理員連接 (DAC) 進行任何控制，</span><span class="sxs-lookup"><span data-stu-id="1235e-149">Resource Governor does not impose any controls on a dedicated administrator connection (DAC).</span></span> <span data-ttu-id="1235e-150">因為根本不需要分類在內部工作負載群組和資源集區中執行的 DAC 查詢。</span><span class="sxs-lookup"><span data-stu-id="1235e-150">There is no need to classify DAC queries, which run in the internal workload group and resource pool.</span></span>  
  
 <span data-ttu-id="1235e-151">在資源管理員的內容中，您可以將上述概念視為元件。</span><span class="sxs-lookup"><span data-stu-id="1235e-151">In the context of Resource Governor, you can treat the preceding concepts as components.</span></span> <span data-ttu-id="1235e-152">下圖將顯示這些元件以及它們在 Database Engine 環境中存在時，彼此的關聯性。</span><span class="sxs-lookup"><span data-stu-id="1235e-152">The following illustration shows these components and their relationship with each other as they exist in the database engine environment.</span></span> <span data-ttu-id="1235e-153">從處理的觀點而言，簡化的流程如下所示：</span><span class="sxs-lookup"><span data-stu-id="1235e-153">From a processing perspective, the simplified flow is as follows:</span></span>  
  
-   <span data-ttu-id="1235e-154">工作階段 (工作階段 1，共 *n*個) 的內送連接已存在。</span><span class="sxs-lookup"><span data-stu-id="1235e-154">There is an incoming connection for a session (Session 1 of *n*).</span></span>  
  
-   <span data-ttu-id="1235e-155">工作階段進行分類 (分類)。</span><span class="sxs-lookup"><span data-stu-id="1235e-155">The session is classified (Classification).</span></span>  
  
-   <span data-ttu-id="1235e-156">工作階段工作負載路由傳送至某個工作負載群組 (例如，群組 4)。</span><span class="sxs-lookup"><span data-stu-id="1235e-156">The session workload is routed to a workload group, for example, Group 4.</span></span>  
  
-   <span data-ttu-id="1235e-157">工作負載群組使用與它相關聯的資源集區 (例如，集區 2)</span><span class="sxs-lookup"><span data-stu-id="1235e-157">The workload group uses the resource pool it is associated with, for example, Pool 2.</span></span>  
  
-   <span data-ttu-id="1235e-158">資源集區提供並限制應用程式 (例如，應用程式 3) 所需的資源。</span><span class="sxs-lookup"><span data-stu-id="1235e-158">The resource pool provides and limits the resources required by the application, for example, Application 3.</span></span>  
  
 <span data-ttu-id="1235e-159">![Resource Governor 功能性元件](../../database-engine/media/rg-basic-funct-components.gif "Resource Governor 功能性元件")</span><span class="sxs-lookup"><span data-stu-id="1235e-159">![Resource Governor Functional Components](../../database-engine/media/rg-basic-funct-components.gif "Resource Governor Functional Components")</span></span>  
  
## <a name="resource-governor-tasks"></a><span data-ttu-id="1235e-160">資源管理員工作</span><span class="sxs-lookup"><span data-stu-id="1235e-160">Resource Governor Tasks</span></span>  
  
|<span data-ttu-id="1235e-161">工作描述</span><span class="sxs-lookup"><span data-stu-id="1235e-161">Task Description</span></span>|<span data-ttu-id="1235e-162">主題</span><span class="sxs-lookup"><span data-stu-id="1235e-162">Topic</span></span>|  
|----------------------|-----------|  
|<span data-ttu-id="1235e-163">描述如何啟用資源管理員。</span><span class="sxs-lookup"><span data-stu-id="1235e-163">Describes how to enable Resource Governor.</span></span>|[<span data-ttu-id="1235e-164">啟用資源管理員</span><span class="sxs-lookup"><span data-stu-id="1235e-164">Enable Resource Governor</span></span>](resource-governor.md)|  
|<span data-ttu-id="1235e-165">描述如何停用資源管理員。</span><span class="sxs-lookup"><span data-stu-id="1235e-165">Describes how to disable Resource Governor.</span></span>|[<span data-ttu-id="1235e-166">停用資源管理員</span><span class="sxs-lookup"><span data-stu-id="1235e-166">Disable Resource Governor</span></span>](disable-resource-governor.md)|  
|<span data-ttu-id="1235e-167">描述如何建立、改變和卸除資源集區。</span><span class="sxs-lookup"><span data-stu-id="1235e-167">Describes how to create, alter, and drop a resource pool.</span></span>|[<span data-ttu-id="1235e-168">資源管理員資源集區</span><span class="sxs-lookup"><span data-stu-id="1235e-168">Resource Governor Resource Pool</span></span>](resource-governor-resource-pool.md)|  
|<span data-ttu-id="1235e-169">描述如何建立、改變、移動及卸除工作負載群組。</span><span class="sxs-lookup"><span data-stu-id="1235e-169">Describes how to create, alter, move, and drop a workload group.</span></span>|[<span data-ttu-id="1235e-170">資源管理員工作負載群組</span><span class="sxs-lookup"><span data-stu-id="1235e-170">Resource Governor Workload Group</span></span>](resource-governor-workload-group.md)|  
|<span data-ttu-id="1235e-171">描述如何建立和測試分類使用者定義函數。</span><span class="sxs-lookup"><span data-stu-id="1235e-171">Describes how to create and test a classifier user-defined function.</span></span>|[<span data-ttu-id="1235e-172">資源管理員分類函數</span><span class="sxs-lookup"><span data-stu-id="1235e-172">Resource Governor Classifier Function</span></span>](resource-governor-classifier-function.md)|  
|<span data-ttu-id="1235e-173">描述如何使用範本設定資源管理員。</span><span class="sxs-lookup"><span data-stu-id="1235e-173">Describes how to configure Resource Governor using a template.</span></span>|[<span data-ttu-id="1235e-174">使用範本設定資源管理員</span><span class="sxs-lookup"><span data-stu-id="1235e-174">Configure Resource Governor Using a Template</span></span>](configure-resource-governor-using-a-template.md)|  
|<span data-ttu-id="1235e-175">描述如何檢視資源管理員的屬性。</span><span class="sxs-lookup"><span data-stu-id="1235e-175">Describes how to view Resource Governor properties.</span></span>|[<span data-ttu-id="1235e-176">檢視資源管理員屬性</span><span class="sxs-lookup"><span data-stu-id="1235e-176">View Resource Governor Properties</span></span>](view-resource-governor-properties.md)|  
  
## <a name="see-also"></a><span data-ttu-id="1235e-177">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1235e-177">See Also</span></span>  
 [<span data-ttu-id="1235e-178">Database Engine 執行個體 &#40;SQL Server&#41;</span><span class="sxs-lookup"><span data-stu-id="1235e-178">Database Engine Instances &#40;SQL Server&#41;</span></span>](../../database-engine/configure-windows/database-engine-instances-sql-server.md)  
  
  