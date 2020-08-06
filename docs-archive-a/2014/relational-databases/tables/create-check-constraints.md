---
title: 建立檢查條件約束 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table constraints [SQL Server]
- attaching check constraints
- columns [SQL Server], constraints
- constraints [SQL Server], check
- CHECK constraints, attaching
ms.assetid: b8756304-9454-4d39-996a-64516831b7df
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7795ee6eca85a22bdd4e84c90ce49a9449ddff28
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87607344"
---
# <a name="create-check-constraints"></a>建立檢查條件約束
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立資料表的檢查條件約束，以便指定一個或多個資料行可接受的資料值。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來建立新的檢查條件約束：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要資料表的 ALTER 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-new-check-constraint"></a>若要建立新的檢查條件約束  
  
1.  在 [物件總管]  中，展開您想要加入檢查條件約束的資料表、以滑鼠右鍵按一下 [條件約束]  ，然後按一下 [新增條件約束]  。  
  
2.  在 [檢查條件約束]  對話方塊中，按一下 [運算式]  欄位，然後按一下省略符號 **(...)** 。  
  
3.  在 **[檢查條件約束運算式]** 對話方塊中，輸入檢查條件約束的 SQL 運算式。 例如，若要將 `SellEndDate` 資料表之 `Product` 資料行中的項目限制為大於或等於 `SellStartDate` 資料行中日期的值或是 NULL 值，請輸入：  
  
    ```  
    SellEndDate >= SellStartDate OR SellEndDate IS NULL  
    ```  
  
     或者，若要要求 `zip` 資料行中的項目必須是 5 位數，請輸入：  
  
    ```  
    zip LIKE '[0-9][0-9][0-9][0-9][0-9]'  
    ```  
  
    > [!NOTE]  
    >  請務必將任何非數字條件約束值放在單引號 (') 中。  
  
4.  按一下 [確定]  。  
  
5.  在 [識別]  類別目錄中，您可以變更檢查條件約束的名稱，並且加入條件約束的描述 (擴充屬性)。  
  
6.  在 **[資料表設計工具]** 類別目錄中，您可以設定強制執行條件約束的時間。  
  
    |**收件人：**|**請在下列欄位中選取 [是]：**|  
    |-------------|---------------------------------------------|  
    |針對建立條件約束之前存在的資料測試條件約束|**檢查建立或重新啟用時的現有資料**|  
    |每次在此資料表上進行複寫作業時都強制執行條件約束|**強制複寫**|  
    |每次插入或更新此資料表的資料列時都強制執行條件約束|**於 INSERT 及 UPDATE 時強制套用**|  
  
7.  按一下 [關閉]  。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-new-check-constraint"></a>若要建立新的檢查條件約束  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    ALTER TABLE dbo.DocExc   
       ADD ColumnD int NULL   
       CONSTRAINT CHK_ColumnD_DocExc   
       CHECK (ColumnD > 10 AND ColumnD < 50);  
    GO  
    -- Adding values that will pass the check constraint  
    INSERT INTO dbo.DocExc (ColumnD) VALUES (49);  
    GO  
    -- Adding values that will fail the check constraint  
    INSERT INTO dbo.DocExc (ColumnD) VALUES (55);  
    GO  
  
    ```  
  
 如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)。  
  
###  <a name="TsqlExample"></a>  
