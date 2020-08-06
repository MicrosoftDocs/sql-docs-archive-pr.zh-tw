---
title: 運算式中的 Integration Services 資料類型 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- expressions [Integration Services], data types
- data types [Integration Services], expressions
ms.assetid: c296ad10-4080-4988-8c2c-2c250f7a1884
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5b2921da7322c7511facacf3918368d8cd8f2fe6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87701449"
---
# <a name="integration-services-data-types-in-expressions"></a><span data-ttu-id="37e96-102">運算式中的 Integration Services 資料類型</span><span class="sxs-lookup"><span data-stu-id="37e96-102">Integration Services Data Types in Expressions</span></span>
  <span data-ttu-id="37e96-103">運算式評估工具使用 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 資料類型。</span><span class="sxs-lookup"><span data-stu-id="37e96-103">The expression evaluator uses [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] data types.</span></span> <span data-ttu-id="37e96-104">當資料初次進入 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 封裝中的資料流程時，資料流程引擎會將所有資料行的資料轉換成 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 資料類型，而運算式所使用的資料行資料已為 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 資料類型。</span><span class="sxs-lookup"><span data-stu-id="37e96-104">When data first enters a data flow in an [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] package, the data flow engine converts all column data to an [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] data type, and the column data that an expression uses already has an [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] data type.</span></span> <span data-ttu-id="37e96-105">「條件式分割」和「衍生的資料行」轉換中使用的運算式可參考資料行，因為它們是包含資料行資料的資料流程中的一部分。</span><span class="sxs-lookup"><span data-stu-id="37e96-105">Expressions used in the Conditional Split and the Derived Column transformations can reference columns because they are part of a data flow that includes column data.</span></span>

## <a name="variables"></a><span data-ttu-id="37e96-106">變數</span><span class="sxs-lookup"><span data-stu-id="37e96-106">Variables</span></span>
 <span data-ttu-id="37e96-107">運算式亦可使用變數。</span><span class="sxs-lookup"><span data-stu-id="37e96-107">Expressions can also use variables.</span></span> <span data-ttu-id="37e96-108">變數的資料類型為 Variant，且運算式評估工具會先將變數的資料類型從 Variant 子類型轉換成 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 資料類型，然後才評估運算式。</span><span class="sxs-lookup"><span data-stu-id="37e96-108">Variables have a Variant data type and the expression evaluator converts the data type of a variable from a Variant subtype to an [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] data type before it evaluates the expression.</span></span> <span data-ttu-id="37e96-109">變數只能使用 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 資料類型的子集。</span><span class="sxs-lookup"><span data-stu-id="37e96-109">Variables can use only a subset of the [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] data types.</span></span> <span data-ttu-id="37e96-110">例如，變數無法使用「二進位大型物件區塊」(Binary Large Object Block，BLOB) 資料類型。</span><span class="sxs-lookup"><span data-stu-id="37e96-110">For example, a variable cannot use a Binary Large Object Block (BLOB) data type.</span></span>

 <span data-ttu-id="37e96-111">如需 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 資料類型，以及將 Variant 資料類型對應到 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 資料類型的詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)。</span><span class="sxs-lookup"><span data-stu-id="37e96-111">For more information about [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] data types and the mapping of Variant data types to [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] data types, see [Integration Services Data Types](../data-flow/integration-services-data-types.md).</span></span>

