---
title: 重新執行追蹤 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Profiler, replaying traces
- Run to Cursor option
- Toggle Breakpoint option
- traces [SQL Server], replaying
- replaying traces
- playback engine [SQL Server Profiler]
- events [SQL Server], replaying traces
- Profiler [SQL Server Profiler], replaying traces
ms.assetid: da958d3c-7f3e-44c9-aecc-8a9493bea7c0
author: stevestein
ms.author: sstein
ms.openlocfilehash: c485317d1343958f9c430b73d858130097d44d75
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705729"
---
# <a name="replay-traces"></a>重新執行追蹤
  重新執行是重現追蹤中已擷取之活動的能力。 建立或編輯追蹤時，您可以將追蹤儲存至檔案，稍後重新執行它。 您可以使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ，從單一電腦重新執行追蹤活動。 如果是大型工作負載，請使用 Distributed Replay Utility，從多部電腦重新執行追蹤資料。  
  
 本節描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]的重新執行功能。 如需有關 Distributed Replay Utility 的詳細資訊，請參閱 [SQL Server Distributed Replay](../distributed-replay/sql-server-distributed-replay.md)。  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 具有多執行緒播放引擎的功能，可以模擬使用者連線及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 重新執行在排解應用程式或處理序的疑難問題時很有用。 當您找出問題並實作更正後，可以對已更正的應用程式或處理序，執行先前發現潛在問題的追蹤。 然後，重新執行原始追蹤並比較結果。  
  
 追蹤重新執行支援以 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] [重新執行] 功能表上的 [切換中斷點] 和 [執行至資料指標處] 選項來進行偵錯。 這些選項尤其能改善長指令碼的分析，因為可以將追蹤的重新執行分為數個短的區段，再以累加的方式進行分析。  
  
 如需有關重新執行追蹤時所需之權限的詳細資訊，請參閱 [執行 SQL Server Profiler 所需的權限](permissions-required-to-run-sql-server-profiler.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[重新執行需求](replay-requirements.md)|描述追蹤定義中必須包含哪些事件，才可以用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]重新執行。|  
|[重新執行選項 &#40;SQL Server Profiler&#41;](replay-options-sql-server-profiler.md)|描述您可以在 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的 [重新執行組態] 對話方塊中設定的選項。|  
|[重新執行追蹤的考量 &#40;SQL Server Profiler&#41;](considerations-for-replaying-traces-sql-server-profiler.md)|描述不能以 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 重新執行的追蹤事件，以及重新執行追蹤對伺服器效能的影響。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Distributed Replay](../distributed-replay/sql-server-distributed-replay.md)  
  
  
