---
title: 探索和清除資料 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7c888c95-8986-461e-9f11-2395044b9d97
author: minewiskan
ms.author: owend
ms.openlocfilehash: 154c711f735bcbb472e49654139fd16a036a0dd5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584809"
---
# <a name="exploring-and-cleaning-data"></a>瀏覽和清除資料
  資料準備不只是進行資料清理而已。 務必記得，準備資料的方式也會影響最後解譯結果的方式。 資料準備包含下列工作：  
  
-   瀏覽及檢查資料分佈情形。  
  
-   清除不正確的記錄，以及選擇要進行資料採礦的資料行。  
  
-   適當處理 Null。  
  
-   分類收納值，或依不同的時段彙總值。  
  
-   加入標籤來改善結果的可用性。  
  
-   視需要轉換資料類型或將值分類以進行分析。  
  
 如果您是資料模型化的新手，我們建議您閱讀相關主題：[資料採礦準備的檢查清單](checklist-of-preparation-for-data-mining.md)。  
  
## <a name="data-preparation-tools"></a>資料準備工具  
 適用於 Office 的資料採礦增益集包括了可用於資料清理和準備的以下工具：  
  
### <a name="explore-data"></a>瀏覽資料  
 使用 [**流覽資料**] 嚮導來進行這些資料準備工作：  
  
-   預覽資料並識別出必須在分析之前修正的錯誤。  
  
-   收集統計資訊，有助於了解資料的平衡與必要的清除工作。  
  
-   識別對分析有用的資料行，並規劃資料模型化階段。  
  
 [流覽資料 &#40;SQL Server 資料採礦增益集&#41;](explore-data-sql-server-data-mining-add-ins.md)。  
  
### <a name="detect-and-handle-outliers"></a>偵測及處理極端值  
 [極端**值] 嚮導會將資料**中的值分佈繪製成圖形，並協助您移除極端值。 使用 [極端值 **] 工具進行**下列資料準備工作：  
  
-   根據在資料中找到的模式來判斷個別值是否可靠。  
  
-   檢閱不尋常的值並採取行動來刪除或取代它們。  
  
-   將模型限定在某指定範圍的值。 例如，如果您知道某特定商店有極端值，您可以刪除該值並取得更能準確預測其他商店的模型。  
  
 [SQL Server 資料採礦增益集&#41;](outliers-sql-server-data-mining-add-ins.md)的極端值 &#40;。  
  
### <a name="relabel-and-bin-data"></a>重定標籤和分類收納資料  
 重新**標記**的 wizard 會依值將資料分組，讓您可以變更資料上的標籤。 使用重定標籤工具來進行以下這些資料準備工作：  
  
-   將調查結果中使用的數字代碼變更為此數字代碼所代表的文字描述。  
  
     例如，您可以取代資料項目 (例如以 Gender = Female 取代 Gender = 1)。  
  
-   您可以建立代表數量範圍的群組，來分類收納資料。  
  
     例如，您可能會想要將數位的收入資料行取代為標籤，例如**收入-中度**和**收入-高**。  
  
-   將離散值摺疊成類別目錄。  
  
     例如，如果您有太多個別產品偵測到購買模式，您可以嘗試將這些產品指派到更廣泛的類別目錄。  
  
 [重新標記 &#40;SQL Server 資料採礦增益集&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
### <a name="cleanse-data"></a>清理資料  
 資料清理包含各種活動，大部分活動由增益集支援。  
  
-   識別 Null 值，並判斷是否應該將這些值變更為實數值，或視為 `Missing` 值來處理。  
  
-   偵測遺漏的值，然後移除它們或推算一個適當的值，例如平均值、Null 或其他值。  
  
 [流覽資料 &#40;SQL Server 資料採礦增益集&#41;](explore-data-sql-server-data-mining-add-ins.md)  
  
 [重新標記 &#40;SQL Server 資料採礦增益集&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
 [根據範例填滿](fill-from-example-table-analysis-tools-for-excel.md)  
  
### <a name="sample-data"></a>取樣資料  
 取樣資料精靈提供兩種方法，可用來建立定型模型和測試模型的對稱資料集。  
  
-   **隨機取樣。** 使用這個選項即可從較大資料集擷取代表性資料集，以用於定型或測試。 資料採礦增益集會使用*分層取樣*，以確保為每個取樣的變數取得一組平衡的值。  
  
-   **超取樣.** 當您的資料比目標結果所需的資料少，而必須提高資料的加權時，請使用這個選項。 例如，詐欺可能相當罕見，不過您可以超取樣與詐欺相關的案例，為模型取得足夠的資料。  
  
 [SQL Server 資料採礦增益集&#41;的範例資料 &#40;](sample-data-sql-server-data-mining-add-ins.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立資料採礦模型](creating-a-data-mining-model.md)   
 [驗證模型及使用模型進行預測 &#40;適用于 Excel 的資料採礦增益集&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [&#40;適用于 Excel 的資料採礦增益集部署和調整採礦模型&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
