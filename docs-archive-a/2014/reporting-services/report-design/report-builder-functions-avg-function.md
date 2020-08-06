---
title: Avg 函式 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f1276c4c-bb44-44c0-a1bf-386a0c340003
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cfa9d3517e3b3b0c2e4e01853ffa30295ec343df
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87704890"
---
# <a name="avg-function-report-builder-and-ssrs"></a><span data-ttu-id="14e50-102">Avg 函數 (報表產生器及 SSRS)</span><span class="sxs-lookup"><span data-stu-id="14e50-102">Avg Function (Report Builder and SSRS)</span></span>
  <span data-ttu-id="14e50-103">傳回運算式指定的所有非 Null 數值的平均值 (在給定範圍中評估)。</span><span class="sxs-lookup"><span data-stu-id="14e50-103">Returns the average of all non-null numeric values specified by the expression, evaluated in the given scope.</span></span>  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a><span data-ttu-id="14e50-104">語法</span><span class="sxs-lookup"><span data-stu-id="14e50-104">Syntax</span></span>  
  
```  
  
Avg(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a><span data-ttu-id="14e50-105">參數</span><span class="sxs-lookup"><span data-stu-id="14e50-105">Parameters</span></span>  
 <span data-ttu-id="14e50-106">*expression*</span><span class="sxs-lookup"><span data-stu-id="14e50-106">*expression*</span></span>  
 <span data-ttu-id="14e50-107">(`Float`) 要在其上執行彙總的運算式。</span><span class="sxs-lookup"><span data-stu-id="14e50-107">(`Float`) The expression on which to perform the aggregation.</span></span>  
  
 <span data-ttu-id="14e50-108">*範圍 (scope)*</span><span class="sxs-lookup"><span data-stu-id="14e50-108">*scope*</span></span>  
 <span data-ttu-id="14e50-109">(`String`) 選擇性。</span><span class="sxs-lookup"><span data-stu-id="14e50-109">(`String`) Optional.</span></span> <span data-ttu-id="14e50-110">包含要套用彙總函式之報表項目的資料集、群組或資料區的名稱。</span><span class="sxs-lookup"><span data-stu-id="14e50-110">The name of a dataset, group, or data region that contains the report items to which to apply the aggregate function.</span></span> <span data-ttu-id="14e50-111">如果未指定 *scope* ，則使用目前的範圍。</span><span class="sxs-lookup"><span data-stu-id="14e50-111">If *scope* is not specified, the current scope is used.</span></span>  
  
 <span data-ttu-id="14e50-112">*遞迴*</span><span class="sxs-lookup"><span data-stu-id="14e50-112">*recursive*</span></span>  
 <span data-ttu-id="14e50-113">(**列舉型別**) 選擇性。</span><span class="sxs-lookup"><span data-stu-id="14e50-113">(**Enumerated Type**) Optional.</span></span> <span data-ttu-id="14e50-114">`Simple` (預設值) 或 `RdlRecursive`。</span><span class="sxs-lookup"><span data-stu-id="14e50-114">`Simple` (default) or `RdlRecursive`.</span></span> <span data-ttu-id="14e50-115">指定是否要以遞迴方式執行彙總。</span><span class="sxs-lookup"><span data-stu-id="14e50-115">Specifies whether to perform the aggregation recursively.</span></span>  
  
## <a name="return-type"></a><span data-ttu-id="14e50-116">傳回類型</span><span class="sxs-lookup"><span data-stu-id="14e50-116">Return Type</span></span>  
 <span data-ttu-id="14e50-117">十進位運算式會傳回 `Decimal`，所有其他運算式都會傳回 `Double`。</span><span class="sxs-lookup"><span data-stu-id="14e50-117">Returns a `Decimal` for decimal expressions and a `Double` for all other expressions.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="14e50-118">備註</span><span class="sxs-lookup"><span data-stu-id="14e50-118">Remarks</span></span>  
 <span data-ttu-id="14e50-119">運算式中指定的資料集必須具有相同的資料類型。</span><span class="sxs-lookup"><span data-stu-id="14e50-119">The set of data specified in the expression must have the same data type.</span></span> <span data-ttu-id="14e50-120">若要將具有多個數值資料類型的資料轉換成相同的資料類型，請使用 `CInt`、`CDbl` 或 `CDec` 等轉換函數。</span><span class="sxs-lookup"><span data-stu-id="14e50-120">To convert data that has multiple numeric data types to the same data type, use conversion functions like `CInt`, `CDbl` or `CDec`.</span></span> <span data-ttu-id="14e50-121">如需詳細資訊，請參閱 [類型轉換函數](https://go.microsoft.com/fwlink/?LinkId=96142)。</span><span class="sxs-lookup"><span data-stu-id="14e50-121">For more information, see [Type Conversion Functions](https://go.microsoft.com/fwlink/?LinkId=96142).</span></span>  
  
 <span data-ttu-id="14e50-122">*scope* 的值必須是字串常數，而且不得為運算式。</span><span class="sxs-lookup"><span data-stu-id="14e50-122">The value of *scope* must be a string constant and cannot be an expression.</span></span> <span data-ttu-id="14e50-123">如果是未指定其他彙總的外部彙總， *scope* 必須參考目前的範圍或是包含的範圍。</span><span class="sxs-lookup"><span data-stu-id="14e50-123">For outer aggregates or aggregates that do not specify other aggregates, *scope* must refer to the current scope or a containing scope.</span></span> <span data-ttu-id="14e50-124">如果是彙總的彙總，巢狀彙總可以指定子範圍。</span><span class="sxs-lookup"><span data-stu-id="14e50-124">For aggregates of aggregates, nested aggregates can specify a child scope.</span></span>  
  
 <span data-ttu-id="14e50-125">*Expression* 可以包含巢狀彙總函式的呼叫，其中包含下列例外和條件：</span><span class="sxs-lookup"><span data-stu-id="14e50-125">*Expression* can contain calls to nested aggregate functions with the following exceptions and conditions:</span></span>  
  
-   <span data-ttu-id="14e50-126">巢狀彙總的*Scope* 必須與外部彙總的範圍相同或是由外部彙總的範圍所限制。</span><span class="sxs-lookup"><span data-stu-id="14e50-126">*Scope* for nested aggregates must be the same as, or contained by, the scope of the outer aggregate.</span></span> <span data-ttu-id="14e50-127">如果是運算式中的所有相異範圍，一個範圍必須與所有其他範圍之間具有子關聯性。</span><span class="sxs-lookup"><span data-stu-id="14e50-127">For all distinct scopes in the expression, one scope must be in a child relationship to all other scopes.</span></span>  
  
-   <span data-ttu-id="14e50-128">巢狀彙總的*Scope* 不得為資料集的名稱。</span><span class="sxs-lookup"><span data-stu-id="14e50-128">*Scope* for nested aggregates cannot be the name of a dataset.</span></span>  
  
-   <span data-ttu-id="14e50-129">*運算式*不能包含 `First` 、 `Last` 、 `Previous` 或 `RunningValue` 函數。</span><span class="sxs-lookup"><span data-stu-id="14e50-129">*Expression* must not contain `First`, `Last`, `Previous`, or `RunningValue` functions.</span></span>  
  
-   <span data-ttu-id="14e50-130">*Expression* 不得包含指定 *recursive*的巢狀彙總。</span><span class="sxs-lookup"><span data-stu-id="14e50-130">*Expression* must not contain nested aggregates that specify *recursive*.</span></span>  
  
 <span data-ttu-id="14e50-131">如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)。</span><span class="sxs-lookup"><span data-stu-id="14e50-131">For more information, see [Aggregate Functions Reference &#40;Report Builder and SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) and [Expression Scope for Totals, Aggregates, and Built-in Collections &#40;Report Builder and SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).</span></span>  
  
 <span data-ttu-id="14e50-132">如需遞迴彙總的詳細資訊，請參閱[建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。</span><span class="sxs-lookup"><span data-stu-id="14e50-132">For more information about recursive aggregates, see [Creating Recursive Hierarchy Groups &#40;Report Builder and SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="14e50-133">範例</span><span class="sxs-lookup"><span data-stu-id="14e50-133">Example</span></span>  
 <span data-ttu-id="14e50-134">下列兩個程式碼範例提供名為 `Cost` 的資料集所包含的 `Inventory`欄位中所有值的平均值。</span><span class="sxs-lookup"><span data-stu-id="14e50-134">The following two code examples provide an average of all values in the `Cost` field contained in a dataset named `Inventory`.</span></span>  
  
```  
=Avg(Fields!Cost.Value, "Inventory")   
  OR    
=Avg (CDbl(Fields!Cost.Value), "Inventory")  
```  
  
## <a name="see-also"></a><span data-ttu-id="14e50-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="14e50-135">See Also</span></span>  
 <span data-ttu-id="14e50-136">[報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md) </span><span class="sxs-lookup"><span data-stu-id="14e50-136">[Expression Uses in Reports &#40;Report Builder and SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md) </span></span>  
 <span data-ttu-id="14e50-137">[運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md) </span><span class="sxs-lookup"><span data-stu-id="14e50-137">[Expression Examples &#40;Report Builder and SSRS&#41;](expression-examples-report-builder-and-ssrs.md) </span></span>  
 <span data-ttu-id="14e50-138">[運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md) </span><span class="sxs-lookup"><span data-stu-id="14e50-138">[Data Types in Expressions &#40;Report Builder and SSRS&#41;](expressions-report-builder-and-ssrs.md) </span></span>  
 [<span data-ttu-id="14e50-139">總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;</span><span class="sxs-lookup"><span data-stu-id="14e50-139">Expression Scope for Totals, Aggregates, and Built-in Collections &#40;Report Builder and SSRS&#41;</span></span>](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  