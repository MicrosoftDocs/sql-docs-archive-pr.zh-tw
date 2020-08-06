---
title: 資料庫鏡像和複寫 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- replication [SQL Server], database mirroring and
ms.assetid: 82796217-02e2-4bc5-9ab5-218bae11a2d6
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b126aeb8ccd24932706b8798ebfe7088308918e2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705421"
---
# <a name="database-mirroring-and-replication-sql-server"></a><span data-ttu-id="c29f5-102">資料庫鏡像和複寫 (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="c29f5-102">Database Mirroring and Replication (SQL Server)</span></span>
  <span data-ttu-id="c29f5-103">資料庫鏡像可以和複寫一起使用，以改進發行集資料庫的可用性。</span><span class="sxs-lookup"><span data-stu-id="c29f5-103">Database mirroring can be used in conjunction with replication to improve availability for the publication database.</span></span> <span data-ttu-id="c29f5-104">資料庫鏡像是指單一資料庫的兩份副本，而且通常位在不同的電腦上。</span><span class="sxs-lookup"><span data-stu-id="c29f5-104">Database mirroring involves two copies of a single database that typically reside on different computers.</span></span> <span data-ttu-id="c29f5-105">在任何時間內，目前的用戶端都只能使用其中一份資料庫副本，</span><span class="sxs-lookup"><span data-stu-id="c29f5-105">At any given time, only one copy of the database is currently available to clients.</span></span> <span data-ttu-id="c29f5-106">此份資料庫稱為主體資料庫。</span><span class="sxs-lookup"><span data-stu-id="c29f5-106">This copy is known as the principal database.</span></span> <span data-ttu-id="c29f5-107">用戶端對主體資料庫所做的更新會套用到其他份資料庫，也稱為鏡像資料庫。</span><span class="sxs-lookup"><span data-stu-id="c29f5-107">Updates made by clients to the principal database are applied on the other copy of the database, known as the mirror database.</span></span> <span data-ttu-id="c29f5-108">鏡像作業涵蓋了針對主體資料庫上所進行的每個插入、更新或刪除動作，將其交易記錄套用至鏡像資料庫。</span><span class="sxs-lookup"><span data-stu-id="c29f5-108">Mirroring involves applying the transaction log from every insertion, update, or deletion made on the principal database onto the mirror database.</span></span>  
  
 <span data-ttu-id="c29f5-109">發行集資料庫完全支援複寫容錯移轉到鏡像，而散發資料庫則有限支援此功能。</span><span class="sxs-lookup"><span data-stu-id="c29f5-109">Replication failover to a mirror is fully supported for publication databases, with limited support for subscription databases.</span></span> <span data-ttu-id="c29f5-110">散發資料庫不支援資料庫鏡像。</span><span class="sxs-lookup"><span data-stu-id="c29f5-110">Database mirroring is not supported for the distribution database.</span></span> <span data-ttu-id="c29f5-111">如需復原散發資料庫或訂閱資料庫而不需要重新設定複寫的詳細資訊，請參閱 [備份及還原複寫的資料庫](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)。</span><span class="sxs-lookup"><span data-stu-id="c29f5-111">For information about recovering a distribution database or subscription database without any need to reconfigure replication, see [Back Up and Restore Replicated Databases](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md).</span></span> <span data-ttu-id="c29f5-112">如需有關訂閱者資料庫鏡像的詳細資訊，請參閱</span><span class="sxs-lookup"><span data-stu-id="c29f5-112">For information about mirroring the subscriber database, see the</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="c29f5-113">在容錯移轉之後，鏡像會成為主體。</span><span class="sxs-lookup"><span data-stu-id="c29f5-113">After a failover, the mirror becomes the principal.</span></span> <span data-ttu-id="c29f5-114">在此主題中，「主體」和「鏡像」均是指原始的主體和鏡像。</span><span class="sxs-lookup"><span data-stu-id="c29f5-114">In this topic, "principal" and "mirror" always refer to the original principal and mirror.</span></span>  
  
## <a name="requirements-and-considerations-for-using-replication-with-database-mirroring"></a><span data-ttu-id="c29f5-115">使用複寫和資料庫鏡像的需求和考量</span><span class="sxs-lookup"><span data-stu-id="c29f5-115">Requirements and Considerations for Using Replication with Database Mirroring</span></span>  
 <span data-ttu-id="c29f5-116">使用複寫和資料庫鏡像時，請注意下列需求和考量：</span><span class="sxs-lookup"><span data-stu-id="c29f5-116">Be aware of the following requirements and considerations when using replication with database mirroring:</span></span>  
  
