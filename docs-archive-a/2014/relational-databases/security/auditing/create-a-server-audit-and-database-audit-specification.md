---
title: 建立伺服器稽核和資料庫稽核規格 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqlaudit.dbaudit.general.f1
helpviewer_keywords:
- audits [SQL Server], creating database specification
- database audit [SQL Server]
ms.assetid: 26ee85de-6e97-4318-b526-900924d96e62
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0cad01eae45d534f0f74911ce8f57827858cc920
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87700966"
---
# <a name="create-a-server-audit-and-database-audit-specification"></a>建立伺服器稽核和資料庫稽核規格
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中建立伺服器稽核和資料庫稽核規格。  
  
 *「稽核」* (Audit) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的執行個體牽涉到追蹤和記錄系統上所發生的事件。 *SQL Server Audit* 物件會收集要監視之伺服器或資料庫層級動作和動作群組的單一執行個體。 此稽核位於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體層級。 您可以針對每個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體設有多個稽核。 「資料庫層級稽核規格」  物件屬於稽核。 您可以針對每個稽核的每個 SQL Server 資料庫建立一個資料庫稽核規格。 如需詳細資訊，請參閱 [SQL Server Audit &#40;Database Engine&#41;](sql-server-audit-database-engine.md)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目建立伺服器稽核和資料庫稽核規格：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
 資料庫稽核規格是位於給定資料庫內的非安全性實體物件。 當建立資料庫稽核規格之後，它就會處於停用狀態。  
  
 當您在使用者資料庫中建立或修改資料庫稽核規格時，請勿在伺服器範圍的物件 (如系統檢視) 上包含稽核動作。 如果包含了伺服器範圍的物件，將會建立稽核。 但是，將不會包含伺服器範圍的物件，而且不會傳回任何錯誤。 若要稽核伺服器範圍的物件，請在 master 資料庫中使用資料庫稽核規格。  
  
 資料庫稽核規格位於其建立所在的資料庫，但是 `tempdb` 系統資料庫除外。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
  
-   具有 ALTER ANY DATABASE AUDIT 權限的使用者可以建立資料庫稽核規格，並將其繫結至任何稽核。  
  
-   在建立資料庫稽核規格之後，具有 CONTROL SERVER 或 ALTER ANY DATABASE AUDIT 權限的主體，或是系統管理員帳戶將可以檢視此規格。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-server-audit"></a>若要建立伺服器稽核  
  
1.  在 [物件總管] 中，展開 **[安全性]** 資料夾。  
  
2.  以滑鼠右鍵按一下 [**審核**] 資料夾，然後選取 [新增] [ **Audit**...]。如需詳細資訊，請參閱[建立伺服器 audit 和伺服器 Audit 規格](create-a-server-audit-and-server-audit-specification.md)。  
  
3.  當您完成選取選項之後，按一下 **[確定]** 。  
  
#### <a name="to-create-a-database-level-audit-specification"></a>若要建立資料庫層級的稽核規格  
  
1.  在 [物件總管] 中，展開您要建立稽核規格的資料庫。  
  
2.  展開 **[安全性]** 資料夾。  
  
3.  以滑鼠右鍵按一下 [**資料庫 Audit 規格**] 資料夾，然後選取 [**新增資料庫] [audit 規格**...]。  
  
     **[建立資料庫稽核規格]** 對話方塊有下列選項。  
  
     **名稱**  
     資料庫稽核規格的名稱。 當您建立新的伺服器稽核規格時會自動產生這個名稱，但是可加以編輯。  
  
     **稽核**  
     現有資料庫稽核規格的名稱。 請輸入稽核名稱或從清單中選取。  
  
     **稽核動作類型**  
     指定要擷取之資料庫層級的稽核動作群組和稽核動作。 如需資料庫層級稽核動作群組和稽核動作的清單以及其所包含的事件描述，請參閱 [SQL Server Audit 動作群組和動作](sql-server-audit-action-groups-and-actions.md)。  
  
     **物件結構描述**  
     顯示指定之 [物件名稱]  的結構描述。  
  
     **Object Name**  
     要稽核的物件名稱。 這只適用於稽核動作，不適用於稽核群組。  
  
     **省略符號 (...)**  
     開啟 **[選取物件]** 對話方塊來瀏覽及選取可用的物件 (根據指定的 **[稽核動作類型]** )。  
  
     **主體名稱**  
     依據所稽核的物件來篩選稽核的帳戶。  
  
     **省略符號 (...)**  
     開啟 **[選取物件]** 對話方塊來瀏覽及選取可用的物件 (根據指定的 **[物件名稱]** )。  
  
4.  當您完成選取選項之後，按一下 **[確定]**。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-server-audit"></a>若要建立伺服器稽核  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE master ;  
    GO  
    -- Create the server audit.   
    CREATE SERVER AUDIT Payrole_Security_Audit  
        TO FILE ( FILEPATH =   
    'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA' ) ;   
    GO  
    -- Enable the server audit.   
    ALTER SERVER AUDIT Payrole_Security_Audit   
    WITH (STATE = ON) ;  
    ```  
  
#### <a name="to-create-a-database-level-audit-specification"></a>若要建立資料庫層級的稽核規格  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 範例會針對 `Audit_Pay_Tables` 資料表 (以上方定義的伺服器稽核為基礎)，建立可稽核 `dbo` 使用者所執行 SELECT 和 INSERT 陳述式的資料庫稽核規格，其名稱為 `HumanResources.EmployeePayHistory` 。  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    -- Create the database audit specification.   
    CREATE DATABASE AUDIT SPECIFICATION Audit_Pay_Tables  
    FOR SERVER AUDIT Payrole_Security_Audit  
    ADD (SELECT , INSERT  
         ON HumanResources.EmployeePayHistory BY dbo )   
    WITH (STATE = ON) ;   
    GO  
  
    ```  
  
 如需詳細資訊，請參閱 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-transact-sql) 和 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-audit-specification-transact-sql)。  
  
  
