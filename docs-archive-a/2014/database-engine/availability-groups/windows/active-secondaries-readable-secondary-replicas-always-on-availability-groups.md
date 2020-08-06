---
title: 作用中次要資料庫：可讀取的次要複本 (Always On 可用性群組) |Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- connection access to availability replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- readable secondary replicas
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 78f3f81a-066a-4fff-b023-7725ff874fdf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8b85704b8110eb84ea6f4c33dfa79694112c2328
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87607104"
---
# <a name="active-secondaries-readable-secondary-replicas-always-on-availability-groups"></a>使用中次要：可讀取的次要複本 (AlwaysOn 可用性群組)
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 使用中次要功能包含對一個或多個次要複本進行唯讀存取的支援 ( *「可讀取的次要複本」* (Readable Secondary Replicas))。 可讀取的次要複本允許對其所有次要資料庫進行唯讀存取。 但可讀取的次要資料庫並不會設定為唯讀。 這些資料庫是動態的。 隨著對應主要資料庫變更而衍生的給定次要資料庫變更，會套用至次要資料庫。 對於一般次要複本而言，次要資料庫中的資料 (包含持久記憶體最佳化資料表) 幾近即時。 此外，全文檢索索引會與次要資料庫進行同步處理。 在許多情況下，主要資料庫和對應次要資料庫之間的資料延遲只在幾秒鐘內。  
  
 主要資料庫中進行的安全性設定會保存到次要資料庫。 其中包括使用者、資料庫角色和應用程式角色，連同其各自的權限，以及透明資料加密 (TDE) (如果主要資料庫上已啟用)。  
  
> [!NOTE]  
>  雖然您無法將資料寫入次要資料庫，但是您可以寫入裝載次要複本的伺服器執行個體上的讀寫資料庫，包括使用者資料庫和系統資料庫 (例如 **tempdb**)。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 也可將讀取意圖的連接要求重新路由到可讀取的次要複本 ( *「唯讀路由」* (Read-Only Routing))。 如需唯讀路由的相關資訊，請參閱 [使用接聽程式連接到唯讀次要複本 (唯讀路由)](../../listeners-client-connectivity-application-failover.md#ConnectToSecondary)。  
  
 
  
##  <a name="benefits"></a><a name="bkmk_Benefits"></a> 優點  
 將唯讀連接導向至可讀取的次要複本，具有下列優點：  
  
-   從主要複本卸載次要唯讀工作負載，將主要複本的資源保留給關鍵任務工作負載使用。 如果您有關鍵任務的讀取工作負載或不能容忍延遲的工作負載，則應該在主要複本上執行此工作負載。  
  
-   提高裝載可讀取次要複本之系統的投資報酬率。  
  
 此外，可讀取的次要複本對唯讀作業提供強大的支援，如下：  
  
-   可讀取次要資料庫的自動暫時統計資料會最佳化磁碟資料表的唯讀查詢。 對於記憶體最佳化的資料表，系統會自動建立遺漏的統計資料。 不過，過時的統計資料不會自動更新。 您必須手動更新主要複本的統計資料。 如需詳細資訊，請參閱本主題稍後的 [唯讀存取資料庫的統計資料](#Read-OnlyStats)。  
  
-   以磁碟資料表的唯讀工作負載，會使用資料列版本設定以移除對於次要資料庫的封鎖競爭。 針對次要資料庫執行的所有查詢都會自動對應到快照集隔離交易層級，即使已明確設定其他交易隔離等級也是如此。 此外，所有鎖定提示都會被忽略。 這排除了讀取器/寫入器競爭。  
  
-   記憶體最佳化持久資料表的唯讀工作負載存取資料的方式，與主要資料庫上的存取方式完全相同，都是使用原生預存程序或 SQL 互通性，而且具有相同的交易隔離等級限制。 在主要複本上執行的報表工作負載或唯讀查詢可以在次要複本上執行，不需要任何變更。 同樣地，在次要複本上執行的報表工作負載或唯讀查詢也可以在主要複本上執行，不需要任何變更。  與磁碟基礎的資料表類似，對次要資料庫執行的所有查詢都會自動對應到快照集隔離交易層級，即使已明確設定其他交易隔離等級也是如此。  
  
-   次要複本上以磁碟為基礎和記憶體最佳化資料表類型，都允許對資料表變數進行 DML 作業。  
  
##  <a name="prerequisites-for-the-availability-group"></a><a name="bkmk_Prerequisites"></a> 可用性群組的必要條件  
  
-   **可讀取的次要複本 (必要)**  
  
     資料庫管理員必須設定一個或多個複本，以便在以次要角色執行時，這些複本可以允許所有連接 (僅供唯讀存取) 或只允許讀取意圖的連接。  
  
    > [!NOTE]  
    >  除此之外，資料庫管理員也可選擇在以主要角色執行時，將可用性複本設定為排除唯讀連接。  
  
     如需詳細資訊，請參閱本主題稍後的 [關於可用性複本的用戶端連接存取 &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md))。  
  
-   **可用性群組接聽程式**  
  
     若要支援唯讀路由，可用性群組必須具有 [可用性群組接聽程式](../../listeners-client-connectivity-application-failover.md)。 唯讀用戶端必須將其連接要求導向至此接聽程式，且用戶端的連接字串必須將應用程式的意圖指定為「唯讀」。 換句話說必須是 *「讀取意圖的連接要求」* (Read-Intent Connection Request)。  
  
-   **唯讀路由**  
  
     *「唯讀路由」* (Read-Only Routing) 是 SQL Server 功能，可將導向至可用性群組接聽程式之內送讀取意圖的連接要求，路由至可用之可讀取的次要複本。 唯讀路由的必要條件如下：  
  
    -   若要支援唯讀路由，可讀取的次要複本需要唯讀路由 URL。 只有在本機複本以次要角色執行時，此 URL 才會生效。 如有必要，您必須各自指定每個複本的唯讀路由 URL。 每個唯讀路由 URL 可用於將讀取意圖的連接要求路由至特定可讀取的次要複本。 一般而言，每個可讀取的次要複本都有一個指派的唯讀路由 URL。  
  
    -   當支援唯讀路由的可用性複本為主要複本時，每一個可用性複本皆需要唯讀路由清單。 只有本機複本以主要角色執行時，給定的唯讀路由清單才會生效。 如有必要，您必須各自指定每個複本的這份清單。 一般而言，每份唯讀路由清單皆會包含每一個唯讀路由 URL，並在清單結尾提供本機複本的 URL。  
  
        > [!NOTE]  
        >  讀取意圖的連接要求會路由至目前之主要複本的唯讀路由清單上，第一個可用之可讀取的次要複本。 沒有負載平衡。  
  
     如需詳細資訊，請參閱本主題稍後的 [設定可用性群組的唯讀路由 &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md))。  
  
