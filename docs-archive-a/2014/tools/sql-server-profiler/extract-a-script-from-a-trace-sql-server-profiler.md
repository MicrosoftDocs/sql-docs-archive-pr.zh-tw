---
title: 從追蹤中擷取指令碼 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- scripts [SQL Server], traces
- extracting script from trace [SQL Server]
ms.assetid: 431126a6-ff91-4818-8763-4442152bd571
author: stevestein
ms.author: sstein
ms.openlocfilehash: f6633fafb8a39b189093044ef39694afa601af7c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686589"
---
# <a name="extract-a-script-from-a-trace-sql-server-profiler"></a>從追蹤中擷取指令碼 (SQL Server Profiler)
  此主題描述如何從追蹤檔案或資料表中擷取 [!INCLUDE[tsql](../../includes/tsql-md.md)] 事件，並利用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 將它們儲存為 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]指令碼檔案。  
  
### <a name="to-extract-a-transact-sql-script-from-a-trace-file-or-table"></a>若要從追蹤檔案或資料表中擷取 Transact-SQL 指令碼  
  
1.  開啟包含您要儲存到 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼檔案之 [!INCLUDE[tsql](../../includes/tsql-md.md)] 事件的追蹤檔案或資料表。 如需詳細資訊，請參閱 [開啟追蹤檔案 &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) 或 [開啟追蹤資料表 &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)隨附的預先定義「微調」範本。  
  
2.  在 [檔案]  功能表上，依序指向 [匯出]  和 [擷取 SQL Server 事件]  ，然後按一下 [擷取 Transact-SQL 事件]  。  
  
3.  在 **[另存新檔]** 對話方塊中，輸入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 檔案的名稱，然後按一下 **[儲存]** 。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
