---
title: 將追蹤結果儲存至檔案 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 74f80667-62f3-4e14-bb1a-f0c2b6ef3402
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 644fc812bbb4863c336ff2f53f5b2d67ee0a4d5e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585785"
---
# <a name="save-trace-results-to-a-file"></a>將追蹤結果儲存至檔案
  您可以將追蹤結果儲存至檔案。 追蹤檔案是用來寫入追蹤結果的檔案。 追蹤檔案可以位於本機目錄 (例如 C:\\  \\檔案名稱.trc  ) 或網路目錄 (例如 \\\電腦名稱\共用名稱\檔案名稱.trc)。  
  
 您可以使用追蹤檔案來執行下列動作：  
  
-   重新執行追蹤  
  
-   稽核 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   進行效能分析  
  
-   使追蹤事件與效能計數器相互關聯，以加強問題偵測  
  
-   執行 Database Engine Tuning Advisor 分析  
  
-   完成查詢最佳化。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]當 **@tracefile** 預存程式**sp_trace_create**的引數指定路徑和檔案名時，會將追蹤結果儲存至檔案。  
  
> [!NOTE]  
>  若要將路徑指定到 **sp_trace_create** 預存程序以儲存追蹤檔案，則其必須是伺服器可存取的目錄。 另請注意，若要在 **sp_trace_create**指定本機目錄，此目錄必須是伺服器電腦上的本機目錄。  
  
 如果使用了 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ，您就可以將追蹤結果儲存到檔案或資料表。 將追蹤結果儲存到資料表與將追蹤儲存到檔案一樣，都允許稍後進行存取，但是儲存到資料表還有一項優點，就是可以透過查詢資料表來搜尋特定事件。  
  
 如需儲存追蹤結果的詳細資訊，請參閱[將追蹤結果儲存到資料表 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md) 和[將追蹤結果儲存至檔案 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)。  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)   
 [建立追蹤 &#40;Transact-SQL&#41;](../sql-trace/create-a-trace-transact-sql.md)   
 [建立追蹤 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
  
