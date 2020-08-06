---
title: " (Analysis Services) 中授與資料格資料的自訂存取權 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.celldata.f1
helpviewer_keywords:
- user access rights [Analysis Services], cell data
- permissions [Analysis Services], cells
- read contingent permissions
- read permissions
- cells [Analysis Services]
- custom cell data access [Analysis Services]
ms.assetid: 3b13a4ae-f3df-4523-bd30-b3fdf71e95cf
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9ac8113348a749837867a6dacba7fa23fb5e85f2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686518"
---
# <a name="grant-custom-access-to-cell-data-analysis-services"></a><span data-ttu-id="a43f1-102">授與資料格資料的自訂存取權 (Analysis Services)</span><span class="sxs-lookup"><span data-stu-id="a43f1-102">Grant custom access to cell data (Analysis Services)</span></span>
  <span data-ttu-id="a43f1-103">資料格安全性可用來允許或拒絕存取 Cube 內的量值資料。</span><span class="sxs-lookup"><span data-stu-id="a43f1-103">Cell security is used to allow or deny access to measure data within a cube.</span></span> <span data-ttu-id="a43f1-104">下圖顯示在利用其角色僅允許存取特定量值的使用者身分連接時，樞紐分析表中允許和拒絕的量值組合。</span><span class="sxs-lookup"><span data-stu-id="a43f1-104">The following illustration shows a combination of allowed and denied measures in a PivotTable, when connected as a user whose role only allows access to certain measures.</span></span> <span data-ttu-id="a43f1-105">在此範例中， **Reseller Sales Amount** 及 **Reseller Total Product Cost** 是唯二能夠透過此角色取得的量值。</span><span class="sxs-lookup"><span data-stu-id="a43f1-105">In this example, **Reseller Sales Amount** and **Reseller Total Product Cost** are the only measures available through this role.</span></span> <span data-ttu-id="a43f1-106">所有其他量值都會明確遭到拒絕 (下一節＜允許存取特定量值＞將提供用來取得這個結果的步驟)。</span><span class="sxs-lookup"><span data-stu-id="a43f1-106">All other measures are implicitly denied (the steps used to get this result are provided below in the next section, Allow access to specific measures).</span></span>  
  
 <span data-ttu-id="a43f1-107">![顯示允許與拒絕之資料格的樞紐分析表](../media/ssas-permscellsallowed.png "顯示允許與拒絕之資料格的樞紐分析表")</span><span class="sxs-lookup"><span data-stu-id="a43f1-107">![Pivottable showing allowed and denied cells](../media/ssas-permscellsallowed.png "Pivottable showing allowed and denied cells")</span></span>  
  
 <span data-ttu-id="a43f1-108">資料格權限適用於資料格內部的資料，不適用於它的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="a43f1-108">Cell permissions apply to data inside the cell, and not to its metadata.</span></span> <span data-ttu-id="a43f1-109">請注意資料格如何仍在查詢結果中顯示，但顯示的是 `#N/A` 的值，而非實際的資料格值。</span><span class="sxs-lookup"><span data-stu-id="a43f1-109">Notice how the cell is still visible in the results of a query, displaying a value of `#N/A` instead of the actual cell value.</span></span> <span data-ttu-id="a43f1-110">此 `#N/A` 值會出現在資料格中，除非用戶端應用程式轉譯值，或在連接字串中設定安全的資料格值屬性來指定另一個值。</span><span class="sxs-lookup"><span data-stu-id="a43f1-110">The `#N/A` value appears in the cell unless the client application translates the value, or another value is specified by setting the Secured Cell Value property in the connection string.</span></span>  
  
 <span data-ttu-id="a43f1-111">若要完全隱藏資料格，您必須限制可以看見的成員-維度、維度屬性和維度屬性成員。</span><span class="sxs-lookup"><span data-stu-id="a43f1-111">To hide the cell entirely, you have to limit the members-dimensions, dimension attributes, and dimension attribute members-that are viewable.</span></span> <span data-ttu-id="a43f1-112">如需詳細資訊，請參閱 [授與維度資料的自訂存取權 &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md)。</span><span class="sxs-lookup"><span data-stu-id="a43f1-112">For more information, see [Grant custom access to dimension data &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md).</span></span>  
  
 <span data-ttu-id="a43f1-113">身為管理員，您可以指定角色成員對 Cube 內的資料格是否擁有讀取、意外讀取或讀取/寫入權限。</span><span class="sxs-lookup"><span data-stu-id="a43f1-113">As an administrator, you can specify whether role members have read, read contingent, or read/write permissions on cells within a cube.</span></span> <span data-ttu-id="a43f1-114">在資料格中設定權限是允許的最低安全性層級，因此，在您開始套用這個層級的權限之前，請務必記住下列幾項事實：</span><span class="sxs-lookup"><span data-stu-id="a43f1-114">Putting permissions on a cell is the lowest level of security allowed, so before you start applying permissions at this level, it's important to keep a few facts in mind:</span></span>  
  
