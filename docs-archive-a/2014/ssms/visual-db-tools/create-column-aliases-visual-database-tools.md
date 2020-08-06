---
title: 建立資料行別名 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], aliases
- aliases [SQL Server], columns
ms.assetid: e2e1c166-8ea7-47a2-b6a7-e419bf0fa3bb
author: stevestein
ms.author: sstein
ms.openlocfilehash: febe7ed27ed10a283cab549bc65299577d69761c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593752"
---
# <a name="create-column-aliases-visual-database-tools"></a>建立資料行別名 (Visual Database Tools)
  您可以建立資料行名稱的別名，來更輕鬆地使用資料行名稱、計算和彙總值。 例如，您可以建立資料行別名來：  
  
-   針對諸如 `(quantity * unit_price)` 的運算式或彙總函式，建立一個如 Total Amount (總數量) 的資料行名稱。  
  
-   建立資料行名稱的縮短形式，例如， `"d_id"` 代表 `"discounts.stor_id."`  
  
 在定義資料行別名後，您可以在選取查詢中使用別名，來指定查詢的輸出項目。  
  
### <a name="to-create-a-column-alias"></a>若要建立資料行別名  
  
1.  在 [準則窗格]  中，找出包含您想要建立別名之資料行的資料列，並且視輸出需要標示該資料列。 如果資料行不在方格中，將其加入。  
  
2.  在該資料列的 [別名]  資料行中，輸入別名。 別名必須遵循所有 SQL 的命名慣例。 如果所輸入的別名包含空白字元，[查詢和檢視設計師] 會自動在別名前後加入分隔符號。  
  
## <a name="see-also"></a>另請參閱  
 [將資料行加入至查詢 &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [排序和分組查詢結果 &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [&#40;Visual Database Tools&#41;匯總查詢結果](summarize-query-results-visual-database-tools.md)   
 [使用查詢執行基本作業 &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
