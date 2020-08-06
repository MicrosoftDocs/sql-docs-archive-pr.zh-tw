---
title: 建立內含資料行的索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index size [SQL Server]
- index keys [SQL Server]
- index columns [SQL Server]
- size [SQL Server], indexes
- key columns [SQL Server]
- included columns
- nonclustered indexes [SQL Server], included columns
- designing indexes [SQL Server], included columns
- nonkey columns
ms.assetid: d198648d-fea5-416d-9f30-f9d4aebbf4ec
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e5a464f9791ea635236069555647229bf1f0d79e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708310"
---
# <a name="create-indexes-with-included-columns"></a>建立內含資料行的索引
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中加入內含 (或非索引鍵) 資料行，以擴充非叢集索引的功能。 藉由加入非索引鍵資料行，您可以建立涵蓋更多查詢的非叢集索引。 這是因為非索引鍵之索引資料行有下列好處：  
  
-   與索引鍵資料行一樣，它們可以是不允許的資料類型。  
  
-   計算索引鍵資料行數或索引鍵大小時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 不會考慮它們。  
  
 查詢中所有的資料行在索引中當做索引鍵或非索引鍵資料行時，非索引鍵資料行的索引可以大幅改進查詢效能。 因為查詢最佳化工具可以在索引中找到所有資料行值，所以可以提高效能；不存取資料表或叢集索引資料，導致磁碟 I/O 作業變少。  
  
> [!NOTE]  
>  索引包含查詢參考的所有資料行時，通常就是指「涵蓋查詢」。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [設計建議](#DesignRecs)  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用下列方法建立非索引鍵資料行的索引：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="design-recommendations"></a><a name="DesignRecs"></a> 設計建議  
  
-   重新設計具有大型索引鍵大小的非叢集索引，如此僅有用於搜尋與查閱的資料行才會是索引鍵資料行。 讓涵蓋查詢的所有其他資料行都做為非索引鍵資料行。 如此一來，您將擁有涵蓋查詢所需的所有資料行，但是索引鍵本身會變得很小而且很有效率。  
  
-   在非叢集索引中包含非索引鍵資料行，以避免超出目前索引大小限制 (最大 16 個索引鍵資料行，最大 900 個位元組索引鍵大小) 計算索引鍵資料行數或索引鍵大小時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 不會考慮非索引鍵之索引資料行。  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   非索引鍵資料行只能在非叢集索引上定義。  
  
-   除了 `text`、`ntext` 和 `image`，所有資料類型都可以做為非索引鍵資料行。  
  
-   具決定性之精確或非精確的計算資料行都可以當做非索引鍵資料行。 如需詳細資訊，請參閱 [計算資料行的索引](indexes-on-computed-columns.md)。  
  
-   只要計算資料行資料類型可以做為非索引鍵索引資料行，則從 `image`、`ntext` 與 `text` 資料類型衍生的計算資料行即可以是非索引鍵資料行。  
  
-   必須先卸除資料表的索引，才能從資料表卸除非索引鍵資料行。  
  
-   除非執行下列動作，否則無法變更非索引鍵之索引資料行：  
  
    -   將資料行的 Null 屬性從 NOT NULL 變更為 NULL。  
  
    -   增加 `varchar`、`nvarchar` 或 `varbinary` 資料行的長度。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要資料表或檢視表的 ALTER 權限。 使用者必須是 **系統管理員** 固定伺服器角色的成員，或是 **db_ddladmin** 和 **db_owner** 固定資料庫角色的成員。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-an-index-with-nonkey-columns"></a>建立非索引鍵資料行的索引  
  
1.  在 [物件總管] 中，按一下加號展開資料庫，此資料庫包含您要建立非索引鍵資料行之索引的資料表。  
  
2.  按一下加號展開 **[資料表]** 資料夾。  
  
3.  按一下加號展開要建立非索引鍵資料行之索引的資料表。  
  
4.  以滑鼠右鍵按一下 [索引] 資料夾，指向 [新增索引]，然後選取 [非叢集索引…]。  
  
5.  在 **[新增索引]** 對話方塊，於 **[一般]** 頁面上的 **[索引名稱]** 方塊中輸入新索引的名稱。  
  
6.  按一下 [索引鍵資料行] 索引標籤底下的 [加入...]。  
  
7.  在 [**從**_Table_name_選取資料行] 對話方塊中，選取要加入至索引之資料表資料行的核取方塊。  
  
8.  按一下 [確定]。  
  
9. 按一下 [包含的資料行] 索引標籤底下的 [加入...]。  
  
10. 在 [**從**_Table_name_選取資料行] 對話方塊中，選取要加入至索引中做為非索引鍵資料行之資料表資料行或資料行的核取方塊。  
  
11. 按一下 [確定]。  
  
12. 在 **[新增索引]** 對話方塊中，按一下 **[確定]** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-an-index-with-nonkey-columns"></a>建立非索引鍵資料行的索引  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Creates a nonclustered index on the Person.Address table with four included (nonkey) columns.   
    -- index key column is PostalCode and the nonkey columns are  
    -- AddressLine1, AddressLine2, City, and StateProvinceID.  
    CREATE NONCLUSTERED INDEX IX_Address_PostalCode  
    ON Person.Address (PostalCode)  
    INCLUDE (AddressLine1, AddressLine2, City, StateProvinceID);  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)。  
  
  
