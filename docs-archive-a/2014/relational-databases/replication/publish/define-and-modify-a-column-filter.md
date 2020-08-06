---
title: 定義及修改資料行篩選 | Microsoft 文件
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server replication], column
- modifying filters, column
- modifying filters
- column filters [SQL Server replication]
ms.assetid: d7c3186a-9a8c-45d8-ab34-05beec4c26dd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3a655976f925f83d8c9446cab99016f32ab14887
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606758"
---
# <a name="define-and-modify-a-column-filter"></a>定義及修改資料行篩選
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中定義及修改資料行篩選。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
-   **若要定義及修改資料行篩選，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   某些資料行無法進行篩選；如需詳細資訊，請參閱[篩選發行的資料](filter-published-data.md)。 如果您要在初始化訂閱後修改資料行篩選，則必須在進行變更後產生新的快照集並重新初始化所有訂閱。 如需屬性變更需求的詳細資訊，請參閱[變更發行集與發行項屬性](change-publication-and-article-properties.md)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在「新增發行集精靈」的 **[發行項]** 頁面中定義資料行篩選。 如需使用「新增發行集精靈」的詳細資訊，請參閱[建立發行集](create-a-publication.md)。  
  
 在 [發行集屬性 - \<Publication>] 對話方塊的 [發行項] 頁面上定義及修改資料行篩選。 如需發行集和發行項屬性的詳細資訊，請參閱[檢視及修改發行集屬性](view-and-modify-publication-properties.md)。  
  
#### <a name="to-define-a-column-filter"></a>若要定義資料行篩選  
  
1.  在「新增發行集精靈」的 **[發行項]** 頁面中，展開要在 **[發行的物件]** 窗格中篩選的資料表。  
  
2.  清除您要篩選之每個資料行旁邊的核取方塊。  
  
#### <a name="to-modify-column-filtering"></a>若要修改資料行篩選  
  
1.  在 [發行集屬性 - \<Publication>] 對話方塊的 [發行項] 頁面中，展開要在 [發行的物件] 窗格中篩選的資料表。  
  
2.  清除每個您要篩選之資料行旁邊的核取方塊，並確保為每個應包含在發行項中的資料行選取核取方塊。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 在建立資料表發行項時，您可以定義要將哪些資料行包含在發行項中，並在定義發行項之後變更資料行。 您可以使用複寫預存程序來以程式設計的方式建立及修改篩選的資料行。  
  
> [!NOTE]  
>  下列程序假設基礎資料表尚未變更。 如需複寫已發行之資料表的資料定義語言 (DDL) 變更的詳細資訊，請參閱[對發行集資料庫進行結構描述變更](make-schema-changes-on-publication-databases.md)。  
  
#### <a name="to-define-a-column-filter-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>針對快照式或交易式發行集中發行的發行項定義資料行篩選  
  
1.  定義要篩選的發行項。 如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。  
  
2.  在發行集資料庫的發行者上，執行 [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql)。 這樣會定義要在發行項中包含或移除的資料行。  
  
    -   如果只要從包含許多資料行的資料表發行一些資料行，請針對加入的每一個資料行執行 [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql) 一次。 為 **\@column** 指定資料行名稱，並為 **\@operation** 指定 **add** 值。  
  
    -   如果要在包含許多資料行的資料表中發行大多數的資料行，請執行 [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql)、為 **\@column** 指定 **null** 值，以及為 **\@operation** 指定 **add** 值來新增所有資料行。 然後為每一個排除的資料行執行 [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql) 一次，為 **\@operation** 指定 **drop** 值，並為 **\@column** 指定排除的資料行名稱。  
  
3.  在發行集資料庫的發行者上，執行 [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql)。 為 **\@publication** 指定發行集名稱，並為 **\@article** 指定篩選的發行項名稱。 這樣會針對篩選的發行項建立同步處理物件。  
  
#### <a name="to-change-a-column-filter-to-include-additional-columns-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>針對快照式或交易式發行集中發行的發行項變更要包含其他資料行的資料行篩選  
  
1.  在發行集資料庫的發行者上，針對每一個加入的資料行執行 [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql) 一次。 為 **\@column** 指定資料行名稱，並為 **\@operation** 指定 **add** 值。  
  
2.  在發行集資料庫的發行者上，執行 [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql)。 為 **\@publication** 指定發行集名稱，並為 **\@article** 指定篩選的發行項名稱。 如果此發行集有現有的訂閱，請為 **\@change_active** 指定 **1** 值。 這樣會針對篩選的發行項重新建立同步處理物件。  
  
