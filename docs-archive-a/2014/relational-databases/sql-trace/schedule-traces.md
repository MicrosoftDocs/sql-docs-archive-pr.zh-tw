---
title: 排程追蹤 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], events
- traces [SQL Server]
- traces [SQL Server], stopping
- events [SQL Server], filters
- scheduling traces [SQL Server]
- traces [SQL Server], scheduling
- stopping traces
ms.assetid: 620b79db-924b-4502-8af3-39efcfca245d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a698d88db35c84f7611293cf45807203c883865a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597761"
---
# <a name="schedule-traces"></a>排程追蹤
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]有兩個方法可以排程追蹤。 您可以：  
  
-   啟用追蹤停止時間。  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來排程追蹤。  
  
## <a name="specifying-a-stop-time"></a>指定停止時間  
 如果使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序或 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，您可以指定追蹤停止時間。 最初設定追蹤時，必須設定停止時間。  
  
## <a name="scheduling-traces-by-using-sql-server-agent"></a>使用 SQL Server Agent 來排程追蹤  
 排程追蹤最好的方法是利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 啟動追蹤，然後使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序 **sp_trace_setstatus**或 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]指定追蹤停止時間。  
  
 **若要設定追蹤的結束時間篩選**  
  
 [根據事件結束時間篩選事件 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)  
  
## <a name="see-also"></a>另請參閱  
 [自動化管理工作 &#40;SQL Server Agent&#41;](../../ssms/agent/sql-server-agent.md)  
  
  
