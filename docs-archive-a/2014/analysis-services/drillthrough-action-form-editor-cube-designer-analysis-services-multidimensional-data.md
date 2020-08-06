---
title: '[ (動作] 索引標籤、Cube 設計工具)  (Analysis Services-多維度資料) | 中的 [動作表單編輯器]Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.drillthroughaction.f1
ms.assetid: 225fd818-b5ea-494f-b67b-66e09798274a
author: minewiskan
ms.author: owend
ms.openlocfilehash: 546448bd05f3af45b7093acb2dbb9d1e1a8f1bd5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599247"
---
# <a name="drillthrough-action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>鑽研動作表單編輯器 (動作索引標籤，設計師) (Analysis Services - 多維度資料)
  在 Cube 設計師中，使用 **[動作]** 索引標籤的 **[鑽研動作表單編輯器]** 窗格，即可修改 **[動作組合管理]** 窗格中選取的鑽研動作。 如需鑽研動作的詳細資訊，請參閱[動作 &#40;Analysis Services - 多維度資料&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md)。  
  
> [!NOTE]  
>  鑽研動作不再向下鑽研至基礎資料存放區。 鑽研動作存取的資訊，必須是使用維度或階層成員包含在 Cube 模型中的資訊。  
  
## <a name="options"></a>選項  
 **name**  
 鍵入動作的名稱。  
  
 **動作目標**  
 展開即可檢視 [量值群組成員]**** 選項。  
  
 **量值群組成員**  
 選取要與鑽研動作建立關聯的量值群組。  
  
 **條件 (選擇性)**  
 輸入描述選擇性條件的多維度運算式 (MDX) 運算式，搭配 [量值群組成員]**** 一起使用，進一步限制何時可以使用動作。 此運算式必須傳回布林值，如果此值為 True，則表示可使用該動作。  
  
 從 **[計算工具]** 窗格中，將選取的元素拖曳到這個選項，以包括所選元素的 MDX 語法。  
  
 **鑽研資料行**  
 展開即可顯示方格，以指出使用者執行此動作時傳回的屬性。  
  
> [!NOTE]  
>  您可以選取一個以上的維度，但維度在一個鑽研動作中不能使用一次以上。  
  
 方格包含下列資料行：  
  
|資料行|描述|  
|------------|-----------------|  
|**維度**|選取衍生所傳回屬性的維度。 選取 MEASURES 即可在量值上進行鑽研。|  
|**傳回資料行**|從選取的維度中選取執行動作時要傳回的屬性或量值。|  
  
 **其他屬性**  
 展開以檢視 [預設值]****、[最大資料列數]****、[引動過程]****、[應用程式]****、[描述]****、[標題]**** 及 [標題是 MDX]**** 選項。  
  
 **預設值**  
 選取 [True]**** 以包含此鑽研動作作為預設鑽研動作，否則，請選取 [False]****。  
  
 如果 `RETURN` 從 `DRILLTHROUGH` 用戶端應用程式所執行的 MDX 語句中省略子句，實例就會 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 評估所有預設的鑽取動作，並執行第一個傳回非空白集合的預設「鑽取」動作。 如需 MDX 語句的詳細資訊 `DRILLTHROUGH` ，請參閱[&#40;mdx&#41;](/sql/mdx/mdx-data-manipulation-drillthrough)的「鑽看」語句。  
  
> [!NOTE]  
>  此選項用於回溯相容性用途。  
  
 **最大資料列數**  
 鍵入鑽研動作要傳回的最大資料列數。 將此選項設定為零或空的值，表示鑽研動作將會傳回該動作擷取的所有資料列給用戶端應用程式。  
  
 **引動過程**  
 選取設定，以指出何時該執行此動作。  
  
> [!NOTE]  
>  此選項只提供用戶端應用程式何時要執行動作的建議，並不會直接控制動作的叫用。  
  
 下表描述可用的設定。  
  
|值|描述|  
|-----------|-----------------|  
|Batch|此動作應該當作批次作業的一部份或 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 工作來執行。|  
|互動式|此動作會在使用者叫用動作時執行。|  
|開啟時|此動作會在第一次開啟 Cube 時執行。|  
  
 **應用程式**  
 鍵入可以執行鑽研動作的應用程式名稱。  
  
 您也可以使用此選項來識別哪一個用戶端應用程式最常使用這個動作，以及在快顯功能表的該動作旁邊顯示適當的圖示。  
  
> [!NOTE]  
>  此選項只提供用戶端應用程式應該執行哪些動作的建議，並不會直接控制動作的存取。 用戶端應用程式應隱藏與其他用戶端應用程式相關聯的動作。  
  
 **說明**  
 鍵入動作的選擇性描述。  
  
 **Caption**  
 如果 [標題是 MDX]**** 設為 [False]****，則請鍵入要顯示在用戶端應用程式中的動作標題。  
  
 如果 [標題是 MDX]**** 設定為 [True]****，則請鍵入會傳回標題字串的多維度運算式 (MDX) 運算式。  
  
 **標題是 MDX**  
 選取 [False]**** 以指出 [標題]**** 包含一個常值字串，代表要顯示在用戶端應用程式中的動作標題。  
  
 選取 **[True]** 以指出 **[標題]** 包含一個會傳回字串的 MDX 運算式，字串代表要顯示在用戶端應用程式中的動作標題。 在動作傳回至用戶端應用程式之前，必須先解析 MDX 運算式。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;MDX&#41; 參考的多維度運算式](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [&#40;Cube 設計師的動作&#41; &#40;Analysis Services 多維度資料&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [工具列 &#40;動作] 索引標籤，Cube 設計工具&#41; &#40;Analysis Services 多維度資料&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [動作召集人 &#40;動作] 索引標籤、Cube 設計工具&#41; &#40;Analysis Services 多維度資料&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [[計算工具] &#40;[動作] 索引標籤、[Cube 設計師]&#41; &#40;Analysis Services 多維度資料&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [[操作表單編輯器] &#40;[動作] 索引標籤、[Cube 設計師]&#41; &#40;Analysis Services 多維度資料&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [報表操作表單編輯器 &#40;動作] 索引標籤、Cube 設計工具&#41; &#40;Analysis Services 多維度資料&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
