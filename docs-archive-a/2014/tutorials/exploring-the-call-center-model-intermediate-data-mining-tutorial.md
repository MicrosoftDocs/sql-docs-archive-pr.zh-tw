---
title: 流覽撥打電話中心模型 (元資料採礦教學課程) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9095212c-9068-4dd8-85ce-17a467adeabb
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2aceec298ba78e29988571293f8422ab9e55aa97
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87703557"
---
# <a name="exploring-the-call-center-model-intermediate-data-mining-tutorial"></a>探索撥接中心模型 (中繼資料採礦教學課程)
  現在您已經建立了探勘模型，您可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 所提供的下列工具深入了解您的資料。  
  
-   [Microsoft 類神經網路查看](#bkmk_NNviewer)器 **：** 您可以在資料採礦設計師的 [**採礦模型檢視器**] 索引標籤中使用此檢視器，其設計目的是要協助您試驗資料中的互動。  
  
-   [Microsoft 一般內容樹狀檢視器](#bkmk_genviewer) **：** 這個標準檢視器可提供在產生模型時，演算法發現的模式和統計資料的深入詳細資料。  
  
##  <a name="microsoft-neural-network-viewer"></a><a name="bkmk_NNviewer"></a>Microsoft 類神經網路檢視器  
 檢視器有三個窗格-**輸入**、**輸出**和**變數**。  
  
 藉由使用 [**輸出**] 窗格，您可以為可預測的屬性或相依變數選取不同的值。 如果您的模型包含多個可預測的屬性，您可以從 [**輸出屬性**] 清單中選取屬性。  
  
 [**變數**] 窗格會比較您在參與屬性或變數方面所選擇的兩個結果。 彩色列以視覺方式表示變數影響目標結果的強度。 您也可以檢視變數的增益分數。 增益分數會根據您所使用的採礦模型類型而有不同的計算方式，但在使用此屬性進行預測時，通常會告訴您模型的增進部分。  
  
 [**輸入**] 窗格可讓您將影響因素加入至模型，以嘗試各種假設情況。  
  
### <a name="using-the-output-pane"></a>使用輸出窗格  
 在此初始模型中，您可能有興趣想要查看各種因數如何影響服務等級。 若要這樣做，您可以從輸出屬性清單中選取 [服務等級]，然後從 [**值 1** ] 和 [**值 2**] 的下拉式清單中選取範圍，藉以比較不同層級的服務。  
  
##### <a name="to-compare-lowest-and-highest-service-grades"></a>若要比較最低和最高的服務等級  
  
1.  針對 [**值 1**]，選取具有最低值的範圍。 例如，範圍 0-0-0.7 表示最低的放棄率，因此是最佳的服務等級。  
  
    > [!NOTE]  
    >  在此範圍中的實際值可能會隨著您設定模型的方式而有所不同。  
  
2.  在 [**值 2**] 中，選取最高值的範圍。 例如，值為 >= 0.12 的範圍代表最高的放棄率，因此是最差的服務等級。 換句話說，在此排班期間打電話的客戶之中，有 12% 的客戶在與服務人員通話前，就會掛斷電話。  
  
     [**變數**] 窗格的內容會更新，以比較構成結果值的屬性。 因此，左側資料行會顯示與最佳服務等級相關聯的屬性，而右側資料行則顯示與最差服務等級相關聯的屬性。  
  
### <a name="using-the-variables-pane"></a>使用變數窗格  
 在此模型中，它會顯示 `Average Time Per Issue` 為重要因素。 此變數表示回應通話所需的平均時間，無論通話類型為何。  
  
##### <a name="to-view-and-copy-probability-and-lift-scores-for-an-attribute"></a>若要檢視與複製屬性的機率和增益分數  
  
1.  在 [**變數**] 窗格中，將滑鼠游標暫留在第一個資料列的彩色橫條上。  
  
     這個彩色的橫條會顯示您 `Average Time Per Issue` 對服務等級的貢獻程度。 工具提示會針對變數和目標結果的每個組合，顯示整體分數、機率，以及增益分數。  
  
2.  在 [**變數**] 窗格中，以滑鼠右鍵按一下任何彩色橫條，然後選取 [**複製**]。  
  
3.  在 Excel 工作表中，以滑鼠右鍵按一下任何資料格，然後選取 [**貼**上]。  
  
     此報表就會貼上為 HTML 表格，並僅顯示每列的分數。  
  
4.  在不同的 Excel 工作表中，以滑鼠右鍵按一下任何資料格，然後選取 [**貼上特殊**]。  
  
     此報表會以文字格式貼上，並包含下節所描述的相關統計資料。  
  
### <a name="using-the-input-pane"></a>使用輸入窗格  
 假設您有興趣查看特定因數的效果，例如排班或操作員數目。 您可以使用 [**輸入**] 窗格來選取特定變數，[**變數**] 窗格會自動更新，以比較先前選取的兩個群組（指定的變數）。  
  
##### <a name="to-review-the-effect-on-service-grade-by-changing-input-attributes"></a>若要變更輸入屬性來檢閱對於服務等級的效果  
  
1.  在 [**輸入**] 窗格中，針對 [**屬性**] 選取 [移位]。  
  
2.  針對 [**值**]，選取 [ **AM**]。  
  
     [**變數**] 窗格會更新，以顯示當位移為**AM**時，對模型的影響。 所有其他選項都維持不變，您仍在比較最低和最高的服務等級。  
  
3.  針對 [**值**]，選取 [ **PM1**]。  
  
     [**變數**] 窗格會更新，以顯示當移位變更時，對模型的影響。  
  
4.  在 [**輸入**] 窗格中，按一下 [**屬性**] 底下的下一個空白資料列，然後選取 [呼叫]。 針對 [**值**]，選取表示最大呼叫次數的範圍。  
  
     新的輸入條件就會加入至清單中。 [**變數**] 窗格會更新，以顯示呼叫量最高時，對特定排班之模型的影響。  
  
5.  繼續變更 [排班] 和 [通話] 的值，以尋找排班、通話量，以及服務等級之間任何有趣的相互關聯。  
  
    > [!NOTE]  
    >  若要清除 [**輸入**] 窗格，讓您可以使用不同的屬性，請按一下 [重新整理**檢視器內容]**。  
  
### <a name="interpreting-the-statistics-provided-in-the-viewer"></a>解譯檢視器中所提供的統計資料  
 較長的等待時間是一項代表高放棄率的準確預測指標，同時也意味著較差的服務等級。 這似乎是一個明顯的結論，不過，採礦模型會提供您一些額外的統計資料以協助您解譯這些趨勢。  
  
-   **分數**：指出此變數在結果之間群集辨識之整體重要性的值。 分數越高，表示變數對於結果的效果越強。  
  
-   **值1的**機率：百分比，表示此結果的這個值的機率。  
  
-   **值2的**機率：百分比，表示此結果的這個值的機率。  
  
-   **值 1**的增益和**值2的**增益：表示使用這個特定變數來預測值1和值2結果之影響的分數。 分數越高，表示變數越能預測結果。  
  
 下表包含最重要之影響因數的一些範例值。 例如，**值 1**的機率為60.6%，而**值 2**的機率為8.30%，表示當每個問題的平均時間介於44-70 分鐘的範圍內時，60.6% 的案例就會在最高服務等級的轉移中 (值 1) ，而8.30% 的案例則是在較差的服務等級 (值 2) 的轉移中。  
  
 從這個資訊中，您可以得到一些結論。 較短的通話回應時間 (範圍是 44-70) 對於較佳的服務等級 (範圍是 0.00-0.07) 有強大的影響。 此分數 (92.35) 表示這個變數非常重要。  
  
 不過，當您向下查看影響的因數清單時，可以看到一些其他的因數，以及比較不容易理解也比較難解譯的效果。 例如，排班似乎會影響服務，但是增益分數和相對機率卻指出排班不是主要的因數。  
  
|屬性|值|優先 \< 0.07|優先 >= 0.12|  
|---------------|-----------|--------------------|----------------------|  
|每個問題的平均時間|89.087-120.000||分數：100<br /><br /> Value1 的機率：4.45%<br /><br /> Value2 的機率：51.94%<br /><br /> Value1 的增益：0.19<br /><br /> Value2 的增益：1.94|  
|每個問題的平均時間|44.000-70.597|分數：92.35<br /><br /> 值 1 的機率：60.06 %<br /><br /> 值 2 的機率：8.30 %<br /><br /> 值 1 的增益：2.61<br /><br /> 值 2 的增益：0.31||  
  
 [回到頁首](#bkmk_NNviewer)  
  
##  <a name="microsoft-generic-content-tree-viewer"></a><a name="bkmk_genviewer"></a>Microsoft 一般內容樹狀檢視器  
 此檢視器可用於在處理模型時，檢視由演算法所建立的更詳細資訊。 **MicrosoftGeneric 內容樹狀檢視器**會以一系列節點來表示「採礦模型」，其中每個節點都代表學習到有關定型資料的知識。 此檢視器可以搭配所有模型使用，但是節點的內容會隨著模型類型而有所不同。  
  
 在類神經網路模型或羅吉斯迴歸模型中，您可能會發現 `marginal statistics node` 特別實用。 此節點包含關於資料中值分佈的衍生統計資料。 如果您想要得到資料的摘要，但是不想撰寫許多 T-SQL 查詢，此資訊就非常有幫助。 在前一個主題中分類收納值的圖表便是衍生自臨界統計資料節點。  
  
#### <a name="to-obtain-a-summary-of-data-values-from-the-mining-model"></a>若要從採礦模型取得資料值的摘要  
  
1.  在 [資料採礦設計師] 的 [**採礦模型檢視器**] 索引標籤中，選取 \<mining model name> 。  
  
2.  從 [**檢視器]** 清單中，選取 [ **Microsoft 一般內容樹狀檢視器]**。  
  
     採礦模型的檢視會重新整理，在左窗格中顯示節點階層，並在右窗格中顯示 HTML 表格。  
  
3.  在 [**節點標題**] 窗格中，按一下名稱為10000000000000000的節點。  
  
     模型中任何最頂部的節點永遠是模型根節點。 在類神經網路或羅吉斯迴歸模型中，位於該節點正下方的節點是臨界統計資料節點。  
  
4.  在 [**節點詳細資料**] 窗格中，向下 NODE_DISTRIBUTION，直到您找到資料列為止。  
  
5.  向下捲動到 NODE_DISTRIBUTION 資料表以檢視如類神經網路演算法所計算的值分佈。  
  
 若要在報表中使用這個資料，您可以選取然後複製特定資料列的資訊，或者也可以使用下列資料採礦延伸模組 (DMX) 查詢來擷取節點的完整內容。  
  
```  
SELECT *   
FROM [Call Center EQ4].CONTENT  
WHERE NODE_NAME = '10000000000000000'  
```  
  
 您也可以使用 NODE_DISTRIBUTION 資料表中的節點階層與詳細資料來周遊類神經網路中的個別路徑，並檢視隱藏層的統計資料。 如需詳細資訊，請參閱類[神經網路模型查詢範例](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md)。  
  
 [回到頁首](#bkmk_NNviewer)  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [&#40;元資料採礦教學課程中，將羅吉斯回歸模型加入至撥中心結構&#41;](../../2014/tutorials/add-logistic-regression-model-to-call-center-intermediate-data-mining.md)  
  
## <a name="see-also"></a>另請參閱  
 [類神經網路模型的採礦模型內容 &#40;Analysis Services 資料採礦&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [類神經網路模型查詢範例](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md)   
 [Microsoft 類神經網路演算法技術參考](../../2014/analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)   
 [變更採礦模型中的資料行離散化](../../2014/analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md)  
  
  