> [!NOTE]  
>  如需可用性群組接聽程式的相關資訊，以及唯讀路由的詳細資訊，請參閱 [可用性群組接聽程式、用戶端連接性及應用程式容錯移轉 &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)。  
  
##  <a name="limitations-and-restrictions"></a><a name="bkmk_LimitationsRestrictions"></a> 限制事項  
 某些作業未完全受到支援，如下所示：  
  
-   一旦可讀取的複本啟用讀取之後，它就可以開始接受其次要資料庫的連接。 但是，如果主要複本上有任何使用中交易，在對應的次要資料庫上無法完全使用資料列版本。 設定次要複本時，主要複本上若有使用中交易，則必須認可或回復這些交易。 完成此程序之前，次要資料庫的交易隔離等級對應並不完整，而且查詢會暫時封鎖。  
  
    > [!WARNING]  
    >  對於磁碟和記憶體最佳化資料表，執行長時間交易都會影響保存的版本資料列數目。  
  
-   在具有記憶體最佳化資料表的次要資料庫上，即使系統一定會對記憶體最佳化的資料表產生資料列版本，查詢仍然會遭到封鎖，直到次要複本啟用讀取時，存在於主要複本中的所有使用中交易都完成為止。 這樣可確保報表工作負載與唯讀查詢可以同時使用磁碟基礎的和記憶體最佳化的資料表。  
  
-   在屬於可讀取次要複本的次要資料庫上，不支援變更追蹤和異動資料擷取：  
  
    -   次要資料庫上已明確停用變更追蹤。  
  
    -   次要資料庫上可以啟用異動資料擷取，但是這不受支援。  
  
