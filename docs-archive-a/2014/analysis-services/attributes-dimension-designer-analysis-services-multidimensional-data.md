---
title: 屬性 (維度結構索引標籤、維度設計師)  (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.attributespane.f1
ms.assetid: 627eaa08-7638-4edd-bdfa-0d8175a7cde5
author: minewiskan
ms.author: owend
ms.openlocfilehash: cb47a02d0b1118d34e8e282bb127444b6a03eb3e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593161"
---
# <a name="attributes-dimension-structure-tab-dimension-designer-analysis-services---multidimensional-data"></a><span data-ttu-id="32f83-102">屬性 (維度結構索引標籤，維度設計師) (Analysis Services - 多維度資料)</span><span class="sxs-lookup"><span data-stu-id="32f83-102">Attributes (Dimension Structure Tab, Dimension Designer) (Analysis Services - Multidimensional Data)</span></span>
  <span data-ttu-id="32f83-103">使用此窗格即可管理與選取之維度相關聯的屬性。</span><span class="sxs-lookup"><span data-stu-id="32f83-103">Use this pane to manage the attributes associated with the selected dimension.</span></span> <span data-ttu-id="32f83-104">您可以將屬性從這個窗格拖曳到 **[階層]** 窗格，以便建立階層和層級。</span><span class="sxs-lookup"><span data-stu-id="32f83-104">Attributes can be dragged from this pane to the **Hierarchies** pane to create hierarchies and levels.</span></span> <span data-ttu-id="32f83-105">如需詳細資訊，請參閱階層[&#40;維度結構索引標籤、維度設計師&#41; &#40;Analysis Services 多維度資料&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md)。</span><span class="sxs-lookup"><span data-stu-id="32f83-105">For more information, see [Hierarchies &#40;Dimension Structure Tab, Dimension Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md).</span></span>  
  
 <span data-ttu-id="32f83-106">若要建立屬性，在清單模式、樹狀模式或檢視模式時，請將資料行從 **[資料來源檢視]** 窗格拖曳到 **[屬性]** 窗格。</span><span class="sxs-lookup"><span data-stu-id="32f83-106">To create an attribute, drag a column from the **Data Source View** pane to the **Attributes** pane while in list, tree, or view mode.</span></span> <span data-ttu-id="32f83-107">若要移除屬性，請選取快速鍵功能表中的 **[刪除]** 。</span><span class="sxs-lookup"><span data-stu-id="32f83-107">To remove an attribute, select **Delete** on the shortcut menu.</span></span>  
  
 <span data-ttu-id="32f83-108">**顯示屬性窗格**</span><span class="sxs-lookup"><span data-stu-id="32f83-108">**To display the Attributes pane**</span></span>  
  
1.  <span data-ttu-id="32f83-109">在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案，然後開啟所需的維度。</span><span class="sxs-lookup"><span data-stu-id="32f83-109">In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], open the [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] project, and then open the dimension that you want.</span></span>  
  
2.  <span data-ttu-id="32f83-110">如果沒有選取，請按一下 **[維度結構]** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="32f83-110">If not selected, click the **Dimension Structure** tab.</span></span>  
  
## <a name="options"></a><span data-ttu-id="32f83-111">選項</span><span class="sxs-lookup"><span data-stu-id="32f83-111">Options</span></span>  
 <span data-ttu-id="32f83-112">**屬性**</span><span class="sxs-lookup"><span data-stu-id="32f83-112">**Attributes**</span></span>  
 <span data-ttu-id="32f83-113">顯示選取之維度可以使用的屬性。</span><span class="sxs-lookup"><span data-stu-id="32f83-113">Displays the attributes available to the selected dimension.</span></span> <span data-ttu-id="32f83-114">可以在下列模式中檢視此選項：</span><span class="sxs-lookup"><span data-stu-id="32f83-114">This option can be viewed in the following modes:</span></span>  
  
-   <span data-ttu-id="32f83-115">清單模式</span><span class="sxs-lookup"><span data-stu-id="32f83-115">List mode</span></span>  
  
     <span data-ttu-id="32f83-116">使用此模式即可建立和修改階層。</span><span class="sxs-lookup"><span data-stu-id="32f83-116">Use this mode to create and modify hierarchies.</span></span> <span data-ttu-id="32f83-117">若要在清單模式中檢視屬性，請選取快速鍵功能表中的 **[顯示屬性於]** ，然後按一下 **[清單]**。</span><span class="sxs-lookup"><span data-stu-id="32f83-117">To view the attributes in list mode, select **Show Attributes in** on the shortcut menu, and then click **List**.</span></span>  
  
-   <span data-ttu-id="32f83-118">樹狀模式</span><span class="sxs-lookup"><span data-stu-id="32f83-118">Tree mode</span></span>  
  
     <span data-ttu-id="32f83-119">使用此模式即可建立和修改階層。</span><span class="sxs-lookup"><span data-stu-id="32f83-119">Use this mode to create and modify hierarchies.</span></span> <span data-ttu-id="32f83-120">若要在樹狀模式中檢視屬性，請選取快速鍵功能表中的 **[顯示屬性於]** ，然後按一下 **[樹狀]**。</span><span class="sxs-lookup"><span data-stu-id="32f83-120">To view the attributes in tree mode, select **Show Attributes in** on the shortcut menu, and then click **Tree**.</span></span>  
  
-   <span data-ttu-id="32f83-121">方格模式</span><span class="sxs-lookup"><span data-stu-id="32f83-121">Grid mode</span></span>  
  
     <span data-ttu-id="32f83-122">使用此模式即可手動建立維度，或修改屬性 (Attribute) 的屬性 (Property)。</span><span class="sxs-lookup"><span data-stu-id="32f83-122">Use this mode to create dimensions manually, or to modify attribute properties.</span></span> <span data-ttu-id="32f83-123">若要在方格模式中檢視屬性，請選取快速鍵功能表中的 **[顯示屬性於]** ，然後按一下 **[方格]**。</span><span class="sxs-lookup"><span data-stu-id="32f83-123">To view the attributes in grid mode, select **Show Attributes in** on the shortcut menu, and then click **Grid**.</span></span>  
  
## <a name="grid-mode-options"></a><span data-ttu-id="32f83-124">方格模式選項</span><span class="sxs-lookup"><span data-stu-id="32f83-124">Grid Mode Options</span></span>  
 <span data-ttu-id="32f83-125">在方格模式中檢視屬性時，您有權存取下表列出的資料行。</span><span class="sxs-lookup"><span data-stu-id="32f83-125">When viewing attributes in grid mode, you have access to the columns listed in the following table.</span></span>  
  
 <span data-ttu-id="32f83-126">**名稱**</span><span class="sxs-lookup"><span data-stu-id="32f83-126">**Name**</span></span>  
 <span data-ttu-id="32f83-127">顯示屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="32f83-127">Displays the name of the attribute.</span></span>  
  
 <span data-ttu-id="32f83-128">**使用量**</span><span class="sxs-lookup"><span data-stu-id="32f83-128">**Usage**</span></span>  
 <span data-ttu-id="32f83-129">設定選取之屬性的使用方式。</span><span class="sxs-lookup"><span data-stu-id="32f83-129">Sets the usage of the selected attribute.</span></span> <span data-ttu-id="32f83-130">按一下向下箭號，即可從下列選擇中選取：</span><span class="sxs-lookup"><span data-stu-id="32f83-130">Click the down arrow to select from the following choices:</span></span>  
  
|<span data-ttu-id="32f83-131">值</span><span class="sxs-lookup"><span data-stu-id="32f83-131">Value</span></span>|<span data-ttu-id="32f83-132">描述</span><span class="sxs-lookup"><span data-stu-id="32f83-132">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="32f83-133">定期</span><span class="sxs-lookup"><span data-stu-id="32f83-133">Regular</span></span>|<span data-ttu-id="32f83-134">識別一般屬性。</span><span class="sxs-lookup"><span data-stu-id="32f83-134">Identifies a regular attribute.</span></span>|  
|<span data-ttu-id="32f83-135">Key</span><span class="sxs-lookup"><span data-stu-id="32f83-135">Key</span></span>|<span data-ttu-id="32f83-136">識別維度的索引鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="32f83-136">Identifies the key attribute for the dimension.</span></span> <span data-ttu-id="32f83-137">這會對應至維度的分葉成員。</span><span class="sxs-lookup"><span data-stu-id="32f83-137">This corresponds to the leaf members of the dimension.</span></span> <span data-ttu-id="32f83-138">每維度只能有一個索引鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="32f83-138">There can only be one key attribute per dimension.</span></span> <span data-ttu-id="32f83-139">若要修改，請在 [屬性]\*\*\*\* 窗格中按一下 [KeyColumns]\*\*\*\* 屬性旁的省略符號按鈕 (**...**)。</span><span class="sxs-lookup"><span data-stu-id="32f83-139">To modify, click the ellipsis button (**...**) next to the **KeyColumns** property in the **Properties** pane.</span></span>|  
|<span data-ttu-id="32f83-140">父系</span><span class="sxs-lookup"><span data-stu-id="32f83-140">Parent</span></span>|<span data-ttu-id="32f83-141">代表父子式關聯性的父屬性。</span><span class="sxs-lookup"><span data-stu-id="32f83-141">Denotes the parent attribute for a parent-child relationship.</span></span> <span data-ttu-id="32f83-142">此關聯性中的子屬性必須永遠為索引鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="32f83-142">The child attribute in this relationship must always be the key attribute.</span></span>|  
|<span data-ttu-id="32f83-143">AccountType</span><span class="sxs-lookup"><span data-stu-id="32f83-143">AccountType</span></span>|<span data-ttu-id="32f83-144">代表帳戶類型屬性。</span><span class="sxs-lookup"><span data-stu-id="32f83-144">Denotes an account type attribute.</span></span> <span data-ttu-id="32f83-145">當量值的彙總函式設定為「依帳戶」時，會由伺服器或引擎使用此屬性。</span><span class="sxs-lookup"><span data-stu-id="32f83-145">This is used by the server or engine when the aggregation function for a measure is set to "by account."</span></span>|  
  
 <span data-ttu-id="32f83-146">**型別**</span><span class="sxs-lookup"><span data-stu-id="32f83-146">**Type**</span></span>  
 <span data-ttu-id="32f83-147">設定屬性的類型。</span><span class="sxs-lookup"><span data-stu-id="32f83-147">Sets the type of the attribute.</span></span> <span data-ttu-id="32f83-148">按一下向下箭號，即可從可用的選擇中選取。</span><span class="sxs-lookup"><span data-stu-id="32f83-148">Click the down arrow to select from the available choices.</span></span>  
  
 <span data-ttu-id="32f83-149">**索引鍵資料行**</span><span class="sxs-lookup"><span data-stu-id="32f83-149">**Key Column**</span></span>  
 <span data-ttu-id="32f83-150">顯示基礎資料行的資料類型。</span><span class="sxs-lookup"><span data-stu-id="32f83-150">Displays the data type of the underlying columns.</span></span> <span data-ttu-id="32f83-151">建立新屬性時，按一下向下箭號，即可從可用的選擇中選取。</span><span class="sxs-lookup"><span data-stu-id="32f83-151">When creating a new attribute, click the down arrow to select from the available choices.</span></span>  
  
 <span data-ttu-id="32f83-152">**名稱資料行**</span><span class="sxs-lookup"><span data-stu-id="32f83-152">**Name Column**</span></span>  
 <span data-ttu-id="32f83-153">顯示基礎資料行的位置。</span><span class="sxs-lookup"><span data-stu-id="32f83-153">Displays the location of the underlying column.</span></span> <span data-ttu-id="32f83-154">建立新屬性時，按一下向下箭號，即可在 **[與索引鍵相同]** 和 **[分隔資料行]** 之間選取。</span><span class="sxs-lookup"><span data-stu-id="32f83-154">When creating a new attribute, click the down arrow to select between **Same as key** and **Separate column**.</span></span> <span data-ttu-id="32f83-155">如果選擇 **[分隔資料行]** ，則 **[屬性]** 窗格中的 **[NameColumn]** 屬性 (Property) 會設定儲存用於屬性 (Attribute) 之名稱的資料行。</span><span class="sxs-lookup"><span data-stu-id="32f83-155">If **Separate column** is chosen, the **NameColumn** property in the **Properties** pane sets the column that stores the name to use for the attribute.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="32f83-156">另請參閱</span><span class="sxs-lookup"><span data-stu-id="32f83-156">See Also</span></span>  
 <span data-ttu-id="32f83-157">[維度結構 &#40;維度設計師&#41; &#40;Analysis Services-多維度資料&#41;](dimension-structure-dimension-designer-analysis-services-multidimensional-data.md) </span><span class="sxs-lookup"><span data-stu-id="32f83-157">[Dimension Structure &#40;Dimension Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](dimension-structure-dimension-designer-analysis-services-multidimensional-data.md) </span></span>  
 <span data-ttu-id="32f83-158">[階層 &#40;維度結構索引標籤、維度設計師&#41; &#40;Analysis Services-多維度資料&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md) </span><span class="sxs-lookup"><span data-stu-id="32f83-158">[Hierarchies &#40;Dimension Structure Tab, Dimension Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md) </span></span>  
 [<span data-ttu-id="32f83-159">工具列 &#40;維度結構索引標籤、維度設計師&#41; &#40;Analysis Services-多維度資料&#41;</span><span class="sxs-lookup"><span data-stu-id="32f83-159">Toolbar &#40;Dimension Structure Tab, Dimension Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;</span></span>](toolbar-dimension-structure-designer-analysis-services-multidimensional-data.md)  
  
  
