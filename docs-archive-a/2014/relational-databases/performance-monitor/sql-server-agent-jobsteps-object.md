---
title: SQL Server Agent、JobSteps 物件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- JobSteps object
- SQLAgent:JobSteps
ms.assetid: 44f9983c-1753-4fe0-8475-973aa2460b3a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3759303807714e2bb7f71f59e644bc485d36cfcb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593342"
---
# <a name="sql-server-agent-jobsteps-object"></a>SQL Server Agent、JobSteps 物件
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的 **JobSteps** 效能物件包含可報告 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業步驟相關資訊的效能計數器。 下表列出這個物件包含的計數器。  
  
 下表包含 **SQLAgent:JobSteps** 計數器。  
  
|Name|描述|  
|----------|-----------------|  
|**Active steps**|此計數器會報告目前在執行中的作業步驟數目。|  
|**Queued steps**|此計數器會報告準備供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 執行，但尚未開始執行的作業步驟數目。|  
|**Total step retries**|此計數器會報告自從伺服器上次重新啟動之後，[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重試作業步驟的總次數。|  
  
 物件中的每個計數器均包含下列執行個體：  
  
|執行個體|描述|  
|--------------|-----------------|  
|**_Total**|所有作業步驟的資訊。|  
|**ActiveScripting**|使用 **ActiveScripting** 子系統之作業步驟的資訊。|  
|**ANALYSISCOMMAND**|使用 ANALYSISCOMMAND 子系統之作業步驟的資訊。|  
|**ANALYSISQUERY**|使用 ANALYSISQUERY 子系統之作業步驟的資訊。|  
|**CmdExec**|使用 **CmdExec** 子系統之作業步驟的資訊。|  
|**Distribution**|使用 **Distribution** 子系統之作業步驟的資訊。|  
|**Dts**|使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 子系統之作業步驟的資訊。|  
|**LogReader**|使用 **LogReader** 子系統之作業步驟的資訊。|  
|**合併式**|使用 **Merge** 子系統之作業步驟的資訊。|  
|**PowerShell**|使用 **PowerShell** 子系統之作業步驟的資訊。|  
|**QueueReader**|使用 **QueueReader** 子系統之作業步驟的資訊。|  
|**快照式**|使用 **Snapshot** 子系統之作業步驟的資訊。|  
|**TSQL**|執行 [!INCLUDE[tsql](../../includes/tsql-md.md)]之作業步驟的資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [管理作業步驟](../../ssms/agent/manage-job-steps.md)   
 [使用效能物件](../../ssms/agent/use-performance-objects.md)   
 [監視資源使用狀況 &#40;System Monitor&#41;](monitor-resource-usage-system-monitor.md)  
  
  