3.  針對此發行集重新執行快照集代理程式作業，以產生更新的快照集。  
  
4.  重新初始化訂閱。 如需詳細資訊，請參閱 [重新初始化訂閱](../reinitialize-subscriptions.md)。  
  
#### <a name="to-change-a-column-filter-to-remove-columns-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>針對快照式或交易式發行集中發行的發行項變更要移除資料行的資料行篩選  
  
1.  在發行集資料庫的發行者上，針對每一個移除的資料行執行 [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql) 一次。 為 **\@column** 指定資料行名稱，並為 **\@operation** 指定 **drop** 值。  
  
2.  在發行集資料庫的發行者上，執行 [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql)。 為 **\@publication** 指定發行集名稱，並為 **\@article** 指定篩選的發行項名稱。 如果此發行集有現有的訂閱，請為 **\@change_active** 指定 **1** 值。 這樣會針對篩選的發行項重新建立同步處理物件。  
  
3.  針對此發行集重新執行快照集代理程式作業，以產生更新的快照集。  
  
4.  重新初始化訂閱。 如需詳細資訊，請參閱 [重新初始化訂閱](../reinitialize-subscriptions.md)。  
  
#### <a name="to-define-a-column-filter-for-an-article-published-in-a-merge-publication"></a>針對合併式發行集中發行的發行項定義資料行篩選  
  
1.  定義要篩選的發行項。 如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。  
  
2.  在發行集資料庫的發行者上，執行 [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql)。 這樣會定義要在發行項中包含或移除的資料行。  
  
    -   如果只要從包含許多資料行的資料表發行一些資料行，請針對加入的每一個資料行執行 [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) 一次。 為 **\@column** 指定資料行名稱，並為 **\@operation** 指定 **add** 值。  
  
    -   如果要在包含許多資料行的資料表中發行大多數的資料行，請執行 [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql)、為 **\@column** 指定 **null** 值，以及為 **\@operation** 指定 **add** 值來新增所有資料行。 然後為每一個排除的資料行執行 [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) 一次，為 **\@operation** 指定 **drop** 值，並為 **\@column** 指定排除的資料行名稱。  
  
#### <a name="to-change-a-column-filter-to-include-additional-columns-for-an-article-published-in-a-merge-publication"></a>針對合併式發行集中發行的發行項變更要包含其他資料行的資料行篩選  
  
1.  在發行集資料庫的發行者上，針對每一個加入的資料行執行 [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) 一次。 為 **\@column** 指定資料行名稱、為 **\@operation** 指定 **add** 值，以及為 **\@force_invalidate_snapshot** 和 **\@force_reinit_subscription** 指定 **1** 值。  
  
2.  針對此發行集重新執行快照集代理程式作業，以產生更新的快照集。  
  
3.  重新初始化訂閱。 如需詳細資訊，請參閱 [重新初始化訂閱](../reinitialize-subscriptions.md)。  
  
#### <a name="to-change-a-column-filter-to-remove-columns-for-an-article-published-in-a-merge-publication"></a>針對合併式發行集中發行的發行項變更要移除資料行的資料行篩選  
  
1.  在發行集資料庫的發行者上，針對每一個移除的資料行執行 [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) 一次。 為 **\@column** 指定資料行名稱、為 **\@operation** 指定 **drop** 值，以及為 **\@force_invalidate_snapshot** 和 **\@force_reinit_subscription** 指定 **1** 值。  
  
2.  針對此發行集重新執行快照集代理程式作業，以產生更新的快照集。  
  
3.  重新初始化訂閱。 如需詳細資訊，請參閱 [重新初始化訂閱](../reinitialize-subscriptions.md)。  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> 範例 &#40;Transact-SQL&#41;  
 此異動複寫範例會從根據 `DaysToManufacture` 資料表的發行項中移除 `Product` 資料行。  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../snippets/tsql/SQL15/replication/howto/tsql/createtranpub.sql#sp_addtranarticle)]  
  
 此合併式複寫範例會從根據 `CreditCardApprovalCode` 資料表的發行項中移除 `SalesOrderHeader` 資料行。  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepub.sql#sp_addmergearticle)]  
  
## <a name="see-also"></a>另請參閱  
 [變更發行集與發行項屬性](change-publication-and-article-properties.md)   
 [篩選發行的資料](filter-published-data.md)   
 [合併式複寫之篩選發行資料](../merge/filter-published-data-for-merge-replication.md)  
  
  
