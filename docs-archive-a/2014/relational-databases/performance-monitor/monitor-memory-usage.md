---
title: 監視記憶體使用量 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- tuning databases [SQL Server], memory
- monitoring server performance [SQL Server], memory usage
- isolating memory [SQL Server]
- paging rate [SQL Server]
- memory [SQL Server], monitoring usage
- monitoring [SQL Server], memory usage
- low-memory conditions
- database monitoring [SQL Server], memory usage
- available memory [SQL Server]
- page faults [SQL Server]
- monitoring performance [SQL Server], memory usage
- server performance [SQL Server], memory
ms.assetid: 1aee3933-a11c-4b87-91b7-32f5ea38c87f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1986d9576f9b067cad18f27d4febbf097ed52703
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707402"
---
# <a name="monitor-memory-usage"></a>監視記憶體使用量
  定期監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，以確認記憶體使用量是在正常範圍內。  
  
 若要監視低記憶體的狀況，請使用以下物件計數器：  
  
-   **記憶體：Available Bytes**  
  
-   **記憶體：Pages/sec**  
  
 **Available Bytes** 計數器代表目前有多少記憶體位元組可供處理序使用。 **Pages/sec** 計數器會顯示由於硬體分頁錯誤而自磁碟取出，或由於分頁錯誤而寫入磁碟，以釋出工作集內空間的分頁數。  
  
 若 **Available Bytes** 計數器的數值偏低，代表電腦整體地缺乏記憶體，或有某個應用程式沒有釋出記憶體。 **Pages/sec** 計數器數值過高可能代表過度分頁。 監視**記憶體：Page Faults/sec** 計數器可確認磁碟活動並非分頁所造成。  
  
 分頁率 (連同分頁錯誤) 低是正常的，即使有許多可用記憶體的電腦也是如此。 當「Microsoft Windows 虛擬記憶體管理員 (VMM)」修剪 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和其他處理序的工作集大小時，它會從這些處理序取得分頁。 此 VMM 活動會造成分頁錯誤。 若要判斷 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或其他處理序是否為過度分頁的原因，您可以監視**處理序：Page Faults/sec** 計數器 (針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序執行個體)。  
  
 如需有關解決過度分頁的詳細資訊，請參閱 Windows 作業系統文件。  
  
## <a name="isolating-memory-used-by-sql-server"></a>隔離 SQL Server 所使用的記憶體  
 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會根據可用的系統資源，動態變更它的記憶體需求。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要更多記憶體，它將詢問作業系統以判斷是否有可用的實體記憶體，並使用可用的記憶體。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並不需要目前配置給它的記憶體，它會釋出記憶體給作業系統。 不過，您可以使用 **minservermemory**和 **maxservermemory** 伺服器組態選項，覆寫選項以動態使用記憶體。 如需詳細資訊，請參閱＜ [伺服器記憶體選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)＞。  
  
 若要監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所使用的記憶體數量，請檢查下列效能計數器：  
  
-   **處理序：Working Set**  
  
-   **SQL Server：緩衝區管理員：Buffer Cache Hit Ratio**  
  
-   **SQL Server：緩衝區管理員：Database Pages**  
  
-   **SQL Server：記憶體管理員：Total Server Memory (KB)**  
  
 **WorkingSet** 計數器顯示處理序使用的記憶體數量。 如果這個數字一直低於 **「最小伺服器記憶體」** 與 **「最大伺服器記憶體」** 伺服器選項設定的記憶體數量，則代表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定的記憶體過多。  
  
 **Buffer Cache Hit Ratio** 計數器專供應用程式使用。 不過，其數值最好為 90% 或更高。 請持續增加記憶體，直到該數值持續大於 90%。 數值大於 90% 代表有超過 90% 的資料要求，可自資料快取中得到所需的資料。  
  
 若 **TotalServerMemory (KB)** 計數器和電腦中的實體記憶體數量相比一直很高，可能代表需要更多的記憶體。  
  
## <a name="determining-current-memory-allocation"></a>決定目前的記憶體配置  
 以下查詢會傳回目前配置之記憶體的相關資訊。  
  
```  
SELECT  
(physical_memory_in_use_kb/1024) AS Memory_usedby_Sqlserver_MB,  
(locked_page_allocations_kb/1024) AS Locked_pages_used_Sqlserver_MB,  
(total_virtual_address_space_kb/1024) AS Total_VAS_in_MB,  
process_physical_memory_low,  
process_virtual_memory_low  
FROM sys.dm_os_process_memory;  
```  
  
  
