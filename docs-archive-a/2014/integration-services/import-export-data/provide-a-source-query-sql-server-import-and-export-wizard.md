---
title: 提供來源查詢 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.providesourcequery.f1
ms.assetid: c8cbd07e-b9c3-422f-94b8-d6fc8cf31cf5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b21100f51c279e9ba764c8f82565af9d6e391ef3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597926"
---
# <a name="provide-a-source-query-sql-server-import-and-export-wizard"></a>提供來源查詢 (SQL Server 匯入和匯出精靈)
  使用 [**提供來源查詢**] 頁面，輸入將產生要從資料來源複製到目的地之資料的 SQL 語句。  
  
 若要深入瞭解此嚮導，請參閱[SQL Server 匯入和匯出嚮導](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要瞭解用來啟動精靈的選項，以及成功執行嚮導所需的許可權，請參閱[執行 SQL Server 匯入和匯出嚮導](start-the-sql-server-import-and-export-wizard.md)。  
  
 「SQL Server 匯入和匯出精靈」的用途在於將資料從來源複製到目的地。 這個精靈也可以為您建立目的地資料庫和目的地資料表。 不過，如果您必須複製多個資料庫或資料表，或複製其他種類的資料庫物件，則應該改用「複製資料庫精靈」。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>選項  
 **SQL 語句**  
 輸入查詢陳述式，即可從來源資料庫擷取選取的資料列。 例如，下列查詢陳述式會從 AdventureWorks 資料庫中，擷取佣金百分比超過 1.5% 之業務員的 **SalesPersonID**、 **SalesQuota**以及 **SalesYTD** 。  
  
```  
SELECT SalesPersonID, SalesQuota, SalesYTD  
FROM Sales.SalesPerson  
WHERE CommissionPct > 0.015  
```  
  
 **剖析**  
 檢查 [SQL 陳述式]**** 文字方塊中，SQL 陳述式的語法。  
  
> [!NOTE]  
>  如果檢查陳述式語法所需的時間超過逾時值 30 秒，剖析就會停止並產生錯誤。 在剖析成功之前，您將無法移過精靈的這個頁面。 有一種解決方法是建立以查詢為基礎的資料庫檢視，然後從精靈查詢此檢視，而非直接輸入查詢文字。  
  
 **瀏覽**  
 使用 [**開啟**] 對話方塊來選取包含 SQL 語句的檔案。 選取檔案就會將該檔案的文字複製到 **[查詢陳述式]** 文字方塊中。  
  
  
