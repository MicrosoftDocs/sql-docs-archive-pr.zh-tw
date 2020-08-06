---
title: 預設追蹤已啟用伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], traces
- traces [SQL Server], logs
- default trace enabled option
ms.assetid: 1322d668-44f4-469e-8fd6-e0d02a81c8f2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8d40305de7375f2ae10d563871fd40b7acfa463f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707857"
---
# <a name="default-trace-enabled-server-configuration-option"></a>預設追蹤已啟用伺服器組態選項
  使用 **default trace enabled** 選項，啟用或停用預設的追蹤記錄檔。 預設追蹤功能可針對主要與組態選項相關的活動和變更提供豐富、永續的記錄檔。  
  
> [!WARNING]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用擴充事件。  
  
## <a name="purpose"></a>目的  
 預設追蹤可為資料庫管理員提供疑難排解協助，確定他們有必要的記錄檔資料，能在問題發生的第一時間進行診斷。  
  
## <a name="viewing"></a>檢視  
 預設追蹤記錄檔可由 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 開啟和檢查，或使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 系統函數，利用 `fn_trace_gettable` 進行查詢。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 開啟預設追蹤記錄檔的方式，與開啟一般追蹤輸出檔案一樣。 根據預設，預設追蹤記錄檔是使用換用追蹤檔案，儲存在 `\MSSQL\LOG` 目錄中。 預設追蹤記錄檔的基底檔案名稱是 `log.trc`。 在典型的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝中，會啟用預設追蹤，因此它會變成 TraceID 1。 如果在安裝之後及建立其他追蹤之後啟用它，此 TraceID 可能會變成較大的數目。  
  
 如需使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler 來檢視此追蹤檔案的詳細資訊，請參閱[開啟追蹤檔案 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)  
  
### <a name="example"></a>範例：  
 以下陳述式可開啟預設位置中的預設追蹤記錄檔：  
  
```  
SELECT *   
FROM fn_trace_gettable  
('C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\LOG\log.trc', default);  
GO  
  
```  
  
## <a name="configuring"></a>進行設定  
 設為 1 時， **default trace enabled** 選項會啟用 **「預設的追蹤」** 功能。 這個選項的預設值是 1 (ON)。 設為 0 則會關閉追蹤功能。  
  
 **default trace enabled** 屬於進階選項。 如果您要使用 **sp_configure** 系統預存程序來變更設定，只有在 [顯示進階選項] 設定為 1 時，才能變更 [預設追蹤已啟用] 選項。 設定會立即生效，伺服器不必重新啟動。  
  
## <a name="see-also"></a>另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
