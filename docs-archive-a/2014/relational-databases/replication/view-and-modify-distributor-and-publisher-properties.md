---
title: 檢視及修改散發者和發行者屬性 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing replication properties
- Distributors [SQL Server replication], modifying
- modifying replication properties, Distributors
- Distributors [SQL Server replication], properties
ms.assetid: 5dae1d59-c377-4c6e-adc9-b68c5b328f79
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 571f6f3a0d44f0fc87c67885249fca441776946d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593921"
---
# <a name="view-and-modify-distributor-and-publisher-properties"></a>檢視及修改散發者和發行者屬性
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中檢視及修改「散發者」和「發行者」屬性。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要檢視及修改「散發者」和「發行者」屬性，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   對於執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 之前版本的「發行者」，**sysadmin** 固定伺服器角色中的使用者可在 [訂閱者] 頁面上註冊「訂閱者」。 從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]開始，它不再需要明確註冊複寫的「訂閱者」。  
  
###  <a name="security"></a><a name="Security"></a> Security  
 可能的話，會在執行階段提示使用者輸入安全性認證。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-and-modify-distributor-properties"></a>檢視和修改散發者屬性  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的散發者，然後展開伺服器節點。  
  
2.  以滑鼠右鍵按一下 **[複寫]** 資料夾，然後按一下 **[散發者屬性]** 。  
  
3.  檢視和修改 [散發者屬性 - \<Distributor>] 對話方塊中的屬性。  
  
    -   若要檢視和修改散發資料庫的屬性，請按一下對話方塊中 [一般] 頁面上資料庫的屬性按鈕 ( **...** )。  
  
    -   若要檢視和修改與「散發者」相關聯的「發行者」屬性，請按一下對話方塊中 **[發行者]** 頁面上「發行者」的屬性按鈕 ( **[...]** )。  
  
    -   若要存取複寫代理程式的設定檔，請按一下對話方塊中 **[一般]** 頁面上的 **[設定檔預設值]** 按鈕。 如需相關資訊，請參閱 [Replication Agent Profiles](agents/replication-agent-profiles.md)。  
  
    -   若要變更在「發行者」端執行管理預存程序以及在「散發者」端更新資訊時所使用之帳戶的密碼，請在對話方塊中 **[發行者]** 頁面上的 **[密碼]** 和 **[確認密碼]** 方塊內輸入新的密碼。 如需詳細資訊，請參閱[保護散發者](security/secure-the-distributor.md)。  
  
4.  必要時修改任何屬性，然後按一下 **[確定]** 。  
  
#### <a name="to-view-and-modify-publisher-properties"></a>檢視和修改發行者屬性  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  以滑鼠右鍵按一下 **[複寫]** 資料夾，然後按一下 **[發行者屬性]** 。  
  
3.  在 [**發行者屬性- \< Publisher > ** ] 對話方塊中，查看及修改屬性。  
  
    -   **sysadmin** 固定伺服器角色中的使用者能啟用 **[發行集資料庫]** 頁面上複寫的資料庫。 啟用資料庫不會發行此資料庫；不過，它允許該資料庫之 **db_owner** 固定資料庫角色中的任何使用者在資料庫中建立一個或多個發行集。  
  
4.  必要時修改任何屬性，然後按一下 **[確定]** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式檢視發行者和散發者屬性。  
  
#### <a name="to-view-distributor-and-distribution-database-properties"></a>檢視散發者和散發資料庫屬性  
  
1.  執行 [sp_helpdistributor](/sql/relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql) ，傳回有關散發者、散發資料庫和工作目錄的資訊。  
  
2.  執行 [sp_helpdistributiondb](/sql/relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql) ，傳回指定之散發資料庫的屬性。  
  
#### <a name="to-change-distributor-and-distribution-database-properties"></a>變更散發者和散發資料庫屬性  
  
1.  在散發者上，執行 [sp_changedistributor_property](/sql/relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql) 來修改散發者屬性。  
  
2.  在散發者上，執行 [sp_changedistributiondb](/sql/relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql) 來修改散發資料庫屬性。  
  
3.  在散發者上，執行 [sp_changedistributor_password](/sql/relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql) 來變更散發者密碼。  
  
    > [!IMPORTANT]  
    >  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您將認證儲存在指令碼檔案中，必須保護該檔案免於未經授權的存取。  
  
