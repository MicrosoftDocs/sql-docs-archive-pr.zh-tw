---
title: 設定平行索引作業 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index parallel operations [SQL Server]
- processors [SQL Server], parallel index operations
- max degree of parallelism option
- MAXDOP index option, parallel index operations
- parallel index operations [SQL Server]
ms.assetid: 8ec8c71e-5fc1-443a-92da-136ee3fc7f88
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8831aadae15af03a05f4ab03cfe514e54566df1f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585385"
---
# <a name="configure-parallel-index-operations"></a>設定平行索引作業
  本主題定義平行處理原則的最大程度，並說明如何在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]修改此設定。 在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise 或更新版本的多處理器電腦上，索引陳述式可能會如同其他查詢般，使用多個處理器來執行與索引陳述式相關聯的掃描、排序和索引作業。 執行單一索引陳述式所用的處理器數目，取決於 [平行處理原則的最大程度](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 組態選項、目前的工作負載以及索引統計資料。 max degree of parallelism 選項會決定用於執行平行計畫的最大處理器數目。 如果 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 偵測到系統忙碌中，在陳述式執行開始之前，會先自動降低索引作業之平行處理原則的程度。 如果非資料分割索引的前端索引鍵資料行具有有限的相異值數目，或者每個相異值的頻率具有大幅差異， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 也可能會降低平行處理原則的程度。  
  
> [!NOTE]  
>  並非所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本都可使用平行索引作業。 如需詳細資訊，請參閱＜ [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)＞。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要設定平行處理原則的最大程度，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   查詢最佳化工具所使用的處理器數目通常可以提供最佳的效能。 然而，諸如建立、重建、卸除非常大的索引都需要大量的資源，並可能在索引作業期間造成其他應用程式和資料庫作業的資源不足。 當發生此問題時，您可以限制索引作業要使用的處理器數目，藉以手動設定執行索引陳述式要使用的最大處理器數目。  
  
-   MAXDOP 索引選項只會針對指定此選項的查詢來覆寫 max degree of parallelism 組態選項。 下表列出可以使用 max degree of parallelism 組態選項及 MAXDOP 索引選項指定的有效整數值。  
  
    |值|描述|  
    |-----------|-----------------|  
    |0|指定伺服器會根據目前的系統工作負載來決定所使用的 CPU 數目。 這是預設值且為建議的設定。|  
    |1|隱藏平行計畫的產生。 作業必須循序執行。|  
    |2-64|將處理器的數目限制成指定的值。 視目前的工作負載而定來使用較少的處理器。 如果指定的值大於可用的 CPU 個數，就會使用實際可用的 CPU 個數。|  
  
-   平行索引執行與 MAXDOP 索引選項適用於下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    -   CREATE INDEX  
  
    -   ALTER INDEX REBUILD  
  
    -   DROP INDEX (僅適用於叢集索引。)  
  
    -   ALTER TABLE ADD (索引) CONSTRAINT  
  
    -   ALTER TABLE DROP (叢集索引) CONSTRAINT  
  
-   在 ALTER INDEX REORGANIZE 陳述式中無法指定 MAXDOP 索引選項。  
  
-   如果查詢最佳化工具將平行處理原則的程度套用至建立作業，則需要排序的資料分割索引作業可能需要更多的記憶體。 平行處理原則的程度愈高，所需的記憶體就愈大。 如需詳細資訊，請參閱＜ [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md)＞。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要資料表或檢視表的 ALTER 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-set-max-degree-of-parallelism-on-an-index"></a>若要在索引上設定平行處理原則的最大程度  
  
1.  在 [物件總管] 中，按一下加號展開資料庫，此資料庫包含您要設定索引之平行處理原則最大程度的資料表。  
  
2.  展開 **[資料表]** 資料夾。  
  
3.  按一下加號展開包含您要設定索引之平行處理原則最大程度的資料表。  
  
4.  展開 **[索引]** 資料夾。  
  
5.  以滑鼠右鍵按一下要設定平行處理原則最大程度的索引，然後選取 [屬性]  。  
  
6.  在 **[選取頁面]** 底下，選取 **[選項]** 。  
  
7.  選取 **[平行處理原則的最大程度]** ，然後輸入介於 1 和 64 之間的一些值。  
  
8.  按一下 [確定]  。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-set-max-degree-of-parallelism-on-an-existing-index"></a>若要在現有索引上設定平行處理原則的最大程度  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    /*Alters the IX_ProductVendor_VendorID index on the Purchasing.ProductVendor table so that, if the server has eight or more processors, the Database Engine will limit the execution of the index operation to eight or fewer processors.  
    */  
    ALTER INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor  
    REBUILD WITH (MAXDOP=8);   
    GO  
    ```  
  
 如需詳細資訊，請參閱 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)。  
  
#### <a name="set-max-degree-of-parallelism-on-a-new-index"></a>在新索引上設定平行處理原則的最大程度  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE INDEX IX_ProductVendor_NewVendorID   
    ON Purchasing.ProductVendor (BusinessEntityID)  
    WITH (MAXDOP=8);  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)。  
  
  