## <a name="literals"></a><span data-ttu-id="37e96-112">常值</span><span class="sxs-lookup"><span data-stu-id="37e96-112">Literals</span></span>
 <span data-ttu-id="37e96-113">此外，運算式還可包含字串、布林，以及數值常值。</span><span class="sxs-lookup"><span data-stu-id="37e96-113">In addition, expressions can include string, Boolean, and numeric literals.</span></span> <span data-ttu-id="37e96-114">如需將數值常值轉換為數值 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 資料類型的詳細資訊，請參閱[常值 &#40;SSIS&#41;](numeric-string-and-boolean-literals.md)。</span><span class="sxs-lookup"><span data-stu-id="37e96-114">For more information about converting numeric literals to numeric [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] data types, see [Literals &#40;SSIS&#41;](numeric-string-and-boolean-literals.md).</span></span>

## <a name="implicit-data-conversion"></a><span data-ttu-id="37e96-115">隱含資料轉換</span><span class="sxs-lookup"><span data-stu-id="37e96-115">Implicit Data Conversion</span></span>
 <span data-ttu-id="37e96-116">當運算式評估工具自動將資料從一種資料類型轉換為另一種資料類型時，會發生資料類型的隱含轉換。</span><span class="sxs-lookup"><span data-stu-id="37e96-116">An implicit conversion of a data type occurs when the expression evaluator automatically converts the data from one data type to another.</span></span> <span data-ttu-id="37e96-117">例如，如果將 `smallint` 與 `int` 做比較，就會先將 `smallint` 隱含轉換成 `int`，然後再執行比較。</span><span class="sxs-lookup"><span data-stu-id="37e96-117">For example, if a `smallint` is compared to an `int`, the `smallint` is implicitly converted to `int` before the comparison is performed.</span></span>

 <span data-ttu-id="37e96-118">當引數和運算元的資料類型不相容時，運算式評估工具無法執行隱含資料轉換。</span><span class="sxs-lookup"><span data-stu-id="37e96-118">The expression evaluator cannot perform implicit data conversion when the arguments and operands have incompatible data types.</span></span> <span data-ttu-id="37e96-119">此外，運算式評估工具無法將任何值隱含轉換為布林。</span><span class="sxs-lookup"><span data-stu-id="37e96-119">In addition, the expression evaluator cannot implicitly convert any value to a Boolean.</span></span> <span data-ttu-id="37e96-120">而必須使用轉換運算子隱含轉換引數和運算元。</span><span class="sxs-lookup"><span data-stu-id="37e96-120">Instead, the arguments and operands must be explicitly converted by using the cast operator.</span></span> <span data-ttu-id="37e96-121">如需詳細資訊，請參閱 [Cast &#40;SSIS 運算式&#41;](cast-ssis-expression.md)。</span><span class="sxs-lookup"><span data-stu-id="37e96-121">For more information, see [Cast &#40;SSIS Expression&#41;](cast-ssis-expression.md).</span></span>

 <span data-ttu-id="37e96-122">下圖顯示 BINARY 運算之隱含轉換的結果類型。</span><span class="sxs-lookup"><span data-stu-id="37e96-122">The following diagram shows the result type of implicit conversions of BINARY operations.</span></span> <span data-ttu-id="37e96-123">此資料表中資料行和資料列的交集為具有左 (從) 和右 (至) 類型之運算元的二進位運算結果類型。</span><span class="sxs-lookup"><span data-stu-id="37e96-123">The intersection of column and row in this table is the result type of a binary operation with operands of the left (From) and right (To) types.</span></span>

 <span data-ttu-id="37e96-124">![資料類型之間的隱含資料類型轉換](../media/mw-dts-impl-conver-02.gif "資料類型之間的隱含資料類型轉換")</span><span class="sxs-lookup"><span data-stu-id="37e96-124">![Implicit data type conversion between data types](../media/mw-dts-impl-conver-02.gif "Implicit data type conversion between data types")</span></span>

 <span data-ttu-id="37e96-125">帶正負號和不帶正負號的整數之間的交集，應是大於任一引數的帶正負號整數。</span><span class="sxs-lookup"><span data-stu-id="37e96-125">The intersection of a signed and an unsigned integer is a signed integer that is potentially larger than either argument.</span></span>

 <span data-ttu-id="37e96-126">運算子會比較字串、日期、布林和其他資料類型。</span><span class="sxs-lookup"><span data-stu-id="37e96-126">Operators compare strings, dates, Booleans, and other data types.</span></span> <span data-ttu-id="37e96-127">在運算子比較兩個值之前，運算式評估工具會先執行某些隱含轉換。</span><span class="sxs-lookup"><span data-stu-id="37e96-127">Before an operator compares two values, the expression evaluator performs certain implicit conversions.</span></span> <span data-ttu-id="37e96-128">運算式評估工具會固定將字串常值轉換為 DT_WSTR 資料類型，以及將布林常值轉換為 DT_BOOL 資料類型。</span><span class="sxs-lookup"><span data-stu-id="37e96-128">The expression evaluator always converts string literals to the DT_WSTR data type and converts Boolean literals to the DT_BOOL data type.</span></span> <span data-ttu-id="37e96-129">運算式評估工具會將所有加上引號的值解譯為字串。</span><span class="sxs-lookup"><span data-stu-id="37e96-129">The expression evaluator interprets all values enclosed in quotation marks as strings.</span></span> <span data-ttu-id="37e96-130">數值常值會轉換為其中一種數值 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 資料類型。</span><span class="sxs-lookup"><span data-stu-id="37e96-130">Numeric literals are converted to one of the numeric [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] data types.</span></span>

> [!NOTE]
>  <span data-ttu-id="37e96-131">布林值是邏輯值，而非數字。</span><span class="sxs-lookup"><span data-stu-id="37e96-131">Boolean values are logical values, not numbers.</span></span> <span data-ttu-id="37e96-132">雖然布林值可以在某些環境下顯示為數字，但不會儲存為數字，而且不同的程式設計語言將布林值表示成數值的方式各有不同，.NET Framework 方法也是如此。</span><span class="sxs-lookup"><span data-stu-id="37e96-132">Although Boolean values may be displayed as numbers in some environments, they are not stored as numbers, and various programming languages represent Boolean values as numeric values differently, as do the .NET Framework methods.</span></span>
> 
>  <span data-ttu-id="37e96-133">例如，Visual Basic 提供的轉換函數會將 `True` 轉換為 -1；然而 .NET Framework 中的 `System.Convert.ToInt32` 方法會將 `True` 轉換為 +1。</span><span class="sxs-lookup"><span data-stu-id="37e96-133">For example, the conversion functions available in Visual Basic convert `True` to -1; however, the `System.Convert.ToInt32` method in the .NET Framework converts `True` to +1.</span></span> <span data-ttu-id="37e96-134">[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 運算式語言則會將 `True` 轉換為 -1。</span><span class="sxs-lookup"><span data-stu-id="37e96-134">The [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] Expression Language converts `True` to -1.</span></span>
> 
>  <span data-ttu-id="37e96-135">若要避免錯誤或非預期結果，您所撰寫的程式碼不應該以特定數值表示 `True` 和 `False`。</span><span class="sxs-lookup"><span data-stu-id="37e96-135">To avoid errors or unexpected results, you should not write code that relies on particular numeric values for `True` and `False`.</span></span> <span data-ttu-id="37e96-136">您應該盡可能將布林變數的使用限制在當初所設計的邏輯值上。</span><span class="sxs-lookup"><span data-stu-id="37e96-136">Wherever possible, you should restrict usage of Boolean variables to the logical values for which they are designed.</span></span>

 <span data-ttu-id="37e96-137">如需詳細資訊，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="37e96-137">For more information, see the following topics:</span></span>

-   [<span data-ttu-id="37e96-138">== &#40;等於&#41; &#40;SSIS 運算式&#41;</span><span class="sxs-lookup"><span data-stu-id="37e96-138">== &#40;Equal&#41; &#40;SSIS Expression&#41;</span></span>](equal-ssis-expression.md)

-   [<span data-ttu-id="37e96-139">！ = &#40;SSIS 運算式&#41; &#40;不相等&#41;</span><span class="sxs-lookup"><span data-stu-id="37e96-139">!= &#40;Unequal&#41; &#40;SSIS Expression&#41;</span></span>](unequal-ssis-expression.md)

-   [<span data-ttu-id="37e96-140">&#62; &#40;大於&#41; &#40;SSIS 運算式&#41;</span><span class="sxs-lookup"><span data-stu-id="37e96-140">&#62; &#40;Greater Than&#41; &#40;SSIS Expression&#41;</span></span>](greater-than-ssis-expression.md)

-   [<span data-ttu-id="37e96-141">&#60; &#40;小於&#41; &#40;SSIS 運算式&#41;</span><span class="sxs-lookup"><span data-stu-id="37e96-141">&#60; &#40;Less Than&#41; &#40;SSIS Expression&#41;</span></span>](less-than-ssis-expression.md)

-   [<span data-ttu-id="37e96-142">&#62;= &#40;大於或等於&#41; &#40;SSIS 運算式&#41;</span><span class="sxs-lookup"><span data-stu-id="37e96-142">&#62;= &#40;Greater Than or Equal To&#41; &#40;SSIS Expression&#41;</span></span>](greater-than-or-equal-to-ssis-expression.md)

-   [<span data-ttu-id="37e96-143">&#60;= &#40;小於或等於&#41; &#40;SSIS 運算式&#41;</span><span class="sxs-lookup"><span data-stu-id="37e96-143">&#60;= &#40;Less Than or Equal To&#41; &#40;SSIS Expression&#41;</span></span>](less-than-or-equal-to-ssis-expression.md)

 <span data-ttu-id="37e96-144">使用單一引數之函數所傳回的結果與引數具有相同資料類型，但有下列例外狀況：</span><span class="sxs-lookup"><span data-stu-id="37e96-144">A function that uses a single argument returns a result with the same data type as the argument, with the following exceptions:</span></span>

-   <span data-ttu-id="37e96-145">DAY、MONTH 和 YEAR 接受日期並傳回整數 (DT_I4) 結果。</span><span class="sxs-lookup"><span data-stu-id="37e96-145">DAY, MONTH, and YEAR accept a date and return an integer (DT_I4) result.</span></span>

-   <span data-ttu-id="37e96-146">ISNULL 接受任何 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 資料類型的運算式，並傳回布林 (DT_BOOL) 結果。</span><span class="sxs-lookup"><span data-stu-id="37e96-146">ISNULL accepts an expression of any [!INCLUDE[ssIS](../../includes/ssis-md.md)] data type and returns a Boolean (DT_BOOL) result.</span></span>

-   <span data-ttu-id="37e96-147">SQUARE 和 SQRT 接受數值運算式並傳回非整數的數值 (DT_R8) 結果。</span><span class="sxs-lookup"><span data-stu-id="37e96-147">SQUARE and SQRT accept a numeric expression and return a non-integral numeric (DT_R8) result.</span></span>

 <span data-ttu-id="37e96-148">如果引數的資料類型相同，則結果為該類型。</span><span class="sxs-lookup"><span data-stu-id="37e96-148">If the arguments have the same data type, the result is of that type.</span></span> <span data-ttu-id="37e96-149">唯一的例外為關於兩個 DT_DECIMAL 資料類型之值的二進位運算結果，其會傳回 DT_NUMERIC 資料類型的結果。</span><span class="sxs-lookup"><span data-stu-id="37e96-149">The only exception is the result of a binary operation on two values with the DT_DECIMAL data type, which returns a result with the DT_NUMERIC data type.</span></span>

## <a name="requirements-for-data-used-in-expressions"></a><span data-ttu-id="37e96-150">運算式中所用資料的需求</span><span class="sxs-lookup"><span data-stu-id="37e96-150">Requirements for Data Used in Expressions</span></span>
 <span data-ttu-id="37e96-151">運算式評估工具支援所有的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 資料類型。</span><span class="sxs-lookup"><span data-stu-id="37e96-151">The expression evaluator supports all [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] data types.</span></span> <span data-ttu-id="37e96-152">不過，根據運算和函數而定，運算元和引數會需要特定資料類型。</span><span class="sxs-lookup"><span data-stu-id="37e96-152">However, depending on the operation or the function, the operands and arguments require certain data types.</span></span> <span data-ttu-id="37e96-153">運算式評估工具對於運算式中使用的資料，有下列資料類型需求的規定︰</span><span class="sxs-lookup"><span data-stu-id="37e96-153">The expression evaluator imposes the following data type requirements on data used in expressions:</span></span>

-   <span data-ttu-id="37e96-154">**邏輯** 運算中使用的運算元評估結果必須為布林。</span><span class="sxs-lookup"><span data-stu-id="37e96-154">Operands used in **logical** operations must evaluate to a Boolean.</span></span> <span data-ttu-id="37e96-155">例如，ColumnA > 1&&ColumnB < 2。</span><span class="sxs-lookup"><span data-stu-id="37e96-155">For example, ColumnA > 1&&ColumnB < 2.</span></span>

-   <span data-ttu-id="37e96-156">**數學** 運算中使用的運算元評估結果必須為數值。</span><span class="sxs-lookup"><span data-stu-id="37e96-156">Operands used in **mathematical** operations must evaluate to a numeric value.</span></span> <span data-ttu-id="37e96-157">例如，23.75 \* 4。</span><span class="sxs-lookup"><span data-stu-id="37e96-157">For example, 23.75 \* 4.</span></span>

-   <span data-ttu-id="37e96-158">比較運算中使用的運算元 (例如邏輯和等式運算) 必須評估為相容的資料類型。</span><span class="sxs-lookup"><span data-stu-id="37e96-158">Operands used in comparison operations, such as logical and equality operations, must evaluate to compatible data types.</span></span>

     <span data-ttu-id="37e96-159">例如，下列範例中的其中一個運算式使用 DT_DBTIMESTAMPOFFSET 資料類型：</span><span class="sxs-lookup"><span data-stu-id="37e96-159">For example, one of the expressions in the following example uses the DT_DBTIMESTAMPOFFSET data type:</span></span>

     `(DT_DBTIMESTAMPOFFSET,3) "1999-10-11 20:34:52.123 -3:30" != (DT_DBDATE)"1999-10-12"`

     <span data-ttu-id="37e96-160">系統會將運算式 `(DT_DBDATE)"1999-10-12"`轉換為 DT_DBTIMESTAMPOFFSET。</span><span class="sxs-lookup"><span data-stu-id="37e96-160">The system converts the expression, `(DT_DBDATE)"1999-10-12"`, to DT_DBTIMESTAMPOFFSET.</span></span> <span data-ttu-id="37e96-161">轉換的運算式會變成 "1999-10-12 00:00:00.000 +00:00" (不等於其他運算式 `(DT_DBTIMESTAMPOFFSET,3) "1999-10-11 20:34:52.123 -3:30"`的值)，因此，此範例會評估為 TRUE。</span><span class="sxs-lookup"><span data-stu-id="37e96-161">The example evaluates to TRUE because the converted expression becomes "1999-10-12 00:00:00.000 +00:00", which is not equal to the value of the other expression, `(DT_DBTIMESTAMPOFFSET,3) "1999-10-11 20:34:52.123 -3:30"`.</span></span>

-   <span data-ttu-id="37e96-162">傳遞至數學函數的引數評估結果必須為數值資料類型。</span><span class="sxs-lookup"><span data-stu-id="37e96-162">Arguments passed to mathematical functions must evaluate to a numeric data type.</span></span> <span data-ttu-id="37e96-163">根據函數或運算而定，可能會需要特定的數值資料類型。</span><span class="sxs-lookup"><span data-stu-id="37e96-163">Depending on the function or operation, a specific numeric data type may be required.</span></span> <span data-ttu-id="37e96-164">例如，HEX 函數需要帶正負號或不帶正負號的整數。</span><span class="sxs-lookup"><span data-stu-id="37e96-164">For example, the HEX function requires a signed or unsigned integer.</span></span>

-   <span data-ttu-id="37e96-165">傳遞至字串函數的引數評估結果必須為字元資料類型︰DT_STR 或 DT_WSTR。</span><span class="sxs-lookup"><span data-stu-id="37e96-165">Arguments passed to string functions must evaluate to a character data type: DT_STR or DT_WSTR.</span></span> <span data-ttu-id="37e96-166">例如，UPPER("flower")。</span><span class="sxs-lookup"><span data-stu-id="37e96-166">For example, UPPER("flower").</span></span> <span data-ttu-id="37e96-167">某些字串函數 (例如 SUBSTRING) 的起始位置和字串長度需要額外的整數引數。</span><span class="sxs-lookup"><span data-stu-id="37e96-167">Some string functions, such as SUBSTRING, require additional integer arguments for the start position and the length of the string.</span></span>

-   <span data-ttu-id="37e96-168">傳遞至日期和時間函數的引數評估結果必須為有效的日期。</span><span class="sxs-lookup"><span data-stu-id="37e96-168">Arguments passed to date and time functions must evaluate to a valid date.</span></span> <span data-ttu-id="37e96-169">例如，DAY(GETDATE())。</span><span class="sxs-lookup"><span data-stu-id="37e96-169">For example, DAY(GETDATE()).</span></span> <span data-ttu-id="37e96-170">某些函數 (例如 DATEADD) 針對其加入至日期的日數，需要額外的整數引數。</span><span class="sxs-lookup"><span data-stu-id="37e96-170">Some functions, such as DATEADD, require an additional integer argument for the number of days the function adds to a date.</span></span>

 <span data-ttu-id="37e96-171">結合不帶正負號八位元組整數和帶正負號整數的運算需要明確轉換，才能明定結果格式。</span><span class="sxs-lookup"><span data-stu-id="37e96-171">Operations that combine an unsigned eight-byte integer and a signed integer require an explicit cast to clarify the result format.</span></span> <span data-ttu-id="37e96-172">如需詳細資訊，請參閱 [Cast &#40;SSIS 運算式&#41;](cast-ssis-expression.md)。</span><span class="sxs-lookup"><span data-stu-id="37e96-172">For more information, see [Cast &#40;SSIS Expression&#41;](cast-ssis-expression.md).</span></span>

 <span data-ttu-id="37e96-173">許多運算和函數的結果都需要預定的資料類型。</span><span class="sxs-lookup"><span data-stu-id="37e96-173">Results of many operations and functions have predetermined data types.</span></span> <span data-ttu-id="37e96-174">此資料類型可能是引數的資料類型，或運算式評估工具轉換結果的資料類型。</span><span class="sxs-lookup"><span data-stu-id="37e96-174">This can be the data type of the argument or the data type to which the expression evaluator casts the result.</span></span> <span data-ttu-id="37e96-175">例如，邏輯 OR 運算子 (||) 的結果固定為布林、ABS 函數的結果為引數的數值資料類型，而乘法的結果為可保留結果且不會遺失的最小數值資料類型。</span><span class="sxs-lookup"><span data-stu-id="37e96-175">For example, the result of a logical OR operator (||) is always a Boolean, the result of the ABS function is the numeric data type of the argument, and the result of multiplication is the smallest numeric data type that can hold the result without loss.</span></span> <span data-ttu-id="37e96-176">如需結果之資料類型的詳細資訊，請參閱[運算子 &#40;SSIS 運算式&#41;](operators-ssis-expression.md) 和[函數 &#40;SSIS 運算式&#41;](functions-ssis-expression.md)。</span><span class="sxs-lookup"><span data-stu-id="37e96-176">For more information about the data types of results, see [Operators &#40;SSIS Expression&#41;](operators-ssis-expression.md) and [Functions &#40;SSIS Expression&#41;](functions-ssis-expression.md).</span></span>

## <a name="related-tasks"></a><span data-ttu-id="37e96-177">相關工作</span><span class="sxs-lookup"><span data-stu-id="37e96-177">Related Tasks</span></span>
 [<span data-ttu-id="37e96-178">在資料流程元件中使用運算式</span><span class="sxs-lookup"><span data-stu-id="37e96-178">Use an Expression in a Data Flow Component</span></span>](../use-an-expression-in-a-data-flow-component.md)

## <a name="related-content"></a><span data-ttu-id="37e96-179">相關內容</span><span class="sxs-lookup"><span data-stu-id="37e96-179">Related Content</span></span>

-   <span data-ttu-id="37e96-180">pragmaticworks.com 上的技術文件： [SSIS 運算式小抄](https://pragmaticworks.com/Resources/Cheat-Sheets/SSIS-Expression-Cheat-Sheet3)</span><span class="sxs-lookup"><span data-stu-id="37e96-180">Technical article, [SSIS Expression Cheat Sheet](https://pragmaticworks.com/Resources/Cheat-Sheets/SSIS-Expression-Cheat-Sheet3), on pragmaticworks.com</span></span>

-   <span data-ttu-id="37e96-181">social.technet.microsoft.com 上的技術文件： [SSIS 運算式範例](https://go.microsoft.com/fwlink/?LinkId=220761)</span><span class="sxs-lookup"><span data-stu-id="37e96-181">Technical article, [SSIS Expression Examples](https://go.microsoft.com/fwlink/?LinkId=220761), on social.technet.microsoft.com</span></span>