-   <span data-ttu-id="a43f1-115">資料格層級安全性無法延伸已在較高層級中受到限制的權限。</span><span class="sxs-lookup"><span data-stu-id="a43f1-115">Cell-level security cannot expand rights that have been restricted at a higher level.</span></span> <span data-ttu-id="a43f1-116">範例：如果角色拒絕對維度資料的存取，資料格層級安全性便無法覆寫拒絕的集合。</span><span class="sxs-lookup"><span data-stu-id="a43f1-116">An example: if a role denies access to dimension data, cell-level security cannot override the denied set.</span></span> <span data-ttu-id="a43f1-117">另一個範例：假設有一個具有 `Read` cube 許可權的角色，以及一個資料格的**讀取/寫入**許可權，則資料格資料許可權將不會是**讀取/寫入**，它會是 `Read` 。</span><span class="sxs-lookup"><span data-stu-id="a43f1-117">Another example: consider a role with `Read` permission on a cube and **Read/Write** permission on a cell ─ the cell data permission will not be **Read/Write**; it will be `Read`.</span></span>  
  
-   <span data-ttu-id="a43f1-118">自訂權限通常需要在維度成員與同一角色內的資料格之間協調。</span><span class="sxs-lookup"><span data-stu-id="a43f1-118">Custom permissions often need to be coordinated between dimension members and cells within the same role.</span></span> <span data-ttu-id="a43f1-119">例如，假設您想要針對不同的轉售商組合拒絕對數個與折扣相關之量值的存取。</span><span class="sxs-lookup"><span data-stu-id="a43f1-119">For example, suppose you want to deny access to several discount-related measures for different combinations of resellers.</span></span> <span data-ttu-id="a43f1-120">假設 **Resellers** 是維度， **Discount Amount** 是量值，您就必須在相同角色中，結合量值的權限 (遵循本主題中的指示) 與維度成員的權限。</span><span class="sxs-lookup"><span data-stu-id="a43f1-120">Given **Resellers** as dimension data and **Discount Amount** as a measure, you would need to combine within the same role permissions on both the measure (using the instructions in this topic), as well as on dimension members.</span></span> <span data-ttu-id="a43f1-121">如需設定維度權限的詳細資訊，請參閱 [授與維度資料的自訂存取權 &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) 。</span><span class="sxs-lookup"><span data-stu-id="a43f1-121">See [Grant custom access to dimension data &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) for details on setting dimension permissions.</span></span>  
  
 <span data-ttu-id="a43f1-122">資料格層級安全性是透過 MDX 運算式所指定。</span><span class="sxs-lookup"><span data-stu-id="a43f1-122">Cell-level security is specified through MDX expressions.</span></span> <span data-ttu-id="a43f1-123">由於資料格是 Tuple (也就是，可能橫跨數個維度和量值的交集點)，因此需要使用 MDX 來識別特定資料格。</span><span class="sxs-lookup"><span data-stu-id="a43f1-123">Because a cell is a tuple (that is, an intersection point across potentially multiple dimensions and measures), it is necessary to use MDX to identify specific cells.</span></span>  
  
