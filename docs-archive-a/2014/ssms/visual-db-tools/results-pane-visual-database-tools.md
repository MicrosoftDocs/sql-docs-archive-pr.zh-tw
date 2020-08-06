---
title: 結果窗格 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- result sets [SQL Server], queries
- synchronization [SQL Server], query results with definition
- displaying query results in grid
- grid showing query results [SQL Server]
- showing query results in grid
- Query Designer [SQL Server], Results pane
- results [SQL Server], query
- viewing query results
- queries [SQL Server], results
- Results pane
ms.assetid: 6309a1bc-a628-4141-8bb5-b35924bd19f9
author: stevestein
ms.author: sstein
ms.openlocfilehash: f0db32336931f74777be56befcde9501dc484b69
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584938"
---
# <a name="results-pane-visual-database-tools"></a>結果窗格 (Visual Database Tools)
  [結果] 窗格顯示的是最近執行 SELECT 查詢的結果 (其他查詢類型的結果則顯示在訊息方塊中)。若要開啟結果窗格、開啟或建立查詢或檢視，或傳回資料表的資料。 如果結果窗格未預設顯示，可從 [ **查詢設計工具** ] 功能表，指向 [ **窗格**]，然後按一下 [ **結果**]。  
  
## <a name="what-you-can-do-in-the-results-pane"></a>結果窗格的功用  
  
-   檢視格式類似工作表方格的最近執行 SELECT 查詢結果集。  
  
-   針對來自單一資料表或檢視所顯示的查詢或檢視資料，您可以在結果集內的個別資料行中編輯值、加入新的記錄列以及刪除現有的資料列。  
  
## <a name="limitations-in-the-results-pane"></a>結果窗格中的限制  
  
-   資料表值函數所傳回的結果，只能在某些情況下更新。  
  
-   包含來自一個以上資料表或檢視的資料行之查詢或檢視，無法更新。  
  
-   由預存程序所傳回的結果無法更新。  
  
-   使用 GROUP  BY 或 DISTINCT 子句的查詢或檢視無法更新。  
  
## <a name="navigating-in-the-results-pane"></a>在結果窗格中巡覽  
 您可使用在 [結果] 窗格下方的巡覽列快速巡覽資料錄。  
  
 有按鈕可移至第一筆與最後一筆資料錄、下一筆與前一筆資料錄，以及移至特定資料錄。  
  
 若要移至特定資料錄，在巡覽列文字方塊中輸入列號，然後按 ENTER。  
  
 如需在查詢和檢視表設計工具中使用鍵盤快速鍵的詳細資訊，請參閱[在查詢和檢視表設計工具中巡覽 &#40;Visual Database Tools&#41;](visual-database-tools.md)。  
  
## <a name="keeping-the-results-set-synchronized-with-the-query-definition"></a>保持結果集與查詢定義同步處理  
 當您在處理查詢或檢視結果時，[結果] 窗格中的資料錄可能未與查詢定義保持同步處理。 例如，若您在資料表中執行五個資料行其中四個的查詢，然後使用 [圖表窗格] 在查詢定義中加入第五個資料行，則第五個資料行的資料將不會自動加入至 [結果] 窗格中。 若要讓 [結果] 窗格反映新的查詢定義，請再次執行查詢。  
  
 如果查詢變更，在 [結果] 窗格的右下角會有警告圖示，並且會出現「已變更的查詢」文字。 圖示會在窗格的左上角重複出現。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Visual Database Tools 建立查詢&#41;](create-queries-visual-database-tools.md)   
 [&#40;Visual Database Tools 執行查詢&#41;](run-queries-visual-database-tools.md)   
 [設計查詢和觀看 how to 主題 &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [&#40;Visual Database Tools&#41;的圖表窗格](diagram-pane-visual-database-tools.md)   
 [&#40;Visual Database Tools&#41;的 [準則窗格]](criteria-pane-visual-database-tools.md)   
 [使用結果窗格中的資料 &#40;Visual Database Tools&#41;](results-pane-visual-database-tools.md)  
  
  
