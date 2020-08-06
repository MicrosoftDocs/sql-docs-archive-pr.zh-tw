---
title: 為記憶體最佳化物件定義持久性 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 0fe85fbf-8e8d-4983-96fd-d04b3c7d6d65
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 325f50a74ea75270dd62fc3564200c59255dc6cb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593379"
---
# <a name="defining-durability-for-memory-optimized-objects"></a>為記憶體最佳化的物件定義持久性
  記憶體中 OLTP 可保證完整的不可部分完成性、一致性、隔離性與完全持久性 (ACID) 屬性。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境和記憶體最佳化的資料表中的持久性會提供下列保證：  
  
 交易持久性  
 當您認可一項對記憶體最佳化資料表進行 (DDL 或 DML) 變更的完全持久交易時，對持久的記憶體最佳化資料表所做的變更就會變成永久變更。  
  
 當您將延遲的持久交易認可到記憶體最佳化資料表時，只有將記憶體中的交易記錄儲存至磁碟之後，交易才會變成持久。  
  
 重新啟動持久性  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在當機或計劃中的關機之後重新啟動時，記憶體最佳化的持久性資料表會重新具現化，以還原到關機或當機之前的狀態。  
  
 媒體故障持久性  
 如果故障或損毀的磁碟包含持久性記憶體最佳化物件的一個或多個保存複本， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份和還原功能會在新的媒體上還原記憶體最佳化的資料表。  
  
 記憶體最佳化的資料表有兩個持久性選項：  
  
 SCHEMA_ONLY (非持久性資料表)  
 此選項可確保資料表結構描述的持久性，包括索引在內。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新啟動時，非持久性資料表會重新建立，但是一開始沒有資料  (這不同於 tempdb 中的資料表，後者的資料表及資料表資料都會在重新啟動之後遺失)。建立非持久性資料表的典型案例為儲存暫時性資料，例如 ETL 處理序的暫存資料表。 SCHEMA_ONLY 持久性會避免交易記錄和檢查點，這樣可大幅減少 I/O 作業。  
  
 SCHEMA_AND_DATA (持久性資料表)  
 此選項提供結構描述和資料的持久性。 資料持久性層級取決於您是否將交易認可為完全持久或具有延遲持久性。 完全持久交易提供與資料和結構描述相同的持久性保證，類似以磁碟為基礎的資料表。 延遲持久性可增進效能，但是在伺服器當機或容錯移轉的情況下可能會導致資料損失。 (如需延遲持久性的詳細資訊，請參閱 [控制交易持久性](../logs/control-transaction-durability.md)。)  
  
 系統會將記憶體最佳化的資料表的結構描述保存在資料庫的主要檔案群組中，類似於以磁碟為基礎的資料表。  
  
 持久的記憶體最佳化資料表中的資料會儲存在資料和差異檔案組中。  
  
 記憶體最佳化的資料表中定義的索引只保存在中繼資料中，不會保存在儲存體中。 載入記憶體最佳化的資料表時，將會產生索引結構。  
  
 資料列會由 DELETE 陳述式明確刪除或由 UPDATE 陳述式間接刪除。 UPDATE 作業會當做插入之後的刪除來執行。 刪除資料列時，資料檔案不會進行任何變更，但是識別已刪除之資料列的新資料列會附加到對應的差異檔案。  
  
 在復原或還原作業期間，記憶體中 OLTP 引擎會讀取資料和差異檔案，以便將資料載入實體記憶體中。 載入時間是由以下條件所決定：  
  
-   要載入的資料數量。  
  
-   連續 I/O 頻寬。  
  
-   平行處理原則的程度，取決於檔案容器和處理器核心的數量。  
  
-   記錄檔記錄的數目，這些記錄位於需要重做之記錄檔的使用中部分。  
  
## <a name="see-also"></a>另請參閱  
 [建立及管理記憶體最佳化物件的儲存體](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
