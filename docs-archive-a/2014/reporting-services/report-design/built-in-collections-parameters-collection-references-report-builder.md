---
title: 參數集合參考 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c4b47e15-0484-4c13-9182-898db825f01f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 163fe7c93c61088e48d37d0567674d5cee1a79a0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87704958"
---
# <a name="parameters-collection-references-report-builder-and-ssrs"></a><span data-ttu-id="1f675-102">參數集合參考 (報表產生器及 SSRS)</span><span class="sxs-lookup"><span data-stu-id="1f675-102">Parameters Collection References (Report Builder and SSRS)</span></span>
  <span data-ttu-id="1f675-103">報表參數是您可以從運算式參考的其中一個內建集合。</span><span class="sxs-lookup"><span data-stu-id="1f675-103">Report parameters are one of the built-in collections you can reference from an expression.</span></span> <span data-ttu-id="1f675-104">您可以在運算式中包含參數，以根據使用者所做的選擇來自訂報表資料及外觀。</span><span class="sxs-lookup"><span data-stu-id="1f675-104">By including parameters in an expression, you can customize report data and appearance based on choices a user makes.</span></span> <span data-ttu-id="1f675-105">運算式可用於提供 (*Fx*) 或選項的任何報表專案屬性或文字方塊屬性 \<**Expression**> 。</span><span class="sxs-lookup"><span data-stu-id="1f675-105">Expressions can be used for any report item property or text box property that provides the (*Fx*) or \<**Expression**> option.</span></span> <span data-ttu-id="1f675-106">您也可以用其他方法來使用運算式控制報表的內容及外觀。</span><span class="sxs-lookup"><span data-stu-id="1f675-106">Expressions are also used to control report content and appearance in other ways.</span></span> <span data-ttu-id="1f675-107">如需詳細資訊，請參閱[運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)。</span><span class="sxs-lookup"><span data-stu-id="1f675-107">For more information, see [Expression Examples &#40;Report Builder and SSRS&#41;](expression-examples-report-builder-and-ssrs.md).</span></span>  
  
 <span data-ttu-id="1f675-108">在執行階段比較參數值與資料集欄位值時，所比較的兩個項目的資料類型必須相同。</span><span class="sxs-lookup"><span data-stu-id="1f675-108">When you compare parameter values with dataset field values at run time, the data types for the two items you are comparing must be the same.</span></span> <span data-ttu-id="1f675-109">報表參數可以是以下其中一個類型：布林、日期時間、整數、浮點數或文字 (代表基礎資料類型「字串」)。</span><span class="sxs-lookup"><span data-stu-id="1f675-109">Report parameters can be one of the following types: Boolean, DateTime, Integer, Float, or Text, which represents the underlying data type String.</span></span> <span data-ttu-id="1f675-110">如有必要，也可以將參數值的資料類型轉換成符合資料集值。</span><span class="sxs-lookup"><span data-stu-id="1f675-110">If necessary, you might have to convert the data type of the parameter value to match the dataset value.</span></span> <span data-ttu-id="1f675-111">如需詳細資訊，請參閱 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)。</span><span class="sxs-lookup"><span data-stu-id="1f675-111">For more information, see [Data Types in Expressions &#40;Report Builder and SSRS&#41;](expressions-report-builder-and-ssrs.md).</span></span>  
  
 <span data-ttu-id="1f675-112">若要在運算式中包含參數參考，您必須了解如何指定參數參考的正確語法，此語法會根據參數是單一值或多重值參數而改變。</span><span class="sxs-lookup"><span data-stu-id="1f675-112">In order to include a parameter reference in an expression, you must understand how to specify the correct syntax for the parameter reference, which varies depending on whether the parameter is a single-value or multivalue parameter.</span></span>  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="using-a-single-valued-parameter-in-an-expression"></a><a name="Single"></a> <span data-ttu-id="1f675-113">在運算式中使用單一值參數</span><span class="sxs-lookup"><span data-stu-id="1f675-113">Using a Single-Valued Parameter in an Expression</span></span>  
 <span data-ttu-id="1f675-114">下表顯示當您在運算式中加入任何資料類型之單一值參數的參考時，所要使用的語法範例。</span><span class="sxs-lookup"><span data-stu-id="1f675-114">The following table shows examples of the syntax to use when you include a reference to a single-value parameter of any data type in an expression.</span></span>  
  
|<span data-ttu-id="1f675-115">範例</span><span class="sxs-lookup"><span data-stu-id="1f675-115">Example</span></span>|<span data-ttu-id="1f675-116">描述</span><span class="sxs-lookup"><span data-stu-id="1f675-116">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="1f675-117">`=Parameters!` *\<ParameterName>* `.IsMultiValue`</span><span class="sxs-lookup"><span data-stu-id="1f675-117">`=Parameters!` *\<ParameterName>* `.IsMultiValue`</span></span>|<span data-ttu-id="1f675-118">傳回 `False`。</span><span class="sxs-lookup"><span data-stu-id="1f675-118">Returns `False`.</span></span><br /><br /> <span data-ttu-id="1f675-119">檢查參數是否為多重值。</span><span class="sxs-lookup"><span data-stu-id="1f675-119">Checks if a parameter is multivalue.</span></span> <span data-ttu-id="1f675-120">如果為 `True`，表示參數為多重值，且為物件的集合。</span><span class="sxs-lookup"><span data-stu-id="1f675-120">If `True`, the parameter is multivalue and it is a collection of objects.</span></span> <span data-ttu-id="1f675-121">如果為 `False`，表示參數為單一值，且為單一物件。</span><span class="sxs-lookup"><span data-stu-id="1f675-121">If `False`, the parameter is single-value and is a single object.</span></span>|  
|<span data-ttu-id="1f675-122">`=Parameters!` *\<ParameterName>* `.Count`</span><span class="sxs-lookup"><span data-stu-id="1f675-122">`=Parameters!` *\<ParameterName>* `.Count`</span></span>|<span data-ttu-id="1f675-123">傳回整數值 1。</span><span class="sxs-lookup"><span data-stu-id="1f675-123">Returns the integer value 1.</span></span> <span data-ttu-id="1f675-124">如果是單一值參數，此計數一定會是 1。</span><span class="sxs-lookup"><span data-stu-id="1f675-124">For a single-value parameter, the count is always 1.</span></span>|  
|<span data-ttu-id="1f675-125">`=Parameters!` *\<ParameterName>* `.Label`</span><span class="sxs-lookup"><span data-stu-id="1f675-125">`=Parameters!` *\<ParameterName>* `.Label`</span></span>|<span data-ttu-id="1f675-126">會傳回參數標籤，經常當做可用值下拉式清單中的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="1f675-126">Returns the parameter label, frequently used as the display name in a drop-down list of available values.</span></span>|  
|<span data-ttu-id="1f675-127">`=Parameters!` *\<ParameterName>* `.Value`</span><span class="sxs-lookup"><span data-stu-id="1f675-127">`=Parameters!` *\<ParameterName>* `.Value`</span></span>|<span data-ttu-id="1f675-128">會傳回參數值。</span><span class="sxs-lookup"><span data-stu-id="1f675-128">Returns the parameter value.</span></span> <span data-ttu-id="1f675-129">如果尚未設定 Label 屬性，這個值會出現在可用值下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="1f675-129">If the Label property has not been set, this value appears in the drop-down list of available values.</span></span>|  
|<span data-ttu-id="1f675-130">`=CStr(Parameters!`  *\<ParameterName>* `.Value)`</span><span class="sxs-lookup"><span data-stu-id="1f675-130">`=CStr(Parameters!`  *\<ParameterName>* `.Value)`</span></span>|<span data-ttu-id="1f675-131">會傳回字串形式的參數值。</span><span class="sxs-lookup"><span data-stu-id="1f675-131">Returns the parameter value as a string.</span></span>|  
|<span data-ttu-id="1f675-132">`=Fields(Parameters!` *\<ParameterName>* `.Value).Value`</span><span class="sxs-lookup"><span data-stu-id="1f675-132">`=Fields(Parameters!` *\<ParameterName>* `.Value).Value`</span></span>|<span data-ttu-id="1f675-133">會傳回與參數同名之欄位的值。</span><span class="sxs-lookup"><span data-stu-id="1f675-133">Returns the value for the field that has the same name as the parameter.</span></span>|  
  
 <span data-ttu-id="1f675-134">如需在篩選中使用參數的詳細資訊，請參閱[新增資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)。</span><span class="sxs-lookup"><span data-stu-id="1f675-134">For more information about using parameters in a filter, see [Add Dataset Filters, Data Region Filters, and Group Filters &#40;Report Builder and SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md).</span></span>  
  
##  <a name="using-a-multivalue-parameter-in-an-expression"></a><a name="Multi"></a> <span data-ttu-id="1f675-135">在運算式中使用多重值參數</span><span class="sxs-lookup"><span data-stu-id="1f675-135">Using a Multivalue Parameter in an Expression</span></span>  
 <span data-ttu-id="1f675-136">下表顯示當您在運算式中加入任何資料類型之多重值參數的參考時，所要使用的語法範例。</span><span class="sxs-lookup"><span data-stu-id="1f675-136">The following table shows examples of the syntax to use when you include a reference to a multivalue parameter of any data type in an expression.</span></span>  
  
|<span data-ttu-id="1f675-137">範例</span><span class="sxs-lookup"><span data-stu-id="1f675-137">Example</span></span>|<span data-ttu-id="1f675-138">描述</span><span class="sxs-lookup"><span data-stu-id="1f675-138">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="1f675-139">`=Parameters!` *\<MultivalueParameterName>* `.IsMultiValue`</span><span class="sxs-lookup"><span data-stu-id="1f675-139">`=Parameters!` *\<MultivalueParameterName>* `.IsMultiValue`</span></span>|<span data-ttu-id="1f675-140">傳回 `True` 或 `False`。</span><span class="sxs-lookup"><span data-stu-id="1f675-140">Returns `True` or `False`.</span></span><br /><br /> <span data-ttu-id="1f675-141">檢查參數是否為多重值。</span><span class="sxs-lookup"><span data-stu-id="1f675-141">Checks if a parameter is multivalue.</span></span> <span data-ttu-id="1f675-142">如果為 `True`，表示參數為多重值，且為物件的集合。</span><span class="sxs-lookup"><span data-stu-id="1f675-142">If `True`, the parameter is multivalue and is a collection of objects.</span></span> <span data-ttu-id="1f675-143">如果為 `False`，表示參數為單一值，且為單一物件。</span><span class="sxs-lookup"><span data-stu-id="1f675-143">If `False`, the parameter is single-valued and is a single object.</span></span>|  
|<span data-ttu-id="1f675-144">`=Parameters!` *\<MultivalueParameterName>* `.Count`</span><span class="sxs-lookup"><span data-stu-id="1f675-144">`=Parameters!` *\<MultivalueParameterName>* `.Count`</span></span>|<span data-ttu-id="1f675-145">傳回整數值。</span><span class="sxs-lookup"><span data-stu-id="1f675-145">Returns an integer value.</span></span><br /><br /> <span data-ttu-id="1f675-146">參考值的數目。</span><span class="sxs-lookup"><span data-stu-id="1f675-146">Refers to the number of values.</span></span> <span data-ttu-id="1f675-147">如果是單一值參數，此計數一定會是 1。</span><span class="sxs-lookup"><span data-stu-id="1f675-147">For a single-value parameter, the count is always 1.</span></span> <span data-ttu-id="1f675-148">如果是多重值參數，此計數是 0 或以上。</span><span class="sxs-lookup"><span data-stu-id="1f675-148">For a multivalue parameter, the count is 0 or more.</span></span>|  
|<span data-ttu-id="1f675-149">`=Parameters!` *\<MultivalueParameterName>* `.Value(0)`</span><span class="sxs-lookup"><span data-stu-id="1f675-149">`=Parameters!` *\<MultivalueParameterName>* `.Value(0)`</span></span>|<span data-ttu-id="1f675-150">傳回多重值參數中的第一個值。</span><span class="sxs-lookup"><span data-stu-id="1f675-150">Returns the first value in a multivalue parameter.</span></span>|  
|<span data-ttu-id="1f675-151">`=Parameters!` *\<MultivalueParameterName>* `.Value(Parameters!` *\<MultivalueParameterName>* `.Count-1)`</span><span class="sxs-lookup"><span data-stu-id="1f675-151">`=Parameters!` *\<MultivalueParameterName>* `.Value(Parameters!` *\<MultivalueParameterName>* `.Count-1)`</span></span>|<span data-ttu-id="1f675-152">傳回多重值參數中的最後一個值。</span><span class="sxs-lookup"><span data-stu-id="1f675-152">Returns the last value in a multivalue parameter.</span></span>|  
|`=Split("Value1,Value2,Value3",",")`|<span data-ttu-id="1f675-153">傳回數值的陣列。</span><span class="sxs-lookup"><span data-stu-id="1f675-153">Returns an array of values.</span></span><br /><br /> <span data-ttu-id="1f675-154">針對多重值的 `String` 參數建立數值陣列。</span><span class="sxs-lookup"><span data-stu-id="1f675-154">Create an array of values for a multivalue `String` parameter.</span></span> <span data-ttu-id="1f675-155">您可以在第二個參數中使用任何分隔符號來分隔。</span><span class="sxs-lookup"><span data-stu-id="1f675-155">You can use any delimiter in the second parameter to Split.</span></span> <span data-ttu-id="1f675-156">這個運算式可用來設定多重值參數的預設值或是建立多重值參數，以傳送至子報表或鑽研報表。</span><span class="sxs-lookup"><span data-stu-id="1f675-156">This expression can be used to set defaults for a multivalue parameter or to create a multivalue parameter to send to a subreport or drillthrough report.</span></span>|  
|<span data-ttu-id="1f675-157">`=Join(Parameters!` *\<MultivalueParameterName>* `.Value,", ")`</span><span class="sxs-lookup"><span data-stu-id="1f675-157">`=Join(Parameters!` *\<MultivalueParameterName>* `.Value,", ")`</span></span>|<span data-ttu-id="1f675-158">傳回 `String`，此值是由多重值參數中以逗號分隔的值清單所組成。</span><span class="sxs-lookup"><span data-stu-id="1f675-158">Returns a `String` that consists of a comma-delimited list of values in a multivalue parameter.</span></span> <span data-ttu-id="1f675-159">您可以在第二個參數中使用任何分隔符號來聯結。</span><span class="sxs-lookup"><span data-stu-id="1f675-159">You can use any delimiter in the second parameter to Join.</span></span>|  
  
 <span data-ttu-id="1f675-160">如需在篩選中使用參數的詳細資訊，請參閱[報表參數 &#40;報表產生器和報表設計師&#41;](report-parameters-report-builder-and-report-designer.md)。</span><span class="sxs-lookup"><span data-stu-id="1f675-160">For more information about using parameters in a filter, see [Report Parameters &#40;Report Builder and Report Designer&#41;](report-parameters-report-builder-and-report-designer.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1f675-161">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1f675-161">See Also</span></span>  
 <span data-ttu-id="1f675-162">[運算式 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md) </span><span class="sxs-lookup"><span data-stu-id="1f675-162">[Expressions &#40;Report Builder and SSRS&#41;](expressions-report-builder-and-ssrs.md) </span></span>  
 <span data-ttu-id="1f675-163">[常用的篩選 &#40;報表產生器及 SSRS&#41;](commonly-used-filters-report-builder-and-ssrs.md) </span><span class="sxs-lookup"><span data-stu-id="1f675-163">[Commonly Used Filters &#40;Report Builder and SSRS&#41;](commonly-used-filters-report-builder-and-ssrs.md) </span></span>  
 <span data-ttu-id="1f675-164">[加入、變更或刪除報表參數 &#40;報表產生器及 SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md) </span><span class="sxs-lookup"><span data-stu-id="1f675-164">[Add, Change, or Delete a Report Parameter &#40;Report Builder and SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md) </span></span>  
 <span data-ttu-id="1f675-165">[教學課程：將參數新增至報表 &#40;報表產生器&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md) </span><span class="sxs-lookup"><span data-stu-id="1f675-165">[Tutorial: Add a Parameter to Your Report &#40;Report Builder&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md) </span></span>  
 <span data-ttu-id="1f675-166">[教學課程 &#40;報表產生器&#41;](../report-builder-tutorials.md) </span><span class="sxs-lookup"><span data-stu-id="1f675-166">[Tutorials &#40;Report Builder&#41;](../report-builder-tutorials.md) </span></span>  
 [<span data-ttu-id="1f675-167">運算式中的內建集合 &#40;報表產生器及 SSRS&#41;</span><span class="sxs-lookup"><span data-stu-id="1f675-167">Built-in Collections in Expressions &#40;Report Builder and SSRS&#41;</span></span>](built-in-collections-in-expressions-report-builder.md)  
  
  