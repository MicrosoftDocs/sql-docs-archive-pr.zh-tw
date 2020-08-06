---
title: 資料集欄位集合 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: b3884576-1f7e-4d40-bb7d-168312333bb3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7850cb575ff50848c97fd4591835517853a0e2cc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687502"
---
# <a name="dataset-fields-collection-report-builder-and-ssrs"></a><span data-ttu-id="898ee-102">資料集欄位集合 (報表產生器及 SSRS)</span><span class="sxs-lookup"><span data-stu-id="898ee-102">Dataset Fields Collection (Report Builder and SSRS)</span></span>
  <span data-ttu-id="898ee-103">資料集欄位代表資料連接中的資料。</span><span class="sxs-lookup"><span data-stu-id="898ee-103">Dataset fields represent the data from a data connection.</span></span> <span data-ttu-id="898ee-104">欄位可以代表數值或非數值資料。</span><span class="sxs-lookup"><span data-stu-id="898ee-104">A field can represent either numeric or non-numeric data.</span></span> <span data-ttu-id="898ee-105">範例包括銷售量、總銷售額、客戶名稱、資料庫識別碼、URL、影像、空間資料及電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="898ee-105">Examples include sales amounts, total sales, customer names, database identifiers, URLs, images, spatial data, and e-mail addresses.</span></span> <span data-ttu-id="898ee-106">在設計介面上，欄位會以報表項目 (如文字方塊、資料表和圖表) 中的運算式形式出現。</span><span class="sxs-lookup"><span data-stu-id="898ee-106">On the design surface, fields appear as expressions in report items such as text boxes, tables, and charts.</span></span>  
  
 <span data-ttu-id="898ee-107">報表擁有三種類型的欄位，而且會將其顯示於 [報表資料] 窗格中：資料集欄位、資料集導出欄位和內建欄位。</span><span class="sxs-lookup"><span data-stu-id="898ee-107">A report has three types of fields and displays them in the Report Data pane: dataset fields, dataset calculated fields, and built-in fields.</span></span>  
  
-   <span data-ttu-id="898ee-108">**資料集欄位。**</span><span class="sxs-lookup"><span data-stu-id="898ee-108">**Dataset fields.**</span></span> <span data-ttu-id="898ee-109">代表欄位集合的中繼資料，當針對資料來源執行資料集查詢時，將會傳回這些欄位。</span><span class="sxs-lookup"><span data-stu-id="898ee-109">The metadata that represents the collection of fields that will be returned when the dataset query runs on the data source.</span></span>  
  
-   <span data-ttu-id="898ee-110">**資料集導出欄位。**</span><span class="sxs-lookup"><span data-stu-id="898ee-110">**Dataset calculated fields.**</span></span> <span data-ttu-id="898ee-111">您針對資料集建立的其他欄位。</span><span class="sxs-lookup"><span data-stu-id="898ee-111">Additional fields that you create for the dataset.</span></span> <span data-ttu-id="898ee-112">每一個導出欄位的建立方式都是藉由評估您所定義的運算式。</span><span class="sxs-lookup"><span data-stu-id="898ee-112">Each calculated field is created by evaluating an expression that you define.</span></span>  
  
