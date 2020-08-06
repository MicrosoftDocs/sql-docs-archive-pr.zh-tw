---
title: " (XMLA) 設計匯總 |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- statistical information [XML for Analysis]
- batches [XML for Analysis]
- aggregations [Analysis Services], XML for Analysis
- XMLA, aggregations
- queries [XMLA]
- XML for Analysis, aggregations
- iterative aggregation process [XMLA]
ms.assetid: 4dd27afa-10c7-408d-bc24-ca74217ddbcb
author: minewiskan
ms.author: owend
ms.openlocfilehash: 632cc071605cff6e42adec4acd32c9bd9949fc77
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599234"
---
# <a name="designing-aggregations-xmla"></a>設計彙總 (XMLA)
  彙總設計會與特定量值群組的資料分割關聯，以確保資料分割在儲存彙總時會使用相同的結構。 針對資料分割使用相同的儲存結構，可讓您輕鬆地定義稍後使用[MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla)命令合併的資料分割。 如需匯總設計的詳細資訊，請參閱匯總[和匯總設計](../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)。  
  
 若要定義匯總設計的匯總，您可以在 XML for Analysis (XMLA) 中使用[DesignAggregations](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/designaggregations-element-xmla)命令。 `DesignAggregations` 命令具有一些屬性，可識別要使用哪個彙總設計做為參考，以及如何根據該參考控制設計程序。 使用 `DesignAggregations` 命令及其屬性，您可以反覆或用批次方式設計彙總，然後檢視產生的設計統計資料以評估設計程序。  
  
## <a name="specifying-an-aggregation-design"></a>指定彙總設計  
 命令的[object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)屬性 `DesignAggregations` 必須包含現有匯總設計的物件參考。 物件參考包含資料庫識別碼、Cube 識別碼、量值群組識別碼以及彙總設計識別碼。 如果彙總設計尚未存在，就會發生錯誤。  
  
## <a name="controlling-the-design-process"></a>控制設計程序  
 您可以使用 `DesignAggregations` 命令的下列屬性來控制為彙總設計定義彙總的演算法。  
  
-   [[步驟](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/steps-element-xmla)] 屬性會決定命令在將 `DesignAggregations` 控制權傳回給用戶端應用程式之前，應採取多少次反覆運算。  
  
-   [Time](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/time-element-xmla)屬性會決定命令將控制權傳回 `DesignAggregations` 給用戶端應用程式之前，應採取的毫秒數。  
  
-   [[優化](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/optimization-element-xmla)] 屬性 `DesignAggregations` 會決定命令應該嘗試達到的效能改進估計百分比。 如果您反覆設計彙總，只需要在第一個命令上傳送此屬性。  
  
-   [Storage](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/storage-element-xmla)屬性會決定命令所使用的磁片儲存體預估量（以位元組為單位） `DesignAggregations` 。 如果您反覆設計彙總，只需要在第一個命令上傳送此屬性。  
  
-   [具體化](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/materialize-element-xmla)屬性會決定命令是否 `DesignAggregations` 應該建立在設計過程中定義的匯總。 如果您反覆地設計彙總，此屬性應該設定為 False，直到您準備儲存設計的彙總為止。 當設定為 True 時，目前的設計程序會結束，而定義的彙總會加入指定的彙總設計。  
  
## <a name="specifying-queries"></a>指定查詢  
 DesignAggregations 命令會 `Query` 在 [[查詢](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/queries-element-xmla)] 屬性中包含一或多個元素，以支援基於使用方式的優化命令。 `Queries`屬性可以包含一個或多個[查詢](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/query-element-xmla)元素。 如果 `Queries` 屬性不包含任何 `Query` 元素，在 `Object` 元素中指定的彙總設計，會使用包含一組一般彙總的預設結構。 這組一般彙總的設計，是為了符合在 `Optimization` 命令的 `Storage` 與 `DesignAggregations` 屬性中所指定的準則。  
  
 每個 `Query` 元素都代表一個目標查詢，而且設計處理序會使用此查詢來定義以最常用查詢為目標的彙總。 您可以指定自己的目標查詢，也可以使用查詢記錄檔中實例所儲存的資訊， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 來抓取最常使用之查詢的相關資訊。 「基於使用方式的最佳化精靈」會在傳送 `DesignAggregations` 命令時，依據時間、使用方式或是指定的使用者，使用查詢記錄擷取目標查詢。 如需詳細資訊，請參閱[基於使用方式的優化 Wizard F1](../usage-based-optimization-wizard-f1-help.md)說明。  
  
 如果您要反覆地設計彙總，只需要將目標查詢傳入第一個 `DesignAggregations` 命令即可，因為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體會儲存這些目標查詢，然後在後續的 `DesignAggregations` 命令執行期間使用這些查詢。 當您將目標查詢傳入反覆處理序的第一個 `DesignAggregations` 命令之後，任何在 `DesignAggregations` 屬性中包含目標查詢的後續 `Queries` 命令就會產生錯誤。  
  
 `Query` 元素包含具有下列引數的逗號分隔值：  
  
 *Frequency*,*Dataset*[,*Dataset*...]  
  
 *頻率*  
 對應至查詢先前執行次數的加權因數。 如果專案 `Query` 代表新的查詢， *Frequency*值代表設計進程用來評估查詢的加權因數。 當頻率值變大時，在設計處理序期間放置於查詢的加權就會增加。  
  
 *資料集*  
 指定維度的哪些屬性要包含在查詢中的數值字串。 這個字串必須與維度中的屬性數目具有相同的字元數目。 零 (0) 表示指定之序數位置中的屬性沒有包含在指定維度的查詢中，而一 (1) 則表示指定之序數位置中的屬性已包含在指定維度的查詢中。  
  
 例如，字串 "011" 是指涉及含有三個屬性之維度的查詢，其中第二和第三個屬性包含在查詢中。  
  
