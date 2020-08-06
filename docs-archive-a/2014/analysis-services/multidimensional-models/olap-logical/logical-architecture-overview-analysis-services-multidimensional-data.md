---
title: 邏輯架構總覽 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- cubes [Analysis Services], examples
- cubes [Analysis Services], about cubes
ms.assetid: 1a547bce-dacf-4d32-bc0f-3829f4b026e1
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8dc9c46cf4ddcc7ff04f0c9002bff59cdb3ba370
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87710922"
---
# <a name="logical-architecture-overview-analysis-services---multidimensional-data"></a>邏輯架構概觀 (Analysis Services - 多維度資料)
  Analysis Services 會以伺服器部署模式運作，該模式可判斷不同類型的 Analysis Services 模型所使用的記憶體架構和執行階段環境。 伺服器模式是在安裝期間決定。 多**維度和資料採礦模式**支援傳統的 OLAP 和資料採礦。 **表格式模式**支援表格式模型。 **SharePoint 整合模式**指的是安裝為 PowerPivot for SharePoint 的 Analysis Services 實例，用於載入和查詢活頁簿內的 Excel 或 PowerPivot 資料模型。

 本主題說明 Analysis Services 以多維度和資料採礦模式運作時的基本架構。 如需其他模式的詳細資訊，請參閱[表格式模型 &#40;Ssas 表格式&#41;](../../tabular-models/tabular-models-ssas.md)和[比較 &#40;SSAS&#41;的表格式和多維度方案](https://docs.microsoft.com/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)。

## <a name="basic-architecture"></a>基本架構
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的執行個體可包含多個資料庫，而且資料庫可同時有 OLAP 物件和資料採礦物件。 應用程式會連接到指定的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體和指定的資料庫。 伺服器電腦可主控多個 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體。 的實例 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會命名為 " \<ServerName> \\<InstanceName \> "。 下圖顯示物件之間所有提及的關聯性 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 。

 ![執行中 AMO 物件的關聯性](../../dev-guide/media/amo-runningobjects.gif "執行中 AMO 物件的關聯性")

 基本類別是建立 Cube 所需的最小一組物件。 此最小一組的物件是維度、量值群組和資料分割。 彙總是選擇性。

 維度是從屬性和階層建立而來。 階層是由一組排序的屬性所組成，集合的每一個屬性都會對應到階層中的某個層級。

 Cube 是從維度和量值群組建立而來。 Cube 之維度集合中的維度屬於資料庫的維度集合。 量值群組是具有相同資料來源檢視而且具有 Cube 中相同維度子集的量值集合。 量值群組有一或多個資料分割可管理實體資料。 量值群組可以有預設的彙總設計， 預設彙總設計可由量值群組中的所有資料分割所使用；此外，每一個資料分割都可以有它自己的彙總設計。

 伺服器物件的每個實例 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 在 AMO 中會被視為不同的伺服器物件，每個不同的實例會透過不同的連接連接到 <xref:Microsoft.AnalysisServices.Server> 物件。 每一個伺服器物件都包含一個或多個資料來源、資料來源檢視和資料庫物件，以及組件和安全性角色。

 維度物件每個資料庫物件都包含多個維度物件。 每一個維度物件都包含一或多個屬性，這些屬性會組織成若干階層。

 Cube 物件每個資料庫物件都包含一個或多個 cube 物件。 Cube 是由其量值和維度所定義。 Cube 中的量值和維度是衍生自 Cube 所依據之資料來源檢視中的資料表和檢視，或是從量值和維度定義所產生。

## <a name="object-inheritance"></a>物件繼承
 ASSL 物件模型包含許多重複元素群組。 例如，元素群組「包含」會 `Dimensions` `Hierarchies` 定義元素的維度階層。 `Cubes` 和 `MeasureGroups` 都包含元素群組「`Dimensions` 包含 `Hierarchies`」。

 除非明確被覆寫，否則元素會從更高的層級繼承這些重複元素群組的詳細資料。 例如，`Translations` 對於 `CubeDimension` 與 `Translations` 對於它的上階項目 `Cube` 是相同的作用。

 若要明確覆寫從更高層物件繼承而來的屬性，物件不需要明確重複整個結構及更高層物件的屬性。 物件需要明確陳述的唯一屬性是物件想要覆寫的那些屬性。 例如，`CubeDimension` 可能只會列出需要在 `Hierarchies` 中停用、需要變更可見性，或是尚未在 `Cube` 層級上提供某些 `Level` 詳細資料的那些 `Dimension`。

 物件上指定的某些屬性會針對子物件或下階物件上的相同屬性提供預設值。 例如，`Cube.StorageMode` 會針對 `Partition.StorageMode` 提供預設值。 若是繼承的預設值，ASSL 會針對繼承的預設值套用這些規則：

-   當子物件的屬性在 XML 中為 null 持，此屬性的值會預設為繼承的值。 但是，如果您從伺服器查詢此值，伺服器會傳回 XML 元素的 null 值。

-   您無法以程式設計方式判斷出子物件的屬性是直接在子物件上設定的，還是繼承而來。

## <a name="example"></a>範例
 Imports Cube 包含 Packages 和 Last 兩個量值，以及 Route、Source 和 Time 三個相關維度。

 ![Cube 範例 1](../../dev-guide/media/cubeintro1.gif "Cube 範例 1")

 圍繞 Cube 的較小英數字值是該維度的成員。 範例成員為 ground (Route 維度的成員)、Africa (Source 維度的成員) 和 1st quarter (Time 維度的成員)。

### <a name="measures"></a>量值
 Cube 資料格內的值代表 Packages 和 Last 兩個量值。 Packages 量值代表所匯入的封裝數，而 `Sum` 函數則是用來彙總事實。 Last 量值代表回條日期，而 `Max` 函數則是用來彙總事實。

### <a name="dimensions"></a>維度
 Route 維度表示匯入到達目的地的方式。 這個維度的成員包括 ground、nonground、air、sea、road 或 rail。 Source 維度代表製造進口產品的地點，例如 Africa 或 Asia。 Time 維度表示某季或半年度。

### <a name="aggregates"></a>彙總
 因為 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會視需要彙總較高層級的值，所以不論維度內的成員層級如何，Cube 的商務使用者都可決定每個維度之每個成員的任何量值。 例如，上圖中的量值可以根據標準行事曆階層來匯總，方法是使用時間維度中的行事歷時間階層，如下圖所示。

 ![按照時間維度所組織之量值的圖表](../../dev-guide/media/cubeintro2.gif "按照時間維度所組織之量值的圖表")

 除了使用單一維度來彙總量值之外，也可使用不同維度的成員組合來彙總量值。 這可讓商務使用者同時使用多個維度來評估量值。 例如，如果商務使用者想要分析每季從 Eastern Hemisphere 和 Western Hemisphere 的空運進口，則商務使用者可對 Cube 發出查詢，以擷取下列資料集。

||||套件|||Last|||
|-|-|-|--------------|-|-|----------|-|-|
||||All Sources|Eastern Hemisphere|Western Hemisphere|All Sources|Eastern Hemisphere|Western Hemisphere|
|All Time|||25110|6547|18563|Dec-29-99|Dec-22-99|Dec-29-99|
||1st half||11173|2977|8196|Jun-28-99|六月-20-99|Jun-28-99|
|||1st quarter|5108|1452|3656|Mar-30-99|Mar-19-99|Mar-30-99|
|||2nd quarter|6065|1525|4540|Jun-28-99|六月-20-99|Jun-28-99|
||2nd half||13937|3570|10367|Dec-29-99|Dec-22-99|Dec-29-99|
|||3rd quarter|6119|1444|4675|Sep-30-99|Sep-18-99|Sep-30-99|
|||4th quarter|7818|2126|5692|Dec-29-99|Dec-22-99|Dec-29-99|

 定義 Cube 之後，您可以建立新的彙總，或變更現有的彙總以設定選項 (例如，在查詢的處理或計算期間，是否要預先計算彙總)。 **相關主題：**[匯總和匯總設計](../../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)。

### <a name="mapping-measures-attributes-and-hierarchies"></a>對應量值、屬性和階層
 範例 Cube 的量值、屬性和階層都是衍生自 Cube 事實和維度資料表的下列資料行。

|量值或屬性 (層級)|成員|來源資料表|來源資料行|範例資料行值|
|------------------------------------|-------------|------------------|-------------------|-------------------------|
|封裝量值|不適用|ImportsFactTable|套件|12|
|最新的量值|不適用|ImportsFactTable|Last|May-03-99|
|Route 維度中的 Route 類別層級|nonground,ground|RouteDimensionTable|Route_Category|Nonground|
|Route 維度的 Route 屬性|air,sea,road,rail|RouteDimensionTable|路由|Sea|
|Source 維度的 Hemisphere 屬性|Eastern Hemisphere,Western Hemisphere|SourceDimensionTable|Hemisphere|Eastern Hemisphere|
|Source 維度的 Continent 屬性|Africa,Asia,AustraliaEurope,N.  America,S.  America|SourceDimensionTable|Continent|歐洲|
|Time 維度的 Half 屬性|1st half,2nd half|TimeDimensionTable|Half|2nd half|
|Time 維度的 Quarter 屬性|1st quarter,2nd quarter,3rd quarter,4th quarter|TimeDimensionTable|季|3rd quarter|

 單一 Cube 資料格的資料通常衍生自事實資料表的多個資料列。 例如，位於空中成員、非洲成員和第1季成員交集處的 cube 資料格包含的值，是藉由在**ImportsFactTable**事實資料表中匯總下列資料列來衍生。

|||||||
|-|-|-|-|-|-|
|Import_ReceiptKey|RouteKey|SourceKey|TimeKey|套件|Last|
|3516987|1|6|1|15|Jan-10-99|
|3554790|1|6|1|40|Jan-19-99|
|3572673|1|6|1|34|Jan-27-99|
|3600974|1|6|1|45|Feb-02-99|
|3645541|1|6|1|20|Feb-09-99|
|3674906|1|6|1|36|Feb-17-99|

 在上表中，每個資料列的**RouteKey**、 **SourceKey**和**TimeKey**資料行都有相同的值，表示這些資料列會構成相同的 cube 資料格。

 此處所顯示的範例代表極簡單的 Cube，而在該範例中，Cube 含有單一量值群組，且所有維度資料表都是以星狀結構描述來聯結至事實資料表。 另一個通用結構描述是雪花式結構描述，其中一或多份維度資料表會聯結至另一份維度資料表，而不是直接聯結至事實資料表。 **相關主題：**[維度 &#40;Analysis Services 多維資料&#41;](../../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)。

 此處所顯示的範例只包含單一事實資料表。 當 Cube 具有多份事實資料表時，會將每份事實資料表的量值組成量值群組，並根據定義的維度關聯性讓量值群組與特定的維度集產生關聯。 而透過指定資料來源檢視的參與資料表和關聯性的資料粒度，即可建立這些關聯性。 **相關主題：**[維度關聯](../../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)性。

## <a name="see-also"></a>另請參閱
 [多維度模型資料庫 &#40;SSAS&#41;](../multidimensional-model-databases-ssas.md)


