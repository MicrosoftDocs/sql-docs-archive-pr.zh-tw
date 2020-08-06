---
title: 設定或變更資料庫定序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], database
- database collations [SQL Server]
ms.assetid: 1379605c-1242-4ac8-ab1b-e2a2b5b1f895
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6d7f7c3e3ddba7ba0ea9701993dbe0fad3a8d975
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606900"
---
# <a name="set-or-change-the-database-collation"></a>設定或變更資料庫定序
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中設定及變更資料庫定序。 如果沒有指定定序，會使用伺服器定序。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目設定或變更資料庫定序：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   僅限 Windows Unicode 定序只能搭配 COLLATE 子句使用，以便將定序套用至資料行層級和運算式層級資料的 `nchar`、`nvarchar` 和 `ntext` 資料類型。 這些定序無法搭配 COLLATE 子句使用，以變更資料庫或伺服器執行個體的定序。  
  
-   如果指定的定序或所參考物件所用的定序使用 Windows 不支援的字碼頁， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 就會顯示錯誤。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   您可以在 [Windows 定序名稱 &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql) 和 [SQL Server 定序名稱 &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql)中找到支援的定序名稱；您也可以使用 [sys.fn_helpcollations &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql) 系統函數。  
  
-   當您變更資料庫定序時，會變更下列各項：  
  
    -   系統資料表中的任何 `char`、`varchar`、`text`、`nchar`、`nvarchar`，或 `ntext` 資料行都會變更為新定序。  
  
    -   預存程序與使用者定義函數的任何現有 `char`、`varchar`、`text`、`nchar`、`nvarchar`，或 `ntext` 參數和純量傳回值，都會變更為新定序。  
  
    -   `char`、`varchar`、`text`、`nchar`、`nvarchar`，或 `ntext` 系統資料類型，以及以這些系統資料類型為基礎的所有使用者定義資料類型，都會變更為新的預設定序。  
  
-   您可以使用 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) 陳述式的 COLLATE 子句，變更在使用者資料庫中建立的任何新物件的定序。 此陳述式不會變更現有使用者自訂資料表中的資料行定序。 您可以使用 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql)的 COLLATE 子句進行變更。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 CREATE DATABASE  
 需要**master**資料庫中的 create DATABASE 許可權，或需要 CREATE any DATABASE 或 ALTER any database 許可權。  
  
 ALTER DATABASE  
 需要資料庫的 ALTER 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-set-or-change-the-database-collation"></a>若要設定或變更資料庫定序  
  
1.  在 [物件總管]  中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，展開該執行個體，然後展開 [資料庫]  。  
  
2.  如果您要建立新資料庫，以滑鼠右鍵按一下 **[資料庫]** ，然後按一下 **[新增資料庫]** 。 如果不要預設定序，請按一下 **[選項]** 頁面，然後從 **[定序]** 下拉式清單中選取定序。  
  
     或者，如果資料庫已經存在，以滑鼠右鍵按一下所要的資料庫，然後按一下 **[屬性]** 。 按一下 **[選項]** 頁面，然後從 **[定序]** 下拉式清單中選取定序。  
  
3.  完成後，請按一下 **[確定]** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-set-the-database-collation"></a>若要設定資料庫定序  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例示範如何使用 [COLLATE](/sql/t-sql/statements/collations) 子句來指定定序名稱。 範例會建立使用 `MyOptionsTest` 定序的 `Latin1_General_100_CS_AS_SC` 資料庫。 在您建立資料庫之後，執行 `SELECT` 陳述式以驗證設定。  
  
```sql  
USE master;  
GO  
IF DB_ID (N'MyOptionsTest') IS NOT NULL  
DROP DATABASE MyOptionsTest;  
GO  
CREATE DATABASE MyOptionsTest  
COLLATE Latin1_General_100_CS_AS_SC;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
  
```  
  
#### <a name="to-change-the-database-collation"></a>若要變更資料庫定序  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例示範如何在 [ALTER DATABASE](/sql/t-sql/statements/collations) 陳述式中使用 [COLLATE](/sql/t-sql/statements/alter-database-transact-sql) 子句，以變更定序名稱。 執行 `SELECT` 陳述式以驗證變更。  
  
```sql  
USE master;  
GO  
ALTER DATABASE MyOptionsTest  
COLLATE French_CI_AS ;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [定序與 Unicode 支援](collation-and-unicode-support.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [SQL Server 定序名稱 &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql)   
 [Windows 定序名稱 &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql)   
 [COLLATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/collations)   
 [定序優先順序 &#40;Transact-SQL&#41;](/sql/t-sql/statements/collation-precedence-transact-sql)   
 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
