---
title: 記載 (適用于 Excel 的資料採礦增益集) 的採礦模型 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- documenting models
- mining structures, managing
- mining models, managing
- model properties
ms.assetid: 0a663e11-e40c-4708-ad18-fabb6c976fa4
author: minewiskan
ms.author: owend
ms.openlocfilehash: 00d84f7ff1dc27d19d497dd11315d3efde603f60
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599252"
---
# <a name="documenting-mining-models-data-mining-add-ins-for-excel"></a>記錄採礦模型 (適用於 Excel 的資料採礦增益集)
  ![資料採礦功能區中的文件模型按鈕](media/dmc-docmodel.gif "資料採礦功能區中的文件模型按鈕")  
  
 [**檔模型**] wizard 會建立一份報表，提供有關您已建立之採礦模型的實用資訊。 您可以藉由記錄所建立的模型來追蹤產生模型所使用之資料的來源、取得處理模型時間的其他相關資訊，以及追蹤影響模型結果的參數變更。  
  
## <a name="using-the-document-model-wizard"></a>使用文件模型精靈  
  
1.  按一下 [**資料採礦**] 索引標籤。  
  
2.  在 [**模型使用**方式] 群組中，按一下 [**檔模型**]。  
  
3.  在 [**選取模型**] 對話方塊中，選取要報告的模型，然後按 **[下一步]**。 您必須針對想要記載的每個模型，分別執行 [**檔模型**]。  
  
4.  在 [**選取檔詳細資料**] 對話方塊中，選擇下列兩個選項的其中一個： [**完整資訊**] 或 [**摘要資訊**]。  
  
5.  按一下 [完成] 。  
  
6.  Wizard 會自動建立新的工作表，其中包含指定的報表，標題為**Model 檔**，  
  
## <a name="understanding-the-report"></a>了解報表  
 當您建立記錄資料採礦模型的報表時，您可以建立摘要報表 (其中含有包含模型之名稱和描述的基本資訊)，或完整報表 (其中包含基礎結構的相關詳細資料，以及採礦模型的相關進階資訊)。  
  
 系統會根據建立模型所使用的演算法，提供不同類型的資訊。 例如，在關聯模型中，您會對於所產生之項目與規則的數目比較感興趣。 但如果是群集模型，叢集的數目則比較有趣。  
  
 下表列出一些選項以及報表中每個選項所提供的資訊。  
  
> [!NOTE]  
>  根據預設，報表中的資料行會設定為特定的大小。 因此，如果資料行名稱或值非常冗長，則可能會看不到，或在 Excel 中顯示為 ###。 若要顯示這些值，您可以調整資料列的大小。 如果有選取資料格，您可以在公式列的右邊按一下並拖曳雙箭頭，就可以顯示完整的值或字串。  
  
### <a name="summary-report"></a>摘要報表  
  
||||  
|-|-|-|  
|**中繼資料**|模型名稱<br /><br /> 模型描述<br /><br /> 演算法名稱<br /><br /> 上次處理的日期||  
|**模型結果**|關聯|項目集的計數<br /><br /> 規則的計數|  
||叢集|叢集的計數<br /><br /> 每個叢集的支援|  
||決策樹|樹狀結構數目<br /><br /> 每個樹狀結構中的節點數目|  
||線性迴歸|樹狀結構數目 (永遠為 1)<br /><br /> 節點數目 (永遠為 1)|  
||貝氏機率分類|重要屬性|  
||類神經網路|輸入節點的數目<br /><br /> 輸出節點的數目<br /><br /> 隱藏節點的數目|  
||時序群集|叢集數目|  
  
### <a name="complete-report"></a>完整報表  
 完整報表包含摘要報表中的所有資訊，加上模型中使用之資料的資料行詳細資訊以及分析結果：  
  
||||  
|-|-|-|  
|**中繼資料**|模型中繼資料|演算法參數與值|  
||資料行中繼資料|資料行名稱<br /><br /> 使用量<br /><br /> 資料類型<br /><br /> 內容類型<br /><br /> 值 (離散值的清單或值的範圍)|  
|**模型統計資料**|連續資料行|平均值<br /><br /> 最小值<br /><br /> 最大值<br /><br /> 均方根誤差<br /><br /> 平均絕對誤差<br /><br /> 對數分數<br /><br /> 迴歸公式 (僅適用於線性迴歸模型)|  
||離散資料行|通過的計數<br /><br /> 失敗的計數<br /><br /> 對數分數<br /><br /> 增益|  
  
> [!NOTE]  
>  您可以記錄 SQL Server Analysis Services 支援的任何模型類型。 因此，此資料表會列出使用「資料表分析工具」或使用「資料採礦用戶端」之精靈無法建立的一些模型類型。 不過，您可以使用 [ **Advanced Data 挖掘查詢編輯器**] 來建立所有模型類型。 如需詳細資訊，請參閱[SQL Server 資料採礦增益集&#41;的查詢 &#40;](query-sql-server-data-mining-add-ins.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;適用于 Excel 的資料採礦增益集部署和調整採礦模型&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
