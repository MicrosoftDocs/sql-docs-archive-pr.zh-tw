---
title: 變更工作負載群組設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- workload groups [SQL Server], alter
- Resource Governor, workload group alter
ms.assetid: 73b6109c-2ad0-4915-b11b-d40d5a0fdc25
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 579aad71d32a629d75f1eecd76e7dacfe32d94f2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584373"
---
# <a name="change-workload-group-settings"></a>變更工作負載群組設定
  您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來變更工作負載群組設定。  
  
-   **開始之前：** [限制事項](#LimitationsRestrictions)、[權限](#Permissions)  
  
-   **若要變更工作負載群組的設定，請使用下列方式：** [SQL Server Management Studio](#ChgWGProp)、[Transact-SQL](#ChgWGTSQL)  
  
## <a name="before-you-begin"></a>開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> 限制事項  
 您可以變更預設工作負載群組和使用者定義工作負載群組的設定。  
  
 **REQUEST_MAX_MEMORY_GRANT_PERCENT**  
  
 非對齊式資料分割資料表上之索引建立所耗用的記憶體，與相關的資料分割數目成正比。 如果所需的總記憶體超出工作負載群組設定所設的每個查詢限制 (REQUEST_MAX_MEMORY_GRANT_PERCENT)，這個索引建立動作可能會失敗。 由於預設工作負載群組允許查詢超過每個查詢限制，而且基於 SQL Server 2005 相容性會啟動所需的記憶體下限，因此使用者或許能夠在預設工作負載群組中執行相同的索引建立動作，但前提是預設資源集區有設定足夠的總記憶體來執行這類查詢。  
  
 允許索引建立使用比一開始授與之記憶體更多的記憶體工作空間來改善效能。 資源管理員支援這種特殊的處理，不過，初始授與和任何額外的記憶體授與都受到工作負載群組和資源集區設定的限制。  
  
###  <a name="permissions"></a><a name="Permissions"></a> 權限  
 變更工作負載群組設定需要 CONTROL SERVER 權限。  
  
##  <a name="change-workload-group-settings-using-sql-server-management-studio"></a><a name="ChgWGProp"></a> 使用 SQL Server Management Studio 變更工作負載群組設定  
 **若要使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  在 [物件總管] 中，遞迴地向下展開 **[管理]** 節點至 **[資源管理員]** 資料夾，此資料夾包含要修改的工作負載群組。  
  
2.  以滑鼠右鍵按一下要修改的工作負載群組，然後選取 [屬性]。  
  
3.  在 **[資源管理員屬性]** 頁面的 **[資源集區的工作負載群組]** 方格中，選取工作負載群組的資料列 (如果系統沒有自動選取的話)。  
  
4.  在資料列中按一下或按兩下要變更的資料格，然後輸入新值。  
  
5.  若要儲存變更，請按一下 **[確定]** 。  
  
##  <a name="change-workload-group-settings-using-transact-sql"></a><a name="ChgWGTSQL"></a> 使用 Transact-SQL 變更工作負載群組設定  
 **若要使用 Transact-SQL 來變更工作負載群組設定**  
  
1.  執行 ALTER WORKLOAD GROUP 陳述式，指定要變更的屬性值。  
  
2.  執行 ALTER RESOURCE GOVERNOR RECONFIGURE 陳述式。  
  
### <a name="example-transact-sql"></a>範例 &#40;Transact-SQL&#41;  
 下列範例會變更名為 `groupAdhoc`的工作負載群組的最大記憶體授與百分比設定。  
  
```  
ALTER WORKLOAD GROUP groupAdhoc  
WITH (REQUEST_MAX_MEMORY_GRANT_PERCENT = 30);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資源管理員](resource-governor.md)   
 [建立工作負載群組](create-a-workload-group.md)   
 [建立資源集區](create-a-resource-pool.md)   
 [變更資源集區設定](change-resource-pool-settings.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-workload-group-transact-sql)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
