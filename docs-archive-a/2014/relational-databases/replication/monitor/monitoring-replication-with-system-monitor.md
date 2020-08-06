---
title: 使用系統監視器監視複寫 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], System Monitor
- System Monitor [SQL Server], replication
- performance counters [SQL Server replication]
ms.assetid: 8cd3a270-0328-4bfd-bf23-b1d759cc120c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ad94c0d9cb559bc3a323ba2f72a31771fb5fe1d4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593936"
---
# <a name="monitoring-replication-with-system-monitor"></a>使用系統監視器監視複寫
  「[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 系統監視器」可讓您使用圖形、圖表和報告來量測電腦的效率、識別和排除可能的問題 (例如不平衡的資源用量、硬體不足或不良的程式設計)，以及規劃其他硬體需求。 如需詳細資訊，請參閱[監視資源使用狀況 &#40;系統監視器&#41;](../../performance-monitor/monitor-resource-usage-system-monitor.md)。  
  
 「系統監視器」使用效能物件和計數器，這些工具可以提供各種處理之效能的資訊。 您可以透過與複寫代理程式相關的計數器來衡量複寫效能：  
  
|代理程式|效能物件|計數器|描述|  
|-----------|------------------------|-------------|-----------------|  
|所有代理程式|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]：複寫代理程式|執行中|目前正在執行的複寫代理程式數。|  
|快照集代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:複寫快照|Snapshot:Delivered Cmds/sec|每秒傳送到散發者的命令數。|  
|快照集代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:複寫快照|Snapshot:Delivered Trans/sec|每秒傳送到散發者的交易數。|  
|記錄讀取器代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:Replication Logreader|Logreader:Delivered Cmds/sec|每秒傳送到散發者的命令數。|  
|記錄讀取器代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:Replication Logreader|Logreader:Delivered Trans/sec|每秒傳送到散發者的交易數。|  
|記錄讀取器代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:Replication Logreader|Logreader:Delivery Latency|「發行者」套用交易時，該交易傳送至「散發者」所花費的時間，以毫秒為單位。|  
|散發代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:Replication Dist.|Dist:Delivered Cmds/sec|每秒傳遞至「訂閱者」的命令數。|  
|散發代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:Replication Dist.|Dist:Delivered Trans/sec|每秒傳遞至「訂閱者」的交易數。|  
|散發代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:Replication Dist.|Dist:Delivery Latency|目前從交易傳送到分配者到交易在「訂閱者」套用所經過的時間 (毫秒)。|  
|合併代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:複寫合併|Conflicts/sec|合併處理期間每秒所發生的衝突數。|  
|合併代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:複寫合併|Downloaded Changes/sec|每秒從「發行者」複寫至「訂閱者」的資料列數。|  
|合併代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:複寫合併|Uploaded Changes/sec|每秒從「訂閱者」複寫至「發行者」的資料列數。|  
  
## <a name="see-also"></a>另請參閱  
 [監視 &#40;複寫&#41;](../monitoring-replication.md)  
  
  
