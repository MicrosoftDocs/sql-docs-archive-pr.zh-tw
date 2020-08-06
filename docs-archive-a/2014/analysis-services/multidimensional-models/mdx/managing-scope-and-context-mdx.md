---
title: " (MDX) 管理範圍和內容 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- scripts [MDX], context
- scope [MDX]
- CALCULATE statement
- This function [MDX]
- SCOPE statement
- scripts [MDX], scope
ms.assetid: 631e7c20-8be9-4c35-8609-76516aef19d1
author: minewiskan
ms.author: owend
ms.openlocfilehash: f7cf1e6cea8df00b632e114a5a8756373738ca6e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594743"
---
# <a name="managing-scope-and-context-mdx"></a>管理範圍及內容 (MDX)
  在中 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ， (MDX) 腳本的多維度運算式可以在腳本執行內的特定點套用至整個 cube 或 cube 的特定部分。 MDX 指令碼會透過使用計算行程，對 Cube 內的計算採用分層方法。  
  
> [!NOTE]  
>  如需計算行程如何影響計算的詳細資訊，請參閱[了解行程順序和解決順序 &#40;MDX&#41;](mdx-data-manipulation-understanding-pass-order-and-solve-order.md)。  
  
 若要控制計算行程、範圍及 MDX 指令碼內的內容，您可以特別使用 CACULATE 陳述式、`This` 函數及 SCOPE 陳述式。  
  
## <a name="using-the-calculate-statement"></a>使用 CALCULATE 陳述式  
 CALCULATE 陳述式會以彙總資料擴展 Cube 中的每個資料格。 例如，MDX 指令碼在指令碼的開始處會有一個 CALCULATE 陳述式。  
  
 如需 CALCULATE 陳述式語法的詳細資訊，請參閱 [CALCULATE 陳述式 &#40;MDX&#41;](/sql/mdx/mdx-scripting-calculate)。  
  
> [!NOTE]  
>  如果指令碼包含了內含 CALCULATE 陳述式的 SCOPE 陳述式，MDX 會評估 SCOPE 陳述式定義之 Subcube 內容內的 CALCULATE 陳述式，而不是評估整個 Cube。  
  
## <a name="using-the-this-function"></a>使用 This 函數  
 您可以使用 `This` 函數擷取目前在 MDX 指令碼內的 Subcube。 您可以使用 `This` 函數對 MDX 運算式快速地設定目前  Subcube 內的資料格值。 您通常會使用 `This` 函數配合 SCOPE 陳述式，在特定的計算行程期間變更特定  Subcube 的內容。  
  
> [!NOTE]  
>  如果指令碼包含了內含 `This` 函數的 SCOPE 陳述式，MDX 會評估 SCOPE 陳述式定義之 Subcube 的內容內的 `This` 函數，而不是評估整個 Cube。  
  
### <a name="this-function-example"></a>This 函數範例  
 在 [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)] 範例 Cube 的 Finance 量值群組中，下列 MDX 指令碼命令範例是使用 `This` 函數增加 Amount 量值的值，其比 Customer 維度中 Redmond 成員的子系高出 10%：  
  
```  
/* This SCOPE statement defines the current subcube */  
SCOPE([Customer].&[Redmond].MEMBERS,   
    [Measures].[Amount], *);  
        /* This expression sets the value of the Amount measure */  
        THIS = [Measures].[Amount] * 1.1;  
END SCOPE;  
```  
  
 如需函數語法的詳細資訊 `This` ，請參閱[這 &#40;MDX&#41;](/sql/mdx/this-mdx)。  
  
## <a name="using-the-scope-statement"></a>使用 SCOPE 陳述式  
 SCOPE 陳述式會定義目前的 Subcube，此 Subcube 包含 MDX 指令碼內的其他 MDX 運算式及陳述式，而且會指定它們的範圍。 MDX 會評估 Subcube 內容中此其他的 MDX 運算式及陳述式，包括 `This` 函數及 CALCULATE 陳述式在內。  
  
 SCOPE 陳述式本質上是動態但不反覆。 SCOPE 陳述式內包含的陳述式只會執行一次，但可以動態地決定 Subcube 本身。 例如，您有一個稱為 SampleCube 的 Cube。 您可以對 SampleCube Cube 套用以下 SCOPE 陳述式，以定義在 Measures 維度內將內容定義為 ALLMEMBERS 的 Subcube：  
  
 `SCOPE([Measures].ALLMEMBERS);`  
  
 `THIS = [Measures].ALLMEMBERS.COUNT;`  
  
 `END SCOPE;`  
  
 this 函數的 SCOPE 陳述式內的陳述式及運算式只會執行一次。  
  
 現在，商業使用者可以對 SampleCube Cube 執行以下包含一個稱為 ExistingMeasure 之量值的 MDX 查詢：  
  
 `WITH MEMBER [Measures].[NewMeasure] AS '1'`  
  
 `SELECT`  
  
 `[Measures].ALLMEMBERS ON COLUMNS,`  
  
 `[Customer].DEFAULTMEMBER ON ROWS`  
  
 `FROM`  
  
 `[SampleCube]`  
  
 查詢傳回的資料格集與下表顯示的輸出類似。  
  
||[ExistingMeasure]|[NewMeasure]|  
|-|-------------------------|--------------------|  
|[Customer].[All]|2|2|  
  
 請查看傳回的資料格集，注意在定義量值 NewMeasure 之後，是如何動態更新 MDX 指令碼內的 SCOPE 陳述式包括的 ExistingMeasure 值，  
  
 SCOPE 陳述式在另一個 SCOPE 陳述式內可為巢狀。 但是，因為 SCOPE 陳述式不會反覆執行，巢狀 SCOPE 陳述式的主要用途是為了進行特殊處理而進一步細分 Subcube。  
  
### <a name="scope-statement-example"></a>SCOPE 陳述式範例  
 下列 MDX 指令碼範例在 [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)] 範例 Cube 的 Finance 量值群組中，使用 SCOPE 陳述式將 Amount 量值的值設為高於 Customer 維度中 Redmond 成員的子系 10%。 但是，其他 SCOPE 陳述式會變更 Subcube 以包括 2002 日曆年度之子系的 Amount 量值。 最後，Amount 量值指會對那個 Subcube 進行彙總，而讓其他日曆年度中 Amount 量值的彙總值保持不變。  
  
```  
/* Calculate the entire cube first. */  
CALCULATE;  
/* This SCOPE statement defines the current subcube */  
SCOPE([Customer].&[Redmond].MEMBERS,   
    [Measures].[Amount], *);  
        /* This expression sets the value of the Amount measure */  
        THIS = [Measures].[Amount] * 1.1;  
END SCOPE;  
```  
  
 如需 SCOPE 陳述式語法的詳細資訊，請參閱 [SCOPE 陳述式 &#40;MDX&#41;](/sql/mdx/mdx-scripting-scope)。  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 語言參考 &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)   
 [基本 MDX 腳本 &#40;MDX&#41;](the-basic-mdx-script-mdx.md)   
 [MDX 查詢基礎觀念 &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
