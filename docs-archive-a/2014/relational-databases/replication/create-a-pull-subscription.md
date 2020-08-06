---
title: 建立提取訂閱 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- pull subscriptions [SQL Server replication], creating
- merge replication subscribing [SQL Server replication], pull subscriptions
- subscriptions [SQL Server replication], pull
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: 41d1886d-59c9-41fc-9bd6-a59b40e0af6e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 12ef7d658496c0fb7281827259e8e46f0c5fac64
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87607375"
---
# <a name="create-a-pull-subscription"></a>建立提取訂閱
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立提取訂閱。  
  
 為 P2P 複寫設定提取訂閱可透過指令碼來進行，但無法透過精靈進行。  
  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 使用「新增訂閱精靈」在「發行者」或「訂閱者」端建立提取訂閱。 依照精靈中各頁面進行：  
  
-   指定發行者和發行集。  
  
-   選取要執行複寫代理程式的位置。 對於提取訂閱，根據發行集類型在 **[散發代理程式位置]** 頁面或 **[合併代理程式位置]** 頁面上選取 **[在訂閱者端執行每一個代理程式 (提取訂閱)]** 。  
  
-   指定訂閱者與訂閱資料庫。  
  
-   指定複寫代理程式要連接用的登入和密碼：  
  
    -   針對快照集和交易式發行集的訂閱，請於 **[散發代理程式安全性]** 頁面指定認證。  
  
    -   針對合併式發行集的訂閱，請於 **[合併代理程式安全性]** 頁面指定認證。  
  
     如需有關各代理程式需要的權限資訊，請參閱＜ [複寫代理程式安全性模型](security/replication-agent-security-model.md)＞。  
  
-   指定同步處理排程，以及訂閱者要初始化的時間。  
  
-   指定合併式發行集的其他選項：訂閱類型；參數化篩選的值；以及如果針對 Web 同步處理啟用該發行集時，透過 HTTPS 同步處理的資訊。  
  
-   為交易式發行集指定其他選項，以允許更新訂閱：訂閱者是否應立即在發行者端認可變更，或者應寫入佇列；認證用來連接訂閱者和發行者。  
  
-   選擇性的編寫訂閱指令碼。  
  
#### <a name="to-create-a-pull-subscription-from-the-publisher"></a>若要從發行者建立提取訂閱  
  
1.  連線到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要建立一個或多個訂閱的發行集，然後按一下 **[新增訂閱]** 。  
  
4.  在新增訂閱精靈中完成頁面。  
  
#### <a name="to-create-a-pull-subscription-from-the-subscriber"></a>若要從訂閱者建立提取訂閱  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的訂閱者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾。  
  
3.  以滑鼠右鍵按一下 **[區域訂閱]** 資料夾，然後按一下 **[新增訂閱]** 。  
  
4.  在 [新增訂閱] 精靈的 [發行集] 頁面上，從 [發行者] 下拉式清單中選取 [\<Find SQL Server Publisher>] 或 [\<Find Oracle Publisher>]。  
  
5.  連接到 **[連接到伺服器]** 對話方塊中的發行者。  
  
6.  選取 **[發行集]** 頁面上的發行集。  
  
7.  在新增訂閱精靈中完成頁面。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序以程式設計的方式建立提取訂閱。 使用哪些預存程序要依訂閱所屬的發行集類型而定。  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>若要建立快照式或交易式發行集的提取訂閱  
  
1.  在發行者端，執行 [sp_helppublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql) 來確認發行集可支援提取訂閱。  
  
    -   如果結果集中 **allow_pull** 的值為 **1**，則發行集支援提取訂閱。  
  
    -   如果**allow_pull**的值為**0**，請執行[sp_changepublication &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)，並針對指定**allow_pull** **@property** `true` **@value** 。  
  
2.  在訂閱者端，執行 [sp_addpullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql)。 指定 **@publisher** 和 **@publication** 。 如需有關更新訂閱的詳細資訊，請參閱＜ [建立交易式發行集的可更新訂閱](publish/create-an-updatable-subscription-to-a-transactional-publication.md)＞。  
  