-   <span data-ttu-id="c29f5-117">主體和鏡像必須共用「散發者」。</span><span class="sxs-lookup"><span data-stu-id="c29f5-117">The principal and mirror must share a Distributor.</span></span> <span data-ttu-id="c29f5-118">建議您使用遠端「散發者」，以在「發行者」發生未規劃的容錯移轉時提供更大的容錯能力。</span><span class="sxs-lookup"><span data-stu-id="c29f5-118">We recommend that this be a remote Distributor, which provides greater fault tolerance if the Publisher has an unplanned failover.</span></span>  
  
-   <span data-ttu-id="c29f5-119">在合併式複寫以及使用唯讀「訂閱者」或佇列更新「訂閱者」的異動複寫中，複寫可支援發行集資料庫的鏡像。</span><span class="sxs-lookup"><span data-stu-id="c29f5-119">Replication supports mirroring the publication database for merge replication and for transactional replication with read-only Subscribers or queued updating Subscribers.</span></span> <span data-ttu-id="c29f5-120">不支援立即更新「訂閱者」、「Oracle 發行者」、點對點拓撲中的「發行者」以及重新發行。</span><span class="sxs-lookup"><span data-stu-id="c29f5-120">Immediate updating Subscribers, Oracle Publishers, Publishers in a peer-to-peer topology, and republishing are not supported.</span></span>  
  
-   <span data-ttu-id="c29f5-121">存在於資料庫之外的中繼資料和物件不會複製到鏡像，包括登入、作業、連結的伺服器等等。</span><span class="sxs-lookup"><span data-stu-id="c29f5-121">Metadata and objects that exist outside the database are not copied to the mirror, including logins, jobs, linked servers, and so on.</span></span> <span data-ttu-id="c29f5-122">如果您需要在鏡像端使用這些中繼資料和物件，則必須手動加以複製。</span><span class="sxs-lookup"><span data-stu-id="c29f5-122">If you require the metadata and objects at the mirror, you must copy them manually.</span></span> <span data-ttu-id="c29f5-123">如需詳細資訊，請參閱[角色切換後針對登入和作業進行管理 &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)。</span><span class="sxs-lookup"><span data-stu-id="c29f5-123">For more information, see [Management of Logins and Jobs After Role Switching &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md).</span></span>  
  
## <a name="configuring-replication-with-database-mirroring"></a><span data-ttu-id="c29f5-124">設定複寫和資料庫鏡像</span><span class="sxs-lookup"><span data-stu-id="c29f5-124">Configuring Replication with Database Mirroring</span></span>  
 <span data-ttu-id="c29f5-125">設定複寫和資料庫鏡像包含五個步驟。</span><span class="sxs-lookup"><span data-stu-id="c29f5-125">Configuring replication and database mirroring involves five steps.</span></span> <span data-ttu-id="c29f5-126">每個步驟會在下一節中更詳細地說明。</span><span class="sxs-lookup"><span data-stu-id="c29f5-126">Each step is described in more detail in the following section.</span></span>  
  
1.  <span data-ttu-id="c29f5-127">設定「發行者」。</span><span class="sxs-lookup"><span data-stu-id="c29f5-127">Configure the Publisher.</span></span>  
  
2.  <span data-ttu-id="c29f5-128">設定資料庫鏡像。</span><span class="sxs-lookup"><span data-stu-id="c29f5-128">Configure database mirroring.</span></span>  
  
3.  <span data-ttu-id="c29f5-129">將鏡像設定為使用與主體相同的「散發者」。</span><span class="sxs-lookup"><span data-stu-id="c29f5-129">Configure the mirror to use the same Distributor as the principal.</span></span>  
  
4.  <span data-ttu-id="c29f5-130">設定用於容錯移轉的複寫代理程式。</span><span class="sxs-lookup"><span data-stu-id="c29f5-130">Configure replication agents for failover.</span></span>  
  
5.  <span data-ttu-id="c29f5-131">將主體和鏡像加入「複寫監視器」。</span><span class="sxs-lookup"><span data-stu-id="c29f5-131">Add the principal and mirror to Replication Monitor.</span></span>  
  
 <span data-ttu-id="c29f5-132">步驟 1 和 2 的執行順序可以對調。</span><span class="sxs-lookup"><span data-stu-id="c29f5-132">Steps 1 and 2 can also be performed in the opposite order.</span></span>  
  
#### <a name="to-configure-database-mirroring-for-a-publication-database"></a><span data-ttu-id="c29f5-133">設定發行集資料庫的資料庫鏡像</span><span class="sxs-lookup"><span data-stu-id="c29f5-133">To configure database mirroring for a publication database</span></span>  
  
