---
title: 在資料採礦設計工具中建立單一查詢 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- singleton queries [Analysis Services]
- Mining Model Prediction [Analysis Services], singleton queries
ms.assetid: 6cdca8a0-cf16-46eb-a652-0bff820625ab
author: minewiskan
ms.author: owend
ms.openlocfilehash: 07491924dbcf0bd35d049e6a7c290d49becfb45d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592334"
---
# <a name="create-a-singleton-query-in-the-data-mining-designer"></a>在資料採礦設計師中建立單一查詢
  如果您想要針對單一案例建立預測，單一查詢便很有用。 如需單一查詢的詳細資訊，請參閱 [資料採礦查詢](data-mining-queries.md)。  
  
 在資料採礦設計師的 [採礦模型預測]**** 索引標籤中，您可以建立許多不同類型的查詢。 您可以使用此設計師或輸入資料採礦延伸模組 (DMX) 陳述式，藉以建立查詢。 此外，您也可以從設計師開始，然後透過變更 DMX 陳述式或加入 WHERE 或 ORDER BY 子句，修改它所建立的查詢。  
  
 若要在查詢設計檢視與查詢文字檢視之間切換，請按一下工具列上的第一個按鈕。 您在查詢文字檢視中時，可以檢視預測查詢產生器所建立的 DMX 程式碼。 您也可以執行查詢、修改查詢，以及執行修改過的查詢。 不過，您若切換回查詢設計檢視，修改過的查詢並不會保存。  
  
 下列程式碼顯示針對目標郵寄模型 TM_Decision_Tree 進行單一查詢的範例。  
  
```  
SELECT [Bike Buyer], PredictProbability([Bike Buyer]) as ProbableBuyer  
FROM [TM_Decision_Tree]  
NATURAL PREDICTION JOIN  
(SELECT '2' AS [Number Children At Home], '45' as [Age])  
AS [t]  
```  
  
 下列步驟將說明如何建立此預測查詢。  
  
### <a name="to-create-a-singleton-query-by-using-the-data-mining-designer"></a>使用資料採礦設計師來建立單一查詢  
  
1.  按一下資料採礦設計師中的 **[採礦模型預測]** 索引標籤。  
  
2.  按一下 **[採礦模型]** 資料表上的 **[選取模型]** 。  
  
     **[選取採礦模型]** 對話方塊就會開啟，以顯示存在於目前專案中的所有採礦結構。  
  
     選取您想要用來建立預測的模型。  
  
     例如，若要建立本主題開頭所顯示的範例程式碼，請選取 TM_Decision_Tree，然後按一下 [確定]****。  
  
3.  在 [採礦模型預測]**** 索引標籤的工具列上，按一下 [單一查詢]****。  
  
     [單一查詢輸入]**** 資料表就會出現在索引標籤上，其中的資料行會自動對應到 [採礦模型]**** 資料表中的資料行。  
  
4.  在 [單一查詢輸入]**** 資料表上，選取 [值]**** 資料行中的值來描述您要建立預測的案例。  
  
     例如，針對 [在家中的**數位子**系] 選取 [ **2** ]，然後 `45` 針對 [ **Age**] 輸入。  
  
5.  將可預測資料行從 [**採礦模型**] 資料表拖曳到索引標籤底部的 [**源**資料行]。您也可以選擇輸入資料行的別名。  
  
     例如，將 [Bike Buyer]**** 拖曳至 [來源]**** 資料行。  
  
6.  從 [來源]**** 資料行的下拉式清單中，選取 [預測函數]**** 或 [自訂運算式]****，將其他功能加入至查詢中。  
  
     例如，按一下 [預測函數]****，然後選取 [PredictProbability]****。  
  
7.  按一下 [PredictProbability]**** 資料列中的 [準則/引數]****，然後輸入要預測的資料行名稱，並選擇性地輸入要預測的特定值。  
  
     例如，輸入 `[Bike Buyer], 1`。  
  
8.  按一下 [PredictProbability]**** 資料列中的 [別名]**** 方塊，然後輸入代表新資料行的名稱。  
  
     例如，輸入 `ProbableBuyer`。  
  
9. 在 [採礦模型預測]**** 索引標籤的工具列上，按一下 [切換到查詢結果檢視]****。  
  
     這時會開啟新的畫面，以顯示查詢的結果。 若要檢視您剛建立的 DMX 陳述式，請按一下 [SQL]****。  
  
## <a name="see-also"></a>另請參閱  
 [預測查詢 &#40;資料採礦&#41;](prediction-queries-data-mining.md)  
  
  
