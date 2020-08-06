---
title: 設定 recovery interval 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- restoring recovery interval [SQL Server]
- checkpoints [SQL Server]
- recovery interval option [SQL Server]
- default recovery interval option
- time [SQL Server], recovery interval
- interval for recovery [SQL Server]
- maximum number of minutes per database recovery
- recovery [SQL Server], recovery interval option
ms.assetid: e4734b3b-8fbe-4b65-9c48-91b5a3dd18e1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 560d514ba8dd1503b59b3b59ecf404d876e24cd2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592239"
---
# <a name="configure-the-recovery-interval-server-configuration-option"></a>設定 recovery interval 伺服器組態選項
  此主題描述如何使用 **或** ，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] recovery interval [!INCLUDE[tsql](../../includes/tsql-md.md)]伺服器組態選項。 **recovery interval** 選項會定義資料庫的復原時間上限。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 使用此選項的指定值，來決定 [automatic checkpoints](../../relational-databases/logs/database-checkpoints-sql-server.md) 在給定資料庫上發出自動檢查點的大約頻率。  
  
 預設復原間隔值為 0，代表允許 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 自動設定復原間隔。 一般而言，使用中的資料庫之預設復原間隔大約是一分鐘執行一次自動檢查點，而復原總時間不超過一分鐘。 較高的值表示復原預計最長時間，以分鐘為單位。 例如，設定復原間隔為 3 表示復原的最長時間約 3 分鐘。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目設定 recovery interval 伺服器組態選項：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **後續操作：** [設定復原間隔項之後](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   復原間隔只會影響使用預設目標復原時間 (0) 的資料庫。 若要覆寫資料庫上的伺服器復原間隔，請在資料庫上設定非預設目標復原時間。 如需詳細資訊，請參閱 [變更資料庫的目標復原時間 &#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md)伺服器組態選項。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   這個選項是進階選項，只有有經驗的資料庫管理員或通過認證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術人員才可變更。  
  
-   除非出現效能問題，不然通常我們會建議您將復原間隔維持在 0。 如果您決定增加復原間隔設定，我們建議您逐漸少量增加此設定，並評估每次累加對於復原效能的影響。  
  
-   如果您使用 **sp_configure** 將 **recovery interval** 選項設為大於 60 (分鐘) 的值，請指定 RECONFIGURE WITH OVERRIDE。 WITH OVERRIDE 會停用組態值的檢查 (對於無效或非建議值的值)。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 以同時設定兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式時，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **若要設定復原間隔**  
  
1.  在 [物件總管] 中，以滑鼠右鍵按一下伺服器執行個體，然後選取 **[屬性]** 。  
  
2.  按一下 **[資料庫設定]** 節點。  
  
3.  於 **[復原間隔 (分鐘)]** 方塊的 **[復原]** 下，輸入或選取介於 0 到 32767 之間的任一數值 (以分鐘為單位)，設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動時，回復每個資料庫所花費的時間上限。 預設值是 0，指出由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]自動組態。 實務上，這表示復原時間小於一分鐘，而且使用中資料庫幾乎每分鐘有一次檢查點。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-set-the-recovery-interval"></a>若要設定復原間隔  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例示範如何使用 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 將 `recovery interval` 選項的值設定為 `3` 分鐘。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'recovery interval', 3 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 如需詳細資訊，請參閱 [伺服器設定選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)伺服器組態選項。  
  
##  <a name="follow-up-after-you-configure-the-recovery-internal-option"></a><a name="FollowUp"></a> 後續操作：設定復原間隔選項之後  
 設定會立即生效，不需要重新啟動伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [變更資料庫的目標復原時間 &#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md)   
 [資料庫檢查點 &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [顯示伺服器組態選項進階選項](show-advanced-options-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
