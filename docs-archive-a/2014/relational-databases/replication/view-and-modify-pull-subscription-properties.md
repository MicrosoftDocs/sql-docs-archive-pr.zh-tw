---
title: 檢視及修改提取訂閱屬性 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- modifying subscriptions
- viewing replication properties
- modifying replication properties, pull subscriptions
- pull subscriptions [SQL Server replication], modifying
- subscriptions [SQL Server replication], pull
- pull subscriptions [SQL Server replication], properties
- modifying subscriptions, SQL Server Management Studio
ms.assetid: 1601e54f-86f0-49e8-b023-87a5d1def033
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1b847a22d31bbf3ea7540c55339fe27531134125
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585250"
---
# <a name="view-and-modify-pull-subscription-properties"></a>檢視及修改提取訂閱屬性
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中檢視及修改提取訂閱屬性。  
  
 **本主題內容**  
  
-   **若要檢視及修改提取訂閱屬性，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在 [訂閱屬性 - \<Publisher>：\<PublicationDatabase>] 對話方塊中檢視發行者或訂閱者的提取訂閱屬性，該對話方塊可從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 取得。 「訂閱者」可看見更多屬性，而屬性可於「訂閱者」端修改。 您也可以從 **[所有訂閱]** 索引標籤上的「發行者」檢視屬性，該索引標籤位於「複寫監視器」中。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](monitor/start-the-replication-monitor.md)。  
  
#### <a name="to-view-pull-subscription-properties-from-the-publisher-in-management-studio"></a>從 Management Studio 中的發行者檢視提取訂閱屬性  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  展開適當的發行集，以滑鼠右鍵按一下訂閱，然後按一下 **[屬性]** 。  
  
4.  檢視屬性，然後按一下 **[確定]** 。  
  
#### <a name="to-view-and-modify-pull-subscription-properties-from-the-subscriber-in-management-studio"></a>從 Management Studio 中的訂閱者檢視和修改提取訂閱屬性  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的訂閱者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機訂閱]** 資料夾。  
  
3.  以滑鼠右鍵按一下訂閱，然後按一下 **[屬性]** 。  
  
4.  必要時修改任何屬性，然後按一下 **[確定]** 。  
  
#### <a name="to-view-pull-subscription-properties-from-the-publisher-in-replication-monitor"></a>從複寫監視器中的發行者檢視提取訂閱屬性  
  
1.  在複寫監視器的左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 **[所有訂閱]** 索引標籤。  
  
3.  以滑鼠右鍵按一下訂閱，然後按一下 **[屬性]** 。  
  
4.  檢視屬性，然後按一下 **[確定]** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式修改提取訂閱及存取其屬性。 使用哪些預存程序要依訂閱所屬的發行集類型而定。  
  
#### <a name="to-view-the-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>檢視快照式或交易式發行集之提取訂閱的屬性  
  
1.  在訂閱者上，執行 [sp_helppullsubscription](/sql/relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql)。 指定 **@publisher** 、 **@publisher_db** 和 **@publication** 。 這樣會傳回儲存於訂閱者上之系統資料表內的訂閱相關資訊。  
  
2.  在訂閱者上，執行 [sp_helpsubscription_properties](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql)。 指定 **@publisher** 、 **@publisher_db** 、 **@publication** 和的下列其中一個值 **@publication_type** ：  
  
    -   **0** - 訂閱屬於交易式發行集。  
  
    -   **1** - 訂閱屬於快照式發行集。  
  
3.  在發行者上，執行 [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql)。 指定 **@publication** 和 **@subscriber** 。  
  
4.  在發行者上，執行[sp_helpsubscriberinfo](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql)，並指定 **@subscriber** 。 這樣會顯示與訂閱者有關的資訊。  
  
#### <a name="to-change-the-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>變更快照式或交易式發行集之提取訂閱的屬性  
  
1.  在訂閱者上，執行[sp_change_subscription_properties](/sql/relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql)，並指定 **@publisher** 、 **@publisher_db** 、 **@publication** 、 **0** (交易式) 的值或**1** (的快照集) **@publication_type** 、做為變更的訂閱屬性， **@property** 以及做為的新值 **@value** 。  
  
2.  (選擇性) 在訂閱資料庫的訂閱者上，執行 [sp_changesubscriptiondtsinfo](/sql/relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql)。 針對指定散發代理程式作業的識別碼 **@jobid** ，並將下列資料轉換服務 (DTS) 封裝屬性：  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     這樣會變更訂閱的 DTS 封裝屬性。  
  
    > [!NOTE]  
    >  可以執行 [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql)來取得作業識別碼。  
  
#### <a name="to-view-the-properties-of-a-pull-subscription-to-a-merge-publication"></a>檢視合併式發行集之提取訂閱的屬性  
  
1.  在訂閱者上，執行 [sp_helpmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql)。 指定 **@publisher** 、 **@publisher_db** 和 **@publication** 。  
  
2.  在訂閱者上，執行 [sp_helpsubscription_properties](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql)。 指定 **@publisher** 、 **@publisher_db** 、 **@publication** ，以及2的值 **@publication_type** 。  
  
3.  在發行者上執行 [sp_helpmergesubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql) ，以顯示訂閱資訊。 若要傳回特定訂閱的相關資訊，您必須指定 **@publication** 、 **@subscriber** ，以及的**pull**值 **@subscription_type** 。  
  
4.  在發行者上，執行[sp_helpsubscriberinfo](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql)，並指定 **@subscriber** 。 這樣會顯示與訂閱者有關的資訊。  
  
#### <a name="to-change-the-properties-of-a-pull-subscription-to-a-merge-publication"></a>變更合併式發行集之提取訂閱的屬性  
  
1.  在訂閱者上，執行 [sp_changemergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql)。 指定 **@publication** 、 **@publisher** 、 **@publisher_db** 、將變更為的訂閱屬性 **@property** ，並將新的值指定為 **@value** 。  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 用於檢視或修改提取訂閱屬性的 RMO 類別，將取決於該提取訂閱所訂閱的發行集類型而定。  
  
#### <a name="to-view-or-modify-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>檢視或修改快照式或交易式發行集之提取訂閱的屬性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與「訂閱者」的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 類別的執行個體。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>和 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 屬性。  
  
4.  針對 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定步驟 1 中的連接。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 `false`，則表示步驟 3 中的訂閱屬性定義不正確，或者此訂閱不存在於伺服器上。  
  
6.  (選擇性) 若要變更屬性，請針對其中一個可設定的 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 屬性設定新的值，然後呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  (選擇性) 若要檢視新的設定，請呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 方法，重新載入發行項的屬性。  
  
8.  關閉所有連接。  
  
#### <a name="to-view-or-modify-properties-of-a-pull-subscription-to-a-merge-publication"></a>檢視或修改合併式發行集之提取訂閱的屬性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與「訂閱者」的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 類別的執行個體。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>和 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 屬性。  
  
4.  針對 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定步驟 1 中的連接。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 `false`，則表示步驟 3 中的訂閱屬性定義不正確，或者此訂閱不存在於伺服器上。  
  
6.  (選擇性) 若要變更屬性，請針對其中一個可設定的 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 屬性設定新的值，然後呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  (選擇性) 若要檢視新的設定，請呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 方法，重新載入發行項的屬性。  
  
8.  關閉所有連接。  
  
## <a name="see-also"></a>另請參閱  
 [使用複寫監視器來檢視資訊及執行工作](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [訂閱發行集](subscribe-to-publications.md)  
  
  
