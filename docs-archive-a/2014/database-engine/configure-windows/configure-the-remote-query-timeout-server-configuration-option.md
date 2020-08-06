---
title: 設定 remote query timeout 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- time limit for remote queries [SQL Server]
- remote query timeout option
ms.assetid: 888c8448-933b-41e3-8aa1-c206bc0cdb78
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 74f82d621d7f0375a6a3ca604abba00f83fc6024
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707862"
---
# <a name="configure-the-remote-query-timeout-server-configuration-option"></a>設定 remote query timeout 伺服器組態選項
  此主題描述如何使用 **或** ，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] remote query timeout [!INCLUDE[tsql](../../includes/tsql-md.md)]伺服器組態選項。 **remote query timeout** 選項會指定在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 逾時之前，遠端作業可以執行多久 (以秒為單位)。此選項的預設值是 600，這允許 10 分鐘的等待。 此值可套用到由 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 啟始做為遠端查詢的傳出連接。 此值對 [!INCLUDE[ssDE](../../includes/ssde-md.md)]收到的查詢沒有影響。 若要停用逾時，請將值設定為 0。 查詢會等候，直到完成。  
  
 對於異質性查詢，[遠端查詢逾時] 可指定遠端提供者在等候查詢結果集時，應等候幾秒 (使用 DBPROP_COMMANDTIMEOUT 資料列集屬性在命令物件中初始化) 後，查詢才會逾時。這個值也用來設定 DBPROP_GENERALTIMEOUT (如果遠端提供者支援的話)。 這會使其他任何作業在指定秒數後變逾時。  
  
 對於遠端預存程序， **remote query timeout** 會指定在傳送遠端 `EXEC` 陳述式之後，遠端預存程序逾時之前必須經過的秒數。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [先決條件](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **使用下列方法設定 remote query timeout 選項：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **後續操作：** [設定遠端查詢逾時選項之後](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
  
-   設定這個數值之前必須先允許遠端伺服器連接。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 以同時設定兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式時，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-remote-query-timeout-option"></a>設定 remote query timeout 選項  
  
1.  在物件總管中，請以滑鼠右鍵按一下伺服器，然後選取 [屬性]。  
  
2.  按一下 **[連接]** 節點。  
  
3.  請在 **[遠端伺服器連接]** 下方的 **[遠端查詢逾時]** 方塊中，輸入或選取從 0 至 2,147,483,647 的值，以設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在逾時之前要等待的最大秒數。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-remote-query-timeout-option"></a>設定 remote query timeout 選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例示範如何使用 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 將 `remote query timeout` 選項的值設定為 `0` ，以停用逾時。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'remote query timeout', 0 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
 如需詳細資訊，請參閱 [伺服器設定選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)伺服器組態選項。  
  
##  <a name="follow-up-after-you-configure-the-remote-query-timeout-option"></a><a name="FollowUp"></a> 後續操作：設定遠端查詢逾時選項之後  
 設定會立即生效，不需要重新啟動伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [資料列集屬性和行為](../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
