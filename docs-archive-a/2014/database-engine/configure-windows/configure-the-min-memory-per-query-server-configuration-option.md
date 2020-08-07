---
title: 設定 min memory per query 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- memory [SQL Server], queries
- minimum query memory
- queries [SQL Server], memory
- min memory per query option
ms.assetid: ecd3fb79-b4a6-432f-9ef5-530e0d42d5a6
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 56d85f36840f0900c8b5e986334a99ba610d3930
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597339"
---
# <a name="configure-the-min-memory-per-query-server-configuration-option"></a>設定 min memory per query 伺服器組態選項
  本主題描述如何 `min memory per query` 使用或，在中設定 server configuration 選項 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 `min memory per query`選項會指定將為執行查詢而配置的最小記憶體數量) （以 kb 為單位） (。 例如，如果 `min memory per query` 設定為 2048 KB，則查詢保證至少會取得記憶體總計。 預設值為 1,024 KB。 最小值是 512 KB，最大值則是 2,147,483,647 KB (2 GB)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **使用下列方法設定 min memory per query 選項：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **後續操作：** [設定每個查詢的最小記憶體選項之後](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   [每個查詢的最小記憶體] 的優先順序高於 [[索引建立記憶體] 選項](configure-the-index-create-memory-server-configuration-option.md)。 若您同時變更了兩個選項，且索引建立記憶體選項小於每個查詢的最小記憶體，您會看到警告訊息，但仍會設定該值。 執行查詢時，您會看到另一個類似的警告。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   這個選項是進階選項，只有有經驗的資料庫管理員或通過認證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術人員才可變更。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢處理器會嘗試判斷要配置給查詢的最佳記憶體數量。 min memory per query 選項可讓系統管理員指定任何單一查詢所接收的最小記憶體數量。 若查詢中含有大量資料的雜湊和排序作業，則這些查詢通常會接收比此值更多的記憶體。 提高 min memory per query 的值也許可以改善一些小型至中型查詢的效能，但這樣做也可能導致競用記憶體資源的情形增加。 每個查詢的最小記憶體選項包含了為進行排序所配置的記憶體。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 以同時設定兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式時，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-min-memory-per-query-option"></a>設定 min memory per query 選項  
  
1.  在物件總管中，請以滑鼠右鍵按一下伺服器，然後選取 [屬性]。  
  
2.  按一下 **[記憶體]** 節點。  
  
3.  在 **[每個查詢的最小記憶體]** 方塊中，輸入將為執行查詢而配置的最小記憶體數量 (以 KB 為單位)。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-min-memory-per-query-option"></a>設定 min memory per query 選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例示範如何使用 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 將 `min memory per query` 選項的值設定為 `3500` KB。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'min memory per query', 3500 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
##  <a name="follow-up-after-you-configure-the-min-memory-per-query-option"></a><a name="FollowUp"></a> 後續操作：設定每個查詢的最小記憶體選項之後  
 設定會立即生效，不需要重新啟動伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [設定 index create memory 伺服器組態選項](configure-the-index-create-memory-server-configuration-option.md)  
  
  
