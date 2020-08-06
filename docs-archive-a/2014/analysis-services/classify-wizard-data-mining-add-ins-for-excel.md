---
title: 適用于 Excel) 的資料採礦增益集 (分類嚮導 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data modeling [data mining]
- classification [data mining]
ms.assetid: 409c5076-c4c3-4f09-8f30-d3297df45f13
author: minewiskan
ms.author: owend
ms.openlocfilehash: b82fc98df10ae2e6754a378dacea108f9f3379ca
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593072"
---
# <a name="classify-wizard-data-mining-add-ins-for-excel"></a>分類精靈 (適用於 Excel 的資料採礦增益集)
  ![資料採礦功能區中的分類精靈](media/dmc-classify.gif "資料採礦功能區中的分類精靈")  
  
 [**分類**] wizard 可協助您根據 excel 資料表、excel 範圍或外部資料源中的現有資料，建立分類模型。  
  
 分類模型會擷取可指示資料相似性的模式，並協助您根據值的分組來做出預測。 例如，分類模型可能會用來根據收入或花費模式預測風險。  
  
## <a name="using-the-classify-wizard"></a>使用分類精靈  
  
1.  在 [**資料採礦**] 功能區中，按一下 [**分類**]，然後按 **[下一步]**。  
  
2.  在 [**選取來源資料**] 頁面中，選擇要分析的資料。  
  
     此精靈支援多種資料類型：Excel 資料表、Excel 範圍和外部資料來源。 使用外部資料時，您可以將資料加入 Excel，或者在 Analysis Services 資料來源中選擇一組資料表或檢視。 您也可以新增資料表並變更資料行，以建立隨選資料來源。  
  
3.  在 [**分類**] 頁面上，選擇您想要分類的資料行。  
  
     請檢查清單中的資料行、**輸入資料行**，然後取消選取任何具有唯一值的資料行，因此不適合用來建立模式，例如 ID 號碼、客戶名稱等等。 您也應該將基本上與可分類資料行重複的資料行移除。  
  
     例如，如果您想分類產品類別的預測，應該排除含有已知商務規則的子類別欄位，否則該規則的強度可能會防止您探索其他相互關聯。  
  
4.  （選擇性）按一下 [**參數**] 以變更演算法參數，並自訂群集模型的行為。  
  
5.  在 [將**資料分割成定型集和測試集**] 頁面上，指定要保留多少資料來進行測試。 定型模型時，一律會使用其餘資料。  
  
     預設設定為 30% 測試資料和 70% 定型資料。  
  
6.  在 [**完成]** 頁面上，為您的資料集和模型提供描述性的名稱，並設定下列選項來控制如何使用完成的模型：  
  
    -   **流覽模型**。 選取這個選項時，一旦 wizard 完成模型的處理，就會開啟 **[流覽**] 視窗以協助您流覽結果。 檢視器的內容取決於建立的模型類型。 如需詳細資訊，請參閱[流覽決策樹模型](browsing-a-decision-trees-model.md)和[流覽類神經網路模型](browsing-a-neural-network-model.md)。  
  
    -   **啟用 [鑽取**]。 選取此選項可檢視完成模型中的基礎資料。 只有建立決策樹模型時，才能使用這個選項。  
  
    -   **使用暫時性模型**。 如果選取這個選項，此模型將無法儲存到伺服器。 當您關閉 Excel 時，即會刪除暫時性模型。  
  
## <a name="more-about-classification-models"></a>深入了解分類模型  
 在 [**演算法參數**] 對話方塊中，您也可以從 Analysis Services 所提供的演算法中選擇分類方法：  
  
-   Microsoft 決策樹  
  
-   Microsoft 羅吉斯迴歸  
  
-   Microsoft 貝氏機率分類  
  
-   Microsoft 類神經網路  
  
 雖然演算法可能產生類似的結果，但是其分析資料的方式並不同，因此建議嘗試數種演算法並比較結果。 預設方法是 Microsoft 決策樹。  
  
 在 [**參數**] 清單中，您可以變更 [advanced options]，這取決於您選擇的演算法類型。 每個演算法的參數在《SQL Server 線上叢書》中有更詳細的說明。  
  
 [Microsoft 決策樹演算法技術參考](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Microsoft 羅吉斯迴歸演算法技術參考](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Microsoft 貝氏機率分類演算法技術參考](data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)  
  
 [Microsoft 類神經網路演算法技術參考資料](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>需求  
 若要使用 [**分類**] wizard，您必須連接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫。 如需有關如何建立連線的詳細資訊，請參閱[連接到來源資料 &#40;適用于 Excel&#41;的資料採礦用戶端](connect-to-source-data-data-mining-client-for-excel.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立資料採礦模型](creating-a-data-mining-model.md)  
  
  
