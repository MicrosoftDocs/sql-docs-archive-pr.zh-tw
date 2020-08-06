---
title: 使用計畫指南指定查詢參數化行為 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- TEMPLATE plan guide
- PARAMETERIZATION FORCED option
- PARAMETERIZATION option
- PARAMETERIZATION SIMPLE option
- parameterization [SQL Server]
- overriding parameterization behavior
- plan guides [SQL Server], parameterization
- parameterized queries [SQL Server]
ms.assetid: f0f738ff-2819-4675-a8c8-1eb6c210a7e6
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f595b9f0e0a6d7bceffc5cb283c60b6f40e025b3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606806"
---
# <a name="specify-query-parameterization-behavior-by-using-plan-guides"></a>使用計畫指南指定查詢參數化行為
  當 PARAMETERIZATION 資料庫選項設定為 SIMPLE 時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢最佳化工具可能會選擇將查詢參數化。 這意謂著任何包含在查詢中的常值將會以參數替代。 此處理序稱為簡易參數化。 當 SIMPLE 參數化生效時，您無法控制哪些查詢要參數化以及哪些查詢不要參數化。 但是，您可以將 PARAMETERIZATION 資料庫選項設定為 FORCED，藉以指定要參數化資料庫中的所有查詢。 此處理序稱為強制參數化。  
  
 您可以透過下列方式使用計畫指南來覆寫資料庫的參數化行為：  
  
-   當 PARAMETERIZATION 資料庫選項設定為 SIMPLE 時，您可以指定在特定的查詢類別強制參數化。 作法是在查詢的參數化表單上建立 TEMPLATE 計畫指南，並在 [sp_create_plan_guide](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql) 預存程序中指定 PARAMETERIZATION FORCED 查詢提示。 您可以考慮將此類的計畫指南做為只在某類別的查詢 (而不是所有的查詢) 中啟用強制參數化的方式。  
  
-   當 PARAMETERIZATION 資料庫選項設定為 FORCED 時，您可以指定在特定的查詢類別只嘗試簡單參數化，但不嘗試強制參數化。 作法是在查詢的強制參數化表單上建立 TEMPLATE 計畫指南，並在 **sp_create_plan_guide**中指定 PARAMETERIZATION SIMPLE 查詢提示。  
  
 請考慮在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中的下列查詢：  
  
```  
SELECT pi.ProductID, SUM(pi.Quantity) AS Total  
FROM Production.ProductModel AS pm   
    INNER JOIN Production.ProductInventory AS pi   
        ON pm.ProductModelID = pi.ProductID   
WHERE pi.ProductID = 101   
GROUP BY pi.ProductID, pi.Quantity HAVING SUM(pi.Quantity) > 50;  
```  
  
 身為資料庫管理員，您已決定不要啟用資料庫中所有查詢的強制參數化。 不過，您想要對在語法上與上一個查詢相等，但僅其常值不同的所有查詢，省下其編譯成本。 換句話說，您想要參數化查詢，這樣才能拒絕這類的查詢計畫。 在此情況下，請完成下列步驟：  
  
1.  擷取查詢的參數化格式。 取得這個值供 **sp_create_plan_guide** 使用的唯一安全方法，是使用 [sp_get_query_template](/sql/relational-databases/system-stored-procedures/sp-get-query-template-transact-sql) 系統預存程序。  
  
2.  在查詢的參數化格式上建立計畫指南，以指定 PARAMETERIZATION FORCED 查詢提示。  
  
    > [!IMPORTANT]  
    >  在參數化查詢時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會指派資料類型給取代常值的參數，端視常值的值與大小而定。 相同的程式會發生在傳遞至 sp_get_query_template 之輸出參數的常數常值 **@stmt** 。 **sp_get_query_template** 因為在 sp_create_plan_guide 的引數中指定的資料類型 **@params** 必須符合參數化時的查詢，所以**sp_create_plan_guide** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 您可能必須建立一個以上的計劃指南，以涵蓋查詢的可能參數值的完整範圍。  
  
 下列指令碼可用以擷取參數化查詢，並在該查詢上建立計畫指南：  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT pi.ProductID, SUM(pi.Quantity) AS Total   
      FROM Production.ProductModel AS pm   
      INNER JOIN Production.ProductInventory AS pi ON pm.ProductModelID = pi.ProductID   
      WHERE pi.ProductID = 101   
      GROUP BY pi.ProductID, pi.Quantity   
      HAVING sum(pi.Quantity) > 50',  
    @stmt OUTPUT,   
    @params OUTPUT;  
EXEC sp_create_plan_guide   
    N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 相同的，在已經啟用強制參數化的資料庫中，您可以確定讓範例查詢以及其他句法相同的項目 (常數常值除外)，都根據簡單參數化規則加以參數化。 作法是指定 OPTION 子句中的 PARAMETERIZATION SIMPLE，而不是 PARAMETERIZATION FORCED。  
  
> [!NOTE]  
>  TEMPLATE 計畫指南可使陳述式配合僅由單一陳述式組成的批次中所提交的查詢。 TEMPLATE 計畫指南無法配合多重陳述式批次中的陳述式。  
  
  
