---
title: XTP (記憶體內部 OLTP) 效能計數器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: fe3cbaf4-65f4-44c5-acc6-7b735cda0c5d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4363a526ada3694e92d18cac0d7abe8a26f6a92f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87698044"
---
# <a name="xtp-in-memory-oltp-performance-counters"></a>XTP (記憶體中 OLTP) 效能計數器
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供物件和計數器，可供效能監視器用來監視記憶體中 OLTP 活動。  
  
##  <a name="xtp-in-memory-oltp-performance-objects"></a><a name="SQLServerPOs"></a>XTP (記憶體內部 OLTP) 效能物件  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件。  
  
|效能物件|描述|  
|------------------------|-----------------|  
|[XTP 資料指標](../cursors.md)|XTP 資料指標效能物件包含與內部 XTP 引擎資料指標相關的計數器。 資料指標是 XTP 引擎用來處理 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢的低階建置組塊。 因此，您通常不會有這些指標的直接控制權。|  
|[XTP 記憶體回收](sql-server-xtp-garbage-collection.md)|XTP 記憶體回收效能物件包含與 XTP 引擎記憶體回收行程相關的計數器。|  
|[XTP 虛設處理器](sql-server-xtp-phantom-processor.md)|XTP 虛設處理器效能物件包含與 XTP 引擎的虛設處理子系統相關的計數器。 此元件負責偵測在 SERIALIZABLE 隔離等級執行之交易中的虛設項目列。|  
|[XTP 儲存體](sql-server-xtp-storage.md)|XTP 儲存體效能物件包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中與 XTP 儲存體相關的計數器。|  
|[XTP 交易記錄](sql-server-xtp-transaction-log.md)|XTP 交易記錄效能物件包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中與 XTP 交易記錄相關的計數器。|  
|[XTP 交易](sql-server-xtp-transactions.md)|XTP 交易效能物件包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中與 XTP 引擎交易相關的計數器。|  
  
  
