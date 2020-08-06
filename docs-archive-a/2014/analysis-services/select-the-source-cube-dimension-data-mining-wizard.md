---
title: 選取 [資料採礦嚮導] ([來源 Cube] 維度) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.selectsourcecube.f1
ms.assetid: 556e216b-5e21-4160-967d-4c57591fbab4
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6295a5312b4501236e0ce8f5776fc43c0d014581
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592889"
---
# <a name="select-the-source-cube-dimension-data-mining-wizard"></a>選取來源 Cube 維度 (資料採礦精靈)
  使用 [選取來源 Cube 維度]**** 頁面，即可從包含您要分析之案例的 Cube 中選取維度。 例如，如果您要建立根據人口統計分析客戶購買行為的模型，您要選取 [客戶] 維度，其中通常包含每個客戶的唯一記錄，以及表示人口統計的各種屬性，例如性別、居住地或收入。 在此精靈的後半部，您將有機會加入與此案例資料表相關的資料表：例如，您可以加入顯示客戶已購買之產品的巢狀資料表。  
  
> [!NOTE]  
>  唯有在精靈的 [選取定義方法] **** 頁面上選取了 [從現有的 Cube] **** 之後，才會顯示這個頁面。  
  
## <a name="options"></a>選項  
 **選取來源 Cube 維度**  
 選取提供採礦結構之來源資料的 Cube 維度。  
  
## <a name="choosing-a-dimension"></a>選擇維度  
 由於您僅能選取一個維度用於模型中，因此，了解 Cube 結構並選取為您的模型提供最佳資訊的維度相當重要。 如果您不確定要使用哪個維度，請瀏覽 Cube 並使用維度設計師檢閱其中的欄位和資料，應該有所幫助。 如需詳細資訊，請參閱[在維度設計師中瀏覽維度資料](multidimensional-models/database-dimensions-browse-dimension-data-in-dimension-designer.md)。  
  
 如果您不熟悉一般維度，請參閱[維度簡介 &#40;Analysis Services - 多維度資料&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)。  
  
 如需單一維度中通常會包含的資訊類型，以及有助於資料採礦之屬性和量值的詳細資訊，請參閱[維度關聯性](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)。  
  
 如果您選擇的維度不包含建立資料採礦模型所需的所有相關屬性，您可能需要修改維度。 如需詳細資訊，請參閱 [定義資料庫維度](multidimensional-models/define-database-dimensions.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦嚮導 F1 說明 &#40;Analysis Services-資料採礦&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [建立資料採礦結構 &#40;資料採礦嚮導&#41;](create-the-data-mining-structure-data-mining-wizard.md)   
 [選取 [資料採礦嚮導] &#40;[案例金鑰]&#41;](select-the-case-key-data-mining-wizard.md)  
  
  
