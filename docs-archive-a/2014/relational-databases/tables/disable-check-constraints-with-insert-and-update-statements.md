---
title: 停用 INSERT 與 UPDATE 陳述式的檢查條件約束 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- CHECK constraints, disabling
- constraints [SQL Server], disabling
- disabling constraints
- constraints [SQL Server], check
ms.assetid: c7287ad1-50d2-4e80-bc0c-b5570f7e5f69
author: stevestein
ms.author: sstein
ms.openlocfilehash: 780a2c1bfd9f21c71367ad61f200ec19ab44a608
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595869"
---
# <a name="disable-check-constraints-with-insert-and-update-statements"></a>使用 INSERT 與 UPDATE 陳述式停用檢查條件約束
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中停用 INSERT 和 UPDATE 交易的檢查條件約束。 停用檢查條件約束之後，未來將不會根據條件約束的條件驗證資料行的插入或更新作業。 如果您確知新資料將違反現有條件約束，或是條件約束只適用於已經在資料庫中的資料，請使用此選項。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來停用 INSERT 和 UPDATE 陳述式的檢查條件約束：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要資料表的 ALTER 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-disable-a-check-constraint-for-insert-and-update-statements"></a>若要停用 INSERT 和 UPDATE 陳述式的檢查條件約束  
  
1.  在 **[物件總管]** 中，展開含有條件約束的資料表，然後展開 **[條件約束]** 資料夾。  
  
2.  以滑鼠右鍵按一下條件約束，然後選取 **[修改]** 。  
  
3.  在 **[資料表設計工具]** 底下的方格中，按一下 **[於 INSERT 及 UPDATE 時強制套用]** ，然後從下拉式功能表中選取 **[否]** 。  
  
4.  按一下 [關閉]  。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-disable-a-check-constraint-for-insert-and-update-statements"></a>若要停用 INSERT 和 UPDATE 陳述式的檢查條件約束  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Purchasing.PurchaseOrderHeader  
    NOCHECK CONSTRAINT CK_PurchaseOrderHeader_Freight;   
    GO  
    ```  
  
 如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)。  
  
###  <a name="TsqlExample"></a>  