> [!NOTE]  
>  某些屬性會從資料集的考量中排除。 如需排除屬性的詳細資訊，請參閱[&#40;XMLA&#41;的查詢元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/query-element-xmla)。  
  
 量值群組中包含匯總設計的每個維度，都是以元素中的*資料集*值來表示 `Query` 。 *Dataset* 值的順序必須與量值群組中包含維度的順序相符。  
  
## <a name="designing-aggregations-using-iterative-or-batch-processes"></a>使用反覆或批次程序來設計彙總  
 您可以在反覆程序或是批次程序中使用 `DesignAggregations` 命令，端視設計程序所需的互動性而定。  
  
### <a name="designing-aggregations-using-an-iterative-process"></a>使用反覆程序來設計彙總  
 若要反覆設計彙總，您可以傳送多個 `DesignAggregations` 命令，以提供設計程序的良好控制。 「彙總設計精靈」使用這個相同的方法來提供設計程序的良好控制。 如需詳細資訊，請參閱[匯總設計嚮導 F1](../aggregation-design-wizard-f1-help.md)說明。  
  
> [!NOTE]  
>  需要明確的工作階段，以反覆設計彙總。 如需明確會話的詳細資訊，請參閱[&#40;XMLA&#41;管理連接和會話](managing-connections-and-sessions-xmla.md)。  
  
 若要開始反覆程序，請先傳送包含下列資訊的 `DesignAggregations` 命令：  
  
-   以整個設計程序為目標的 `Storage` 與 `Optimization` 屬性值。  
  
-   限制設計程序之第一個步驟的 `Steps` 與 `Time` 屬性值。  
  
-   如果您想要基於使用方式的最佳化，還要提供 `Queries` 屬性，其中包含整個設計程序的目標查詢。  
  
-   設定為 False 的 `Materialize` 屬性。 將此屬性設定為 False，表示設計程序不會在命令完成時將定義的彙總儲存至彙總設計。  
  
 當第一個 `DesignAggregations` 命令完成時，命令會傳回包含設計統計資料的資料列集。 您可以評估這些設計統計資料，以判斷設計程序是否應該繼續或者設計程序是否已完成。 如果程序應該繼續，則請傳送另一個 `DesignAggregations` 命令，以包含限制設計程序此步驟的 `Steps` 與 `Time` 值。 您可以評估產生的統計資料，然後判斷設計程序是否應該繼續。 傳送 `DesignAggregations` 命令與評估結果的反覆程序會繼續，直到您達成目標並且有一組適當定義的彙總為止。  
  
 在您達到所需的彙總之後，傳送最後一次的 `DesignAggregations` 命令。 這個最後的 `DesignAggregations` 命令應該將 `Steps` 屬性設定為 1，並將其 `Materialize` 屬性設定為 True。 透過使用這些設定，這個最後的 `DesignAggregations` 命令會完成設計程序，並將定義的彙總儲存到彙總設計。  
  
### <a name="designing-aggregations-using-a-batch-process"></a>使用批次程序來設計彙總  
 您也可以透過傳送單一 `DesignAggregations` 命令，以包含以整個設計程序為目標並使其受限的 `Steps`、`Time`、`Storage` 和 `Optimization` 屬性值，從而在批次程序中設計彙總。 如果您想要基於使用方式的最佳化，以設計程序為目標的目標查詢也應該包含在 `Queries` 屬性中。 另外請確定 `Materialize` 屬性是設定為 True，這樣設計程序就會在命令完成時，將定義的彙總儲存到彙總設計。  
  
 您可以在隱含或明確的工作階段中使用批次程序來設計彙總。 如需隱含和明確會話的詳細資訊，請參閱[&#40;XMLA&#41;管理連接和會話](managing-connections-and-sessions-xmla.md)。  
  
## <a name="returning-design-statistics"></a>傳回設計統計資料  
 當 `DesignAggregations` 命令將控制權還給用戶端應用程式時，命令會傳回包含單一資料列的資料列集，該資料列代表命令的設計統計資料。 資料列集包含下表中列出的資料行。  
  
|資料行|資料類型|描述|  
|------------|---------------|-----------------|  
|步驟|整數|在將控制權還給用戶端應用程式之前，命令所使用的步驟數目。|  
|Time|長整數|在將控制權還給用戶端應用程式之前，命令所花費的毫秒數目。|  
|Optimization|Double|在將控制權還給用戶端應用程式之前，命令所達成的效能改善估計百分比。|  
|儲存體|長整數|在將控制權還給用戶端應用程式之前，命令所使用的位元組估計數目。|  
|彙總|長整數|在將控制權還給用戶端應用程式之前，命令所定義的彙總數目。|  
|LastStep|Boolean|指出在資料列集中的資料是否代表設計程序中的最後一個步驟。 如果命令的 `Materialize` 屬性設定為 True，就會將這個資料行值設定為 True。|  
  
 您可以將每一個 `DesignAggregations` 命令之後傳回的資料列集內所含的設計統計資料用在反覆設計或批次設計。 在反覆設計中，您可以使用設計統計資料以判斷和顯示進度。 當您以批次方式設計彙總時，可以使用設計統計資料來判斷命令所建立的彙總數目。  
  
## <a name="see-also"></a>另請參閱  
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  
