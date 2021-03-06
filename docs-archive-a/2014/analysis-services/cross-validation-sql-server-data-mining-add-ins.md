---
title: SQL Server 資料採礦增益集的交叉驗證 () |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cross-validation
- partitioning data [data mining]
- mining models, testing
ms.assetid: bf9483b3-4099-41c4-bbc5-da7005e07bcd
author: minewiskan
ms.author: owend
ms.openlocfilehash: a615de9d20106041f2f01e9912928b64597bc895
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594862"
---
# <a name="cross-validation-sql-server-data-mining-add-ins"></a>交叉驗證 (SQL Server 資料採礦增益集)
  ![資料採礦功能區中的交叉驗證按鈕](media/dmc-xvalid.gif "資料採礦功能區中的交叉驗證按鈕")  
  
 交叉驗證是一項標準分析工具，而且它是協助您開發並微調資料採礦模型的重要功能。 在您建立了採礦模型之後，就可以使用交叉驗證來確定模型的有效性，並在建立相關的採礦模型之後，比較彼此的結果。  
  
 交叉驗證包含兩個階段：定型和產生報表。 您將完成下列步驟：  
  
-   選取目標採礦結果或採礦模型。  
  
-   指定目標值 (如果適用)。  
  
-   指定分割結構資料的交叉*區段或折*迭數目。  
  
 **交叉驗證**的 wizard 接著會在每個折迭上建立新的模型，在另一個折迭上測試模型，然後報告模型的精確度。 完成時，**交叉驗證**嚮導會建立一個報表，其中會顯示每個折迭的計量，並提供匯總中模型的摘要。 這項資訊可用於判斷基礎資料對於模型的良好程度，或者用於比較根據相同資料建立的不同模型。  
  
## <a name="using-the-cross-validation-wizard"></a>使用交叉驗證精靈  
 您可以針對暫存模型與存放在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 之執行個體上的模型使用交叉驗證。  
  
#### <a name="to-create-a-cross-validation-report"></a>建立交叉驗證報表  
  
1.  在 [**資料採礦**] 功能區的 [**精確度和驗證**] 群組中，按一下 [**交叉驗證**]。  
  
2.  在 [**選取結構或模型**] 對話方塊中，選取現有的 [採礦結構] 或 [採礦模型]。 如果選取結構，此精靈將會針對以具有相同可預測屬性之結構為基礎的所有模型，使用交叉驗證。 如果選擇模型，此精靈將只會針對該模型使用交叉驗證。  
  
3.  在 [**指定交叉驗證參數**] 對話方塊的 [折迭**計數**] 方塊中，選擇要用來分割資料集的折迭數目。 折疊是隨機選取的交叉資料。  
  
4.  （選擇性）在 [**最大資料列**數] 文字方塊中輸入數位，以設定要在交叉驗證中使用的最大資料列數目。  
  
    > [!NOTE]  
    >  您使用的資料列越多，結果將會越精確。 不過，處理時間可能也會明顯增加。 所選擇的數目取決於資料，但一般而言，您應該在不犧牲效能的情況下，盡可能選擇最多的數目。 若要提升效能，您也可以指定較少的折疊。  
  
5.  從 [**目標屬性**] 下拉式清單中選取資料行。 此清單只會顯示一開始建立模型時，設定為可預測屬性的資料行。 模型可以包含多個可預測屬性，但是您可以只選擇其中一個。  
  
6.  從 [**目標狀態**] 下拉式清單中選取一個值。  
  
     如果可預測的資料行包含連續數值資料，就無法使用此選項。  
  
7.  （選擇性）指定要在將預測計算為正確時作為**目標閾值**的值。 這個值會以機率的方式表示，也就是介於 0 和 1 之間的數字，其中 1 表示預測保證是正確的，0 則表示預測不可能正確，而 .5 則視為隨機猜測。  
  
     如果可預測的資料行包含連續數值資料，就無法使用此選項。  
  
8.  按一下 [完成] 。 隨即建立新的工作表，名為**交叉驗證**。  
  
    > [!NOTE]  
    >  當系統正在將模型分割為折疊，而且每個折疊都在進行測試時，Microsoft Excel 可能會暫時變成沒有回應。  
  
### <a name="requirements"></a>需求  
 若要建立交叉驗證報表，您必須已經建立了資料採礦結構和相關的模型。 精靈會提供一個對話方塊來協助您選擇現有的結構和模型。  
  
 如果您選擇支援多個採礦模型的採礦結構，而且模型使用不同的可預測屬性，交叉驗證精靈將會只測試共用相同可預測屬性的模型。  
  
 如果您選擇同時支援群集模型和其他種類模型的結構，將不會測試群集模型。  
  
