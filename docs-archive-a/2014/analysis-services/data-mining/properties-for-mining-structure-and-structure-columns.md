---
title: 用於採礦結構和結構資料行的屬性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], column properties
- data mining [Analysis Services], properties
- columns [data mining], properties
- properties [data mining]
ms.assetid: ce90f684-bb8c-4eca-b9e6-000794dbee16
author: minewiskan
ms.author: owend
ms.openlocfilehash: d83052c91b62f2c8873a80084b02200f276b4aac
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87703425"
---
# <a name="properties-for-mining-structure-and-structure-columns"></a>採礦結構和結構資料行的屬性
  您可以使用 [資料採礦設計師] 的 [採礦結構]**** 索引標籤，來設定或變更採礦結構及其相關聯資料行和巢狀資料表的屬性。 在此索引標籤中設定的屬性會傳播至與結構相關聯的每一個採礦模型。  
  
> [!NOTE]  
>  如果您在採礦結構中變更了任何屬性的值，甚至是中繼資料 (例如名稱或描述)，就必須先重新處理該採礦結構及其模型，然後才能檢視或查詢模型。  
  
## <a name="properties-of-mining-structures-and-mining-structure-columns"></a>採礦結構和採礦結構資料行的屬性  
 下表描述的是採礦結構的屬性，以及資料採礦特有的採礦結構資料行，您可以在 [**採礦結構**] 索引標籤中查看或設定。若要查看或設定這些屬性，請以滑鼠右鍵按一下樹狀檢視中的元素，然後按一下 [**屬性**]。  
  
-   若要檢視結構的屬性，請按一下採礦結構標題。  
  
-   若要檢視資料行或巢狀資料表的屬性，請按一下資料行名稱。  
  
### <a name="properties-of-the-mining-structure"></a>採礦結構的屬性  
  
|屬性|描述|  
|--------------|-----------------|  
|**CacheMode**|指定在培訓完成之後，應該快取或捨棄培訓中所使用的案例。<br /><br /> 注意：這個屬性必須設定為， `KeepTrainingCases` 才能啟用 [鑽取] 和 [維持]。|  
|**定序**|指定資料行的預設定序。 如果沒有指定定序，就會使用伺服器的定序。|  
|**說明**|描述採礦結構。 可能的話，描述最好指出結構中資料的用途和構成要素。|  
|**ErrorConfiguration (預設值)**|針對錯誤的特殊處理方式指定選項 (如果有的話)。|  
|**HoldoutMaxCases**|指定可保留成測試資料集的最大結構案例數目。  **HoldoutMaxCases** 和 **HoldoutPercent**如已指定值，就會組合這些條件。<br /><br /> 注意：若要設定這個屬性， <xref:Microsoft.AnalysisServices.MiningStructure.CacheMode%2A> 必須將設定為 `KeepTrainingCases` 。|  
|**HoldoutPercent**|指定要保留成測試資料集的結構案例百分比。 **HoldoutMaxCases** 和 **HoldoutPercent**如已指定值，就會組合這些條件。<br /><br /> 注意：若要設定這個屬性， <xref:Microsoft.AnalysisServices.MiningStructure.CacheMode%2A> 必須將設定為 `KeepTrainingCases` 。|  
|**HoldoutSeed**|指定要初始化鑑效組測試集之資料分割的種子，以便確保測試資料集可重新建立。<br /><br /> 注意：若要設定這個屬性， <xref:Microsoft.AnalysisServices.MiningStructure.CacheMode%2A> 必須將設定為 `KeepTrainingCases` 。|  
|**識別碼**|顯示採礦結構的唯一識別碼。<br /><br /> 在建立採礦結構時您指派給結構的名稱會當做識別碼使用。 如果您之後針對 `Name` 屬性輸入新的值，藉以變更此名稱，新的名稱只會當做別名使用。識別碼不會變更。|  
|**語言**|針對採礦結構中的標題指定語言。|  
|`Name`|指定採礦結構的名稱或別名。<br /><br /> 如果您變更 Name 屬性的值，新的名稱只會當做標題或別名使用。採礦結構的識別碼不會變更。|  
|**Source**|顯示資料來源的名稱和資料來源的類型。|  
  
### <a name="properties-of-the-mining-structure-columns"></a>採礦結構資料行的屬性  
  
|屬性|描述|  
|--------------|-----------------|  
|**ClassifiedColumns**|識別分類資料行描述的資料行。|  
|**內容**|資料行的內容類型。|  
|**說明**|描述資料行。 可能的話，資料行的描述最好提供有關資料行中的資料如何針對資料採礦衍生或更改的資訊。|  
|**DiscretizationBucketCount**|顯示離散化資料行中的值區數目。<br /><br /> 只有當內容類型設定為 `Discretized` 時才啟用。<br /><br /> 這個屬性是唯讀的。|  
|**DiscretizationMethod**|顯示用來離散化資料行的方法。<br /><br /> 只有當內容類型設定為 `Discretized` 時才啟用。<br /><br /> 這個屬性是唯讀的。|  
|**Distribution**|指定資料行中之內容的散發。|  
|**識別碼**|顯示資料行的識別碼。<br /><br /> 如果您變更了資料行的 Name 屬性值，並不會影響 ID 屬性的值。|  
|**IsKey**|指出資料行是否為索引鍵資料行。|  
|**KeyColumns**|包含資料行的定義，資料行為屬性的索引鍵或部份索引鍵。|  
|**ModelingFlags**|設定演算法提供的其他參數。|  
|`Name`|資料行名稱。|  
|**NameColumn**|識別提供父元素名稱的資料行。|  
|**Source**|顯示資料行的來源。<br /><br /> 若為關聯式資料來源，此值一律為 **[(無)]**。<br /><br /> 若為以 OLAP Cube 為基礎的結構，此值就是定義當做巢狀資料表來源使用之配量的 MDX 陳述式。|  
|**SourceMeasureGroup**|顯示量值群組的來源。<br /><br /> 若為關聯式資料來源，此值一律為 **[(無)]**。<br /><br /> 若為以 OLAP Cube 為基礎的結構，此值就是定義當做巢狀資料表來源使用之配量的 MDX 陳述式。|  
|**型別**|資料行中之內容的資料類型。|  
  
 如需設定或變更屬性的詳細資訊，請參閱 [採礦結構工作和使用說明](mining-structure-tasks-and-how-tos.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立關聯式的採礦結構](create-a-relational-mining-structure.md)   
 [採礦結構資料行](mining-structure-columns.md)  
  
  