1.  <span data-ttu-id="c29f5-134">設定「發行者」：</span><span class="sxs-lookup"><span data-stu-id="c29f5-134">Configure the Publisher:</span></span>  
  
    1.  <span data-ttu-id="c29f5-135">建議您使用遠端「散發者」。</span><span class="sxs-lookup"><span data-stu-id="c29f5-135">We recommend using a remote Distributor.</span></span> <span data-ttu-id="c29f5-136">如需設定散發的詳細資訊，請參閱 [設定散發](../../relational-databases/replication/configure-distribution.md)。</span><span class="sxs-lookup"><span data-stu-id="c29f5-136">For more information about configuring distribution, see [Configure Distribution](../../relational-databases/replication/configure-distribution.md).</span></span>  
  
    2.  <span data-ttu-id="c29f5-137">您可為快照式與交易式發行集和 (或) 合併式發行集啟用資料庫。</span><span class="sxs-lookup"><span data-stu-id="c29f5-137">You can enable a database for snapshot and transactional publications and/or merge publications.</span></span> <span data-ttu-id="c29f5-138">如果是將包含超過一種類型之發行集的鏡像資料庫，您必須使用 [sp_replicationdboption](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql)，在相同節點上為這兩種類型啟用資料庫。</span><span class="sxs-lookup"><span data-stu-id="c29f5-138">For mirrored databases that will contain more than one type of publication, you must enable the database for both types at the same node using [sp_replicationdboption](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql).</span></span> <span data-ttu-id="c29f5-139">例如，您可以在主體端執行下列預存程序呼叫：</span><span class="sxs-lookup"><span data-stu-id="c29f5-139">For example, you could execute the following stored procedure calls at the principal:</span></span>  
  
        ```  
        exec sp_replicationdboption @dbname='<PublicationDatabase>', @optname='publish', @value=true;  
        exec sp_replicationdboption @dbname='<PublicationDatabase>', @optname='mergepublish', @value=true;  
        ```  
  
         <span data-ttu-id="c29f5-140">如需建立發行集的詳細資訊，請參閱 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="c29f5-140">For more information about creating publications, see [Publish Data and Database Objects](../../relational-databases/replication/publish/publish-data-and-database-objects.md).</span></span>  
  
