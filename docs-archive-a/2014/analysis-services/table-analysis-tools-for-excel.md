---
title: 適用于 Excel 的資料表分析工具 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- getting started
ms.assetid: 6d9d1481-18e4-4108-9efa-68152b0940c9
author: minewiskan
ms.author: owend
ms.openlocfilehash: e566f5213f1ecd98685a3199c57b962be96c5aa7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705449"
---
# <a name="table-analysis-tools-for-excel"></a>適用於 Excel 的資料表分析工具
  [**分析**] 工具列中的資料採礦工具是開始使用資料採礦的最簡單方式。 每個工具都會自動分析資料的散發和類型，並設定參數以確保結果是有效的。 您不需選取演算法或設定複雜參數。  
  
 ![DM](media/dm-tabletoolsanalyze.gif "DM")  
  
 [**分析**] 功能區包含下列工具：  
  
 [&#40;適用于 Excel 的資料表分析工具分析關鍵影響因數&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 您選擇感興趣的資料行或輸出值，然後演算法就會分析所有輸入資料以識別對目標有最大影響的因素。 或者，您可以建立會比較任何兩個值的報表，這樣就可以查看影響因數如何變更。  
  
 [**分析關鍵影響**因數] 工具會使用 Microsoft 的簡單貝氏機率分類演算法。  
  
 [偵測適用于 Excel&#41;&#40;資料表分析工具的分類](detect-categories-table-analysis-tools-for-excel.md)  
 此工具可讓您新增任何資料集和套用叢集以尋找資料的群組。 這適用于尋找相似之處，以及建立群組以進一步分析。  
  
 [偵測**類別目錄**] 工具會使用 Microsoft 群集演算法。  
  
 [&#40;適用于 Excel 的資料表分析工具&#41;的範例填滿](fill-from-example-table-analysis-tools-for-excel.md)  
 此工具會協助您推算遺漏值。 您要提供遺漏值應該會是什麼的一些範例，此工具就會依據資料表中的所有資料來建立模式，然後依據資料模式建議新的值。  
  
 [**根據範例填滿**] 工具會使用 Microsoft 羅吉斯回歸演算法。  
  
 [適用于 Excel&#41;的預測 &#40;資料表分析工具](forecast-table-analysis-tools-for-excel.md)  
 此工具會採用隨著時間而變更的資料，然後預測未來值。  
  
 「**預測**」工具會使用 Microsoft 時間序列演算法。  
  
 [反白顯示 &#40;適用于 Excel 的資料表分析工具的例外狀況&#41;](highlight-exceptions-table-analysis-tools-for-excel.md)  
 這項工具會分析資料表中的模式，並尋找不符合模式的資料列和值。 接著您就可以檢閱這些值並加以更正，然後重新執行模型或標記這些值以供稍後採取動作。  
  
 [**反白顯示例外**狀況] 工具會使用 Microsoft 群集演算法。  
  
 [&#40;適用于 Excel&#41;的資料表分析工具的目標搜尋案例](goal-seek-scenario-table-analysis-tools-for-excel.md)  
 在 [**搜尋目標**] 工具中，您可以指定目標值，而此工具會識別必須變更以符合該目標的基礎因數。 例如，如果您知道必須增加通話滿意度 20%，就可以要求模型預測應該要變更才能達到目標的因數。  
  
 [**搜尋目標**] 工具使用 Microsoft 羅吉斯回歸演算法。  
  
 [適用于 Excel 的資料表分析工具 &#40;假設案例&#41;](what-if-scenario-table-analysis-tools-for-excel.md)  
 [**假設分析**] 工具會補充 [**搜尋目標**] 工具。 使用此工具時，您要輸入您想要變更的值，模型就會預測該變更是否足以達到所要的結果。 例如，您可以要求模型推測若額外增加一個話務員是否能將客戶滿意度提高一個積分點。  
  
 **假設**工具會使用 Microsoft 羅吉斯回歸演算法。  
  
 [預測計算器 &#40;適用于 Excel 的資料表分析工具&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
 這個工具會建立模型，用於分析產生目標結果的因數，然後根據從資料衍生的計分規則預測任何新輸入的結果。 這個工具也會產生互動式決策工作表，讓您輕鬆為新輸入計分。 您還可以建立計分工作表的列印版本，以供離線使用。  
  
 **預測計算器**工具會使用 Microsoft 羅吉斯回歸演算法。  
  
 [適用于 Excel&#41;的購物籃分析 &#40;資料表 AnalysisTools](shopping-basket-analysis-table-analysistools-for-excel.md)  
 這個工具會識別可用於交叉銷售或向上銷售的模式。 它會識別經常一起購買的產品群組，也會根據相關產品組合的價格和成本來產生報表，以輔助您做決策。  
  
 這項工具不限於購物籃分析；您可以將它套用到任何有助於關聯分析的問題。 例如，您可以查看經常一起發生的事件、會導致診斷的因素，或任何其他可能的原因集和結果集。  
  
 [**購物籃分析**] 工具使用 Microsoft 關聯演算法。  
  
## <a name="requirements-for-the-table-analysis-tools-for-excel"></a>適用於 Excel 的資料表分析工具的需求  
 若要使用適用於 Excel 的資料表分析工具，您必須先建立與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。 此連接可讓您存取分析資料時所用的 Microsoft 資料採礦演算法。 如果您無法存取執行個體，建議您請系統管理員設定一個執行個體，讓您能夠用於實驗資料採礦。 如需詳細資訊，請參閱[連接到來源資料 &#40;適用于 Excel&#41;的資料採礦用戶端](connect-to-source-data-data-mining-client-for-excel.md)。  
  
 若要使用資料表分析工具來處理資料，您必須將您要使用的資料範圍轉換成 Excel 資料表。  
  
 如果您看不到 [**分析**] 功能區，請嘗試先在資料表中按一下。 此功能表要等到選取了資料表之後才會啟動。  
  
## <a name="see-also"></a>另請參閱  
 [適用于 Excel &#40;SQL Server 資料採礦增益集的資料採礦用戶端&#41;](data-mining-client-for-excel-sql-server-data-mining-add-ins.md)   
 [針對 Visio 資料採礦圖表進行疑難排解 &#40;SQL Server 資料採礦增益集&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)   
 [適用於 Office 的資料採礦增益集包含的內容](what-s-included-in-the-data-mining-add-ins-for-office.md)  
  
  