3.  在訂閱者端，執行 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)。 指定下列項目：  
  
    -   **@publisher**、 **@publisher_db** 和 **@publication** 參數。  
  
    -   在「 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 訂閱者」端用來執行和之散發代理程式的 Windows 認證 **@job_login** **@job_password** 。  
  
        > [!NOTE]  
        >  使用「Windows 整合式驗證」建立的連接一律使用由和指定的 Windows 認證 **@job_login** **@job_password** 。 散發代理程式一律使用「Windows 整合式驗證」建立與訂閱者的本機連接。 依預設，代理程式會使用「Windows 整合式驗證」連接到「散發者」。  
  
    -   (選擇性) **0** 指定為 **@distributor_security_mode** ，以及 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 **@distributor_login** ，並將 **@distributor_password**登入資訊 (如果您在連接到散發者時需要使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證」)。  
  
    -   此訂閱之散發代理程式作業的排程。 如需詳細資訊，請參閱 [Specify Synchronization Schedules](specify-synchronization-schedules.md)。  
  
4.  在發行者端，執行 [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) 來註冊提取訂閱。 指定 **@publication** 、 **@subscriber** 和 **@destination_db** 。 為 **@subscription_type** 指定為 **@subscription_type**＞。  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication"></a>若要建立合併式發行集的提取訂閱  
  
1.  在發行者端，執行 [sp_helpmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql) 來確認發行集可支援提取訂閱。  
  
    -   如果結果集中 **allow_pull** 的值為 **1**，則發行集支援提取訂閱。  
  
    -   如果**allow_pull**的值為**0**，請執行[sp_changemergepublication &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)，並針對指定**allow_pull** **@property** `true` **@value** 。  
  
2.  在訂閱者端，執行 [sp_addmergepullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql)。 指定 **@publisher** 、 **@publisher_db** 、 **@publication** 和下列參數：  
  
    -   **@subscriber_type**-針對 [用戶端訂閱] 指定 [**本機**]，針對 [伺服器訂閱] 指定 [**全域**]。  
  
    -   **@subscription_priority**-指定訂用帳戶的優先順序 (**0.00**到**99.99**) 。 只需要對主訂閱執行此動作。  
  
         如需詳細資訊，請參閱 [進階合併式複寫衝突偵測與解決](merge/advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
3.  在訂閱者端，執行 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)。 指定下列參數：  
  
    -   **@publisher**、 **@publisher_db** 和 **@publication** 。  
  
    -   在「訂閱者」端用來執行和之合併代理程式的 Windows 認證 **@job_login** **@job_password** 。  
  
        > [!NOTE]  
        >  使用「Windows 整合式驗證」建立的連接一律使用由和指定的 Windows 認證 **@job_login** **@job_password** 。 「合併代理程式」一律使用「Windows 整合式驗證」建立到「訂閱者」的本機連接。 依預設，代理程式會使用「Windows 整合式驗證」連接到「發行者」。  
  
    -   (選擇性) **0** 指定為 **@distributor_security_mode** ，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 **@distributor_login** ，並將 **@distributor_password**登入資訊 (如果您在連接到散發者時需要使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證」)。  
  
    -   (選擇性) **0** 指定為 **@publisher_security_mode** ，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 **@publisher_login** ，並將 **@publisher_password**登入資訊 (如果您在連接到散發者時需要使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證」)。  
  
    -   此訂閱之「合併代理程式」作業的排程。 如需詳細資訊，請參閱 [建立交易式發行集的可更新訂閱](publish/create-an-updatable-subscription-to-a-transactional-publication.md)。  
  