2.  <span data-ttu-id="c29f5-141">設定資料庫鏡像。</span><span class="sxs-lookup"><span data-stu-id="c29f5-141">Configure database mirroring.</span></span> <span data-ttu-id="c29f5-142">如需詳細資訊，請參閱[使用 Windows 驗證建立資料庫鏡像工作階段 &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md) 和[設定資料庫鏡像 &#40;SQL Server&#41;](database-mirroring-sql-server.md)。</span><span class="sxs-lookup"><span data-stu-id="c29f5-142">For more information, see [Establish a Database Mirroring Session Using Windows Authentication &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md) and [Setting Up Database Mirroring &#40;SQL Server&#41;](database-mirroring-sql-server.md).</span></span>  
  
3.  <span data-ttu-id="c29f5-143">為鏡像設定散發。</span><span class="sxs-lookup"><span data-stu-id="c29f5-143">Configure distribution for the mirror.</span></span> <span data-ttu-id="c29f5-144">將鏡像名稱指定為「發行者」，並指定主體所用的相同「散發者」和快照集資料夾。</span><span class="sxs-lookup"><span data-stu-id="c29f5-144">Specify the mirror name as the Publisher, and specify the same Distributor and snapshot folder that the principal uses.</span></span> <span data-ttu-id="c29f5-145">例如，如果您以預存程序設定複寫，請在「散發者」端執行 [sp_adddistpublisher](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql) ，然後在鏡像上執行 [sp_adddistributor](/sql/relational-databases/system-stored-procedures/sp-adddistributor-transact-sql) 。</span><span class="sxs-lookup"><span data-stu-id="c29f5-145">For example, if you are configuring replication with stored procedures, execute [sp_adddistpublisher](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql) at the Distributor; and then execute [sp_adddistributor](/sql/relational-databases/system-stored-procedures/sp-adddistributor-transact-sql) at the mirror.</span></span> <span data-ttu-id="c29f5-146">針對 **sp_adddistpublisher**：</span><span class="sxs-lookup"><span data-stu-id="c29f5-146">For **sp_adddistpublisher**:</span></span>  
  
    -   <span data-ttu-id="c29f5-147">將參數的值設定 **@publisher** 為鏡像的網路名稱。</span><span class="sxs-lookup"><span data-stu-id="c29f5-147">Set the value of the **@publisher** parameter to the network name of the mirror.</span></span>  
  
    -   <span data-ttu-id="c29f5-148">將參數的值設定 **@working_directory** 為主體所使用的快照集資料夾。</span><span class="sxs-lookup"><span data-stu-id="c29f5-148">Set the value of the **@working_directory** parameter to the snapshot folder used by the principal.</span></span>  
  
4.  <span data-ttu-id="c29f5-149">指定 **-PublisherFailoverPartner** 代理程式參數的鏡像名稱。</span><span class="sxs-lookup"><span data-stu-id="c29f5-149">Specify the mirror name for the **-PublisherFailoverPartner** agent parameter.</span></span> <span data-ttu-id="c29f5-150">下列代理程式需要使用這個參數在容錯移轉後識別鏡像：</span><span class="sxs-lookup"><span data-stu-id="c29f5-150">Agent This parameter is required for the following agents to identify the mirror after failover:</span></span>  
  
    -   <span data-ttu-id="c29f5-151">快照集代理程式 (針對所有發行集)。</span><span class="sxs-lookup"><span data-stu-id="c29f5-151">Snapshot Agent (for all publications)</span></span>  
  
    -   <span data-ttu-id="c29f5-152">記錄讀取器代理程式 (針對所有交易式發行集)</span><span class="sxs-lookup"><span data-stu-id="c29f5-152">Log Reader Agent (for all transactional publications)</span></span>  
  
    -   <span data-ttu-id="c29f5-153">佇列讀取器代理程式 (針對支援佇列更新訂閱的交易式發行集)</span><span class="sxs-lookup"><span data-stu-id="c29f5-153">Queue Reader Agent (for transactional publications that support queued updating subscriptions)</span></span>  
  
    -   <span data-ttu-id="c29f5-154">合併代理程式 (針對合併訂閱)</span><span class="sxs-lookup"><span data-stu-id="c29f5-154">Merge Agent (for merge subscriptions)</span></span>  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="c29f5-155">Replication Listener (replisapi.dll：適用於使用 Web 同步處理來進行同步處理的合併訂閱)</span><span class="sxs-lookup"><span data-stu-id="c29f5-155">replication listener (replisapi.dll: for merge subscriptions synchronized using Web synchronization)</span></span>  
  
    -   <span data-ttu-id="c29f5-156">SQL Merge ActiveX Control (針對與控制項同步處理的合併訂閱)</span><span class="sxs-lookup"><span data-stu-id="c29f5-156">SQL Merge ActiveX Control (for merge subscriptions synchronized with the control)</span></span>  
  
     <span data-ttu-id="c29f5-157">「散發代理程式」和 Distribution ActiveX Control 沒有這個參數，因為它們並未連接到「發行者」。</span><span class="sxs-lookup"><span data-stu-id="c29f5-157">The Distribution Agent and Distribution ActiveX Control do not have this parameter because they do not connect to the Publisher.</span></span>  
  
     <span data-ttu-id="c29f5-158">代理程式參數變更會在代理程式下次啟動時生效。</span><span class="sxs-lookup"><span data-stu-id="c29f5-158">Agent parameter changes take effect the next time the agent is started.</span></span> <span data-ttu-id="c29f5-159">如果代理程式連續執行，則必須停止代理程式，然後重新啟動它。</span><span class="sxs-lookup"><span data-stu-id="c29f5-159">If the agent runs continuously, you must stop and restart the agent.</span></span> <span data-ttu-id="c29f5-160">您可以在代理程式設定檔中或從命令提示字元指定參數。</span><span class="sxs-lookup"><span data-stu-id="c29f5-160">Parameters can be specified in agent profiles and from the command prompt.</span></span> <span data-ttu-id="c29f5-161">如需詳細資訊，請參閱</span><span class="sxs-lookup"><span data-stu-id="c29f5-161">For more information, see:</span></span>  
  
    -   [<span data-ttu-id="c29f5-162">檢視並修改複寫代理程式命令提示字元參數 &#40;SQL Server Management Studio&#41;</span><span class="sxs-lookup"><span data-stu-id="c29f5-162">View and Modify Replication Agent Command Prompt Parameters &#40;SQL Server Management Studio&#41;</span></span>](../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [<span data-ttu-id="c29f5-163">Replication Agent Executables Concepts</span><span class="sxs-lookup"><span data-stu-id="c29f5-163">Replication Agent Executables Concepts</span></span>](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
     <span data-ttu-id="c29f5-164">建議您將 **-PublisherFailoverPartner** 加入代理程式設定檔，然後在設定檔中指定鏡像名稱。</span><span class="sxs-lookup"><span data-stu-id="c29f5-164">We recommend adding the **-PublisherFailoverPartner** to an agent profile, and then specifying the mirror name in the profile.</span></span> <span data-ttu-id="c29f5-165">例如，如果您要設定使用預存程序的複寫：</span><span class="sxs-lookup"><span data-stu-id="c29f5-165">For example, if you are configuring replication with stored procedures:</span></span>  
  
    ```  
    -- Execute sp_help_agent_profile in the context of the distribution database to get the list of profiles.  
    -- Select the profile id of the profile that needs to be updated from the result set.  
    -- In the agent_type column returned by sp_help_agent_profile:   
    -- 1 = Snapshot Agent; 2 = Log Reader Agent; 3 = Distribution Agent; 4 = Merge Agent; 9 = Queue Reader Agent.  
  
    exec sp_help_agent_profile;  
  
    -- Setting the -PublisherFailoverPartner parameter in the default Snapshot Agent profile (profile 1).  
    -- Execute sp_add_agent_parameter in the context of the distribution database.  
    exec sp_add_agent_parameter @profile_id = 1, @parameter_name = N'-PublisherFailoverPartner', @parameter_value = N'<Failover Partner Name>';  
  
    -- Setting the -PublisherFailoverPartner parameter in the default Merge Agent profile (profile 6).  
    -- Execute sp_add_agent_parameter in the context of the distribution database.  
    exec sp_add_agent_parameter @profile_id = 6, @parameter_name = N'-PublisherFailoverPartner', @parameter_value = N'<Failover Partner Name>';  
    ```  
  
5.  <span data-ttu-id="c29f5-166">將主體和鏡像加入「複寫監視器」。</span><span class="sxs-lookup"><span data-stu-id="c29f5-166">Add the principal and mirror to Replication Monitor.</span></span> <span data-ttu-id="c29f5-167">如需詳細資訊，請參閱 [從複寫監視器加入及移除發行者](../../relational-databases/replication/monitor/add-and-remove-publishers-from-replication-monitor.md)。</span><span class="sxs-lookup"><span data-stu-id="c29f5-167">For more information, see [Add and Remove Publishers from Replication Monitor](../../relational-databases/replication/monitor/add-and-remove-publishers-from-replication-monitor.md).</span></span>  
  
## <a name="maintaining-a-mirrored-publication-database"></a><span data-ttu-id="c29f5-168">維護鏡像發行集資料庫</span><span class="sxs-lookup"><span data-stu-id="c29f5-168">Maintaining a Mirrored Publication Database</span></span>  
 <span data-ttu-id="c29f5-169">維護鏡像發行集資料庫基本上與維護非鏡像資料庫相同，不過請注意下列事項：</span><span class="sxs-lookup"><span data-stu-id="c29f5-169">Maintaining a mirrored publication database is essentially the same as maintaining a non-mirrored database, with the following considerations:</span></span>  
  
-   <span data-ttu-id="c29f5-170">管理和監視必須在使用中伺服器端發生。</span><span class="sxs-lookup"><span data-stu-id="c29f5-170">Administration and monitoring must occur at the active server.</span></span> <span data-ttu-id="c29f5-171">在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，發行集只會出現在使用中伺服器的 [本機發行集] 資料夾下。</span><span class="sxs-lookup"><span data-stu-id="c29f5-171">In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], publications appear under the **Local Publications** folder only for the active server.</span></span> <span data-ttu-id="c29f5-172">例如，如果您容錯移轉至鏡像，則發行集會在鏡像端顯示，而不會再顯示於主體端。</span><span class="sxs-lookup"><span data-stu-id="c29f5-172">For example, if you failover to the mirror, the publications are displayed at the mirror and are no longer displayed at the principal.</span></span> <span data-ttu-id="c29f5-173">如果資料庫容錯移轉至鏡像，您可能需要手動重新整理 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 和複寫監視器，才能反映出變更。</span><span class="sxs-lookup"><span data-stu-id="c29f5-173">If the database fails over to the mirror, you might need to manually refresh [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] and Replication Monitor for the change to be reflected.</span></span>  
  
-   <span data-ttu-id="c29f5-174">複寫監視器會同時在主體和鏡像的物件樹中顯示「發行者」節點。</span><span class="sxs-lookup"><span data-stu-id="c29f5-174">Replication Monitor displays Publisher nodes in the object tree for both the principal and the mirror.</span></span> <span data-ttu-id="c29f5-175">如果主體為使用中伺服器，則發行集資訊只會顯示在「複寫監視器」的主體節點下。</span><span class="sxs-lookup"><span data-stu-id="c29f5-175">If the principal is the active server, publication information is displayed only under the principal node in Replication Monitor.</span></span>  
  
     <span data-ttu-id="c29f5-176">如果鏡像是使用中伺服器：</span><span class="sxs-lookup"><span data-stu-id="c29f5-176">If the mirror is the active server:</span></span>  
  
    -   <span data-ttu-id="c29f5-177">如果代理程式發生錯誤，錯誤只會在主體節點上指出，在鏡像節點上則不會。</span><span class="sxs-lookup"><span data-stu-id="c29f5-177">If an agent has an error, the error is indicated only on the principal node, not on the mirror node.</span></span>  
  
    -   <span data-ttu-id="c29f5-178">如果主體無法使用，則主體和鏡像節點會顯示相同的發行集清單。</span><span class="sxs-lookup"><span data-stu-id="c29f5-178">If the principal is unavailable, the principal and mirror nodes display identical lists of publications.</span></span> <span data-ttu-id="c29f5-179">監視應在鏡像節點下的發行集上執行。</span><span class="sxs-lookup"><span data-stu-id="c29f5-179">Monitoring should be performed on the publications under the mirror node.</span></span>  
  
-   <span data-ttu-id="c29f5-180">當使用預存程序或 Replication Management Objects (RMO) 在鏡像端管理複寫時，在您指定「發行者」名稱的情況下，您必須指定在其上啟用資料庫以供複寫的執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="c29f5-180">When using stored procedures or Replication Management Objects (RMO) to administer replication at the mirror, for cases in which you specify the Publisher name, you must specify the name of the instance on which the database was enabled for replication.</span></span> <span data-ttu-id="c29f5-181">若要決定適當的名稱，請使用 [publishingservername](/sql/t-sql/functions/replication-functions-publishingservername)函數。</span><span class="sxs-lookup"><span data-stu-id="c29f5-181">To determine the appropriate name, use the function [publishingservername](/sql/t-sql/functions/replication-functions-publishingservername).</span></span>  
  
     <span data-ttu-id="c29f5-182">在完成發行集資料庫的鏡像後，儲存在鏡像資料庫中的複寫中繼資料會與儲存在主體資料庫中的中繼資料相同。</span><span class="sxs-lookup"><span data-stu-id="c29f5-182">When a publication database is mirrored, the replication metadata stored in the mirrored database is identical to the metadata stored in the principal database.</span></span> <span data-ttu-id="c29f5-183">因此，對於在主體端啟用以供複寫的發行集資料庫而言，儲存在鏡像端系統資料表中的「發行者」執行個體名稱是主體的名稱，而不是鏡像的名稱。</span><span class="sxs-lookup"><span data-stu-id="c29f5-183">Consequently, for publication databases enabled for replication at the principal, the Publisher instance name stored in system tables at the mirror is the name of the principal, not the mirror.</span></span> <span data-ttu-id="c29f5-184">如果發行集資料庫容錯移轉至鏡像，這會影響複寫組態和維護。</span><span class="sxs-lookup"><span data-stu-id="c29f5-184">This affects replication configuration and maintenance if the publication database fails over to the mirror.</span></span> <span data-ttu-id="c29f5-185">例如，如果您要在容錯移轉之後使用鏡像上的預存程式來設定複寫，而且您想要將提取訂閱加入在主體上啟用的發行集資料庫，則必須指定主體名稱，而不是 **@publisher** **sp_addpullsubscription**或**sp_addmergepullsubscription**參數的鏡像名稱。</span><span class="sxs-lookup"><span data-stu-id="c29f5-185">For example, if you are configuring replication with stored procedures on the mirror after a failover, and you want to add a pull subscription to a publication database that was enabled at the principal, you must specify the principal name rather than the mirror name for the **@publisher** parameter of **sp_addpullsubscription** or **sp_addmergepullsubscription**.</span></span>  
  
     <span data-ttu-id="c29f5-186">如果您在容錯移轉至鏡像後於鏡像端啟用發行集資料庫，則儲存在系統資料表中的「發行者」實例名稱是鏡像的名稱;在此情況下，您會使用參數的鏡像名稱 **@publisher** 。</span><span class="sxs-lookup"><span data-stu-id="c29f5-186">If you enable a publication database at the mirror after failover to the mirror, the Publisher instance name stored in system tables is the name of the mirror; in this case, you would use the name of the mirror for the **@publisher** parameter.</span></span>  
  
    > [!NOTE]  
    >  <span data-ttu-id="c29f5-187">在某些情況下 (例如 **sp_addpublication**)，只有非 **@publisher** @publisher[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 參數，此時，該參數便與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫鏡像不相關。</span><span class="sxs-lookup"><span data-stu-id="c29f5-187">In some cases, such as **sp_addpublication**, the **@publisher** parameter is supported only for non-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publishers; in these cases, it is not relevant for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database mirroring.</span></span>  
  
-   <span data-ttu-id="c29f5-188">若要在容錯移轉後同步處理 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的訂閱，請從「訂閱者」同步處理提取訂閱，並從使用中「發行者」同步處理發送訂閱。</span><span class="sxs-lookup"><span data-stu-id="c29f5-188">To synchronize a subscription in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] after a failover: synchronize pull subscriptions from the Subscriber; and synchronize push subscriptions from the active Publisher.</span></span>  
  
### <a name="replication-behavior-if-mirroring-is-removed"></a><span data-ttu-id="c29f5-189">移除鏡像時的複寫行為</span><span class="sxs-lookup"><span data-stu-id="c29f5-189">Replication Behavior if Mirroring is Removed</span></span>  
 <span data-ttu-id="c29f5-190">從發行的資料庫移除資料庫鏡像時，請注意下列幾個問題：</span><span class="sxs-lookup"><span data-stu-id="c29f5-190">Keep the following issues in mind if database mirroring is removed from a published database:</span></span>  
  
-   <span data-ttu-id="c29f5-191">如果已不再鏡像主體端的發行集資料庫，則複寫作業仍會對原始主體維持相同的運作。</span><span class="sxs-lookup"><span data-stu-id="c29f5-191">If the publication database at the principal is no longer mirrored, replication continues to work unchanged against the original principal.</span></span>  
  
-   <span data-ttu-id="c29f5-192">如果發行集資料庫從主體容錯移轉至鏡像，且鏡像關聯性隨後被停用或移除，則複寫代理程式將不會對鏡像發生作用。</span><span class="sxs-lookup"><span data-stu-id="c29f5-192">If the publication database fails over from the principal to the mirror and the mirroring relationship is subsequently disabled or removed, replication agents will not function against the mirror.</span></span> <span data-ttu-id="c29f5-193">如果主體永久遺失，請停用複寫，然後以指定為「發行者」的鏡像重新設定複寫。</span><span class="sxs-lookup"><span data-stu-id="c29f5-193">If the principal is permanently lost, disable and then reconfigure replication with the mirror specified as the Publisher.</span></span>  
  
-   <span data-ttu-id="c29f5-194">如果完全移除資料庫鏡像，則鏡像資料庫會處於復原狀態，且必須還原該資料庫才能使其正常運作。</span><span class="sxs-lookup"><span data-stu-id="c29f5-194">If database mirroring is removed completely, the mirror database is in a recovery state and must be restored in order to become functional.</span></span> <span data-ttu-id="c29f5-195">復原的資料庫在複寫方面的行為取決於是否已指定 KEEP_REPLICATION 選項。</span><span class="sxs-lookup"><span data-stu-id="c29f5-195">The behavior of the recovered database with respect to replication depends on whether the KEEP_REPLICATION option is specified.</span></span> <span data-ttu-id="c29f5-196">當還原發行的資料庫至某伺服器而非建立備份的伺服器時，此選項會強制還原作業保留複寫設定。</span><span class="sxs-lookup"><span data-stu-id="c29f5-196">This option forces the restore operation to preserve replication settings when restoring a published database to a server other than that on which the backup was created.</span></span> <span data-ttu-id="c29f5-197">只有在無法使用其他發行集資料庫時，才應該使用 KEEP_REPLICATION 選項。</span><span class="sxs-lookup"><span data-stu-id="c29f5-197">Use the KEEP_REPLICATION option only when the other publication database is unavailable.</span></span> <span data-ttu-id="c29f5-198">如果其他發行集資料庫仍然完整且複寫中，則不支援此選項。</span><span class="sxs-lookup"><span data-stu-id="c29f5-198">The option is not supported if the other publication database is still intact and replicating.</span></span> <span data-ttu-id="c29f5-199">如需 KEEP_REPLICATION 的詳細資訊，請參閱 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="c29f5-199">For more information about KEEP_REPLICATION, see [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).</span></span>  
  
## <a name="log-reader-agent-behavior"></a><span data-ttu-id="c29f5-200">記錄讀取器代理程式行為</span><span class="sxs-lookup"><span data-stu-id="c29f5-200">Log Reader Agent Behavior</span></span>  
 <span data-ttu-id="c29f5-201">下表描述資料庫鏡像的各種作業模式之「記錄讀取器代理程式」行為。</span><span class="sxs-lookup"><span data-stu-id="c29f5-201">The following table describes Log Reader Agent behavior for the various operating modes of database mirroring.</span></span>  
  
|<span data-ttu-id="c29f5-202">作業模式</span><span class="sxs-lookup"><span data-stu-id="c29f5-202">Operating mode</span></span>|<span data-ttu-id="c29f5-203">鏡像無法使用時的記錄讀取器代理程式行為</span><span class="sxs-lookup"><span data-stu-id="c29f5-203">Log Reader Agent behavior if the mirror is unavailable</span></span>|  
|--------------------|------------------------------------------------------------|  
|<span data-ttu-id="c29f5-204">具有自動容錯移轉的高安全性模式</span><span class="sxs-lookup"><span data-stu-id="c29f5-204">High-safety mode with automatic failover</span></span>|<span data-ttu-id="c29f5-205">如果鏡像無法使用，則「記錄讀取器代理程式」會傳播命令至散發資料庫。</span><span class="sxs-lookup"><span data-stu-id="c29f5-205">If the mirror is unavailable, the Log Reader Agent propagates commands to the distribution database.</span></span> <span data-ttu-id="c29f5-206">待鏡像回復連接，且具備主體的所有交易後，主體才能容錯移轉至鏡像。</span><span class="sxs-lookup"><span data-stu-id="c29f5-206">The principal cannot failover to the mirror until the mirror is back online and has all transactions from the principal.</span></span>|  
|<span data-ttu-id="c29f5-207">高效能模式</span><span class="sxs-lookup"><span data-stu-id="c29f5-207">High-performance mode</span></span>|<span data-ttu-id="c29f5-208">如果鏡像無法使用，則主體資料庫會以公開方式執行 (也就是沒有鏡像)。</span><span class="sxs-lookup"><span data-stu-id="c29f5-208">If the mirror is unavailable, the principal database is running exposed (that is, unmirrored).</span></span> <span data-ttu-id="c29f5-209">不過，「記錄讀取器代理程式」只會複寫鏡像上所儲存的交易。</span><span class="sxs-lookup"><span data-stu-id="c29f5-209">However, the Log Reader Agent only replicates those transactions that are hardened on the mirror.</span></span> <span data-ttu-id="c29f5-210">如果強制執行服務，且鏡像伺服器承擔主體的角色，則「記錄讀取器代理程式」會對鏡像發生作用，並開始收取新的交易。</span><span class="sxs-lookup"><span data-stu-id="c29f5-210">If service is forced and the mirror server assumes the role of the principal, the Log Reader Agent will work against the mirror and start picking up the new transactions.</span></span><br /><br /> <span data-ttu-id="c29f5-211">請注意，如果鏡像落後主體，則複寫延遲將會增加。</span><span class="sxs-lookup"><span data-stu-id="c29f5-211">Be aware that replication latency will increase if the mirror falls behind the principal.</span></span>|  
|<span data-ttu-id="c29f5-212">不具有自動容錯移轉的高安全性模式</span><span class="sxs-lookup"><span data-stu-id="c29f5-212">High-safety mode without automatic failover</span></span>|<span data-ttu-id="c29f5-213">所有經過認可的交易一定會存到鏡像的磁碟上。</span><span class="sxs-lookup"><span data-stu-id="c29f5-213">All committed transactions are guaranteed to be hardened to disk on the mirror.</span></span> <span data-ttu-id="c29f5-214">「記錄讀取器代理程式」只會複寫在鏡像上強化的交易。</span><span class="sxs-lookup"><span data-stu-id="c29f5-214">The Log Reader Agent replicates only those transactions that are hardened on the mirror.</span></span> <span data-ttu-id="c29f5-215">如果鏡像無法使用，則主體不會允許在資料庫上有進一步的活動；因此，「記錄讀取器代理程式」便沒有交易可複寫。</span><span class="sxs-lookup"><span data-stu-id="c29f5-215">If the mirror is unavailable, the principal disallows further activity in the database; therefore the Log Reader Agent has no transactions to replicate.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="c29f5-216">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c29f5-216">See Also</span></span>  
 <span data-ttu-id="c29f5-217">[SQL Server 複寫](../../relational-databases/replication/sql-server-replication.md) </span><span class="sxs-lookup"><span data-stu-id="c29f5-217">[SQL Server Replication](../../relational-databases/replication/sql-server-replication.md) </span></span>  
 [<span data-ttu-id="c29f5-218">記錄傳送和複寫 &#40;SQL Server&#41;</span><span class="sxs-lookup"><span data-stu-id="c29f5-218">Log Shipping and Replication &#40;SQL Server&#41;</span></span>](../log-shipping/log-shipping-and-replication-sql-server.md)  
  
  