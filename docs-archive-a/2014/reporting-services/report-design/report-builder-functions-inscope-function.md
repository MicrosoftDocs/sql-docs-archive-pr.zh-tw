---
title: InScope 函式 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 62c4ad5de7af1ac0762df29deaa17953a8a378db
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595717"
---
# <a name="inscope-function-report-builder-and-ssrs"></a>InScope 函數 (報表產生器及 SSRS)
  指出某個項目目前的執行個體是否在指定的範圍內。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>語法  
  
```  
InScope(scope)  
```  
  
#### <a name="parameters"></a>參數  
 *範圍 (scope)*  
 (`String`) 指定範圍之資料集、資料區域或群組的名稱。  
  
## <a name="return-type"></a>傳回類型  
 傳回 `Boolean`。  
  
## <a name="remarks"></a>備註  
 函式會 `InScope` 測試報表專案目前實例的範圍，以尋找*範圍*參數所指定之範圍中的成員資格。  
  
 *Scope* 不能是運算式。  
  
 `InScope` 函數一般會用於具有動態範圍的資料區域。 例如，資料區域資料格中的鑽研連結可以利用 `InScope`，根據按下的資料格來提供不同的報表名稱和不同組的參數。 此範例如下：  
  
-   下列運算式是用做鑽研連結中的報表名稱，如果按下的資料格是在 `ProductDetail` 群組中，便會開啟 `Month` 報表，如果不是，便開啟 `ProductSummary` 報表。  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   下列運算式會用於鑽研報表參數的 `Omit` 屬性，只有按下的資料格在 `Product` 群組中時，才會將參數傳給目標報表。  
  
    ```  
    =Not(InScope("Product"))  
    ```  
  
 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="example"></a>範例  
 下列程式碼範例指出項目目前的執行個體是否位在 `Product` 資料集、資料區域或群組的範圍中。  
  
```  
=InScope("Product")  
```  
  
## <a name="see-also"></a>另請參閱  
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