-   由於讀取作業會對應至快照集隔離交易層級，因此一個或多個次要複本上的交易會封鎖在主要複本上的準刪除記錄清除。 當任何次要複本不再需要準刪除記錄時，準刪除記錄清除工作會自動清除主要複本上以磁碟為基礎之資料表的準刪除記錄。  這類似於在主要複本上執行交易時所完成的作業。 在次要資料庫的極端案例，您需要終止長時間執行、封鎖準刪除清除的讀取查詢。 請注意，如果次要複本中斷連接或在次要資料庫上的資料移動暫停時，可能會封鎖準刪除清除。 這種狀態也會防止記錄截斷，因此如果此狀態持續發生，建議您從可用性群組中移除此次要資料庫。 記憶體最佳化的資料表沒有任何準刪除記錄清除問題，因為資料列版本保留在記憶體中，而且獨立於主要複本上的資料列版本。  
  
-   若檔案包含了次要複本所需要的準刪除記錄，則主要複本上對於包含以磁碟為基礎資料表之檔案的 DBCC SHRINKFILE 作業可能會失敗。  
  
-   從 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]開始，即使主要複本由於使用者動作或失敗而離線，可讀取的次要複本依然可以維持在線上。 但是，唯讀路由在此情況下無法運作，因為可用性群組接聽程式也離線。 用戶端必須直接連接到唯讀工作負載的唯讀次要複本。  
  
> [!NOTE]  
>  對裝載可讀取之次要複本的伺服器執行個體上查詢 [sys.dm_db_index_physical_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql) 動態管理檢視時，可能會發生 REDO 封鎖問題。 這是因為此動態管理檢視會取得指定使用者資料表或檢視表的 IS 鎖定，並因此而封鎖了對該使用者資料表或檢視表之 X 鎖定的 REDO 執行緒要求。  
  
##  <a name="performance-considerations"></a><a name="bkmk_Performance"></a> 效能考量  
 本節討論可讀取次要資料庫的數項效能考量。  
  
 
  
###  <a name="data-latency"></a><a name="DataLatency"></a> 資料延遲  
 如果您的唯讀工作負載可以容忍某些資料延遲時，實作次要複本的唯讀存取會很有用。 在無法接受資料延遲的狀況下，請考慮針對主要複本執行唯讀工作負載。  
  
 主要複本上會將主要資料庫變更的記錄檔記錄傳送到次要複本。 在每個次要資料庫上，專用的重做執行緒會套用記錄檔記錄。 在讀取存取的次要資料庫上，給定資料變更不會出現在查詢結果，除非包含變更的記錄檔記錄已套用至次要資料庫，而且已經在主要資料庫認可交易。  
  
 這表示，主要複本和次要複本之間會有一些延遲 (通常只有幾秒鐘)。 但在很少見的情況下 (例如網路問題減少輸送量的狀況下)，延遲可能會比較長。 在發生 I/O 瓶頸和資料移動暫停時，會增加延遲。 若要監視暫停的資料移動，您可以使用 [AlwaysOn 儀表板](use-the-always-on-dashboard-sql-server-management-studio.md) 或 [sys.dm_hadr_database_replica_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql) 動態管理檢視。  
  
####  <a name="data-latency-on-databases-with-memory-optimized-tables"></a><a name="bkmk_LatencyWithInMemOLTP"></a> 具有記憶體最佳化資料表之資料庫的資料延遲  
 為讀取工作負載存取次要複本上的記憶體最佳化資料表時，會使用「安全時間戳記」 ** ，從早於「安全時間戳記」 ** 認可的交易傳回資料列。 安全時間戳記是記憶體回收執行緒所使用之最舊的時間戳記提示，可在主要複本上進行資料列的記憶體回收。 當記憶體最佳化資料表上的 DML 交易數目超出上次更新時的內部臨界值，就會更新此時間戳記。 每當主要複本上最舊的交易時間戳記更新時，持久記憶體最佳化資料表上的下一個 DML 交易會將要傳送到次要複本的時間戳記，做為特定記錄檔記錄的一部分傳送。 次要複本上的 REDO 執行緒會在處理此記錄檔記錄時，更新安全時間戳記。  
  
#### <a name="the-impact-of-safe-timestamp-on-latency"></a>安全時間戳記對延遲的影響  
  
-   對於具有高交易輸送量的 OLTP 工作負載，延遲應該與磁碟基礎的資料表類似。 我們預期此為常見情況。  
  
-   長時間執行的交易可能會造成安全時間戳記任意延遲。  存取磁碟基礎的資料表時也一樣，因為快照集隔離的時間戳記取決於最舊交易的認可。  
  