## <a name="understanding-cross-validation-results"></a>了解交叉驗證結果  
 交叉驗證的結果會顯示在新的工作表中，標題**為的 \<attribute name> 交叉驗證報表**。 新的工作表包含數個區段：第一個區段是摘要，提供關於經過測試之模型的重要中繼資料，讓您知道這是哪個模型或結構的結果。  
  
 報表中的第二個區段提供統計摘要，表示原始模型的良好程度。 在此摘要中，針對每個折迭所建立的模型之間的差異會針對三個主要量值進行分析：*根平均平方誤差*、*平均絕對錯誤*和*記錄分數*。 這些是標準的統計量值，不但可用於資料採礦，而且也可以用於大部分類型的統計分析。  
  
 整體來說，交叉驗證精靈會針對這些每個量值，透過模型計算平均和標準差。 這會告訴您在不同的資料子集上進行預測時，模型一致性的程度。 例如，如果標準差非常大，表示針對每個折疊所建立的模型有非常不同的結果，因此，模型在特定資料群組上的定型可能太接近，而且不適用於其他資料集。  
  
 下節說明評估模型所使用的量值。  
  
### <a name="tests-and-measures"></a>測試和量值  
 除了一些有關資料中的折疊數以及每個折疊中的資料量等基本資訊外，工作表也會顯示有關每個模型的標準集並以測試類型分類。 例如，群集模型的精確度是透過不同於您用於預測模型的測試進行評估。  
  
 下表列出測試和標準，並提供標準所代表意義的說明。  
  
#### <a name="aggregates-and-general-statistical-measures"></a>彙總和一般統計量值  
 報表中提供的彙總量值表示您在資料中建立之折疊之間的差異。  
  
-   平均和標準差  
  
-   在模型的所有資料分割中，與特定量值平均數的差異平均值。  
  
#### <a name="classification-passfail"></a>分類：通過/失敗  
 當您沒有指定可預測屬性的目標值時，會在分類模型中使用這個量值。 例如，如果您建立可預測多個可能性的模型，這個量值會告訴您該模型在預測所有可能值的妥善程度。  
  
 通過/失敗是由符合下列條件的案例計數計算：如果具有最高機率的預測狀態與輸入狀態相同，且機率大於您為 [**狀態閾值**] 指定的值，則會進行**傳遞**。否則**會失敗**。  
  
#### <a name="classification-true-or-false-positives-and-negatives"></a>分類：真肯定和真否定或誤判和誤否定  
 此測試用於具有指定之目標的所有分類模型。 量值表示每個案例對於下列問題的回應如何進行分類：模型在預測什麼，以及實際的結果是什麼。  
  
|Measure|描述|  
|-------------|-----------------|  
|真肯定|符合這些條件的案例計數：<br /><br /> 案例包含目標值。<br /><br /> 模型預測出案例包含目標值。|  
|誤判|符合這些條件的案例計數：<br /><br /> 實際的值等於目標值。<br /><br /> 模型預測出案例包含目標值。|  
|真否定|符合這些條件的案例計數：<br /><br /> 案例不包含目標值。<br /><br /> 模型預測出案例不包含目標值。|  
|誤否定|符合這些條件的案例計數：<br /><br /> 實際的值不等於目標值。<br /><br /> 模型預測出案例不包含目標值。|  
  
#### <a name="lift"></a>增益  
 增益*是與*可能性相關聯的量值。 當您使用模型時，如果您在進行隨機猜測時，會產生較多的結果，則模型會被稱為提供*正面*增益。 不過，如果模型做出的預測較不可能是隨機機率，增益分數就是*負值*。 因此，這項標準表示使用模型可以達到的改進程度，其分數越高越好。  
  
 系統會將增益當做實際預測機率與測試案例中臨界機率的比率計算。  
  
#### <a name="log-score"></a>對數分數  
 *對數分數*（也稱為預測的*記錄可能性分數*）代表兩個機率之間的比率，轉換成對數刻度。 由於機率會以小數表示，因此對數分數永遠為負數。 分數越接近 0，表示得分越高。  
  
 鑑於原始分數可能具有非常不尋常或偏斜的散發，對數分數會與百分比類似。  
  
#### <a name="root-mean-square-error"></a>均方根誤差  
 *根平均平方誤差* (RMSE) 是統計資料中的標準方法，以查看不同的資料集比較方式，並將輸入的小數位數所能引進的差異平滑化。  
  
 RMSE 代表與實際值相比時，預測值的平均誤差。 它會以所有資料分割案例平均誤差的平方根，除以資料分割中的案例數目來計算，不包括目標屬性擁有遺漏值的資料列。  
  
#### <a name="mean-absolute-error"></a>平均絕對誤差  
 *平均絕對錯誤*是預測值對實際值的平均誤差。 計算方式為，取得誤差總和的絕對值，然後尋找這些誤差的平均值。  
  
 這個值有助於了解分數與平均值距離的變化。  
  
#### <a name="case-likelihood"></a>案例概似值  
 此量值僅用於群集模型，表示新案例屬於特定群集的可能性。  
  
 在群集模型中，根據您建立模型所使用的方法，有兩種群集成員資格。 在某些模型中，根據 K-means 演算法，新案例應該只屬於一個群集。 不過根據預設，Microsoft 群集演算法使用最大期望值方法，假設新案例潛在可能屬於任何群集。 因此在這些模型中，一個案例可以有多個 `CaseLikelihood` 值，但是根據預設回報的值是屬於最符合新案例之群集的案例概似值。  
  
## <a name="see-also"></a>另請參閱  
 [驗證模型及使用模型進行預測 &#40;適用于 Excel 的資料採礦增益集&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
  
