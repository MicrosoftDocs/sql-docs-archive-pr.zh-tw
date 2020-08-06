---
title: Cube 物件 (Analysis Services 多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- cubes [Analysis Services], objects
ms.assetid: 5cee362e-3f95-4467-bc6c-29b1518ecbf3
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0e6dfb75be696ab26893e668b99dc36c7340f86c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596943"
---
# <a name="cube-objects-analysis-services---multidimensional-data"></a>Cube 物件 (Analysis Services - 多維度資料)
    
## <a name="introducing-cube-objects"></a>Cube 物件簡介  
 簡單的 <xref:Microsoft.AnalysisServices.Cube> 物件是由以下項目所組成：基本資訊、維度和量值群組。 基本資訊包括 Cube 的名稱、Cube 的預設量值、資料來源、儲存模式等等。  
  
 Dimensions 集合包含在 Cube 中使用的一組來自資料庫維度集合的實際維度。 所有維度都必須先定義在資料庫的維度集合中，才能在 Cube 中參考。 無法在中使用私用維度 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。  
  
 量值群組是 Cube 中的量值集合。 量值群組是具有共同資料來源檢視及共同一組維度的量值集合。 量值群組是量值的處理單位；量值群組可以個別處理，然後進行瀏覽。  
  
## <a name="in-this-section"></a>本節內容  
  
|||  
|-|-|  
|主題||  
|[動作 &#40;Analysis Services - 多維度資料&#41;](../multidimensional-models/actions-analysis-services-multidimensional-data.md)||  
|[彙總和彙總設計](aggregations-and-aggregation-designs.md)||  
|[計算](calculations.md)||  
|[Cube 資料格 &#40;Analysis Services 多維度資料&#41;](cube-cells-analysis-services-multidimensional-data.md)||  
|[Cube 屬性](cube-properties-multidimensional-model-programming.md)||  
|[Cube 儲存體 &#40;Analysis Services-多維度資料&#41;](cube-storage-analysis-services-multidimensional-data.md)||  
|[Cube 翻譯](cube-translations.md)||  
|[維度關聯性](dimension-relationships.md)||  
|[多維度模型中的關鍵效能指標 &#40;KPI&#41;](../multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)||  
|[量值和量值群組](../multidimensional-models/measures-and-measure-groups.md)||  
|[資料分割 &#40;Analysis Services - 多維度資料&#41;](partitions-analysis-services-multidimensional-data.md)||  
|[檢視方塊](perspectives.md)||  
  
  
