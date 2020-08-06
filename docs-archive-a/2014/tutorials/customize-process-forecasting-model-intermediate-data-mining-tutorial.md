---
title: 自訂及處理預測模型 (中繼資料採礦教學課程) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4bd25e15-9d9e-4528-b7bc-ccb856643aec
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 03dc67907b22750eb1b8539feaddec58f61f702f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598087"
---
# <a name="customizing-and-processing-the-forecasting-model-intermediate-data-mining-tutorial"></a>自訂及處理預測模型 (中繼資料採礦教學課程)
  [!INCLUDE[msCoName](../includes/msconame-md.md)] 時間序列演算法提供會影響模型建立方式以及時間資料分析方式的參數。 變更這些屬性會對採礦模型如何進行預測造成重大的影響。  
  
 在本教學課程的這項工作中，您將執行下列工作以修改模型：  
  
1.  您將會藉由加入*PERIODICITY_HINT*參數的新值，自訂您的模型處理時間週期的方式。  
  
2.  您將學習 Microsoft 時間序列演算法的兩個其他重要參數：FORECAST_METHOD 和 PREDICTION_SMOOTHING。前者讓您控制用於預測的方法，後者則讓您自訂長期和短期預測的混合。  
  
3.  您可以選擇告知演算法要如何計算遺漏值。  
  
4.  進行完所有變更之後，您將部署及處理模型。  
  
## <a name="setting-time-series-parameters"></a>設定時間序列參數  
 **週期性提示**  
  
 *PERIODICITY_HINT*參數會提供演算法，其中包含您預期會在資料中看到的額外時間週期相關資訊。 根據預設，時間序列模型會嘗試自動在資料中偵測模式。 不過，如果您已經知道預期的時間循環，提供週期性提示可能會改進模型的精確度。 提供錯誤的週期性提示則可能會降低精確度；因此，如果您不確定應該使用哪個值，最好使用預設值。  
  
 例如，此模型所用的檢視每月會從 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 彙總銷售資料。 因此，模型所用的每個時間配量表示一個月，所有預測也是以月為單位。 由於一年有12個月，而您預期銷售模式會每年重複一次，因此您會將*PERIODICITY_HINT*參數設定為 `12` ，以指出12個時間配量 (月份) 組成一個完整的銷售週期。  
  
 **預測方法**  
  
 *FORECAST_METHOD*參數可控制是否針對短期或長期預測優化時間序列演算法。 根據預設， *FORECAST_METHOD*參數會設定為 MIXED，這表示兩個不同的演算法會混合和平衡，以提供短期與長期預測的良好結果。  
  
 但是，如果您知道要使用特定的演算法，可以將值變更為 ARIMA 或 ARTXP。  
  
 **加權長期與短期預測的比較**  
  
 您也可以使用 PREDICTION_SMOOTHING 參數來自訂長期和短期預測的混合方式。 依預設，此參數設為 0.5，一般而言可以提供整體精確度的最佳平衡。  
  
#### <a name="to-change-the-algorithm-parameters"></a>若要變更演算法參數  
  
1.  在 [**採礦模型**] 索引標籤上，以滑鼠右鍵按一下 [**預測**]，然後選取 [**設定演算法參數]**。  
  
2.  在 `PERIODICITY_HINT` [**演算法參數**] 對話方塊的資料列中，按一下 [**值**] 資料行，然後輸入 `{12}` ，包括大括弧。  
  
     根據預設，演算法也會加入 {1} 值。  
  
3.  在資料 `FORECAST_METHOD` 列中，確認 [**值**] 文字方塊為空白或設為 `MIXED` 。 如果輸入了不同的值，請輸入，將 `MIXED` 參數變更回預設值。  
  
4.  在 [ **PREDICTION_SMOOTHING** ] 資料列中，確認 [**值**] 文字方塊為空白或設為0.5。 如果輸入了不同的值，請按一下 [**值**] 並輸入，將 `0.5` 參數變更回預設值。  
  
    > [!NOTE]  
    >  PREDICTION_SMOOTHING 參數只適用於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise。 因此，您無法在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard 之中檢視或變更 PREDICTION_SMOOTHING 參數的值。 不過，預設行為是使用兩種演算法並且平均分配其權重。  
  
5.  按一下 [確定]  。  
  
## <a name="handling-missing-data-optional"></a>處理遺漏資料 (選擇性)  
 在許多情況下，您的銷售資料可能有填滿 Null 的間距，或可能有某分店錯過了報告期限，導致序列結尾處出現空白資料格。 在這種情況下，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會發出下列錯誤，而且不處理模型。  
  
 「 (資料採礦) 時發生錯誤：從「採礦模型」的「數列」開始，時間戳記不會同步處理 \<series name> \<model name> 。 所有時間序列都必須在同一個時間標示結束，且不能有任意遺漏資料點。 將 MISSING_VALUE_SUBSTITUTION 參數設定為 Previous 或數值常數，即可在適用時自動修補遺漏的資料點。」  
  
 若要避免這個錯誤，您可以指定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 使用下列任何一個方法，自動提供新值以填滿間距：  
  
-   使用平均值。 平均值是使用相同資料序列中的全部有效值來計算。  
  
-   使用上一個值。 您可以將多個遺漏的資料格取代為上一個值，但是不可以填入起始值。  
  
-   使用您套用的常數值。  
  
#### <a name="to-specify-that-gaps-be-filled-by-averaging-values"></a>若要指定以平均值填滿間距  
  
1.  在 [**採礦模型**] 索引標籤上，以滑鼠右鍵按一下 [**預測**] 資料行，然後選取 [**設定演算法參數]**。  
  
2.  在 [**演算法參數**] 對話方塊的 [ **MISSING_VALUE_SUBSTITUTION** ] 資料列中，按一下 [**值**] 資料行，然後輸入 `Mean` 。  
  
## <a name="build-the-model"></a>建立模型  
 若要使用模型，您必須將它部署至伺服器，然後透過演算法執行定型資料來處理模型。  
  
#### <a name="to-process-the-forecasting-model"></a>若要處理預測模型  
  
1.  在的 [**採礦模型**] 功能表上 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] ，選取 [**處理採礦結構] 和 [所有模型**]。  
  
2.  在詢問您是否要建立及部署專案的警告中，按一下 [**是]**。  
  
3.  在 [**處理採礦結構-預測**] 對話方塊中，按一下 [**執行**]。  
  
     [**處理進度**] 對話方塊隨即開啟，以顯示模型處理的相關資訊。 處理模型可能需要花一些時間。  
  
4.  處理完成之後，按一下 [**關閉**] 以結束 [**處理進度**] 對話方塊。  
  
5.  再按一次 [關閉]，**結束**[**處理採礦結構-預測**] 對話方塊。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [&#40;中繼資料採礦教學課程中探索預測模型&#41;](../../2014/tutorials/exploring-the-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 時間序列演算法技術參考](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Microsoft 時間序列演算法](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [處理需求和考量 (資料採礦)](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