4.  在發行者端，執行 [sp_addmergesubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql)。 指定 **@publication** 、 **@subscriber** 、 **@subscriber_db** 和的**pull**值 **@subscription_type** 。 如此會註冊提取訂閱。  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> 範例 (Transact-SQL)  
 下列範例會建立交易式發行集的提取訂閱。 第一批次在「訂閱者」上執行，而第二批次在「發行者」上執行。 登入和密碼值是在執行階段使用 sqlcmd 指令碼變數提供的。  
  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpullsub.sql#sp_addtranpullsubscriptionagent)]  
  
 [!code-sql[HowTo#sp_addtranpullsubscription](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpullsub.sql#sp_addtranpullsubscription)]  
  
 下列範例會建立合併式發行集的提取訂閱。 第一批次在「訂閱者」上執行，而第二批次在「發行者」上執行。 登入和密碼值是在執行階段使用 **sqlcmd** 指令碼變數所提供。  
  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsub.sql#sp_addmergepullsubscriptionagent)]  
  
 [!code-sql[HowTo#sp_addmergepullsubscription](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsub.sql#sp_addmergepullsubscription)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 用於建立提取訂閱的 RMO 類別依該訂閱所屬的發行集類型而定。  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>若要建立快照式或交易式發行集的提取訂閱  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與訂閱者和發行者的連接。  
  
2.  使用步驟 1 中的發行者連接建立 <xref:Microsoft.SqlServer.Replication.TransPublication> 類別的執行個體。 指定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 和 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果這個方法傳回 `false`，則表示步驟 2 中指定的屬性不正確，或伺服器上沒有該發行集存在。  
  
4.  在 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 屬性和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull> 之間執行位元運算邏輯 AND (Visual C# 中的 `&` 和 Visual Basic 中的 `And`)。 如果結果為 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>，則將 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 設為 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull> 之間位元運算邏輯 OR (Visual C# 中的 `|` 和 Visual Basic 中的 `Or`) 的結果。 然後呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 以啟用提取訂閱。  
  
5.  如果訂閱資料庫不存在，可使用 <xref:Microsoft.SqlServer.Management.Smo.Database> 類別建立它。 如需詳細資訊，請參閱[建立、改變和移除資料庫](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)。  
  
6.  建立 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 類別的執行個體。  
  
7.  設定下列訂閱屬性：  
  
    -   將 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 設為到步驟 1 中建立之「訂閱者」的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>設為訂閱資料庫的名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>設為「發行者」的名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>設為發行集資料庫的名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>設為發行集的名稱。  
  
    -   <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 的 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> (或 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>) 欄位，為「散發代理程式」在「訂閱者」上執行時所使用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶提供認證。 此帳戶用於建立到「訂閱者」的本機連接，以及使用「Windows 驗證」建立遠端連接。  
  
        > [!NOTE]  
        >  當訂閱是由 `sysadmin` 固定伺服器角色的成員建立時，不需要設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>，但還是建議您對其進行設定。 在這種情況下，代理程式會模擬「SQL Server Agent」帳戶。 如需詳細資訊，請參閱 [複寫代理程式安全性模型](security/replication-agent-security-model.md)。  
  
    -   (選擇性) <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> 的 `true` 值，以建立用於同步處理訂閱的代理程式作業。 如果指定 `false` (預設值)，則只能以程式設計的方式同步處理訂閱，而且您在從 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> 屬性存取此物件時必須指定其他屬性 <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A>。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md)。  
  
        > [!NOTE]  
        >  並非所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本都可使用 SQL Server Agent。 如需版本支援的功能清單 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請參閱[SQL Server 2014 版本支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。 當您為 Express 訂閱者指定值 `true` 時，不會建立代理程式作業。 不過，在「訂閱者」上會儲存重要的訂閱相關中繼資料。  
  
    -   (選擇性) 在使用「SQL Server 驗證」連接到「散發者」時，設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 的 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (或 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> ) 欄位。  
  
8.  呼叫 <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> 方法。  
  
9. 使用步驟 2 中 <xref:Microsoft.SqlServer.Replication.TransPublication> 類別的執行個體，呼叫 <xref:Microsoft.SqlServer.Replication.TransPublication.MakePullSubscriptionWellKnown%2A> 方法，以使用「發行者」註冊提取訂閱。 如果此註冊已存在，則會發生例外狀況。  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication"></a>若要建立合併式發行集的提取訂閱  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立到「訂閱者」和「發行者」的連接。  
  
2.  使用步驟 1 中的發行者連接建立 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別的執行個體。 指定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>和 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果這個方法傳回 `false`，則表示步驟 2 中指定的屬性不正確，或伺服器上沒有該發行集存在。  
  
4.  在 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 屬性和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull> 之間執行位元運算邏輯 AND (Visual C# 中的 `&` 和 Visual Basic 中的 `And`)。 如果結果為 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>，則將 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 設為 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull> 之間位元運算邏輯 OR (Visual C# 中的 `|` 和 Visual Basic 中的 `Or`) 的結果。 然後呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 以啟用提取訂閱。  
  
5.  如果訂閱資料庫不存在，可使用 <xref:Microsoft.SqlServer.Management.Smo.Database> 類別建立它。 如需詳細資訊，請參閱[建立、改變和移除資料庫](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)。  
  
6.  建立 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 類別的執行個體。  
  
7.  設定下列訂閱屬性：  
  
    -   將 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 設為到步驟 1 中建立之「訂閱者」的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>設為訂閱資料庫的名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>設為「發行者」的名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>設為發行集資料庫的名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>設為發行集的名稱。  
  
    -   <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 的 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> (或 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>) 欄位，為「合併代理程式」在「訂閱者」上執行時所使用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶提供認證。 此帳戶用於建立到「訂閱者」的本機連接，以及使用「Windows 驗證」建立遠端連接。  
  
        > [!NOTE]  
        >  當訂閱是由 `sysadmin` 固定伺服器角色的成員建立時，不需要設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>，但還是建議您對其進行設定。 在這種情況下，代理程式會模擬「SQL Server Agent」帳戶。 如需詳細資訊，請參閱 [複寫代理程式安全性模型](security/replication-agent-security-model.md)。  
  
    -   (選擇性) <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> 的 `true` 值，以建立用於同步處理訂閱的代理程式作業。 如果指定 `false` (預設值)，則只能以程式設計的方式同步處理訂閱，而且您在從 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> 屬性存取此物件時必須指定其他屬性 <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A>。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md)。  
  
    -   (選擇性) 在使用「SQL Server 驗證」連接到「散發者」時，設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 的 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (或 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> ) 欄位。  
  
    -   (選擇性) 在使用「SQL Server 驗證」連接到「發行者」時，設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 的 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (或 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> ) 欄位。  
  
8.  呼叫 <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> 方法。  
  
9. 使用步驟 2 中 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別的執行個體，呼叫 <xref:Microsoft.SqlServer.Replication.MergePublication.MakePullSubscriptionWellKnown%2A> 方法，以使用「發行者」註冊提取訂閱。 如果此註冊已存在，則會發生例外狀況。  
  
###  <a name="example-rmo"></a><a name="PShellExample"></a> 範例 (RMO)  
 此範例會建立交易式發行集的提取訂閱。 用於建立「散發代理程式」作業的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶認證是在執行階段傳遞的。  
  
 [!code-csharp[HowTo#rmo_CreateTranPullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createtranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createtranpullsub)]  
  
 此範例會建立合併式發行集的提取訂閱。 用於建立「合併代理程式」作業的 Windows 帳戶認證是在執行階段傳遞的。  
  
 [!code-csharp[HowTo#rmo_CreateMergePullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepullsub)]  
  
 此範例會建立合併式發行集的提取訂閱，而不會在 [MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql)中建立相關聯的代理程式作業和訂閱中繼資料。 用於建立「合併代理程式」作業的 Windows 帳戶認證是在執行階段傳遞的。  
  
 [!code-csharp[HowTo#rmo_CreateMergePullSub_NoJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepullsub_nojob)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePullSub_NoJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepullsub_nojob)]  
  
 此範例會建立合併式發行集的提取訂閱，使用 Web 同步處理可以從網際網路對其進行同步處理。 用於建立「合併代理程式」作業的 Windows 帳戶認證是在執行階段傳遞的。 如需詳細資訊，請參閱 [Configure Web Synchronization](configure-web-synchronization.md)。  
  
 [!code-csharp[HowTo#rmo_CreateMergePullSub_WebSync](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepullsub_websync)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePullSub_WebSync](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepullsub_websync)]  
  
## <a name="see-also"></a>另請參閱  
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [檢視及修改提取訂閱屬性](view-and-modify-pull-subscription-properties.md)   
 [Configure Web Synchronization](configure-web-synchronization.md)   
 [Subscribe to Publications](subscribe-to-publications.md)   
 [複寫安全性最佳作法](security/replication-security-best-practices.md)  
  
  