-   自上次安全時間戳記更新後，在主要複本上由交易所做的變更，直到下一次傳輸和更新安全時間戳記之前，都不會在次要複本上看到。 若在超過安全時間戳記更新的內部臨界值之前，主要複本上的交易活動停止，則不會在次要複本上看到上次安全時間戳記變更後所進行的變更。 若要減少此類問題發生，您可能需要在主要複本上，於一個虛擬持久記憶體最佳化的資料表中執行一些 DML 交易。 或者，雖然不建議這麼做，但您可以執行手動檢查點，強制執行安全時間戳記傳送。  
  
#### <a name="monitoring-and-troubleshooting-data-latency-in-memory-optimized-tables"></a>監視和疑難排解記憶體最佳化資料表中的資料延遲  
 您可以藉由在主要複本上執行下列查詢，找出安全時間戳記  
  
```  
  
SELECT MAX(base_generation)   
   AS max_base_generation  
   FROM sys.dm_db_xtp_gc_cycle_stats  
GO  
  
```  
  
 您也可以藉由同時執行下列查詢與使用中讀取工作負載，識別次要複本上使用的安全時間戳記。  
  
```  
  
SELECT begin_tsn   
   FROM sys.dm_db_xtp_transactions  
GO  
  
```  
  
###  <a name="read-only-workload-impact"></a><a name="ReadOnlyWorkloadImpact"></a> 唯讀工作負載的影響  
 將次要複本設定為唯讀存取時，次要資料庫上的唯讀工作負載會耗用系統資源，例如重做執行緒的 CPU 和 I/O (針對以磁碟為基礎之資料表)，特別是當以磁碟為基礎之資料表的唯讀工作負載高密度使用 I/O 資料時。 存取記憶體最佳化的資料表時，不會造成任何 IO 影響，因為所有資料列都位於記憶體中。  
  
 此外，次要複本上的唯讀工作負載可以封鎖透過記錄檔記錄套用的資料定義語言 (DDL) 變更。  
  
-   雖然讀取作業因為資料列版本設定的緣故而不會取得共用鎖定，但是這些作業會取得結構描述穩定性 (Sch-S) 鎖定，而這些鎖定可能會封鎖套用 DDL 變更的重做作業。 DDL 作業包含 ALTER/DROP 資料表和檢視表，但不包含 DROP 或 ALTER 預存程序。 因此，假設您在主要複本上卸除磁碟或記憶體最佳化資料表。 當 REDO 執行緒處理記錄檔記錄以卸除資料表時，它必須取得資料表的 SCH_M 鎖定，而且可能會由存取資料表的執行中查詢封鎖。  此行為與主要複本相同，但是資料表的卸除是在使用者工作階段中完成，而非由 REDO 執行緒完成。  
  
-   還有其他封鎖中的記憶體最佳化資料表。 如果次要複本有同時執行的原生預存程序，則卸除原生預存程序可能會導致 REDO 執行緒封鎖。 此行為與主要複本相同，但是預存程序的卸除是在使用者工作階段中完成，而非由 REDO 執行緒完成。  
  
 請查明建立查詢的最佳作法，並在次要資料庫中執行這些最佳作法。 例如，將長時間執行的查詢 (如資料彙總) 安排在活動較少的期間執行。  
  
> [!NOTE]  
>  如果重做執行緒遭到次要複本上的查詢封鎖，便會引發 **sqlserver.lock_redo_blocked** XEvent。  
  
###  <a name="indexing"></a><a name="bkmk_Indexing"></a> 索引  
 若要將可讀取次要複本上的唯讀工作負載最佳化，您可能會想要在次要資料庫的資料表上建立索引。 因為您無法在次要資料庫上進行結構描述或資料變更，所以請在主要資料庫中建立索引，並允許透過重做處理序將變更傳送到次要資料庫。  
  
 若要監視次要複本的索引使用活動，請查詢 **sys.dm_db_index_usage_stats**動態管理檢視的 **user_seeks**、 **user_scans** 和 [user_lookups](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql) 資料行。  
  
