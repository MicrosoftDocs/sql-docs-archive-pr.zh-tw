---
title: 最佳化參數化資料列篩選 | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- precomputed partitions [SQL Server replication]
- filters [SQL Server replication], parameterized
- merge replication precomputed partitions [SQL Server replication], SQL Server Management Studio
- parameterized filters [SQL Server replication], optimizing
ms.assetid: 49349605-ebd0-4757-95be-c0447f30ba13
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f1c6448d8e2dba7a68fab441d4d08fd4a4a1db4d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708178"
---
# <a name="optimize-parameterized-row-filters"></a>最佳化參數化資料列篩選
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中最佳化參數化資料列篩選。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
-   **若要最佳化參數化資料列篩選，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   在使用參數化篩選器時，您可以在建立發行集時，藉由指定 [使用資料分割群組]  選項或 [保留資料分割變更]  選項來控制合併式複寫要如何處理篩選。 這兩個選項都可以透過在發行集資料庫中儲存其他中繼資料，以提升具有篩選發行項之發行集的同步處理效能。 您可以在建立發行項時，藉由設定 [資料分割選項]  來控制要如何在訂閱者之間共用資料。 如需有關這些需求的詳細資訊，請參閱＜ [參數化資料列篩選器](../merge/parameterized-filters-parameterized-row-filters.md)＞。  
  
     對於 [!INCLUDE[ssEW](../../../includes/ssew-md.md)]SQL Server Compact 訂閱者，必須將 keep_partition_changes 設為 true，才能確保正確傳播刪除。 設為 false 時，訂閱者所擁有的資料列可能比預期多。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 下列設定可用於最佳化參數化資料列篩選器：  
  
 **資料分割選項**  
 您可以在 [發行項屬性 - \<Article>] 對話方塊的 [屬性] 頁面上，或是在 [新增篩選] 對話方塊中，設定此選項。 [新增發行集] 精靈和 [發行集屬性 - \<Publication>] 對話方塊中皆提供這兩個對話方塊。 [發行項屬性 - \<Article>] 對話方塊可讓您針對此選項，指定 [新增篩選] 對話方塊中未提供的其他值。  
  
 **預先計算資料分割**  
 依預設，如果發行集中的發行項符合一組需求，則此選項要設定為 **[True]** 。 如需這些需求的詳細資訊，請參閱[使用預先計算的資料分割最佳化參數化篩選效能](../merge/parameterized-filters-optimize-for-precomputed-partitions.md)。 您可以在 [發行集屬性 - \<Publication>] 對話方塊的 [訂閱選項] 頁面上，修改此選項。  
  
 **最佳化同步處理**  
 只有在 **[預先計算資料分割]** 設定為 **[False]** 時，此選項才應設定為 **[True]** 。 您可以在 [發行集屬性 - \<Publication>] 對話方塊的 [訂閱選項] 頁面上，設定此選項。  
  
 如需使用 [新增發行集] 精靈並存取 [發行集屬性 - \<Publication>] 對話方塊的詳細資訊，請參閱[建立發行集](create-a-publication.md)和[檢視及修改發行集屬性](view-and-modify-publication-properties.md)。  
  
#### <a name="to-set-partition-options-in-the-add-filter-or-edit-filter-dialog-box"></a>若要在加入篩選或編輯篩選對話方塊中設定資料分割選項  
  
1.  在 [新增發行集] 精靈的 [篩選資料表的資料列] 頁面上，或是在 [發行集屬性 - \<Publication>] 對話方塊的 [篩選資料列] 頁面上，按一下 [新增]，然後按一下 [新增篩選]。  
  