## <a name="allow-access-to-specific-measures"></a><span data-ttu-id="a43f1-124">允許存取特定量值</span><span class="sxs-lookup"><span data-stu-id="a43f1-124">Allow access to specific measures</span></span>  
 <span data-ttu-id="a43f1-125">您可以使用資料格安全性，明確選擇要使用哪些量值。</span><span class="sxs-lookup"><span data-stu-id="a43f1-125">You can use cell security to explicitly choose which measures are available.</span></span> <span data-ttu-id="a43f1-126">一旦明確識別允許的成員之後，所有其他成員就會變成無法使用。</span><span class="sxs-lookup"><span data-stu-id="a43f1-126">Once you specifically identify which members are allowed, all other measures become unavailable.</span></span> <span data-ttu-id="a43f1-127">這可能是透過 MDX 指令碼實作的最簡單案例，如同下列步驟所述。</span><span class="sxs-lookup"><span data-stu-id="a43f1-127">This is perhaps the simplest scenario to implement via MDX script, as the following steps illustrate.</span></span>  
  
1.  <span data-ttu-id="a43f1-128">在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體，選取資料庫，開啟 [角色]\*\*\*\* 資料夾，然後按一下資料庫角色 (或建立新的資料庫角色)。</span><span class="sxs-lookup"><span data-stu-id="a43f1-128">In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] connect to the instance of [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], select a database, open the **Roles** folder, and then click a database role (or create a new database role).</span></span> <span data-ttu-id="a43f1-129">成員資格應該已經指定，而角色應該擁有 Cube 的 `Read` 存取權。</span><span class="sxs-lookup"><span data-stu-id="a43f1-129">Membership should already be specified, and the role should have `Read` access to the cube.</span></span> <span data-ttu-id="a43f1-130">如需詳細資訊，請參閱 [授與 Cube 或模型權限 &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md) 。</span><span class="sxs-lookup"><span data-stu-id="a43f1-130">See [Grant cube or model permissions &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md) if you need help with this step.</span></span>  
  
2.  <span data-ttu-id="a43f1-131">在 **[資料格資料]** 中，檢查 Cube 選取項目以確定您已選擇正確的選項，然後選取 **[啟用讀取權限]**。</span><span class="sxs-lookup"><span data-stu-id="a43f1-131">In **Cell Data**, check the cube selection to be sure you have chosen the right one, and then select **Enable read permissions**.</span></span>  
  
     <span data-ttu-id="a43f1-132">如果您只選取這個核取方塊，而且未提供 MDX 運算式，效果就和拒絕存取 Cube 中的所有資料格一樣。</span><span class="sxs-lookup"><span data-stu-id="a43f1-132">If you select just this check box, and do not provide an MDX expression, the effect is the same as denying access to all cells in the cube.</span></span> <span data-ttu-id="a43f1-133">這是因為當 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 解析 Cube 資料格子集時，預設允許的集合是空集合。</span><span class="sxs-lookup"><span data-stu-id="a43f1-133">This is because the default allowed set is an empty set whenever [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] resolves a subset of cube cells.</span></span>  
  
