---
title: 重新組織與重建索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql12.swb.indexproperties.fragmentation.f1
- sql12.swb.index.reorg.f1
- sql12.swb.index.rebuild.f1
helpviewer_keywords:
- large object defragmenting
- indexes [SQL Server], reorganizing
- index reorganization [SQL Server]
- reorganizing indexes
- defragmenting large object data types
- index fragmentation [SQL Server]
- index rebuilding [SQL Server]
- rebuilding indexes
- indexes [SQL Server], rebuilding
- defragmenting indexes
- nonclustered indexes [SQL Server], defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
- LOB data [SQL Server], defragmenting
- clustered indexes, defragmenting
ms.assetid: a28c684a-c4e9-4b24-a7ae-e248808b31e9
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7c00f2128bb4c54064511ffff9e8929c9faf4d59
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707553"
---
# <a name="reorganize-and-rebuild-indexes"></a>重新組織與重建索引
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中重新組織或重建片段索引。 只要對基礎資料進行插入、更新或刪除作業， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 就會自動維護索引。 過一段時間後，這些修改就可能使索引中的資訊變成散佈於資料庫中 (片段)。 當根據索引鍵值的邏輯順序頁面，與資料檔中的實體順序不相符時，就會有片段產生。 片段化嚴重的索引可能會造成查詢效能降低並使應用程式回應變慢。  
  
 您可以重新組織或重建索引以修復索引片段。 對於在資料分割配置上建立的資料分割索引，您可以在完整的索引或在索引的單一資料分割上使用這些方法。 重建索引會卸除和重新建立索引。 這會移除片段；根據指定的或現有的填滿因數設定壓縮頁面來收回磁碟空間，以及重新排序連續頁面中的索引資料列。 當指定 ALL 時，會在單一交易中卸除和重建資料表的所有索引。 重新組織索引所用的系統資源最少。 它會實際重新排序分葉層級的頁面，使它們由左至右符合分葉節點的邏輯順序，以重新組織資料表和檢視表之叢集和非叢集索引的分葉層級。 重新組織也會壓縮索引頁面。 壓縮是以現有填滿因數值為基礎。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [偵測片段](#Fragmentation)  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用下列方法檢查索引的片段：**  
  
     [SQL Server Management Studio](#SSMSProcedureFrag)  
  
     [Transact-SQL](#TsqlProcedureFrag)  
  
-   **使用下列方法重新組織或重建索引：**  
  
     [SQL Server Management Studio](#SSMSProcedureReorg)  
  
     [Transact-SQL](#TsqlProcedureReorg)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="detecting-fragmentation"></a><a name="Fragmentation"></a>偵測片段  
 決定使用重組方法的第一步是分析索引以決定片段的程度。 透過使用系統函數 [sys.dm_db_index_physical_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql)，您就可以在特定的索引中、在資料表或索引檢視表上的所有索引、在資料庫中的所有索引或在所有資料庫的所有索引中偵測片段。 對於資料分割索引而言， **sys.dm_db_index_physical_stats** 也為每個資料分割提供片段資訊。  
  
 **sys.dm_db_index_physical_stats** 函數傳回的結果集包含下列資料行。  
  
|資料行|描述|  
|------------|-----------------|  
|**avg_fragmentation_in_percent**|邏輯片段的百分比 (索引中失序的頁面)。|  
|**fragment_count**|在索引中的片段數目 (實體上為連續的分葉頁面)。|  
|**avg_fragment_size_in_pages**|在索引中一個片段的頁面平均數目。|  
  
 在了解片段的程度後，請使用下表來決定修正片段最好的方法。  
  
|**avg_fragmentation_in_percent** 值|修正的陳述式|  
|-----------------------------------------------|--------------------------|  
|> 5% 和 \< = 30%|ALTER INDEX REORGANIZE|  
|> 30%|ALTER INDEX REBUILD WITH (ONLINE = ON) <sup>1</sup>|

<sup>1</sup> 重建索引可於線上或離線執行。 重新組織索引則一律在線上執行。 若要達到與重新組織選項相似的可用性，您應該在線上重建索引。  
  
> [!TIP]
> 這些值提供概略的方針，讓您可判斷應該在 `ALTER INDEX REORGANIZE` 和 `ALTER INDEX REBUILD` 之間切換的時間點。 不過，實際的值可能隨各種狀況而異。 請務必嘗試不同的值，以判斷適合您環境的最佳臨界值。 例如，如果指定的索引主要用於掃描作業，則移除片段可以改善這些作業的效能。 對於主要用於搜尋作業的索引而言，效能優勢較不明顯。 同樣地，移除堆積中的片段 (沒有叢集索引的資料表) 對於非叢集索引掃描作業特別有用，但對查閱作業則幾乎沒有作用。

您通常不應該使用上述任何命令來處理片段層級過低 (低於 5%) 的情況，因為重組或重建索引的成本遠遠超過移除如此少量片段所獲得的好處。 

> [!NOTE]
> 重建或重新組織小型索引通常不會減少片段。 小型索引的頁面有時候會儲存在混合範圍上， 混合範圍最多可由八個物件所共用，所以當重新組織或重建索引之後，小型索引中的片段可能不會減少。

### <a name="index-defragmentation-considerations"></a>索引磁碟重組考量
在某些情況下，如果非叢集索引記錄中所包含的實體或邏輯識別碼需要變更，則重建叢集索引將會自動重建任何參考叢集索引鍵的非叢集索引。

強制在資料表上自動重建所有非叢集索引的案例：

-  在資料表上建立叢集索引
-  移除叢集索引，使資料表儲存為堆積
-  變更叢集索引鍵以包含或排除資料行

不需要在資料表上自動重建所有非叢集索引的案例：

-  重建唯一的叢集索引
-  重建非唯一的叢集索引
-  變更索引結構描述，例如將資料分割結構描述套用至叢集索引，或將叢集索引移至不同的檔案群組
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
超過 128 個範圍的索引將以兩個不同的階段重建：邏輯和實體。 在邏輯階段中，索引所使用的現有配置單位將以取消配置標示，並複製和排序資料列，然後移到所建立的新配置單位以儲存重建索引。 在實體階段中，會將先前標示為取消配置的配置單位，在背景以短暫的交易實際卸除，而且不需要許多鎖定。 如需範圍的詳細資訊，請參閱[分頁與範圍架構指南](https://docs.microsoft.com/sql/relational-databases/pages-and-extents-architecture-guide)。

`ALTER INDEX REORGANIZE` 陳述式需要包含索引的資料檔案具有可用的空間，因為作業只能配置在相同檔案上的暫存工作頁面，而不是檔案群組內的其他檔案。 因此，雖然檔案群組可能有可用的分頁，但是使用者仍然可能會出現錯誤 1105：`Could not allocate space for object '###' in database '###' because the '###' filegroup is full. Create disk space by deleting unneeded files, dropping objects in the filegroup, adding additional files to the filegroup, or setting autogrowth on for existing files in the filegroup.`

您可以對包含超過 1,000 個分割區的資料表，建立及重建未校正的索引，但並不建議這麼做。 此做法可能會導致在作業期間效能降低或耗用過多記憶體。

如果索引所在的檔案群組離線或設為唯讀，便無法重新組織或重建索引。 當指定 `ALL` 關鍵字，且有一或多個索引在離線或唯讀檔案群組中時，陳述式會失敗。
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 必須具備資料表或檢視的 `ALTER` 權限。 使用者必須是 **系統管理員** 固定伺服器角色的成員，或是 **db_ddladmin** 和 **db_owner** 固定資料庫角色的成員。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedureFrag"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-check-the-fragmentation-of-an-index"></a>若要檢查索引的片段  
  
1.  在 [物件總管] 中，展開包含您要檢查其索引片段之資料表的資料庫。  
  
2.  展開 **[資料表]** 資料夾。  
  
3.  展開要檢查其索引片段的資料表。  
  
4.  展開 **[索引]** 資料夾。  
  
5.  以滑鼠右鍵按一下要檢查其片段的索引，然後選取 **[屬性]** 。  
  
6.  在 **[選取頁面]** 底下，選取 **[片段]** 。  
  
     **[片段]** 頁面上提供下列資訊：  
  
     **頁面飽和度**  
     指出索引頁面的平均飽和度，以百分比表示。 100% 表示索引頁面完全飽和。 50% 表示平均每個索引頁面為半飽和。  
  
     **片段總計**  
     邏輯片段百分比。 這指出索引中未依順序儲存的頁數。  
  
     **平均資料列大小**  
     分葉層級資料列的平均大小。  
  
     **Depth**  
     索引中的層級數目，包括分葉層級。  
  
     **轉送的記錄**  
     在堆積中，有指向另一個資料位置之轉送指標的記錄數目。 (此狀態發生於更新期間，原始位置的空間不足以儲存新資料列時)。  
  
     **準刪除列**  
     標示為刪除但尚未移除的資料列數目。 這些資料列將由清除執行緒在伺服器不忙碌時移除。 這個值不包含因未處理的快照集隔離交易而保留的資料列。  
  
     **索引類型**  
     索引的類型。 可能的值為 **[叢集索引]** 、 **[非叢集索引]** 以及 **[主要 XML]** 。 資料表也可以儲存為堆積 (無索引)，但是無法開啟此 [索引屬性] 頁面。  
  
     **分葉層級資料列**  
     分葉層級資料列的數目。  
  
     **資料列大小上限**  
     分葉層級資料列大小上限。  
  
     **資料列大小下限**  
     最小分葉層級資料列大小。  
  
     **頁面**  
     資料頁的總數。  
  
     **分割區識別碼**  
     包含索引之 B 型樹狀目錄的資料分割識別碼。  
  
     **版本準刪除列**  
     因為未處理的快照集隔離交易而保留的準刪除記錄數目。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedureFrag"></a> 使用 Transact-SQL  
  
#### <a name="to-check-the-fragmentation-of-an-index"></a>若要檢查索引的片段  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Find the average fragmentation percentage of all indexes  
    -- in the HumanResources.Employee table.   
    SELECT a.index_id, name, avg_fragmentation_in_percent  
    FROM sys.dm_db_index_physical_stats (DB_ID(N'AdventureWorks2012'), OBJECT_ID(N'HumanResources.Employee'), NULL, NULL, NULL) AS a  
        JOIN sys.indexes AS b ON a.object_id = b.object_id AND a.index_id = b.index_id;   
    GO  
    ```  
  
     上面的陳述式可能會傳回與下例類似的結果集。  
  
    ```  
    index_id    name                                                  avg_fragmentation_in_percent  
    ----------- ----------------------------------------------------- ----------------------------  
    1           PK_Employee_BusinessEntityID                          0  
    2           IX_Employee_OrganizationalNode                        0  
    3           IX_Employee_OrganizationalLevel_OrganizationalNode    0  
    5           AK_Employee_LoginID                                   66.6666666666667  
    6           AK_Employee_NationalIDNumber                          50  
    7           AK_Employee_rowguid                                   0  
  
    (6 row(s) affected)  
    ```  
  
 如需詳細資訊，請參閱 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedureReorg"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-reorganize-or-rebuild-an-index"></a>若要重新組織或重建索引  
  
1.  在 [物件總管] 中，展開包含您要重新組織其索引之資料表的資料庫。  
  
2.  展開 **[資料表]** 資料夾。  
  
3.  展開您要重新組織其索引的資料表。  
  
4.  展開 **[索引]** 資料夾。  
  
5.  以滑鼠右鍵按一下您要重新組織的索引，然後選取 **[重新組織]** 。  
  
6.  在 **[重新組織索引]** 對話方塊中，確認 **[要重新組織的索引]** 方格中有正確索引，然後按一下 **[確定]** 。  
  
7.  選取 **[壓縮大型物件資料行資料]** 核取方塊，可指定一併壓縮包含大型物件 (LOB) 資料的所有頁面。  
  
8.  按一下 [確定]。  
  
#### <a name="to-reorganize-all-indexes-in-a-table"></a>若要重新組織資料表中的所有索引  
  
1.  在 [物件總管] 中，展開包含您要重新組織其索引之資料表的資料庫。  
  
2.  展開 **[資料表]** 資料夾。  
  
3.  展開您要重新組織其索引的資料表。  
  
4.  以滑鼠右鍵按一下 **[索引]** 資料夾，並選取 **[全部重新組織]** 。  
  
5.  在 **[重新組織索引]** 對話方塊中，確認 **[要重新組織的索引]** 方格中有正確索引。 若要從 **[要重新組織的索引]** 方格中移除索引，請選取索引，然後按下 DELETE 鍵。  
  
6.  選取 **[壓縮大型物件資料行資料]** 核取方塊，可指定一併壓縮包含大型物件 (LOB) 資料的所有頁面。  
  
7.  按一下 [確定]  。  
  
#### <a name="to-rebuild-an-index"></a>若要重建索引  
  
1.  在 [物件總管] 中，展開包含您要重新組織其索引之資料表的資料庫。  
  
2.  展開 **[資料表]** 資料夾。  
  
3.  展開您要重新組織其索引的資料表。  
  
4.  展開 **[索引]** 資料夾。  
  
5.  以滑鼠右鍵按一下您要重新組織的索引，然後選取 **[重新組織]** 。  
  
6.  在 **[重建索引]** 對話方塊中，確認 **[要重建的索引]** 方格中有正確索引，然後按一下 **[確定]** 。  
  
7.  選取 **[壓縮大型物件資料行資料]** 核取方塊，可指定一併壓縮包含大型物件 (LOB) 資料的所有頁面。  
  
8.  按一下 [確定]  。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedureReorg"></a> 使用 Transact-SQL  
  
#### <a name="to-reorganize-a-defragmented-index"></a>若要重新組織重組的索引  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- Reorganize the IX_Employee_OrganizationalLevel_OrganizationalNode index on the HumanResources.Employee table.   
  
    ALTER INDEX IX_Employee_OrganizationalLevel_OrganizationalNode ON HumanResources.Employee  
    REORGANIZE ;   
    GO  
    ```  
  
#### <a name="to-reorganize-all-indexes-in-a-table"></a>若要重新組織資料表中的所有索引  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- Reorganize all indexes on the HumanResources.Employee table.  
    ALTER INDEX ALL ON HumanResources.Employee  
    REORGANIZE ;   
    GO  
    ```  
  
#### <a name="to-rebuild-a-defragmented-index"></a>若要重建重組的索引  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例會在 `Employee` 資料表上重建單一索引。  
  
     [!code-sql[IndexDDL#AlterIndex1](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex1)]  
  
#### <a name="to-rebuild-all-indexes-in-a-table"></a>若要重建資料表中全部的索引  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  將下列範例複製並貼入查詢視窗中。此範例會指定關鍵字 `ALL`。 這會重建與資料表相關聯的所有索引。 指定三個選項。  
  
     [!code-sql[IndexDDL#AlterIndex2](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex2)]  
  
 如需詳細資訊，請參閱 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft SQL Server 2000 索引重組最佳作法](https://technet.microsoft.com/library/cc966523.aspx)  
  
  