2.  建立參數化篩選。 如需詳細資訊，請參閱 [針對合併發行項定義及修改參數化資料列篩選](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
3.  選取符合資料在訂閱者之間共用資料方式的選項：  
  
    -   **這個資料表中的一個資料列會提供給多個訂閱**  
  
    -   **這個資料表中的一個資料列只會提供給一個訂閱**  
  
     若您選取 **[這個資料表中的一個資料列只會提供給一個訂閱]** ，合併式複寫可藉由儲存和處理較少中繼資料來將效能最佳化。 不過您必須確定資料分割方式不會將資料列複寫至多個訂閱者。 如需進一步資訊，請參閱主題＜ [參數化資料列篩選器](../merge/parameterized-filters-parameterized-row-filters.md)＞中的「設定資料分割選項」。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  如果您位於 [發行集屬性 - \<Publication>] 對話方塊中，請按一下 [確定] 以儲存並關閉對話方塊。  
  
#### <a name="to-set-partition-options-in-the-article-properties---article-dialog-box"></a>設定 [發行項屬性 - \<Article>] 對話方塊中的分割區選項  
  
1.  在 [新增發行集] 精靈的 [發行項] 頁面上，或是在 [發行集屬性 - \<Publication>] 對話方塊中，選取一個資料表，然後按一下 [發行項屬性]。  
  
2.  按一下 **[設定反白顯示資料表發行項的屬性]** 或 **[設定所有資料表發行項的屬性]** 。  
  
3.  在 [發行項屬性 - \<Article>] 對話方塊之 [屬性] 索引標籤的 [目的地物件] 區段中，指定 [分割區選項] 的下列其中一個值：  
  
    -   **重疊**  
  
    -   **重疊，不允許變更資料分割外的資料**  
  
    -   **不重疊，單一訂閱**  
  
    -   **不重疊，共用於訂閱之間**  
  
     如需這些選項及其如何與 **[加入篩選]** 和 **[編輯篩選]** 對話方塊中可用之選項相關聯的詳細資訊，請參閱＜ [參數化資料列篩選器](../merge/parameterized-filters-parameterized-row-filters.md)＞的「設定資料分割選項」一節。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  如果您位於 [發行集屬性 - \<Publication>] 對話方塊中，請按一下 [確定] 以儲存並關閉對話方塊。  
  
#### <a name="to-set-precompute-partitions"></a>若要設定預先計算資料分割  
  
1.  在 [發行集屬性 - \<Publication>] 對話方塊的 [訂閱選項] 頁面上，選取 [預先計算分割區] 選項的值。 在下列情況下，該屬性是唯讀的：  
  
    -   發行集不符合預先計算資料分割的需求。  
  
    -   尚未產生此發行集的快照集。 在此情況下，選項會顯示 **[建立快照時會自動設定]** 的值。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-set-optimize-synchronization"></a>若要設定最佳化同步處理  
  
1.  在 [**發行集屬性 \<Publication> -** ] 對話方塊的 [**訂閱選項**] 頁面上，針對 [**優化同步**處理] 選項選取 [ **True** ] 值。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 如需** \@ keep_partition_changes**和** \@ use_partition_groups**篩選選項的定義，請參閱[sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)。  
  
#### <a name="to-specify-merge-filter-optimizations-when-creating-a-new-publication"></a>在建立新的發行集時指定合併篩選最佳化  
  
1.  在發行集資料庫的發行者上，執行 [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)。 針對下列其中一個參數指定** \@ 發行**集和的值 `true` ：  
  
    -   ** \@ use_partition_groups**：-最高效能優化，前提是發行項符合預先計算資料分割的需求。 如需詳細資訊，請參閱[使用預先計算的資料分割最佳化參數化篩選效能](../merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
    -   ** \@ keep_partition_changes** -如果無法使用預先計算的資料分割，請使用此優化。  
  
2.  加入此發行集的快照集作業。 如需詳細資訊，請參閱[建立發行集](create-a-publication.md)。  
  
3.  在發行集資料庫的發行者上，執行 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)並指定下列參數：  
  
    -   ** \@ 發行**集-步驟1中的發行集名稱。  
  
    -   ** \@ 文章**-發行項的名稱  
  
    -   ** \@ source_object** -要發行的資料庫物件。  
  
    -   ** \@ subset_filterclause** -用來以水準方式篩選發行項的選擇性參數化篩選子句。  
  
    -   ** \@ partition_options** -已篩選之發行項的資料分割選項。  
  
4.  針對發行集中的每一個發行項重複步驟 3。  
  
5.  (選擇性) 在發行集資料庫的發行者上，執行 [sp_addmergefilter](/sql/relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql) ，以定義兩個發行項之間的聯結篩選。 如需詳細資訊，請參閱 [定義和修改合併發行項之間的聯結篩選](define-and-modify-a-join-filter-between-merge-articles.md)。  
  
#### <a name="to-view-and-modify-merge-filter-behaviors-for-an-existing-publication"></a>檢視及修改現有發行集的合併篩選行為  
  
1.   (發行集資料庫之發行者上的選擇性) ，請執行[sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql)，指定** \@ 發行**集。 請注意結果集中 **keep_partition_changes** 和 **use_partition_groups** 的值。  
  
2.  (選擇性) 在發行集資料庫的發行者上，執行 [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)。 為 [ ** \@ 屬性**] 指定 [ **use_partition_groups** ] 的值，並為 [值] 指定 `true` 或 `false` 。 ** \@ **  
  
3.  (選擇性) 在發行集資料庫的發行者上，執行 [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)。 為 [ ** \@ 屬性**] 指定 [ **keep_partition_changes** ] 的值，並為 [值] 指定 `true` 或 `false` 。 ** \@ **  
  
    > [!NOTE]  
    >  啟用**keep_partition_changes**時，您必須先停用**use_partition_groups** ，並為** \@ force_reinit_subscription**指定**1**的值。  
  
4.  (選擇性) 在發行集資料庫的發行者上，執行 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)。 為 [ ** \@ 屬性**] 指定 [ **partition_options** ] 的值，並為 [ ** \@ 值**] 指定適當的值。 如需這些篩選選項的定義，請參閱 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) 。  
  
5.  (選擇性) 在必要時，啟動快照集代理程式來重新產生快照集。 如需哪些變更需要產生新快照集的資訊，請參閱[變更發行集與發行項屬性](change-publication-and-article-properties.md)。  
  
## <a name="see-also"></a>另請參閱  
 [在合併發行項之間自動產生一組聯結篩選 &#40;SQL Server Management Studio&#41;](automatically-generate-join-filters-between-merge-articles.md)   
 [針對合併發行項定義及修改參數化資料列篩選](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [參數化資料列篩選器](../merge/parameterized-filters-parameterized-row-filters.md)  
  
  