3.  <span data-ttu-id="a43f1-134">輸入以下 MDX 運算式。</span><span class="sxs-lookup"><span data-stu-id="a43f1-134">Enter the following MDX expression.</span></span>  
  
    ```  
    (Measures.CurrentMember IS [Measures].[Reseller Sales Amount]) OR (Measures.CurrentMember IS [Measures].[Reseller Total Product Cost])  
    ```  
  
     <span data-ttu-id="a43f1-135">這個運算式會明確識別使用者可看見的量值。</span><span class="sxs-lookup"><span data-stu-id="a43f1-135">This expression explicitly identifies which measures are visible to users.</span></span> <span data-ttu-id="a43f1-136">透過這個角色連線的使用者將無法使用其他任何量值。</span><span class="sxs-lookup"><span data-stu-id="a43f1-136">No other measures will be available to users connecting through this role.</span></span> <span data-ttu-id="a43f1-137">請注意，[CurrentMember &#40;MDX&#41;](/sql/mdx/current-mdx) 會設定內容，且後面會接著允許的量值。</span><span class="sxs-lookup"><span data-stu-id="a43f1-137">Notice that [CurrentMember &#40;MDX&#41;](/sql/mdx/current-mdx) sets the context and is followed by the measure that is allowed.</span></span> <span data-ttu-id="a43f1-138">若目前的成員包含 **Reseller Sales Amount** 或 **Reseller Total Product Cost**，則此運算式會顯示值。</span><span class="sxs-lookup"><span data-stu-id="a43f1-138">The effect of this expression is, if the current member includes either the **Reseller Sales Amount** or the **Reseller Total Product Cost**, show the value.</span></span> <span data-ttu-id="a43f1-139">否則，便會拒絕存取。</span><span class="sxs-lookup"><span data-stu-id="a43f1-139">Otherwise, deny access.</span></span> <span data-ttu-id="a43f1-140">運算式含有多個部分，每個部分都會以括號括起來。</span><span class="sxs-lookup"><span data-stu-id="a43f1-140">The expression has multiple parts, with each part enclosed in parentheses.</span></span> <span data-ttu-id="a43f1-141">`OR` 運算子可用來指定多個量值。</span><span class="sxs-lookup"><span data-stu-id="a43f1-141">The `OR` operator is used to specify multiple measures.</span></span>  
  
## <a name="deny-access-to-specific-measures"></a><span data-ttu-id="a43f1-142">拒絕存取特定量值</span><span class="sxs-lookup"><span data-stu-id="a43f1-142">Deny access to specific measures</span></span>  
 <span data-ttu-id="a43f1-143">下列 MDX 運算式（也在**Create Role**  |  **Cell Data**  |  **允許讀取 cube 內容**中指定）具有相反的效果，因而無法使用某些量值。</span><span class="sxs-lookup"><span data-stu-id="a43f1-143">The following MDX expression, also specified in **Create Role** | **Cell Data** | **Allow reading of cube content**, has the opposite effect, making certain measures unavailable.</span></span> <span data-ttu-id="a43f1-144">在此範例中，**折扣金額**和**折扣百分比**無法使用 `NOT` 和運算子來取得 `AND` 。</span><span class="sxs-lookup"><span data-stu-id="a43f1-144">In this example, **Discount Amount** and **Discount Percentage** are made unavailable using the `NOT` and `AND` operators.</span></span> <span data-ttu-id="a43f1-145">透過這個角色連接的使用者將可看見所有其他量值。</span><span class="sxs-lookup"><span data-stu-id="a43f1-145">All other measures will be visible to users connecting through this role.</span></span>  
  
```  
(NOT Measures.CurrentMember IS [Measures].[Discount Amount]) AND (NOT Measures.CurrentMember IS [Measures].[Discount Percentage])  
```  
  
 <span data-ttu-id="a43f1-146">在 Excel 中，可以在下圖中清楚看見資料格安全性：</span><span class="sxs-lookup"><span data-stu-id="a43f1-146">In Excel, cell-security is evident in the following illustration:</span></span>  
  
 <span data-ttu-id="a43f1-147">![將資料格顯示為無法使用狀態的 Excel 資料行](../media/ssas-permscellshidemeasure.png "將資料格顯示為無法使用狀態的 Excel 資料行")</span><span class="sxs-lookup"><span data-stu-id="a43f1-147">![Excel columns showing cells as not-available](../media/ssas-permscellshidemeasure.png "Excel columns showing cells as not-available")</span></span>  
  
## <a name="set-read-permissions-on-calculated-measures"></a><span data-ttu-id="a43f1-148">設定導出量值的讀取權限</span><span class="sxs-lookup"><span data-stu-id="a43f1-148">Set Read permissions on calculated measures</span></span>  
 <span data-ttu-id="a43f1-149">導出量值的權限可以獨立設定它的構成部分。</span><span class="sxs-lookup"><span data-stu-id="a43f1-149">Permissions on a calculated measure can be set independently of its constituent parts.</span></span> <span data-ttu-id="a43f1-150">如果您想要協調導出量值與其相依量值之間的權限，請直接前往下一節有關「意外讀取」的部分。</span><span class="sxs-lookup"><span data-stu-id="a43f1-150">Skip ahead to the next section on Read-Contingent if you want to coordinate permissions between a calculated measure and its dependent measures.</span></span>  
  
 <span data-ttu-id="a43f1-151">若要了解導出量值的讀取權限如何運作，請考量 AdventureWorks 中的 **Reseller Gross Profit** 。</span><span class="sxs-lookup"><span data-stu-id="a43f1-151">To understand how Read permissions work for a calculated measure, consider **Reseller Gross Profit** in AdventureWorks.</span></span> <span data-ttu-id="a43f1-152">它是衍生自 **Reseller Sales Amount** 和 **Reseller Total Product Cost** 量值。</span><span class="sxs-lookup"><span data-stu-id="a43f1-152">It's derived from **Reseller Sales Amount** and **Reseller Total Product Cost** measures.</span></span> <span data-ttu-id="a43f1-153">只要角色擁有 **Reseller Gross Profit** 資料格的讀取權限，就可以檢視這個量值，即使權限在其他量值上明確遭到拒絕也可以檢視。</span><span class="sxs-lookup"><span data-stu-id="a43f1-153">As long as a role has Read permission on **Reseller Gross Profit** cells, this measure is viewable even if permissions are expressly denied on the other measures.</span></span> <span data-ttu-id="a43f1-154">做為示範，請將下列 MDX 運算式複製到 [**建立角色**  |  **資料格資料**] [  |  **允許讀取 cube 內容**]。</span><span class="sxs-lookup"><span data-stu-id="a43f1-154">As a demonstration, copy the following MDX expression into **Create Role** | **Cell Data** | **Allow reading of cube content**.</span></span>  
  
```  
(NOT Measures.CurrentMember IS [Measures].[Reseller Sales Amount])  
AND (NOT Measures.CurrentMember IS [Measures].[Reseller Total Product Cost])  
```  
  
 <span data-ttu-id="a43f1-155">在 Excel 中，使用目前角色連接到 Cube，然後選擇這三個量值來查看資料格安全性的效果。</span><span class="sxs-lookup"><span data-stu-id="a43f1-155">In Excel, connect to the cube using the current role, and choose all three measures to see the effects of cell security.</span></span> <span data-ttu-id="a43f1-156">請注意，拒絕集合中的量值是無法使用的，但使用者可以看見導出量值。</span><span class="sxs-lookup"><span data-stu-id="a43f1-156">Notice that measures in the denied set are unavailable, but the calculated measure is visible to the user.</span></span>  
  
 <span data-ttu-id="a43f1-157">![含有可用與無法使用之資料格的 Excel 資料表](../media/ssas-permscalculatedcells.png "含有可用與無法使用之資料格的 Excel 資料表")</span><span class="sxs-lookup"><span data-stu-id="a43f1-157">![Excel table with available and unavailable cellls](../media/ssas-permscalculatedcells.png "Excel table with available and unavailable cellls")</span></span>  
  
## <a name="set-read-contingent-permissions-on-calculated-measures"></a><span data-ttu-id="a43f1-158">設定導出量值的意外讀取權限</span><span class="sxs-lookup"><span data-stu-id="a43f1-158">Set Read-Contingent permissions on calculated measures</span></span>  
 <span data-ttu-id="a43f1-159">資料格安全性提供另一種選擇 (意外讀取)，用以設定參與計算之相關資料格的權限。</span><span class="sxs-lookup"><span data-stu-id="a43f1-159">Cell-security offers an alternative, Read-Contingent, for setting permissions on the related cells participating in a calculation.</span></span> <span data-ttu-id="a43f1-160">請再次考量 **Reseller Gross Profit** 範例。</span><span class="sxs-lookup"><span data-stu-id="a43f1-160">Consider again the **Reseller Gross Profit** example.</span></span> <span data-ttu-id="a43f1-161">當您輸入上一節所提供的相同 MDX 運算式時，會將此時間放入 [**建立角色**  |  **資料格資料**] 對話方塊的第二個文字區域中 (在下列文字區域中，[允許讀取資料格安全性) 的資料**格內容**]，在 Excel 中觀看時，結果會很明顯。</span><span class="sxs-lookup"><span data-stu-id="a43f1-161">When you enter the same MDX expression provided in the previous section, placed this time into the second text area of the **Create Role** | **Cell data** dialog box (in the text area below **Allow reading of cell content contingent on cell security**), the result is apparent when viewed in Excel.</span></span> <span data-ttu-id="a43f1-162">由於 **Reseller Gross Profit** 會根據 **Reseller Sales Amount** 和 **Reseller Total Product Cost**而定，所以，現在會因為無法存取毛利的構成部分而無法存取毛利。</span><span class="sxs-lookup"><span data-stu-id="a43f1-162">Because **Reseller Gross Profit** is contingent upon **Reseller Sales Amount** and **Reseller Total Product Cost**, gross profit is now inaccessible because its constituent parts are inaccessible.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="a43f1-163">如果您在同一角色內同時設定資料格的讀取和意外讀取權限會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="a43f1-163">What happens if you set both the Read and Read-Contingent permissions on a cell within the same role?</span></span> <span data-ttu-id="a43f1-164">角色將在資料格上提供讀取權限，而非意外讀取權限。</span><span class="sxs-lookup"><span data-stu-id="a43f1-164">The role will provide Read permissions on the cell, and not Read-Contingent.</span></span>  
  
 <span data-ttu-id="a43f1-165">一如前文所述，在只選取 [啟用意外讀取權限]\*\*\*\* 核取方塊，而未提供任何 MDX 運算式的情況下，會拒絕對 Cube 中所有資料格的存取。</span><span class="sxs-lookup"><span data-stu-id="a43f1-165">Recall from previous sections that selecting just the **Enable read-contingent permissions** checkbox, without providing any MDX expression, denies access to all cells in the cube.</span></span> <span data-ttu-id="a43f1-166">這是因為當 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 解析 Cube 資料格子集時，預設允許的集合是空集合。</span><span class="sxs-lookup"><span data-stu-id="a43f1-166">This is because the default allowed set is an empty set whenever [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] resolves a subset of cube cells.</span></span>  
  
## <a name="set-readwrite-permissions-on-a-cell"></a><span data-ttu-id="a43f1-167">設定資料格的讀取/寫入權限</span><span class="sxs-lookup"><span data-stu-id="a43f1-167">Set Read/Write permissions on a cell</span></span>  
 <span data-ttu-id="a43f1-168">假設成員對 Cube 本身具有讀取/寫入權限，即可使用資料格的讀取/寫入權限來啟用回寫功能。</span><span class="sxs-lookup"><span data-stu-id="a43f1-168">Read/write permissions on a cell are used to enable writeback, provided that members have read/write permissions to the cube itself.</span></span> <span data-ttu-id="a43f1-169">在資料格層級授與的權限不得大於在 Cube 層級授與的權限。</span><span class="sxs-lookup"><span data-stu-id="a43f1-169">Permissions that are granted at the cell level cannot be greater than the permissions that are granted at the cube level.</span></span> <span data-ttu-id="a43f1-170">如需詳細資訊，請參閱＜ [Set Partition Writeback](set-partition-writeback.md) ＞。</span><span class="sxs-lookup"><span data-stu-id="a43f1-170">See [Set Partition Writeback](set-partition-writeback.md) for details.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a43f1-171">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a43f1-171">See Also</span></span>  
 <span data-ttu-id="a43f1-172">[MDX 產生器 &#40;Analysis Services 多維度資料&#41;](../mdx-builder-analysis-services-multidimensional-data.md) </span><span class="sxs-lookup"><span data-stu-id="a43f1-172">[MDX Builder &#40;Analysis Services - Multidimensional Data&#41;](../mdx-builder-analysis-services-multidimensional-data.md) </span></span>  
 <span data-ttu-id="a43f1-173">[基本 MDX 腳本 &#40;MDX&#41;](mdx/the-basic-mdx-script-mdx.md) </span><span class="sxs-lookup"><span data-stu-id="a43f1-173">[The Basic MDX Script &#40;MDX&#41;](mdx/the-basic-mdx-script-mdx.md) </span></span>  
 <span data-ttu-id="a43f1-174">[授與處理許可權 &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md) </span><span class="sxs-lookup"><span data-stu-id="a43f1-174">[Grant process permissions &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md) </span></span>  
 <span data-ttu-id="a43f1-175">[授與維度的許可權 &#40;Analysis Services&#41;](grant-permissions-on-a-dimension-analysis-services.md) </span><span class="sxs-lookup"><span data-stu-id="a43f1-175">[Grant permissions on a dimension &#40;Analysis Services&#41;](grant-permissions-on-a-dimension-analysis-services.md) </span></span>  
 <span data-ttu-id="a43f1-176">[將維度資料的自訂存取權授與 &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) </span><span class="sxs-lookup"><span data-stu-id="a43f1-176">[Grant custom access to dimension data &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) </span></span>  
 [<span data-ttu-id="a43f1-177">授與 Cube 或模型權限 &#40;Analysis Services&#41;</span><span class="sxs-lookup"><span data-stu-id="a43f1-177">Grant cube or model permissions &#40;Analysis Services&#41;</span></span>](grant-cube-or-model-permissions-analysis-services.md)  
  
  