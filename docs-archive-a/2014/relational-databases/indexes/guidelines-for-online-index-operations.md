---
title: 線上索引作業的指導方針 | Microsoft Docs
ms.custom: ''
ms.date: 11/11/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- clustered indexes, online operations
- online index operations
- indexes [SQL Server], online operations
- disk space [SQL Server], indexes
- nonclustered indexes [SQL Server], online operations
- transaction logs [SQL Server], indexes
ms.assetid: d82942e0-4a86-4b34-a65f-9f143ebe85ce
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 907fe6a826607fe1cb403ad9b8debe6faf6771fc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606307"
---
# <a name="guidelines-for-online-index-operations"></a>線上索引作業的指導方針
  當您執行線上索引作業時，下列指導方針將適用：  
  
-   當基礎資料表包含下列大型物件 (LOB) 資料類型： `image` 、 **Ntext**和時，必須離線建立、重建或卸載叢集索引 `text` 。  
  
-   您無法在線上建立、重建或卸除本機暫存資料表的索引。 此限制不適用於全域暫存資料表上的索引。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有版本都無法使用線上索引作業。 如需版本支援的功能清單 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請參閱[SQL Server 2014 版本支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
 下表顯示可以線上執行的索引作業以及從這些線上作業排除的索引。 也包含其他限制。  
  
|線上索引作業|排除索引|其他限制|  
|----------------------------|----------------------|------------------------|  
|ALTER INDEX REBUILD|已停用叢集索引或已停用索引檢視<br /><br /> XML 索引 <br /><br />資料行存放區索引<br /><br /> 本機暫存資料表上的索引|當資料表包含排除索引時，指定關鍵字 ALL 可能導致作業失敗。<br /><br /> 重建已停用索引的其他限制也適用。 如需詳細資訊，請參閱 [停用索引和條件約束](disable-indexes-and-constraints.md)。|  
|CREATE INDEX|XML 索引<br /><br /> 在檢視上的初始唯一叢集索引<br /><br /> 本機暫存資料表上的索引||  
|CREATE INDEX WITH DROP_EXISTING|已停用叢集索引或已停用索引檢視<br /><br /> 本機暫存資料表上的索引<br /><br /> XML 索引||  
|DROP INDEX|停用的索引<br /><br /> XML 索引<br /><br /> 非叢集索引<br /><br /> 本機暫存資料表上的索引|不能在單一陳述式中指定多個索引。|  
|ALTER TABLE ADD CONSTRAINT (PRIMARY KEY 或 UNIQUE)|本機暫存資料表上的索引<br /><br /> 叢集索引|一次僅允許一個子子句 (Subclause)。 例如，您無法在同一個 ALTER TABLE 陳述式中加入和卸除 PRIMARY KEY 或 UNIQUE 條件約束。|  
||||  
  
 處理線上索引作業時，不能修改、截斷或卸除基礎資料表。  
  
 當您建立或卸除叢集時，指定的線上選項設定 (ON 或 OFF) 會套用到必須重建的任何非叢集索引。 例如，若是使用 CREATE INDEX WITH DROP_EXISTING, ONLINE=ON 線上建立叢集索引，那麼也會線上重建所有相關聯的非叢集索引。  
  
 線上建立或重建 UNIQUE 索引時，此索引產生器與並行使用者交易可能嘗試要插入同一個索引鍵，因此而違反了唯一性。 若在原始資料列從來源資料表移動到新索引之前，將使用者輸入的資料列插入至新索引(目標)，線上索引作業將失敗。  
  
 雖然這種情形並不常見，但是由於使用者或應用程序活動的原因，線上索引作業與資料庫更新互動時，即會導致死結。 在這些極少數情況下， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 將選擇使用者或應用程序活動作為死結的犧牲者。  
  
 只有在建立多個新的非叢集索引或重新組織非叢集索引時，才能在同一個資料表或檢視上執行並行線上索引 DDL 作業。 同時執行的所有其他線上索引作業都會失敗。 例如，在同一個資料表中線上重建現有索引時，是無法線上建立新的索引。  
  
 如果索引包含大型物件類型的資料行，且在同一交易中另有更新作業早於線上作業，便無法執行該線上作業。 若要解決此問題，請將線上作業移出交易之外，或使其比交易中的任何更新都更早執行。  
  
## <a name="disk-space-considerations"></a>磁碟空間考量因素  
 通常，磁碟空間需求對於線上與離線作業是一樣的。 例外的情形是暫存對應索引需要額外的磁碟空間。 此暫存索引用於建立、重建或卸除叢集索引的線上索引作業。 線上卸除叢集索引與線上建立叢集索引需要一樣多的磁碟空間。 如需詳細資訊，請參閱 [Disk Space Requirements for Index DDL Operations](disk-space-requirements-for-index-ddl-operations.md)。  
  
## <a name="performance-considerations"></a>效能考量  
 雖然線上索引作業允許並行使用者更新活動，但是若更新活動負載繁重，此索引作業將需要更長時間。 一般而言，無論並行更新活動的程度，線上索引作業都將低於同等的離線索引作業。  
  
 由於線上索引作業期間都會維護來源與目標結構，因此會增加插入、更新與刪除交易時所耗用的資源，甚至可能加倍。 這在索引作業期間可能導致效能降低與資源過度耗用，尤其是 CPU 時間。 線上索引作業會完整記錄下來。  
  
 儘管我們推薦線上作業，但您應該評估您的環境與特定要求。 離線執行索引作業可能會是最佳方式。 若要達到這種方式，在作業期間，使用者僅能有限地存取資料，但是將更快完成作業且使用較少的資源。  
  
 在執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的多處理器電腦上，索引陳述式可能會如同其他查詢般，使用更多處理器來執行與索引陳述式相關聯的掃描和排序作業。 您可以使用 MAXDOP 索引選項控制線上索引作業專用的處理器數目。 以此方式，您就可以平衡索引作業所使用的資源以及使用者並行所使用的資源。 如需詳細資訊，請參閱 [設定平行索引作業](configure-parallel-index-operations.md)。 如需有關支援平行索引作業之 SQL Server 版本的詳細資訊，請參閱[SQL Server 2014 版本支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
 因為索引作業的最終階段會保留 S-lock 或 Sch-M 鎖定，所以在明確的使用者交易 (例如 BEGIN TRANSACTION...COMMIT 區塊) 內執行線上索引作業時要特別小心。 這樣做導致交易完後才執行鎖定，而妨礙使用者進行並行作業。  
  
 當線上索引重建可搭配 `MAX DOP > 1` 和 `ALLOW_PAGE_LOCKS = OFF` 選項執行時，可能會增加片段。 如需詳細資訊，請參閱 [運作方式：線上索引重建 - 可能會導致片段增加](https://blogs.msdn.com/b/psssql/archive/2012/09/05/how-it-works-online-index-rebuild-can-cause-increased-fragmentation.aspx)。  
  
## <a name="transaction-log-considerations"></a>交易記錄考量因素  
 大規模的索引作業，無論是離線或線上執行，都會產生大量資料負載，而很快就填滿了交易記錄。 若要確定可以回復索引作業，在索引作業完成以前，不能截斷交易記錄；不過，在索引作業期間可以備份此記錄。 因此，在索引作業期間，交易記錄必須有足夠的空間，才能儲存索引作業交易與任何並行使用者交易。 如需詳細資訊，請參閱 [索引作業的交易記錄磁碟空間](transaction-log-disk-space-for-index-operations.md)。  
  
## <a name="related-content"></a>相關內容  
 [線上索引作業如何運作](how-online-index-operations-work.md)  
  
 [線上執行索引作業](perform-index-operations-online.md)  
  
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)  
  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
  
