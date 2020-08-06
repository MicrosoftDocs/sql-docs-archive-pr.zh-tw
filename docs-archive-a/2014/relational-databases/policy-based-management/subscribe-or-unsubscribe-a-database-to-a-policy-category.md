---
title: 訂閱或取消訂閱原則類別目錄資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.dmf.groupsubscription.f1
ms.assetid: d2c31769-7098-428e-ad9c-ef56541b7c52
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2b4ca6f804352b57b30b42012da93e0d031be8d4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87699454"
---
# <a name="subscribe-or-unsubscribe-a-database--to-a-policy-category"></a>讓資料庫訂閱或取消訂閱原則類別目錄
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中讓資料庫訂閱或取消訂閱原則類別目錄。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列方法讓資料庫訂閱或取消訂閱原則類別目錄：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要 db_owner 固定資料庫角色中的成員資格。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-subscribe-or-unsubscribe-a-database-to-a-policy-category"></a>若要讓資料庫訂閱或取消訂閱原則類別目錄  
  
1.  在 **[物件總管]** 中，按一下加號展開伺服器，此伺服器包含要管理其中類別目錄訂閱的資料庫。  
  
2.  按一下加號展開 **[資料庫]** 資料夾。  
  
3.  以滑鼠右鍵按一下要管理其中類別目錄訂閱的資料庫，指向 [原則]**** 並選取 [類別目錄]****。  
  
     **[類別目錄]** 對話方塊有下列選項：  
  
     展開資料行  
     按一下此選項可展開原則類別目錄。 這個清單會列出此類別目錄中所包含的所有原則。  
  
     **名稱**  
     原則類別目錄的名稱。  
  
     **訂閱**  
     指出目標是否已訂閱原則類別目錄。 如果已停用此核取方塊，會針對 **[託管資料庫訂閱]** 設定原則類別目錄。 這表示，原則類別目錄會套用到伺服器上的所有資料庫。  
  
     **原則**  
     當原則群組展開時，會顯示原則類別目錄中的原則。  
  
     **已啟用**  
     指出原則已啟用或停用。  
  
     **執行模式**  
     顯示原則的執行模式。  
  
     **History**  
     按一下 [檢視記錄] 超連結可開啟記錄檔檢視器，以查看原則記錄。  
  
4.  若要訂閱原則式管理類別目錄，請選取 [已訂閱]**** 資料行下類別目錄的對話方塊。 若要取消訂閱類別目錄，請清除核取方塊。  
  
5.  完成後，請按一下 **[確定]** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-subscribe-a-database-to-a-policy-category"></a>若要讓資料庫訂閱原則類別目錄  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;  
    -- Adds a subscription to the 'Finance' policy category for the AdventureWorks2012 database.  
    EXEC sys.sp_syspolicy_subscribe_to_policy_category @policy_category = N'Finance';  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [sp_syspolicy_subscribe_to_policy_category &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syspolicy-subscribe-to-policy-category-transact-sql)。  
  
#### <a name="to-unsubscribe-a-database-to-a-policy-category"></a>若要讓資料庫取消訂閱原則類別目錄  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;  
    -- Deletes a subscription to the 'Finance' policy category for the AdventureWorks2012 database.  
    EXEC sys.sp_syspolicy_unsubscribe_from_policy_category @policy_category = N'Finance';  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [sp_syspolicy_unsubscribe_from_policy_category &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syspolicy-unsubscribe-from-policy-category-transact-sql)。  
  
  
