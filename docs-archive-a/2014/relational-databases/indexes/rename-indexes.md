---
title: 重新命名索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- renaming indexes
- index names [SQL Server]
- indexes [SQL Server], renaming
ms.assetid: d3d612a1-ea1b-4d99-85d2-0a2ad54f4b0e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 184d6e20f7857c5ea3535e77e21a0630ffc7b678
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606291"
---
# <a name="rename-indexes"></a>重新命名索引
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中重新命名索引。 重新命名索引將以您提供的新索引名稱來取代目前的名稱。 指定的名稱在資料表或檢視內必須是唯一的。 例如，兩個資料表可以同時擁有名稱為 **XPK_1**的索引，但同一個資料表不能具有兩個名稱為 **XPK_1**的索引。 您不能使用與現有停用之索引相同的名稱來建立索引。 重新命名索引並不會重建索引。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用下列方法重新命名索引：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
 當您在資料表上建立 PRIMARY KEY 或 UNIQUE 條件約束時，也會自動為資料表建立一個與條件約束名稱相同的索引。 因為資料表內的索引名稱必須是獨一無二的，所以無法使用與資料表上現有 PRIMARY KEY 或 UNIQUE 條件約束相同的名稱來建立或重新命名索引。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要索引的 ALTER 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-rename-an-index-by-using-the-table-designer"></a>使用資料表設計工具重新命名索引  
  
1.  在 [物件總管] 中，按一下加號展開資料庫，此資料庫包含您要重新命名索引的資料表。  
  
2.  按一下加號展開 **[資料表]** 資料夾。  
  
3.  以滑鼠右鍵按一下要重新命名索引的資料表，然後選取 [設計]  。  
  
4.  在 [資料表設計工具]  功能表上，按一下 [索引/索引鍵]  。  
  
5.  從 [選取的主/唯一索引鍵或索引]  文字方塊中選取要重新命名的索引。  
  
6.  在方格中，按一下 [ **名稱** ]，然後在文字方塊輸入新名稱。  
  
7.  按一下 [關閉]  。  
  
8.  在 [檔案] 功能表上，按一下 [儲存 _資料表名稱_]。  
  
#### <a name="to-rename-an-index-by-using-object-explorer"></a>使用物件總管重新命名索引  
  
1.  在 [物件總管] 中，按一下加號展開資料庫，此資料庫包含您要重新命名索引的資料表。  
  
2.  按一下加號展開 **[資料表]** 資料夾。  
  
3.  按一下加號展開要重新命名索引的資料表。  
  
4.  按一下加號展開 **[索引]** 資料夾。  
  
5.  以滑鼠右鍵按一下您要重新命名的索引，然後選取 [重新命名]  。  
  
6.  鍵入索引的新名稱，然後按 Enter 鍵。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-rename-an-index"></a>若要重新命名索引  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    --Renames the IX_ProductVendor_VendorID index on the Purchasing.ProductVendor table to IX_VendorID.   
  
    EXEC sp_rename N'Purchasing.ProductVendor.IX_ProductVendor_VendorID', N'IX_VendorID', N'INDEX';   
    GO  
    ```  
  
 如需詳細資訊，請參閱 [sp_rename &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql)。  
  
  