-   <span data-ttu-id="898ee-113">**內建欄位。**</span><span class="sxs-lookup"><span data-stu-id="898ee-113">**Built-in fields.**</span></span> <span data-ttu-id="898ee-114">代表報表產生器所提供之欄位集合的中繼資料，這些欄位會在處理報表時提供報表資訊，例如報表名稱或時間。</span><span class="sxs-lookup"><span data-stu-id="898ee-114">The metadata that represents a collection of fields provided by Report Builder that provide report information such as the report name or the time when the report was processed.</span></span> <span data-ttu-id="898ee-115">如需詳細資訊，請參閱[內建的全域和使用者參考 &#40;報表產生器及 SSRS&#41;](../report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)。</span><span class="sxs-lookup"><span data-stu-id="898ee-115">For more information, see [Built-in Globals and Users References &#40;Report Builder and SSRS&#41;](../report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).</span></span>  
  
 <span data-ttu-id="898ee-116">資料集欄位名稱會當做報表資料集定義的一部分來儲存。</span><span class="sxs-lookup"><span data-stu-id="898ee-116">Dataset field names are saved as part of the report dataset definition.</span></span> <span data-ttu-id="898ee-117">如需詳細資訊，請參閱 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。</span><span class="sxs-lookup"><span data-stu-id="898ee-117">For more information, see [Report Embedded Datasets and Shared Datasets &#40;Report Builder and SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).</span></span>  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="dataset-fields-and-queries"></a><a name="Fields"></a> <span data-ttu-id="898ee-118">資料集欄位和查詢</span><span class="sxs-lookup"><span data-stu-id="898ee-118">Dataset Fields and Queries</span></span>  
 <span data-ttu-id="898ee-119">資料集欄位是由資料集查詢命令以及您所定義之任何導出欄位所指定。</span><span class="sxs-lookup"><span data-stu-id="898ee-119">Dataset fields are specified by the dataset query command and by any calculated fields that you define.</span></span> <span data-ttu-id="898ee-120">您在報表中看到的欄位集合取決於您具有的資料集類型：</span><span class="sxs-lookup"><span data-stu-id="898ee-120">The collection of fields that you see in your report depends on the type of dataset you have:</span></span>  
  
-   <span data-ttu-id="898ee-121">**共用資料集。**</span><span class="sxs-lookup"><span data-stu-id="898ee-121">**Shared dataset.**</span></span> <span data-ttu-id="898ee-122">欄位集合是當您直接將共用資料集加入報表，或是當您加入的報表組件已包含共用資料集時，共用資料集定義內查詢的欄位清單。</span><span class="sxs-lookup"><span data-stu-id="898ee-122">The field collection is the list of fields for the query in the shared dataset definition at the time that you directly added the shared dataset to your report, or when you added a report part that included the shared dataset.</span></span> <span data-ttu-id="898ee-123">當報表伺服器上的共用資料集定義變更時，本機欄位集合將不會變更。</span><span class="sxs-lookup"><span data-stu-id="898ee-123">The local field collection does not change when the shared dataset definition changes on the report server.</span></span> <span data-ttu-id="898ee-124">若要更新本機欄位集合，您必須重新整理本機共用資料集的清單。</span><span class="sxs-lookup"><span data-stu-id="898ee-124">To update the local field collection, you must refresh the list for the local shared dataset.</span></span>  
  
-   <span data-ttu-id="898ee-125">**內嵌資料集。**</span><span class="sxs-lookup"><span data-stu-id="898ee-125">**Embedded dataset.**</span></span> <span data-ttu-id="898ee-126">欄位集合是針對資料來源執行目前的查詢時所傳回的欄位清單。</span><span class="sxs-lookup"><span data-stu-id="898ee-126">The field collection is the list of fields that is returned from running the current query against the data source.</span></span>  
  
 <span data-ttu-id="898ee-127">如需詳細資訊，請參閱[加入、編輯、重新整理報表資料窗格中的欄位 &#40;報表產生器及 SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)</span><span class="sxs-lookup"><span data-stu-id="898ee-127">For more information see, [Add, Edit, Refresh Fields in the Report Data Pane &#40;Report Builder and SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)</span></span>  
  

  
### <a name="calculated-fields"></a><span data-ttu-id="898ee-128">導出欄位</span><span class="sxs-lookup"><span data-stu-id="898ee-128">Calculated Fields</span></span>  
 <span data-ttu-id="898ee-129">您可藉由建立運算式來手動指定導出欄位。</span><span class="sxs-lookup"><span data-stu-id="898ee-129">You specify a calculated field manually by creating an expression.</span></span> <span data-ttu-id="898ee-130">導出欄位可用來建立不存在於資料來源上的新值。</span><span class="sxs-lookup"><span data-stu-id="898ee-130">Calculated fields can be used to create new values that do not exist on the data source.</span></span> <span data-ttu-id="898ee-131">例如，導出欄位可代表新值、一組欄位值的自訂排序次序，或是轉換成另一個資料類型的現有欄位。</span><span class="sxs-lookup"><span data-stu-id="898ee-131">For example, a calculated field can represent a new value, a custom sort order for a set of field values, or an existing field that is converted to a different data type.</span></span>  
  
 <span data-ttu-id="898ee-132">導出欄位在報表的本機，而且不能儲存為共用資料集的一部分。</span><span class="sxs-lookup"><span data-stu-id="898ee-132">Calculated fields are local to a report and cannot be saved as part of a shared dataset.</span></span>  
  
 <span data-ttu-id="898ee-133">如需詳細資訊，請參閱[加入、編輯、重新整理報表資料窗格中的欄位 &#40;報表產生器及 SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)。</span><span class="sxs-lookup"><span data-stu-id="898ee-133">For more information, see [Add, Edit, Refresh Fields in the Report Data Pane &#40;Report Builder and SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).</span></span>  
  

  
### <a name="entities-and-entity-fields"></a><span data-ttu-id="898ee-134">實體和實體欄位</span><span class="sxs-lookup"><span data-stu-id="898ee-134">Entities and Entity Fields</span></span>  
 <span data-ttu-id="898ee-135">如果您正在處理報表模型資料來源，您可將實體和實體欄位指定為報表資料。</span><span class="sxs-lookup"><span data-stu-id="898ee-135">If you are working with a report model data source, you specify the entities and entity fields as your report data.</span></span> <span data-ttu-id="898ee-136">在報表模型的查詢設計工具中，您可以透過互動方式來瀏覽及選取相關實體，並選擇您要併入報表資料集的欄位。</span><span class="sxs-lookup"><span data-stu-id="898ee-136">In the query designer for a report model, you can interactively explore and select related entities and choose the fields that you want to include in your report dataset.</span></span> <span data-ttu-id="898ee-137">當您完成查詢的設計之後，您可以在 [報表資料] 窗格內查看實體識別碼和實體欄位的集合。</span><span class="sxs-lookup"><span data-stu-id="898ee-137">After you finish designing the query, you can see the collection of entity identifiers and entity fields in the Report Data pane.</span></span> <span data-ttu-id="898ee-138">實體識別碼是由報表模型自動產生，通常不會對使用者顯示。</span><span class="sxs-lookup"><span data-stu-id="898ee-138">Entity identifiers are generated automatically by the report model and are typically not displayed for the end user.</span></span>  
  
### <a name="using-extended-field-properties"></a><span data-ttu-id="898ee-139">使用擴充欄位屬性</span><span class="sxs-lookup"><span data-stu-id="898ee-139">Using Extended Field Properties</span></span>  
 <span data-ttu-id="898ee-140">支援多維度查詢的資料來源 (例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]) 可支援欄位上欄位屬性。</span><span class="sxs-lookup"><span data-stu-id="898ee-140">Data sources that support multidimensional queries, such as [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], support field properties on fields.</span></span> <span data-ttu-id="898ee-141">欄位屬性會出現在查詢的結果集中，但是在 **[報表資料]** 窗格中則看不到。</span><span class="sxs-lookup"><span data-stu-id="898ee-141">Field properties appear in the result set for a query, but are not visible in the **Report Data** pane.</span></span> <span data-ttu-id="898ee-142">欄位屬性仍然可供您的報表使用。</span><span class="sxs-lookup"><span data-stu-id="898ee-142">They are still available to use in your report.</span></span> <span data-ttu-id="898ee-143">若要參考欄位的屬性，請將欄位拖曳到報表上，然後將預設屬性 `Value` 變更為您想要之屬性的欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="898ee-143">To refer to a property for a field, drag the field onto the report, and change the default property `Value` to the field name of the property you want.</span></span> <span data-ttu-id="898ee-144">例如在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Cube 中，您可以針對 Cube 資料格中的值來定義格式。</span><span class="sxs-lookup"><span data-stu-id="898ee-144">For example, in an [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cube, you can define formats for values in the cube cells.</span></span> <span data-ttu-id="898ee-145">可以使用欄位屬性 `FormattedValue` 來取得格式化的值。</span><span class="sxs-lookup"><span data-stu-id="898ee-145">The formatted value is available by using the field property `FormattedValue`.</span></span> <span data-ttu-id="898ee-146">若要直接使用該值，而不是使用值並設定文字方塊的格式屬性，請將欄位拖曳到文字方塊，並將預設運算式 `=Fields!FieldName.Value` 變更為 `=Fields!FieldName.FormattedValue`。</span><span class="sxs-lookup"><span data-stu-id="898ee-146">To use the value directly instead of using a value and setting the format property of the text box, drag the field to the text box and change the default expression `=Fields!FieldName.Value` to `=Fields!FieldName.FormattedValue`.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="898ee-147">並非所有 `Field` 屬性都可用於所有資料來源。</span><span class="sxs-lookup"><span data-stu-id="898ee-147">Not all `Field` properties can be used for all data sources.</span></span> <span data-ttu-id="898ee-148"> 和  屬性是為所有資料來源定義的。</span><span class="sxs-lookup"><span data-stu-id="898ee-148">The `Value` and `IsMissing` properties are defined for all data sources.</span></span> <span data-ttu-id="898ee-149">其他預先定義的屬性 (例如多維度資料來源的 `Key`、`UniqueName` 和 `ParentUniqueName`) 只有在資料來源有提供這些屬性時，才受到支援。</span><span class="sxs-lookup"><span data-stu-id="898ee-149">Other predefined properties (such as `Key`, `UniqueName`, and `ParentUniqueName` for multidimensional data sources) are supported only if the data source provides those properties.</span></span> <span data-ttu-id="898ee-150">某些資料提供者可支援自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="898ee-150">Custom properties are supported by some data providers.</span></span> <span data-ttu-id="898ee-151">如需詳細資訊，請參閱 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。</span><span class="sxs-lookup"><span data-stu-id="898ee-151">For more information, see specific topics about extended field properties for your data source type in [Report Embedded Datasets and Shared Datasets &#40;Report Builder and SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).</span></span> <span data-ttu-id="898ee-152">例如，如果是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源，請參閱 [Analysis Services 資料庫的擴充欄位屬性 &#40;SSRS&#41;](extended-field-properties-for-an-analysis-services-database-ssrs.md)。</span><span class="sxs-lookup"><span data-stu-id="898ee-152">For example, for a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] data source, see [Extended Field Properties for an Analysis Services Database &#40;SSRS&#41;](extended-field-properties-for-an-analysis-services-database-ssrs.md).</span></span>  
  

  
##  <a name="understanding-default-expressions-for-fields"></a><a name="Defaults"></a> <span data-ttu-id="898ee-153">了解欄位的預設運算式</span><span class="sxs-lookup"><span data-stu-id="898ee-153">Understanding Default Expressions for Fields</span></span>  
 <span data-ttu-id="898ee-154">文字方塊可以是報表主體中的文字方塊報表項目，或是 Tablix 資料區資料格中的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="898ee-154">A text box can be a text box report item in the report body, or a text box in a cell in a tablix data region.</span></span> <span data-ttu-id="898ee-155">當您將欄位與文字方塊連結時，文字方塊的位置會決定欄位參考的預設運算式。</span><span class="sxs-lookup"><span data-stu-id="898ee-155">When you link a field with a text box, the location of the text box determines the default expression for the field reference.</span></span> <span data-ttu-id="898ee-156">在報表主體中，文字方塊值運算式必須指定彙總和資料集。</span><span class="sxs-lookup"><span data-stu-id="898ee-156">In the report body, a text box value expression must specify an aggregate and a dataset.</span></span> <span data-ttu-id="898ee-157">如果報表中只有一個資料集存在，系統會為您建立這個預設運算式。</span><span class="sxs-lookup"><span data-stu-id="898ee-157">If only one dataset exists in the report, this default expression is created for you.</span></span> <span data-ttu-id="898ee-158">如果是代表數值的欄位，預設彙總函式為 Sum。</span><span class="sxs-lookup"><span data-stu-id="898ee-158">For a field that represents a numeric value, the default aggregate function is Sum.</span></span> <span data-ttu-id="898ee-159">如果是代表非數值的欄位，預設彙總函式為 First。</span><span class="sxs-lookup"><span data-stu-id="898ee-159">For a field that represents a non-numeric value, the default aggregate is First.</span></span>  
  
 <span data-ttu-id="898ee-160">在 Tablix 資料區中，預設欄位運算式取決於您加入欄位之文字方塊的資料列和群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="898ee-160">In a tablix data region, the default field expression depends on the row and group memberships of the text box that you add the field to.</span></span> <span data-ttu-id="898ee-161">Sales 欄位的欄位運算式 (當加入到資料表之詳細資料列中的文字方塊時) 為 `[Sales]`。</span><span class="sxs-lookup"><span data-stu-id="898ee-161">The field expression for the field Sales, when added to a text box in the detail row of a table, is `[Sales]`.</span></span> <span data-ttu-id="898ee-162">如果您將相同的欄位加入到群組首中的文字方塊，預設運算式就是 `(Sum[Sales])`，因為群組首會顯示群組的摘要值，而非詳細資料值。</span><span class="sxs-lookup"><span data-stu-id="898ee-162">If you add the same field to a text box in a group header, the default expression is `(Sum[Sales])`, because the group header displays summary values for the group, not detail values.</span></span> <span data-ttu-id="898ee-163">當報表執行時，報表處理器會評估每一個運算式，並替代報表中的結果。</span><span class="sxs-lookup"><span data-stu-id="898ee-163">When the report runs, the report processor evaluates each expression and substitutes the result in the report.</span></span>  
  
 <span data-ttu-id="898ee-164">如需運算式的詳細資訊，請參閱[運算式 &#40;報表產生器及 SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)。</span><span class="sxs-lookup"><span data-stu-id="898ee-164">For more information about expressions, see [Expressions &#40;Report Builder and SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md).</span></span>  
  

  
##  <a name="field-data-types"></a><a name="DataTypes"></a> <span data-ttu-id="898ee-165">欄位資料類型</span><span class="sxs-lookup"><span data-stu-id="898ee-165">Field Data Types</span></span>  
 <span data-ttu-id="898ee-166">當您建立資料集時，資料來源上欄位的資料類型可能不完全是報表中使用的資料類型。</span><span class="sxs-lookup"><span data-stu-id="898ee-166">When you create a dataset, the data types of the fields on the data source may not be exactly the data types used in a report.</span></span> <span data-ttu-id="898ee-167">資料類型可能會經歷一或兩個對應層。</span><span class="sxs-lookup"><span data-stu-id="898ee-167">Data types may go through one or two mapping layers.</span></span> <span data-ttu-id="898ee-168">資料處理延伸模組或資料提供者可以將資料來源中的資料類型對應到 Common Language Runtime (CLR) 資料類型。</span><span class="sxs-lookup"><span data-stu-id="898ee-168">The data processing extension or data provider may map data types from the data source to common language runtime (CLR) data types.</span></span> <span data-ttu-id="898ee-169">資料處理延伸模組所傳回的資料類型會從 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]對應到 Common Language Runtime (CLR) 資料類型的子集。</span><span class="sxs-lookup"><span data-stu-id="898ee-169">The data types returned by data processing extensions are mapped to a subset of common language runtime (CLR) data types from the [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].</span></span>  
  
 <span data-ttu-id="898ee-170">在資料來源上，資料會使用此資料來源所支援的資料類型來儲存。</span><span class="sxs-lookup"><span data-stu-id="898ee-170">On the data source, the data is stored in data types supported by the data source.</span></span> <span data-ttu-id="898ee-171">例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料必須是其中一個支援的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型，例如 `nvarchar` 或 `datetime`。</span><span class="sxs-lookup"><span data-stu-id="898ee-171">For example, data in a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database must be one of the supported [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] data types such as `nvarchar` or `datetime`.</span></span> <span data-ttu-id="898ee-172">當您從此資料來源擷取資料時，資料會透過與資料來源類型相關聯的資料處理延伸模組或資料提供者來傳遞。</span><span class="sxs-lookup"><span data-stu-id="898ee-172">When you retrieve data from the data source, the data passes through a data processing extension or data provider that is associated with the data source type.</span></span> <span data-ttu-id="898ee-173">根據資料處理延伸模組而定，資料可從資料來源使用的資料類型轉換成資料處理延伸模組所支援的資料類型。</span><span class="sxs-lookup"><span data-stu-id="898ee-173">Depending on the data processing extension, data may be converted from the data types used by data source into data types supported by the data processing extension.</span></span> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] <span data-ttu-id="898ee-174">會使用與 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]一起安裝之 Common Language Runtime (CLR) 所支援的資料類型。</span><span class="sxs-lookup"><span data-stu-id="898ee-174">uses data types supported by the common language runtime (CLR) that is installed with [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].</span></span> <span data-ttu-id="898ee-175">資料提供者會將結果集中的每一個資料行從原生資料類型對應到 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Common Language Runtime (CLR) 資料類型。</span><span class="sxs-lookup"><span data-stu-id="898ee-175">The data provider maps each column in the result set from the native data type to a [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] common language runtime (CLR) data type.</span></span>  
  
 <span data-ttu-id="898ee-176">在每一個階段，資料都是由資料類型來表示，如以下清單所述：</span><span class="sxs-lookup"><span data-stu-id="898ee-176">At each stage, the data is represented by the data types as described in the following list:</span></span>  
  
-   <span data-ttu-id="898ee-177">**資料來源** ：您所連接之資料來源類型版本所支援的資料類型。</span><span class="sxs-lookup"><span data-stu-id="898ee-177">**Data source** The data types supported by the version of the type of data source to which you are connecting.</span></span>  
  
     <span data-ttu-id="898ee-178">例如，適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源的一般資料類型包括 `int`、`datetime` 和 `varchar`。</span><span class="sxs-lookup"><span data-stu-id="898ee-178">For example, typical data types for a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] data source include `int`, `datetime`, and `varchar`.</span></span> <span data-ttu-id="898ee-179"> 所導入的資料類型已經加入 、、 和  的支援。</span><span class="sxs-lookup"><span data-stu-id="898ee-179">Data types introduced by [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] added support for `date`, `time`, `datetimetz`, and `datetime2`.</span></span> <span data-ttu-id="898ee-180">如需詳細資訊，請參閱 [資料類型 (Transact-SQL)](https://go.microsoft.com/fwlink/?linkid=98362)。</span><span class="sxs-lookup"><span data-stu-id="898ee-180">For more information, see [Data Types (Transact-SQL)](https://go.microsoft.com/fwlink/?linkid=98362).</span></span>  
  
-   <span data-ttu-id="898ee-181">**資料提供者或資料處理延伸模組** ：當您連接到資料來源時，您所選取之資料處理延伸模組的資料提供者版本所支援的資料類型。</span><span class="sxs-lookup"><span data-stu-id="898ee-181">**Data provider or data processing extension** The data types supported by the version of the data provider of the data processing extension you select when you connect to the data source.</span></span> <span data-ttu-id="898ee-182">以 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 為基礎的資料提供者會使用 CLR 所支援的資料類型。</span><span class="sxs-lookup"><span data-stu-id="898ee-182">Data providers based on the [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] use data types supported by the CLR.</span></span> <span data-ttu-id="898ee-183">如需 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者資料類型的詳細資訊，請參閱 MSDN 上的 [資料類型對應 (ADO.NET)](https://go.microsoft.com/fwlink/?LinkId=112178) 和 [使用基底類型](https://go.microsoft.com/fwlink/?LinkId=112177) 。</span><span class="sxs-lookup"><span data-stu-id="898ee-183">For more information about [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] data provider data types, see [Data Type Mappings (ADO.NET)](https://go.microsoft.com/fwlink/?LinkId=112178) and [Working with Base Types](https://go.microsoft.com/fwlink/?LinkId=112177) on MSDN.</span></span>  
  
     <span data-ttu-id="898ee-184">例如，[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 所支援的一般資料類型包括 `Int32` 和 `String`。</span><span class="sxs-lookup"><span data-stu-id="898ee-184">For example, typical data types supported by the [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] include `Int32` and `String`.</span></span> <span data-ttu-id="898ee-185"> 結構支援日曆上的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="898ee-185">Calendar dates and times are supported by the `DateTime` structure.</span></span> <span data-ttu-id="898ee-186">[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0 Service Pack 1 針對具有時區時差的日期導入了 `DateTimeOffset` 結構的支援。</span><span class="sxs-lookup"><span data-stu-id="898ee-186">The [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0 Service Pack 1 introduced support for the `DateTimeOffset` structure for dates with a time zone offset.</span></span>  
  
    > [!NOTE]  
    >  <span data-ttu-id="898ee-187">報表伺服器會使用報表伺服器上所安裝及設定的資料提供者。</span><span class="sxs-lookup"><span data-stu-id="898ee-187">The report server uses the data providers that are installed and configured on the report server.</span></span> <span data-ttu-id="898ee-188">[預覽] 模式下的報表撰寫用戶端會使用用戶端電腦上所安裝及設定的資料處理延伸模組。</span><span class="sxs-lookup"><span data-stu-id="898ee-188">Report authoring clients in Preview mode use the installed and configured data processing extensions on the client machine.</span></span> <span data-ttu-id="898ee-189">您必須同時在報表用戶端和報表伺服器環境下測試您的報表。</span><span class="sxs-lookup"><span data-stu-id="898ee-189">You must test your report in both the report client and the report server environment.</span></span>  
  
-   <span data-ttu-id="898ee-190">**報表處理器** ：資料類型是以您安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]時所安裝的 CLR 版本為基礎。</span><span class="sxs-lookup"><span data-stu-id="898ee-190">**Report processor** The data types are based on the version of the CLR installed when you installed [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].</span></span>  
  
     <span data-ttu-id="898ee-191">例如， [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 已導入報表處理器用於新日期和時間類型的日期類型，如下表所示：</span><span class="sxs-lookup"><span data-stu-id="898ee-191">For example, the data types the report processor uses for the new date and time types introduced in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] are shown in the following table:</span></span>  
  
    |<span data-ttu-id="898ee-192">SQL 資料類型</span><span class="sxs-lookup"><span data-stu-id="898ee-192">SQL Data Type</span></span>|<span data-ttu-id="898ee-193">CLR 資料類型</span><span class="sxs-lookup"><span data-stu-id="898ee-193">CLR Data Type</span></span>|<span data-ttu-id="898ee-194">描述</span><span class="sxs-lookup"><span data-stu-id="898ee-194">Description</span></span>|  
    |-------------------|-------------------|-----------------|  
    |`Date`|`DateTime`|<span data-ttu-id="898ee-195">僅限日期</span><span class="sxs-lookup"><span data-stu-id="898ee-195">Date only</span></span>|  
    |`Time`|`TimeSpan`|<span data-ttu-id="898ee-196">只有時間</span><span class="sxs-lookup"><span data-stu-id="898ee-196">Time only</span></span>|  
    |`DateTimeTZ`|`DateTimeOffset`|<span data-ttu-id="898ee-197">包含時區時差的日期和時間</span><span class="sxs-lookup"><span data-stu-id="898ee-197">Date and time with time zone offset</span></span>|  
    |`DateTime2`|`DateTime`|<span data-ttu-id="898ee-198">包含毫秒的日期和時間</span><span class="sxs-lookup"><span data-stu-id="898ee-198">Date and time with fractional milliseconds</span></span>|  
  
 <span data-ttu-id="898ee-199">如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫類型的詳細資訊，請參閱 [資料類型 (Database Engine)](https://go.microsoft.com/fwlink/?linkid=98362) 和 [日期和時間資料類型與函數 (Transact-SQL)](https://go.microsoft.com/fwlink/?linkid=98360)。</span><span class="sxs-lookup"><span data-stu-id="898ee-199">For more information about [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database types, see [Data Types (Database Engine)](https://go.microsoft.com/fwlink/?linkid=98362) and [Date and Time Data Types and Functions (Transact-SQL)](https://go.microsoft.com/fwlink/?linkid=98360).</span></span>  
  
 <span data-ttu-id="898ee-200">如需從運算式加入資料集欄位之參考的詳細資訊，請參閱[運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](../report-design/data-types-in-expressions-report-builder-and-ssrs.md)。</span><span class="sxs-lookup"><span data-stu-id="898ee-200">For more information about including references to a dataset field from an expression, see [Data Types in Expressions &#40;Report Builder and SSRS&#41;](../report-design/data-types-in-expressions-report-builder-and-ssrs.md).</span></span>  
  

  
##  <a name="detecting-missing-fields-at-run-time"></a><a name="MissingFields"></a><span data-ttu-id="898ee-201">在執行時間偵測遺漏的欄位</span><span class="sxs-lookup"><span data-stu-id="898ee-201">Detecting Missing Fields at Run Time</span></span>  
 <span data-ttu-id="898ee-202">當報表處理時，資料集的結果集可能不包含指定之所有資料行的值，因為資料行不再存在於資料來源中。</span><span class="sxs-lookup"><span data-stu-id="898ee-202">When the report is processed, the result set for a dataset may not contain values for all of the columns specified because the columns no longer exist on the data source.</span></span> <span data-ttu-id="898ee-203">您可以使用欄位屬性 IsMissing 來偵測是否在執行階段傳回欄位的值。</span><span class="sxs-lookup"><span data-stu-id="898ee-203">You can use the field property IsMissing to detect whether values for a field were returned at run-time.</span></span> <span data-ttu-id="898ee-204">如需詳細資訊，請參閱[資料集 Fields 集合參考 &#40;報表產生器及 SSRS&#41;](../report-design/built-in-collections-dataset-fields-collection-references-report-builder.md)。</span><span class="sxs-lookup"><span data-stu-id="898ee-204">For more information, see [Dataset Fields Collection References &#40;Report Builder and SSRS&#41;](../report-design/built-in-collections-dataset-fields-collection-references-report-builder.md).</span></span>  
  

  
## <a name="see-also"></a><span data-ttu-id="898ee-205">另請參閱</span><span class="sxs-lookup"><span data-stu-id="898ee-205">See Also</span></span>  
 <span data-ttu-id="898ee-206">[資料集屬性對話方塊、欄位 &#40;報表產生器&#41;](../dataset-properties-dialog-box-fields-report-builder.md) </span><span class="sxs-lookup"><span data-stu-id="898ee-206">[Dataset Properties Dialog Box, Fields &#40;Report Builder&#41;](../dataset-properties-dialog-box-fields-report-builder.md) </span></span>  
 <span data-ttu-id="898ee-207">[報表產生器中的報表元件和資料集](report-parts-and-datasets-in-report-builder.md) </span><span class="sxs-lookup"><span data-stu-id="898ee-207">[Report Parts and Datasets in Report Builder](report-parts-and-datasets-in-report-builder.md) </span></span>  
 [<span data-ttu-id="898ee-208">報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;</span><span class="sxs-lookup"><span data-stu-id="898ee-208">Report Embedded Datasets and Shared Datasets &#40;Report Builder and SSRS&#41;</span></span>](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  