4.  在散發者上，執行 [sp_changedistpublisher](/sql/relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql) 來變更使用此散發者之發行者的屬性。  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> 範例 (Transact-SQL)  
 下列範例的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼會傳回有關散發者和散發資料庫的資訊。  
  
 [!code-sql[HowTo#sp_helpdistributor](../../snippets/tsql/SQL15/replication/howto/tsql/changedistpub.sql#sp_helpdistributor)]  
  
 [!code-sql[HowTo#sp_helpdistributiondb](../../snippets/tsql/SQL15/replication/howto/tsql/changedistpub.sql#sp_helpdistributiondb)]  
  
 此範例會變更散發者的保留期限、連接散發者所使用的密碼，以及散發者檢查各種複寫代理程式之狀態的間隔 (也稱為活動訊號間隔)。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您將認證儲存在指令碼檔案中，必須保護該檔案免於未經授權的存取。  
  
 [!code-sql[HowTo#sp_changedistributor_property](../../snippets/tsql/SQL15/replication/howto/tsql/changedistpub.sql#sp_changedistributor_property)]  
  
 [!code-sql[HowTo#sp_changedistributiondb](../../snippets/tsql/SQL15/replication/howto/tsql/changedistpub.sql#sp_changedistributiondb)]  
  
 [!code-sql[HowTo#sp_changedistributor_password](../../snippets/tsql/SQL15/replication/howto/tsql/changedistpub.sql#sp_changedistributor_password)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
  
#### <a name="to-view-and-modify-distributor-properties"></a>檢視和修改散發者屬性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與散發者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 類別的執行個體。 傳遞步驟 1 的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件。  
  
3.  (選擇性) 檢查 <xref:Microsoft.SqlServer.Replication.ReplicationServer.IsDistributor%2A> 屬性，確認目前連接的伺服器為散發者。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> 方法，從伺服器中取得屬性。  
  
5.  (選擇性) 若要變更屬性，請針對 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 物件上可以設定的一或多個散發者屬性設定新的值。  
  
6.  (選擇性) 如果 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 物件上的 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 屬性設定為 `true`，請呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法來認可伺服器的變更。  
  
#### <a name="to-view-and-modify-distribution-database-properties"></a>檢視及修改散發資料庫屬性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與散發者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 類別的執行個體。 指定 name 屬性，並傳遞步驟 1 中的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法，從伺服器中取得屬性。 如果此方法傳回 `false`，則表示伺服器上沒有指定之名稱的資料庫存在。  
  
4.  (選擇性) 若要變更屬性，請針對其中一個可設定的 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 屬性設定新的值。  
  
5.  (選擇性) 如果 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 物件上的 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 屬性設定為 `true`，請呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法來認可伺服器的變更。  
  
#### <a name="to-view-and-modify-publisher-properties"></a>檢視和修改發行者屬性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 類別的執行個體。 指定 <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> 屬性，並傳遞步驟 1 中的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件。  
  
3.  (選擇性) 若要變更屬性，請針對其中一個可設定的 <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 屬性設定新的值。  
  
4.  (選擇性) 如果 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 物件上的 <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 屬性設定為 `true`，請呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法來認可伺服器的變更。  
  
#### <a name="to-change-the-password-for-the-administrative-connection-from-the-publisher-to-the-distributor"></a>變更從發行者到散發者之管理連接的密碼  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與散發者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 類別的執行個體。  
  
3.  將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的連接。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> 方法以取得物件的屬性。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> 方法。 針對 *password* 參數傳遞新的密碼值。  
  
    > [!IMPORTANT]  
    >  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須儲存認證，請使用 [Windows .NET Framework 提供的](https://go.microsoft.com/fwlink/?LinkId=34733) 密碼編譯服務 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
6.  (選擇性) 請執行以下步驟，在使用此散發者的每一個遠端發行者上變更密碼：  
  
    1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
    2.  建立 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 類別的執行個體。  
  
    3.  將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 6a 中建立的連接。  
  
    4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> 方法以取得物件的屬性。  
  
    5.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> 方法。 針對 *password* 參數傳遞步驟 5 中的新密碼值。  
  
###  <a name="example-rmo"></a><a name="PShellExample"></a> 範例 (RMO)  
 這個範例會示範如何變更散發和散發資料庫的屬性。  
  
> [!IMPORTANT]  
>  為了避免在程式碼中儲存認證，會在執行階段提供新的散發者密碼。  
  
 [!code-csharp[HowTo#rmo_ChangeDistPub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_changedistpub)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeDistPub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_changedistpub)]  
  
## <a name="see-also"></a>另請參閱  
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [停用發行和散發](disable-publishing-and-distribution.md)   
 [[設定散發]](configure-distribution.md)   
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [散發者與發行者資訊指令碼](administration/distributor-and-publisher-information-script.md)   
 [Replication System Stored Procedures Concepts](concepts/replication-system-stored-procedures-concepts.md)   
 [使用複寫監視器來檢視資訊及執行工作](monitor/view-information-and-perform-tasks-replication-monitor.md)  
  
  
