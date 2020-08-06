---
title: CountRows 函式 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5b1c403d-6afd-44c8-b5f6-5ecff2a29a45
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6d5311dfc5dfcb89449a4039fdac4100fc5a3b47
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595724"
---
# <a name="countrows-function-report-builder-and-ssrs"></a>CountRows 函數 (報表產生器及 SSRS)
  傳回指定之範圍中的資料列數目，包括具有 Null 值的資料列。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>語法  
  
```  
  
CountRows(scope, recursive)  
```  
  
#### <a name="parameters"></a>參數  
 *範圍 (scope)*  
 (`String`) 包含要計數之報表項目的資料集、資料區域或群組的名稱。  
  
 *遞迴*  
 (**列舉型別**) 選擇性。 `Simple` (預設值) 或 `RdlRecursive`。 指定是否要以遞迴方式執行彙總。  
  
## <a name="return-type"></a>傳回類型  
 傳回 `Integer`。  
  
## <a name="remarks"></a>備註  
 `CountRows` 會計算指定之範圍中所有資料列的數目，包括具有 Null 值的資料列。  
  
 *scope* 的值不能為運算式，且必須參考目前的範圍或包含範圍。  
  
 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 如需遞迴彙總的詳細資訊，請參閱[建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## <a name="example"></a>範例  
 下列程式碼範例顯示的運算式會計算名為 `GroupbyCategory` 的資料列群組中的資料列數目 (以 `[Category]`運算式為基礎)。  
  
```  
="Number of rows: " & CountRows("GroupbyCategory")  
```  
  
## <a name="see-also"></a>另請參閱  
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
