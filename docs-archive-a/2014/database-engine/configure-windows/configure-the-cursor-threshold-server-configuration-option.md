---
title: 設定 cursor threshold 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- cursor threshold option
ms.assetid: 189f2067-c6c4-48bd-9bd9-65f6b2021c12
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0d7fd9ecafda270a02f1fba9f5dd74adc9e299d1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87607092"
---
# <a name="configure-the-cursor-threshold-server-configuration-option"></a>設定 cursor threshold 伺服器組態選項
  此主題描述如何使用 **或** ，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] cursor threshold [!INCLUDE[tsql](../../includes/tsql-md.md)]伺服器組態選項。 **cursor threshold** 選項會指定資料指標集中以非同步方式產生資料指標索引鍵集的列數。 當資料指標為結果集產生索引鍵集時，查詢最佳化工具會估計將在該結果集傳回的資料列數。 如果查詢最佳化工具估計將傳回的列數會大於這個臨界值，就會以非同步方式產生資料指標，讓使用者在資料指標繼續擴展的同時，可以從資料指標擷取資料列。 否則，會以同步的方式產生資料指標，使查詢等到所有資料列都傳回為止。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **使用下列方法設定 cursor threshold 選項：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **後續操作：** [設定資料指標閾值選項之後](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援非同步產生索引鍵集驅動或靜態 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料指標。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料指標作業是以批次方式來處理，因此，不需要非同步產生 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料指標。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會繼續支援非同步索引鍵集驅動或靜態應用程式開發介面 (API) 伺服器資料指標，其中低度延遲 OPEN 會是一個顧慮，因為每一個資料指標作業都需要用戶端往返。  
  
-   查詢最佳化工具用來決定索引鍵集中估計資料列數的精確度，須視資料指標中每個資料表統計資料的準確度而定。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   這個選項是進階選項，只有有經驗的資料庫管理員或通過認證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術人員才可變更。  
  
-   如果將 [資料指標臨界值] 設定為 -1，所有索引鍵集都會以同步方式產生，這有益於小型的資料指標集。 如果將 **cursor threshold** 設成 0，所有資料指標索引鍵集都會以非同步方式產生。 若使用其他值，查詢最佳化工具會比較資料指標集中預期的列數，如果列數超過 **cursor threshold**中設定的數字，就以非同步方式建立索引鍵集。 請不要將 **cursor threshold** 設得太低，因為小的結果集最好是以同步的方式建立。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 以同時設定兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式時，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-cursor-threshold-option"></a>若要設定資料指標臨界值選項  
  
1.  在物件總管中，請以滑鼠右鍵按一下伺服器，然後選取 [屬性]。  
  
2.  按一下 **[進階]** 節點。  
  
3.  在 **[其他]** 下，將 **[資料指標臨界值]** 選項變更為所要的值。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-cursor-threshold-option"></a>若要設定資料指標臨界值選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 這個範例示範如何使用 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 將 `cursor threshold` 選項設定為 `0` ，以便以非同步方式產生資料指標索引鍵集。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'cursor threshold', 0 ;  
GO  
RECONFIGURE  
GO  
  
```  
  
 如需詳細資訊，請參閱 [伺服器設定選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)伺服器組態選項。  
  
##  <a name="follow-up-after-you-configure-the-cursor-threshold-option"></a><a name="FollowUp"></a> 後續操作：設定資料指標閾值選項之後  
 設定會立即生效，不需要重新啟動伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [@@CURSOR_ROWS &#40;Transact-SQL&#41;](/sql/t-sql/functions/cursor-rows-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql)  
  
  