###  <a name="statistics-for-read-only-access-databases"></a><a name="Read-OnlyStats"></a> 唯讀存取資料庫的統計資料  
 資料表資料行和索引檢視表的統計資料可用來最佳化查詢計劃。 對於可用性群組而言，在主要資料庫上建立和維護的統計資料會自動保存至次要資料庫，做為交易記錄檔記錄應用的一部分。 然而，次要資料庫上的唯讀工作負載所需的統計資料，可能與主要資料庫上所建立的統計資料不同。 但因次要資料庫受限為唯讀存取，所以無法在次要資料庫上建立統計資料。  
  
 為了解決此問題，次要複本會在 **tempdb**中建立及維護次要資料庫的暫時統計資料。 暫時統計資料名稱會附加後置詞 suffix _readonly_database_statistic，以便區分暫時統計資料與主要資料庫中保存的永久統計資料。  
  
 只有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以建立和更新暫時統計資料。 但是，您可以使用永久統計資料所使用的相同工具來刪除暫時統計資料及監控其屬性：  
  
-   使用 [DROP STATISTICS](/sql/t-sql/statements/drop-statistics-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式刪除暫時統計資料。  
  
-   使用 **sys.stats** 和 **sys.stats_columns** 目錄檢視監視統計資料。 **sys_stats** 包含 **is_temporary**資料行，以表示哪些統計資料為永久性而哪些統計資料為暫時性。  
  
 主要或次要複本上的記憶體最佳化資料表都不支援自動統計資料更新。 您必須監視次要複本的查詢效能和計劃，並且視需要手動更新主要複本的統計資料。 不過，系統會自動建立主要和次要複本的遺漏統計資料。  
  
 如需 SQL Server 統計資料的詳細資訊，請參閱 [統計資料](../../../relational-databases/statistics/statistics.md)。  
  

  
####  <a name="stale-permanent-statistics-on-secondary-databases"></a><a name="StalePermStats"></a> 次要資料庫上過時的永久統計資料  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會偵測次要資料庫上的永久統計資料何時過時。 但除了對主要資料庫所做的變更以外，無法對永久統計資料進行變更。 為達到查詢最佳化， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會在次要資料庫上建立以磁碟為基礎之資料表的暫時統計資料，並且使用這些統計資料以取代過時的永久統計資料。  
  
 在主要資料庫上更新永久統計資料時，這些統計資料會自動保存至次要資料庫。 然後 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會使用更新的永久統計資資料 (比暫時統計資料還要新)。  
  
 如果可用性群組容錯移轉，所有次要複本上的暫時統計資料都會被刪除。  
  
####  <a name="limitations-and-restrictions"></a><a name="StatsLimitationsRestrictions"></a> 限制事項  
  
-   因為暫時統計資料會儲存在 **tempdb**中，所以重新啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務會導致所有暫時統計資料消失。  
  
-   後置詞 _readonly_database_statistic 會保留給 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]產生的統計資料使用。 當您在主要資料庫上建立統計資料時，將無法使用這個後置詞。 如需詳細資訊，請參閱[統計資料](../../../relational-databases/statistics/statistics.md)。  
  
##  <a name="accessing-memory-optimized-tables-on-a-secondary-replica"></a><a name="bkmk_AccessInMemTables"></a> 存取次要複本上的記憶體最佳化資料表  
 次要複本的讀取工作負載隔離等級僅限於主要複本允許的隔離等級。 系統不會針對次要複本進行任何隔離等級對應。 這樣可確保任何可在主要複本上執行的報表工作負載都能夠在次要複本上執行，不需要任何變更。 如此可讓您輕鬆地將報表工作負載從主要複本移轉至次要複本，反之亦然 (次要複本無法使用時)。  
  
 下列查詢無法在次要複本上執行，其失敗狀況與主要複本很相似。  
  
-   對於只在記憶體最佳化資料表上執行的查詢，支援的隔離等級只有快照集、可重複讀取和可序列化。 除非您在資料庫層級啟用 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT 選項，否則所有具有讀取未認可或讀取認可隔離等級的查詢都會傳回錯誤。  
  
    ```sql  
    SET TRANSACTION ISOLATION LEVEL READ_COMMITTED  
    -- This is not allowed  
    BEGIN TRAN  
    SELECT * FROM t_hk  
    COMMIT  
  
    ```  
  
     錯誤訊息：  
  
    ```  
    Msg 41368, Level 16, State 0, Line 2  
    Accessing memory optimized tables using the CREAD_COMMITTED isolation level is supported only for autocommit transactions. It is not supported for explicit or implicit transactions. Provide a supported isolation level for the memory optimized table using a table hing, such as WITH (SNAPSHOT).  
    ```  
  
