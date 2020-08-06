---
title: 資料庫鏡像和全文檢索目錄 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- full-text catalogs [SQL Server], database mirroring
- catalogs [SQL Server], database mirroring
ms.assetid: e34072ae-fe8a-462d-bb03-02fa0987f793
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 39929f4bed6edbd1e8ec5c1b72dbe8f7aefeec68
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593573"
---
# <a name="database-mirroring-and-full-text-catalogs-sql-server"></a>資料庫鏡像和全文檢索目錄 (SQL Server)
  若要建立具有全文檢索目錄之資料庫的鏡像，請如往常使用備份來建立主體資料庫的完整資料庫備份，然後還原備份，以將該資料庫複製到鏡像伺服器。 如需詳細資訊，請參閱 [準備鏡像資料庫以進行鏡像 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)。  
  
## <a name="full-text-catalog-and-indexes-before-failover"></a>容錯移轉之前的全文檢索目錄和索引  
 在新建立的鏡像資料庫中，全文檢索目錄仍然和備份資料庫當時的目錄相同。 資料庫鏡像啟動之後，DDL 陳述式 (CREATE FULLTEXT CATALOG、ALTER FULLTEXT CATALOG、DROP FULLTEXT CATALOG) 所做的任何目錄層級變更都會記錄下來，並且傳送到鏡像伺服器，以便在鏡像資料庫上重新執行。 不過，索引層級變更不會在鏡像資料庫上重現，因為並未將它記錄到主體伺服器上。 因此，當全文檢索目錄的內容在主體資料庫上變更時，並不會在鏡像資料庫上同步處理全文檢索目錄的內容。  
  
## <a name="full-text-indexes-after-failover"></a>容錯移轉之後的全文檢索索引  
 容錯移轉之後，在新的主體伺服器上為全文檢索索引執行完整搜耙，對下列情況可能有其必要，而且很有幫助：  
  
-   如果關閉全文檢索索引上的變更追蹤功能，您必須使用下列陳述式，在該索引上啟動完整搜耙：  
  
     ALTER FULLTEXT INDEX ON *table_name* START FULL POPULATION  
  
-   如果全文檢索索引設定為自動變更追蹤，全文檢索索引便會自動同步處理。 不過，同步處理會稍微減緩全文檢索效能。 如果效能太慢，則可以將變更追蹤功能設為關閉後再重設為自動，藉以引起完整搜耙：  
  
    -   若要將變更追蹤設定為關閉：  
  
         ALTER FULLTEXT INDEX ON *table_name* SET CHANGE_TRACKING OFF  
  
    -   若要將變更追蹤設定為自動：  
  
         ALTER FULLTEXT INDEX ON *table_name* SET CHANGE_TRACKING AUTO  
  
    > [!NOTE]  
    >  若要查看自動變更追蹤是否已開啟，您可以使用 [OBJECTPROPERTYEX](/sql/t-sql/functions/objectproperty-transact-sql) 函數來查詢資料表的 **TableFullTextBackgroundUpdateIndexOn** 屬性。  
  
 如需詳細資訊，請參閱 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)。  
  
> [!NOTE]  
>  在容錯移轉後啟動搜耙，以及在還原作業後啟動搜耙，這兩者的運作方式完全相同。  
  
## <a name="after-forcing-service"></a>在強制服務之後  
 在將服務強制移轉到鏡像伺服器 (可能發生資料遺失) 之後，會啟動完整搜耙。 啟動完整搜耙所使用的方法將視全文檢索索引是否啟用變更追蹤而定。 如需詳細資訊，請參閱本主題前面的「容錯移轉之後的全文檢索索引」。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-index-transact-sql)   
 [資料庫鏡像 &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [備份並還原全文檢索目錄與索引](../../relational-databases/indexes/indexes.md)  
  
  
