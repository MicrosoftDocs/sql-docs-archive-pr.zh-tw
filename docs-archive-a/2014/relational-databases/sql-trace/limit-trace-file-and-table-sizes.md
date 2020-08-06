---
title: 限制追蹤檔案和資料表的大小 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- maximum file size for traces
- traces [SQL Server], file size
- size [SQL Server], tables
- file rollover option [SQL Server]
- size [SQL Server], files
ms.assetid: 88c31b02-f44c-4a14-be8b-437f2097de12
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b7795dfdadb8fb3bbaa1b55dcd5c962d24a7ba29
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597763"
---
# <a name="limit-trace-file-and-table-sizes"></a>限制追蹤檔案和資料表的大小
  「SQL 追蹤」結果的大小視追蹤所包含的事件類別和 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的使用方式而定。 如果您追蹤經常發生的事件類別，可設定檔案大小上限或最大資料列數目，將追蹤收集的資料量降到最低。 透過指定檔案大小上限或最大資料列數目，您就可以確保追蹤檔或資料表不會擴展超過指定的限制。  
  
> [!NOTE]  
>  如果您將追蹤資料儲存到已存在的檔案，就可以將資料附加到檔案或覆寫檔案。 如果您選擇將資料附加到檔案，而追蹤檔已經達到或超過指定的檔案大小上限時，將會提醒您選擇增加檔案大小上限或指定新的檔案。 追蹤資料表也是如此。  
  
## <a name="maximum-file-size"></a>檔案大小上限  
 已設定檔案大小上限的追蹤，在達到檔案大小上限之後，將會停止儲存追蹤資訊。 此選項可讓您將事件分組為更小、更易於管理的檔案。 此外，限制檔案大小也可讓自動追蹤執行起來較為安全，因為在達到檔案大小上限時追蹤就會停止。 對於透過 Transact-SQL 預存程序或使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]建立的追蹤，您可以設定檔案大小上限。  
  
 檔案大小上限選項的上限是 1 GB。 預設的檔案大小上限是 5 MB。  
  
### <a name="enabling-file-rollover"></a>啟用檔案換用  
 檔案換用選項會使得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在達到最大檔案大小時，關閉目前的檔案並建立新的檔案。 新檔案與舊檔案的名稱一樣，但名稱會附加一個整數來代表其順序。 例如，若原始追蹤檔的名稱為 filename_1.trc，則下一個追蹤檔的名稱為 filename_2.trc，依此類推。 如果指派給新換用檔案的名稱已由現有的檔案使用，則會覆寫現有的檔案 (除非是唯讀)。 將追蹤資料儲存至檔案時，會預設啟用檔案復原選項。  
  
> [!NOTE]  
>  檔案換用選項開啟時，追蹤會一直繼續，直到被其他方法停止為止。 若要在您達到檔案大小限制後停止追蹤，請停用檔案換用選項。  
  
 **若要設定追蹤檔的大小上限**  
  
 [設定追蹤檔案的檔案大小上限 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)  
  
## <a name="maximum-number-of-rows"></a>最大資料列數目  
 已指定最大資料列數目的追蹤，在達到最大資料列數目之後，將會停止將追蹤資訊儲存到資料表。 每個事件佔有一個資料列，所以此參數會在蒐集的事件數目上設定限制。 設定最大資料列數目可以更容易執行自動追蹤。 例如，若您必須啟動追蹤，此追蹤會將追蹤資料儲存到資料表，但在資料表變得過大時必須停止追蹤，您可以自動執行這個動作。  
  
 若已指定最大資料列數目且已達到最大資料列數目時， [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 執行時追蹤也會繼續執行，但不會再記錄追蹤資訊。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 會繼續顯示追蹤結果，直到追蹤停止為止。  
  
 **若要設定追蹤的最大資料列數目**  
  
 [設定追蹤資料表的資料表大小上限 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)  
  
  
