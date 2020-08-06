---
title: 檢視預存程序的定義 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], viewing
- definition of stored procedure
- viewing stored procedures
- displaying stored procedures
ms.assetid: 93318587-a0c5-4788-946f-3b5dc8372ea9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4da455d38f984b08ee1f396f26cd4cc85411be92
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595880"
---
# <a name="view-the-definition-of-a-stored-procedure"></a>檢視預存程序的定義
    
##  <a name="you-can-view-the-definition-of-a-stored-procedure-in-ssmanstudiofull-using-object-explorer-menu-options-or-in-the-query-editor-using-tsql-this-topic-describes-how-to-view-the-definition-of-procedure-in-object-explorer-and-by-using-a-system-stored-procedure-system-function-and-object-catalog-view-in-the-query-editor"></a><a name="Top"></a> 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中使用 [物件總管] 功能表選項，或在查詢編輯器中使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]，檢視預存程序的定義。 本主題描述如何在 [物件總管] 中，以及透過系統預存程序、系統函數和查詢編輯器中的物件目錄檢視，來檢視程序的定義。  
  
-   **開始之前：** [安全性](#Security)  
  
-   **若要檢視程序中的定義，使用：** [SQL Server Management Studio](#SSMSProcedure)、[Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 系統預存程序：`sp_helptext`  
 需要 **public** 角色的成員資格。 系統物件定義是公開顯示的。 凡具有下列任一權限的物件擁有者或承授者，都看得到使用者物件的定義：ALTER、CONTROL、TAKE OWNERSHIP 或 VIEW DEFINITION。  
  
 系統函數：`OBJECT_DEFINITION`  
 系統物件定義是公開顯示的。 凡具有下列任一權限的物件擁有者或承授者，都看得到使用者物件的定義：ALTER、CONTROL、TAKE OWNERSHIP 或 VIEW DEFINITION。 **db_owner**、 **db_ddladmin**和 **db_securityadmin** 固定資料庫角色的成員隱含地擁有這些權限。  
  
 物件目錄檢視：`sys.sql_modules`  
 目錄檢視內中繼資料的可見性會限制在使用者所擁有的安全性實體，或已授與使用者某些權限的安全性實體。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../security/metadata-visibility-configuration.md)。  
  
##  <a name="how-to-view-the-definition-of-a-stored-procedure"></a><a name="Procedures"></a> 如何檢視預存程序的定義  
 您可以使用下列其中一項：  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **在物件總管中檢視程序的定義**  
  
1.  在物件總管中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  依序展開 **[資料庫]** 、程序所屬的資料庫，以及 **[可程式性]** 。  
  
3.  展開 [預存程序]，以滑鼠右鍵按一下程序，然後按一下 [產生預存程序的指令碼為]，然後按一下下列其中一個項目：[建立為]、[變更為] 或 [DROP 並 CREATE 至]。  
  
4.  選取 [新增查詢編輯器視窗]。 這會顯示程序定義。  
  
###  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **在查詢編輯器中檢視程序的定義**  
  
 系統預存程序：`sp_helptext`  
 1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在工具列上，按一下 **[新增查詢]** 。  
  
3.  在查詢視窗中，輸入下列使用 `sp_helptext` 系統預存程序的陳述式。 請變更資料庫名稱和預存程序名稱，使其參考您需要的資料庫和預存程序。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    EXEC sp_helptext N'AdventureWorks2012.dbo.uspLogError';  
    ```  
  
 系統函數：`OBJECT_DEFINITION`  
 1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在工具列上，按一下 **[新增查詢]** 。  
  
3.  在查詢視窗中，輸入下列使用 `OBJECT_DEFINITION` 系統函數的陳述式。 請變更資料庫名稱和預存程序名稱，使其參考您需要的資料庫和預存程序。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT OBJECT_DEFINITION (OBJECT_ID(N'AdventureWorks2012.dbo.uspLogError'));  
    ```  
  
 物件目錄檢視：`sys.sql_modules`  
 1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在工具列上，按一下 **[新增查詢]** 。  
  
3.  在查詢視窗中，輸入下列使用 `sys.sql_modules` 目錄檢視的陳述式。 請變更資料庫名稱和預存程序名稱，使其參考您需要的資料庫和預存程序。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT definition  
    FROM sys.sql_modules  
    WHERE object_id = (OBJECT_ID(N'AdventureWorks2012.dbo.uspLogError'));  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [建立預存程序](create-a-stored-procedure.md)   
 [修改預存程序](modify-a-stored-procedure.md)   
 [刪除預存程序](delete-a-stored-procedure.md)   
 [重新命名預存程序](rename-a-stored-procedure.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](/sql/t-sql/functions/object-definition-transact-sql)   
 [sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)   
 [sp_helptext &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helptext-transact-sql)   
 [OBJECT_ID &#40;Transact-SQL&#41;](/sql/t-sql/functions/object-id-transact-sql)  
  
  
