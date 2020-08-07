---
title: 瞭解表格式物件模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 6077b7e8-cb3e-4480-a5de-bb602cf9d69a
author: minewiskan
ms.author: owend
ms.openlocfilehash: ed120bedfd236dcb55780982f0f611368147f813
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584739"
---
# <a name="understanding-the-tabular-object-model"></a>了解表格式物件模型
  表格式模型是資料表、關聯性、階層、檢視方塊、量值和關鍵效能的邏輯表示法。 本節介紹使用 AMO 進行的內部實作。 如果您之前未曾使用過 AMO，請參閱[流量分析管理物件 &#40;amo&#41;進行開發](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)。  
  
 此處說明的方法採由上而下，表格式模型中的所有相關物件都是以邏輯方式對應至 AMO 物件，並且將說明必要的互動或工作流程。 一個可供您使用 AMO、「AMO 對表格式」建立表格式模型的原始程式碼範例，可從 Codeplex 使用。 有關範例程式碼的重要注意事項：提供此範例的用意只是為了支援這裡所說明的邏輯概念，您不應將其用於生產環境。 此範例之提供不附帶任何支援或擔保。  
  
## <a name="database-representation"></a>資料庫表示法  
 資料庫會為表格式模型提供容器物件。 表格式模型中的所有物件都包含在資料庫內。 就 AMO 物件而言，資料庫表示法與 <xref:Microsoft.AnalysisServices.Database> 之間具有一對一的對應關聯性，而且不需要其他主要 AMO 物件。 請務必注意，這並不表示 AMO 資料庫物件中包含的所有物件都可以在進行模型化時使用。  
  
 如需如何建立及運算元據庫標記法的詳細說明，請參閱[&#40;表格式&#41;的資料庫標記法](database-representation-tabular.md)。  
  
## <a name="connection-representation"></a>連接表示法  
 連接會在表格式模型方案中和模型本身所包含的資料之間建立關聯性。 就 AMO 物件而言，連接與 <xref:Microsoft.AnalysisServices.DataSource> 之間具有一對一的對應關聯性，而且不需要其他主要 AMO 物件。 請務必注意，這並不表示 AMO 資料來源物件中包含的所有物件都可以在進行模型化時使用。  
  
 如需如何建立和運算元據源標記法的詳細說明，請參閱[&#40;表格式&#41;的連接標記法](connection-representation-tabular.md)。  
  
## <a name="table-representation"></a>資料表表示法  
 資料表是包含資料庫資料的資料庫物件。 就 AMO 物件而言，資料表具有一對多的對應關聯性。 資料表是使用下列 AMO 物件來表示：<xref:Microsoft.AnalysisServices.DataSourceView>、<xref:Microsoft.AnalysisServices.Dimension>、<xref:Microsoft.AnalysisServices.Cube>、<xref:Microsoft.AnalysisServices.CubeDimension>、<xref:Microsoft.AnalysisServices.MeasureGroup> 和 <xref:Microsoft.AnalysisServices.Partition> 是主要的必備物件。不過，請務必注意，這並不表示上述 AMO 物件中包含的所有物件都可以在進行模型化時使用。  
  
 如需如何建立和運算元據表標記法的詳細說明，請參閱[資料表標記法 &#40;表格式&#41;](tables-representation-tabular.md) 。  
  
### <a name="calculated-column-representation"></a>導出資料行表示法  
 導出資料行是在資料表中產生資料行的評估運算式，而且系統會針對資料表中的每個資料列計算並儲存新的值。 就 AMO 物件而言，導出資料行具有一對多的對應關聯性。 導出資料行是使用下列 AMO 物件來表示：<xref:Microsoft.AnalysisServices.Dimension> 和 <xref:Microsoft.AnalysisServices.MeasureGroup> 是主要的必備物件。 請務必注意，這並不表示上述 AMO 物件中包含的所有物件都可以在進行模型化時使用。  
  
 如需如何建立及操作計算結果欄標記法的詳細說明，請參閱[&#40;表格式&#41;的匯出資料行標記法](tables-calculated-column-representation.md)。  
  
### <a name="calculated-measure-representation"></a>導出量值表示法  
 導出量值是在部署模型之後根據要求評估的預存運算式。 就 AMO 物件而言，導出量值具有一對多的對應關聯性。 導出資料行是使用下列 AMO 物件來表示：<xref:Microsoft.AnalysisServices.MdxScript.Commands%2A> 和 <xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A> 是主要的必備物件。 請務必注意，這並不表示上述 AMO 物件中包含的所有物件都可以在進行模型化時使用。  
  
> [!NOTE]  
>   物件與表格式模型中的導出量值之間沒有任何關聯性，而且表格式模型不支援這類物件。  
  
 如需如何建立及操作匯出量值標記法的詳細說明，請參閱[&#40;表格式&#41;的匯出量值標記法](tables-calculated-measure-representation.md)。  
  
### <a name="hierarchy-representation"></a>階層表示法  
 階層是一種為使用者提供更豐富之向上鑽研和向下鑽研體驗的機制。 就 AMO 物件而言，階層表示法與 <xref:Microsoft.AnalysisServices.Hierarchy> 之間具有一對一的對應關聯性，而且不需要其他主要 AMO 物件。 請務必注意，這並不表示 AMO 資料庫物件中包含的所有物件都可以在進行表格式模型化時使用。  
  
 如需如何建立及操作階層標記法的詳細說明，請參閱[&#40;表格式&#41;的階層標記法](tables-hierarchy-representation.md)。  
  
### <a name="key-performance-indicator--kpi--representation"></a>關鍵效能指標-KPI-標記法  
 KPI 是用來針對目標值，測量由基底量值定義之值的效能。 就 AMO 物件而言，KPI 表示法具有一對多的對應關聯性。 KPI 是使用下列 AMO 物件來表示：<xref:Microsoft.AnalysisServices.MdxScript.Commands%2A> 和 <xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A> 是主要的必備物件。  請務必注意，這並不表示上述 AMO 物件中包含的所有物件都可以在進行模型化時使用。  
  
> [!NOTE]  
>  此外，也請注意一個重要的區別：<xref:Microsoft.AnalysisServices.Kpi> 物件與表格式模型內的 KPI 之間沒有任何關聯性。 此外，表格式模型內也不提供支援。  
  
 如需如何建立和操作 KPI 標記法的詳細說明，請參閱[&#40;表格式&#41;的關鍵效能指標標記法](tables-key-performance-indicator-representation.md)。  
  
### <a name="partition-representation"></a>資料分割表示法  
 您可以基於作業目的，將資料表分割成不同的資料列子集 (這些子集相結合即構成資料表)。 這些子集各個都是資料表的某一分割區。 就 AMO 物件而言，分割區表示法與 <xref:Microsoft.AnalysisServices.Partition> 之間具有一對一的對應關聯性，而且不需要其他主要 AMO 物件。 請務必注意，這並不表示 AMO 資料庫物件中包含的所有物件都可以在進行模型化時使用。  
  
 如需如何建立及運算元據分割標記法的詳細說明，請參閱[&#40;表格式&#41;的資料分割標記法](tables-partition-representation.md)。  
  
## <a name="relationship-representation"></a>關聯性表示法  
 關聯性是指兩個資料表之間的連接。 關聯性會建立兩個資料表中的資料相互關聯的方式。  
  
 在表格式模型中，可以在兩個資料表之間定義多個關聯性。 如果兩個資料表之間定義了多個關聯性，則只有其中一項可以定義成預設作用中的關聯性。 其餘所有的關聯性皆非作用中。  
  
 就 AMO 物件而言，所有非作用中的關聯性與 <xref:Microsoft.AnalysisServices.Relationship> 之間都有一對一的對應關聯性表示法，而且不需要其他主要 AMO 物件。 若是作用中的關聯性，則會有其他需求，而且還必須對應至 <xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension>。 請務必注意，這並不表示 AMO 關聯性或 referenceMeasureGroupDimension 物件中包含的所有物件都可以在進行模型化時使用。  
  
 如需如何建立和操作關聯性標記法的詳細說明，請參閱[&#40;表格式&#41;的關聯性標記法](relationship-representation-tabular.md)。  
  
## <a name="perspective-representation"></a>檢視方塊表示法  
 檢視方塊是一種簡化或聚焦至模式的機制。 就 AMO 物件而言，關聯性表示法與 <xref:Microsoft.AnalysisServices.Perspective> 之間具有一對一的對應關聯性，而且不需要其他主要 AMO 物件。 請務必注意，這並不表示 AMO 檢視方塊物件中包含的所有物件都可以在進行表格式模型化時使用。  
  
 如需如何建立和操作透視圖標記法的詳細說明，請參閱[&#40;表格式&#41;的觀點標記法](perspective-representation-tabular.md)。  
  
> [!WARNING]  
>  檢視方塊並非安全性機制。使用者仍然可透過其他介面存取檢視方塊外部的物件。  
  
  
