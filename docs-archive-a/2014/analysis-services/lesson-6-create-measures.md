---
title: 第7課：建立量值 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 01bd2ad7-09b7-49ae-ad80-83f25da301aa
author: minewiskan
ms.author: owend
ms.openlocfilehash: d89ea5c847276c7a34b4fc800d8bed7b9cd8ad34
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594778"
---
# <a name="lesson-7-create-measures"></a>第 7 課：建立量值
  在這一課，您將建立要包含在模型中的量值。 量值與您在上一課建立的導出資料行相似，基本上是使用 DAX 公式建立的計算。 不過，與導出資料行不同，量值評估是根據使用者選取的「篩選條件」**。例如，在樞紐分析表的 [資料列標籤] 欄位中新增的特定資料行或交叉分析篩選器。   然後會以套用的量值，計算篩選條件中每個資料格的值。 量值是功能強大且彈性的計算，您會希望將它包含在幾乎所有表格式模型中，以便在數值資料上執行動態計算。 如需詳細資訊，請參閱[量值 &#40;SSAS 表格式&#41;](tabular-models/measures-ssas-tabular.md)。  
  
 您將使用 [量值方格] 建立量值。 根據預設，每個資料表都有一個空白的量值方格，不過，通常您不會為每個資料表建立量值。 在 [資料檢視] 中，量值方格會出現在模型設計師中的資料表下方。 若要隱藏或顯示資料表的量值方格，請按一下 [資料表]**** 功能表，然後按一下 [顯示量值方格]****。  
  
 若要建立量值，您可以按一下量值方格中的空資料格，然後在公式列中輸入 DAX 公式。 按 ENTER 完成公式時，量值就會出現在資料格中。 您也可以按一下資料行，然後按一下工具列上的 [自動加總] 按鈕 (**∑**)，利用標準彙總函式建立量值。 使用 [自動加總] 功能建立的量值會出現在資料行正下方的量值方格資料格中，不過必要時可以將其移除。  
  
 在這一課，您將藉由在公式列中輸入 DAX 公式以及使用 [自動加總] 功能這兩種方式建立量值。  
  
 這堂課的預估完成時間：**30 分鐘**  
  
## <a name="prerequisites"></a>Prerequisites  
 本主題是表格式模型教學課程的一部分，請依序完成。 在執行本課中的工作之前，您應已完成上一課： [第 6 課：建立導出資料行](lesson-5-create-calculated-columns.md)。  
  
## <a name="create-measures"></a>建立量值  
  
#### <a name="to-create-a-days-current-quarter-to-date-measure-in-the-date-table"></a>在日期資料表中建立當季目前為止天數量值  
  
1.  在模型設計師中，按一下 [日期]**** 資料表。  
  
2.  如果資料表下方尚未出現空的量值方格，請按一下 [資料表]**** 功能表，然後按一下 [顯示量值方格]****。  
  
3.  在量值方格中，按一下左上方的空資料格。  
  
4.  在資料表上方的公式列中，輸入下列公式︰  
  
     `=COUNTROWS( DATESQTD( 'Date'[Date]))`  
  
     完成建立公式時，按 ENTER。  
  
     請注意，左上方的資料格現在包含量值名稱 [**量值 1**]，後面接著結果 [ **30**]。 公式列中的公式前面也會有量值名稱。  
  
5.  若要重新命名量值，請在公式列中反白顯示名稱 [**量值 1**]，然後輸入 `Days Current Quarter to Date` ，然後按 enter 鍵。  
  
    > [!TIP]  
    >  在公式列中輸入公式時，您也可以先輸入量值名稱，後面接著冒號 (:)，再接著一個空格，最後是公式。 使用這個方法就不需要重新命名量值。  
  
#### <a name="to-create-a-days-in-current-quarter-measure-in-the-date-table"></a>在日期資料表中建立當季天數量值  
  
1.  在 [日期]**** 資料表於模型設計師中仍為使用中狀態時，在量值方格中按一下您剛剛建立之量值下方的空資料格。  
  
2.  在公式列中，輸入下列公式︰  
  
     `Days in Current Quarter :=COUNTROWS( DATESBETWEEN( 'Date'[Date], STARTOFQUARTER( LASTDATE('Date'[Date])), ENDOFQUARTER('Date'[Date])))`  
  
     請注意，在此公式中，您先包含了量值名稱後面接著冒號 (:)。  
  
     完成建立公式時，按 ENTER。  
  
 在一個不完整期間與前一個期間之間建立比率時，公式必須考慮期間內已經過的比例，並且將它與前一個期間中的相同比例進行比較。 在此案例中，[Days Current Quarter to Date]/[Days in Current Quarter] 會得出目前期間內已經過的比例。  
  
#### <a name="to-create-an-internet-distinct-count-sales-order-measure-in-the-internet-sales-table"></a>在 Internet Sales 資料表中建立網際網路相異計數銷售訂單量值  
  
1.  在模型設計師中，按一下 [網際網路銷售]**** 資料表 (索引標籤)。  
  
     如果量值方格尚未出現，請以滑鼠右鍵按一下 [網際網路銷售]**** 資料表 (索引標籤)，然後按一下 [顯示量值方格]****。  
  
2.  按一下 [銷售訂單號碼]**** 欄位標題。  
  
3.  在工具列上，按一下 「自動加總」 \(**∑**) 按鈕旁的向下箭號，然後選取 **[DistinctCount]**。  
  
     「自動加總」功能會使用 DistinctCount 標準彙總公式，自動為選取的資料行建立量值。  
  
     您會發現，量值方格中該資料行下方的頂部資料格現在包含量值名稱 **Distinct Count Sales Order Number**。 使用 [自動加總] 功能建立的量值會自動放入關聯資料行下方量值方格中的最頂部資料格內。  
  
4.  在量值方格中，按一下新的量值，然後在 [屬性]**** 視窗的 [量值名稱]**** 中，將量值重新命名為 **Internet Distinct Count Sales Order**。  
  
#### <a name="to-create-additional-measures-in-the-internet-sales-table"></a>在 Internet Sales 資料表中建立其他量值  
  
1.  使用「自動加總」功能建立並命名下列量值︰  
  
    |[量值名稱]|資料行|自動加總 (∑)|Formula|  
    |------------------|------------|-------------------|-------------|  
    |Internet Order Lines Count|Sales Order Line Number|計數|=COUNT([Sales Order Line Number])|  
    |Internet Total Units|Order Quantity|加總|=SUM([Order Quantity])|  
    |Internet Total Discount Amount|折扣量|加總|=SUM([Discount Amount])|  
    |Internet Total Product Cost|產品總成本|加總|=SUM([Total Product Cost])|  
    |Internet Total Sales|銷售量|加總|=SUM([Sales Amount])|  
    |Internet Total Margin|Margin|加總|=SUM([Margin])|  
    |Internet Total Tax Amt|稅額|加總|=SUM([Tax Amt])|  
    |Internet Total Freight|Freight|加總|=SUM([Freight])|  
  
2.  藉由按一下量值方格中的空白資料格，以及使用公式列，建立並命名下列量值：  
  
    > [!IMPORTANT]  
    >  您必須依序建立下列量值；後續量值中的公式會參考之前的量值。  
  
    |[量值名稱]|Formula|  
    |------------------|-------------|  
    |Internet Previous Quarter Margin|=CALCULATE([Internet Total Margin],PREVIOUSQUARTER('Date'[Date]))|  
    |Internet Current Quarter Margin|=TOTALQTD([Internet Total Margin],'Date'[Date])|  
    |Internet Previous Quarter Margin Proportion to QTD|=[Internet Previous Quarter Margin]*([Days Current Quarter to Date]/[Days In Current Quarter])|  
    |Internet Previous Quarter Sales|=CALCULATE([Internet Total Sales],PREVIOUSQUARTER('Date'[Date]))|  
    |Internet Current Quarter Sales|=TOTALQTD([Internet Total Sales],'Date'[Date])|  
    |Internet Previous Quarter Sales Proportion to QTD|=[Internet Previous Quarter Sales]*([Days Current Quarter to Date]/[Days In Current Quarter])|  
  
 針對 [Internet Sales] 資料表建立的量值可用來分析關鍵的財務資料，例如使用者選取的篩選所定義的項目銷售額、成本和利率。  
  
## <a name="next-step"></a>後續步驟  
 若要繼續進行本教學課程，請前往下一課： [第 8 課：建立關鍵效能指標](lesson-7-create-key-performance-indicators.md)。  
  
  