-   記憶體最佳化資料表不支援任何鎖定提示。 例如，下列所有查詢都會失敗並出現錯誤。 僅允許 NOLOCK 提示，而搭配記憶體最佳化資料表使用時，則為 NOOP。  
  
    ```sql  
    SELECT * FROM t_hk WITH (PAGLOCK)  
    SELECT * FROM t_hk WITH (READPAST)  
    SELECT * FROM t_hk WITH (ROWLOCK)  
    SELECT * FROM t_hk WITH (READPAST)  
    SELECT * FROM t_hk WITH (TABLOCK)  
    SELECT * FROM t_hk WITH (XLOCK)  
    SELECT * FROM t_hk WITH (UPDLOCK)  
    ```  
  
-   針對跨容器交易，不支援具有會話隔離等級「快照集」的交易來存取記憶體優化資料表。 例如  
  
    ```sql  
    SET TRANSACTION ISOLATION LEVEL SNAPSHOT  
    -- This is not allowed  
    BEGIN TRAN  
       SELECT * FROM t_hk  
    COMMIT  
    ```  
  
     錯誤訊息：  
  
    ```  
    Msg 41332, Level 16, State 0, Line 5  
    Memory optimized tables and natively compiled stored procedures cannot be accessed or created when the session TRANSACTION ISOLATION LEVEL is set to SNAPSHOT.  
    ```  
  
##  <a name="capacity-planning-considerations"></a><a name="bkmk_CapacityPlanning"></a> 容量規劃考量  
  
-   在以磁碟為基礎之資料表案例中，可讀取的次要複本需要 **tempdb** 的空間主要基於以下兩個原因：  
  
    -   快照集隔離等級會將資料列版本複製到 **tempdb**中。  
  
    -   在 **tempdb**中建立和維護次要資料庫的暫時統計資料。 暫時統計資料會導致 **tempdb**略微增大。 如需詳細資訊，請參閱本節稍後的 [唯讀存取資料庫的統計資料](#Read-OnlyStats)。  
  
-   當您設定一個或多個次要複本的讀取權時，主要資料庫會在已刪除、修改或插入的資料列上增加 14 個位元組的額外負擔，以便在以磁碟為基礎之資料表的次要資料庫上，儲存資料列版本的指標。 此 14 個位元組的額外負擔會轉至次要資料庫。 將 14 個位元組的負擔增加到資料列時，可能會發生頁面分割。  
  
     主要資料庫不會產生資料列版本資料， 而是由次要資料庫產生資料列版本。 不過，資料列版本設定會同時增加主要和次要資料庫的資料儲存量。  
  
     系統是否新增資料列版本資料，取決於主要資料庫的快照集隔離或讀取認可快照集隔離 (RCSI) 等級設定。 下表描述在不同磁碟資料表的設定下可讀取次要資料庫的版本設定行為。  
  
    |可讀取的次要複本？|已啟用快照集隔離或 RCSI 等級？|主要資料庫|次要資料庫|  
    |---------------------------------|-----------------------------------------------|----------------------|------------------------|  
    |否|否|沒有資料列版本或 14 個位元組的負擔|沒有資料列版本或 14 個位元組的負擔|  
    |否|是|有資料列版本和 14 個位元組的負擔|沒有資料列版本，但有 14 個位元組的負擔|  
    |是|否|沒有資料列版本，但有 14 個位元組的負擔|有資料列版本和 14 個位元組的負擔|  
    |是|是|有資料列版本和 14 個位元組的負擔|有資料列版本和 14 個位元組的負擔|  
  
##  <a name="related-tasks"></a><a name="bkmk_RelatedTasks"></a> 相關工作  
  
-   [設定可用性複本的唯讀存取 &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [設定可用性群組的唯讀路由 &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [建立或設定可用性群組接聽程式 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [監視可用性群組 &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)  
  
-   [檢視可用性複本屬性 &#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)  
  
-   [使用新增可用性群組對話方塊 &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 相關內容  
  
-   [SQL Server AlwaysOn 團隊部落格：官方 SQL Server AlwaysOn 團隊部落格](https://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [關於可用性複本的用戶端連線存取 &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)   
 [可用性群組接聽程式、用戶端連接性及應用程式容錯移轉 &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [統計資料](../../../relational-databases/statistics/statistics.md)  
  
  
