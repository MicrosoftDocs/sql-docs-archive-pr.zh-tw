---
title: SQL Server 的 Cursor Manager by Type 物件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Cursor Manager by Type object
- SQLServer:Cursor Manager by Type
ms.assetid: d67fbd8a-7554-4a16-96f1-d9ee857a95e3
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7bee15aa2917f7b8890e6c1d3f26cc0e210208a7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592647"
---
# <a name="sql-server-cursor-manager-by-type-object"></a>SQL Server 的 Cursor Manager by Type 物件
  **SQLServer:Cursor Manager by Type** 物件提供計數器，可監視依類型分組的資料指標。  
  
 下表說明 SQL Server **Cursor Manager by Type** 計數器。  
  
|Cursor Manager by Type 計數器|描述|  
|-------------------------------------|-----------------|  
|**Active cursors**|使用中的資料指標數目。|  
|**Cache Hit Ratio**|快取叫用數和查閱數之間的比率|  
|**Cached Cursor Counts**|快取中給定類型的資料指標數目。|  
|**Cursor Cache Use Count/sec**|每種快取資料指標類型的使用次數。|  
|**Cursor memory usage**|資料指標所耗用的記憶體數量，以 KB 為單位。|  
|**Cursor Requests/sec**|伺服器收到的 SQL 資料指標要求數目。|  
|**Cursor worktable usage**|資料指標使用的工作資料表數目。|  
|**Number of active cursor plans**|資料指標計畫的數目。|  
  
 物件中的每個計數器均包含下列執行個體：  
  
|Cursor Manager 執行個體|描述|  
|-----------------------------|-----------------|  
|**_Total**|所有資料指標的相關資訊。|  
|**API Cursor**|僅限 API 資料指標資訊。|  
|**TSQL Global Cursor**|僅限 [!INCLUDE[tsql](../../includes/tsql-md.md)] 全域資料指標資訊。|  
|**TSQL Local Cursor**|僅限 [!INCLUDE[tsql](../../includes/tsql-md.md)] 區域資料指標資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;System Monitor&#41;](monitor-resource-usage-system-monitor.md)  
  
  
