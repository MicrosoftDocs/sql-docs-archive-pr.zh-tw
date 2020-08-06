---
title: Multilookup 函式 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 1fec079e-33b3-4e4d-92b3-6b4d06a49a77
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2f2aff7a2a39e1a072cf4b05f0a04e12ced529af
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595709"
---
# <a name="multilookup-function-report-builder-and-ssrs"></a>Multilookup 函數 (報表產生器及 SSRS)
  從包含名稱/值組的資料集傳回第一組符合指定之名稱集合的值。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>語法  
  
```  
  
Multilookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>參數  
 *source_expression*  
 (`VariantArray`) - 在目前範圍中評估並指定要查閱之名稱或索引鍵集合的運算式。 例如，如果是多值參數 `=Parameters!IDs.value`。  
  
 *destination_expression*  
 (`Variant`) - 針對資料集中的每個資料列評估並指定要比對之名稱或索引鍵的運算式。 例如： `=Fields!ID.Value` 。  
  
 *result_expression*  
  (`Variant`) 在 dataset 中針對資料列評估的運算式，其中*source_expression*  =  *destination_expression*，並指定要取得的值。 例如： `=Fields!Name.Value` 。  
  
 *資料集 (dataset)*  
 指定報表中資料集名稱的常數。 例如，"Colors"。  
  
## <a name="return"></a>傳回  
 傳回 `VariantArray` 或在沒有相符項目時傳回 `Nothing`。  
  
## <a name="remarks"></a>備註  
 使用 `Multilookup` 可從具有一對一關係的每一組名稱/值組的資料集內擷取一組值。 `MultiLookup` 等於針對一組名稱或索引鍵呼叫 `Lookup`。 例如，如果是根據主索引鍵識別碼的多值參數，您可以在資料表中的文字方塊內使用運算式中的 `Multilookup`，從未繫結至參數或資料表的資料集擷取關聯的值。  
  
 `Multilookup` 會執行下列動作：  
  
-   評估目前範圍中的來源運算式，並產生變數物件的陣列。  
  
-   如果是陣列中的每一個物件，則呼叫 [Lookup 函式 &#40;報表產生器及 SSRS&#41;](report-builder-functions-lookup-function.md)，並將結果新增傳回陣列。  
  
-   傳回結果集。  
  
 若要從具有一對一關聯性之名稱/值組的資料集中，擷取指定名稱的單一值，請使用 [Lookup 函式 &#40;報表產生器及 SSRS&#41;](report-builder-functions-lookup-function.md)。 若要從具有一對多關聯性之名稱/值組的資料集中，擷取某個名稱的多個值，請使用 [LookupSet 函式 &#40;報表產生器及 SSRS&#41;](report-builder-functions-lookupset-function.md)。  
  
 適用以下限制：  
  
-   當套用所有篩選運算式之後，便會評估 `Multilookup`。  
  
-   只支援一層的查閱。 來源、目的地或結果運算式不能包含查閱函數的參考。  
  
-   來源和目的地運算式必須評估為相同的資料類型。  
  
-   來源、目的地和結果運算式無法包含報表或群組變數的參考。  
  
-   `Multilookup` 不能當做下列報表項目的運算式使用：  
  
    -   資料來源的動態連接字串。  
  
    -   資料集中的導出欄位。  
  
    -   資料集中的查詢參數。  
  
    -   資料集中的篩選。  
  
    -   報表參數。  
  
    -   Report.Language 屬性。  
  
 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="example"></a>範例  
 假設資料集 "Category" 包含 CategoryList 欄位，這個欄位是包含以逗號分隔之類別目錄識別碼的清單，例如 "2, 4, 2, 1"。  
  
 CategoryNames 資料集包含類別目錄識別碼和類別目錄名稱，如下表所示。  
  
|ID|名稱|  
|--------|----------|  
|1|Accessories|  
|2|Bikes|  
|3|Clothing|  
|4|元件|  
  
 若要查閱對應到識別碼清單的名稱，請使用 `Multilookup`。 您必須先將此清單分割成字串陣列、呼叫 `Multilookup` 來擷取類別目錄名稱，並將結果串連成一個字串。  
  
 當下列運算式置於繫結至 Category 資料集之資料區中的文字方塊內時，將會顯示 "Bikes, Components, Bikes, Accessories"：  
  
```  
=Join(MultiLookup(Split(Fields!CategoryList.Value,","),  
   Fields!CategoryID.Value,Fields!CategoryName.Value,"Category")),  
   ", ")  
```  
  
## <a name="example"></a>範例  
 假設 ProductColors 資料集包含色彩識別碼欄位 ColorID 及色彩值欄位 Color，如下表所示。  
  
|ColorID|Color|  
|-------------|-----------|  
|1|紅色|  
|2|藍色|  
|3|綠色|  
  
 假設多值參數 *MyColors* 沒有繫結至其可用值的資料集。 此參數的預設值為 2 和 3。 當下列運算式置於資料表的文字方塊中時，會將此參數的多個選定值串連成一個以逗號分隔的清單，並顯示 "Blue, Green"。  
  
```  
=Join(MultiLookup(Parameters!MyColors.Value,Fields!ColorID.Value,Fields!Color.Value,"ProductColors"),", ")  
```  
  
## <a name="see-also"></a>另請參閱  
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
