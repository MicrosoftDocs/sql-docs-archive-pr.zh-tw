---
title: 使用記憶體最佳化資料表的需求 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 47d9a7e8-c597-4b95-a58a-dcf66df8e572
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ecb9d388fd0e1362bb8844e874cd89162912e93e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707557"
---
# <a name="requirements-for-using-memory-optimized-tables"></a>使用記憶體最佳化資料表的需求
  除了[安裝 SQL Server 2014 的硬體和軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)以外，以下是使用記憶體內部 OLTP 的需求：  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]64 位元 Enterprise、Developer 或 Evaluation Edition。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要足夠的記憶體，以容納記憶體最佳化的資料表和索引中的資料。 為了說明資料列版本，您應該提供記憶體最佳化的資料表和索引預期大小兩倍的記憶體數量。 但是所需的實際記憶體數目將取決於您的工作負載。 您應該監視記憶體使用量並視需要進行調整。 記憶體最佳化資料表的資料大小不得超過集區所允許的百分比。 若要探索記憶體優化資料表的大小，請參閱[sys.databases &#40;transact-sql&#41;的 dm_db_xtp_table_memory_stats ](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql)。  
  
     如果資料庫中有以磁碟為基礎的資料表，您需要提供足夠的記憶體，讓緩衝集區和查詢能夠在這些資料表上進行處理。  
  
     請務必了解記憶體中 OLTP 應用程式需要多少記憶體。 如需詳細資訊，請參閱 [估計記憶體最佳化資料表的記憶體需求](memory-optimized-tables.md) 。  
  
-   釋放持久的記憶體最佳化資料表大小的兩倍磁碟空間。  
  
-   處理器需要支援指令 **cmpxchg16b** 以使用記憶體內部 OLTP。 所有新型 64 位元處理器都支援 **cmpxchg16b**。  
  
     如果您使用 VM 主機應用程式，並 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 顯示較舊處理器造成的錯誤，請查看應用程式是否有允許**cmpxchg16b**的設定選項。 如果沒有，您可以使用 Hyper-V，它可以支援 **cmpxchg16b** ，而不需要修改組態選項。  
  
-   若要安裝記憶體中 OLTP，請在您安裝 **時選取** [Database Engine Services] [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。  
  
     若要安裝報表產生 ([判斷是否應將資料表或預存程式移植到記憶體內部 oltp](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) ，並 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] (透過物件總管) 來管理記憶體內部 oltp [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，請選取 [**管理工具-基本**] 或 [**管理工具-** 在安裝時進行 Advanced] [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 。  
  
## <a name="important-notes-on-using-hek_2"></a>使用 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]的重要注意事項  
  
-   資料庫中所有持久資料表的記憶體中大小總計不應該超過 250 GB。 如需詳細資訊，請參閱[記憶體優化資料表的持久性](durability-for-memory-optimized-tables.md)。  
  
-   這個 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 版本的目標是在含有 2 或 4 個通訊端且少於 60 個核心的系統上可以最佳化方式執行。  
  
-   檢查點檔案無法手動刪除。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會對不需要的檢查點檔案自動執行記憶體回收。 如需詳細資訊，請參閱在[記憶體優化資料表的持久性](durability-for-memory-optimized-tables.md)中合併資料和差異檔案的討論。  
  
-   在此第一版記憶體中 OLTP (在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]裡) 中，移除記憶體最佳化檔案群組唯一的方式就是卸除資料庫。  
  
-   如果您在嘗試刪除大批資料列時，有並行的插入或更新工作負載會影響您正嘗試刪除的資料列範圍，則刪除作業可能會失敗。 解決方法是先停止插入或更新工作負載，然後執行刪除。 或者，您也可以將交易設定為較小的交易，這樣做比較不容易受到並行工作負載所中斷。 如同記憶體最佳化資料表上的所有寫入作業，使用重試邏輯 ([Guidelines for Retry Logic for Transactions on Memory-Optimized Tables](../../database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md))。  
  
-   如果您建立一個或多個具有記憶體最佳化資料表的資料庫，就應該針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體啟用立即檔案初始化 (將 SE_MANAGE_VOLUME_NAME 使用者權限授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務啟動帳戶)。 如果沒有立即檔案初始化，記憶體最佳化儲存體檔案 (資料和差異檔案) 將會在建立時初始化，而這樣可能會對工作負載的效能造成負面影響。 如需有關立即檔案初始化的詳細資訊，請參閱 [資料庫檔案初始化](../databases/database-instant-file-initialization.md)。 如需有關如何啟用立即檔案初始化的詳細資訊，請參閱 [如何及為何啟用立即檔案初始化](https://blogs.msdn.com/b/sql_pfe_blog/archive/2009/12/23/how-and-why-to-enable-instant-file-initialization.aspx)。  
  
## <a name="did-this-article-help-you-were-listening"></a>這篇文章對您有幫助嗎？ 我們正在接聽  
 您要尋找哪些資訊？找到了嗎？ 我們正在聆聽您的意見反應以改善內容。 請將您的意見提交至 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Requirements%20for%20Using%20Memory-Optimized%20Tables%20page) 。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](in-memory-oltp-in-memory-optimization.md)  
  
  
