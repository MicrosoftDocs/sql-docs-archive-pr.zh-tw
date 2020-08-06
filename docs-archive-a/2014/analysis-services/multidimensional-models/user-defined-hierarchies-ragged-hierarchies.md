---
title: 不完全階層 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ragged hierarchies [Analysis Services]
ms.assetid: e40a5788-7ede-4b0f-93ab-46ca33d0cace
author: minewiskan
ms.author: owend
ms.openlocfilehash: 02cbb24b7ae80facf0ddbb1495fccc8f848df377
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707929"
---
# <a name="ragged-hierarchies"></a><span data-ttu-id="64c40-102">不完全階層</span><span class="sxs-lookup"><span data-stu-id="64c40-102">Ragged Hierarchies</span></span>
  <span data-ttu-id="64c40-103">不完全階層是所含層級數目不平均的使用者定義階層。</span><span class="sxs-lookup"><span data-stu-id="64c40-103">A ragged hierarchy is a user-defined hierarchy that has an uneven number of levels.</span></span> <span data-ttu-id="64c40-104">常見範例包括組織圖 (高階主管同時擁有部門主管級和非主管級直屬員工)，或由國家/地區-區域-城市組成的地理階層 (其中部分城市缺少父州或省，例如華盛頓特區、梵蒂岡或新德里)。</span><span class="sxs-lookup"><span data-stu-id="64c40-104">Common examples include an organizational chart where a high-level manager has both departmental managers and non-managers as direct reports, or geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City, or New Delhi.</span></span>  
  
 <span data-ttu-id="64c40-105">維度中大多數階層每一個層級的上一層級，其成員數與相同層級的任何其他成員相同。</span><span class="sxs-lookup"><span data-stu-id="64c40-105">For most hierarchies in a dimension, each level has the same number of members above it as any other member at the same level.</span></span> <span data-ttu-id="64c40-106">不完全階層的不同之處在於，至少一個成員的邏輯父成員不在成員的上一層級內。</span><span class="sxs-lookup"><span data-stu-id="64c40-106">A ragged hierarchy is different in that the logical parent of at least one member is not in the level immediately above the member.</span></span> <span data-ttu-id="64c40-107">若發生此情形，階層會向下延伸至不同層級的不同鑽研路徑。</span><span class="sxs-lookup"><span data-stu-id="64c40-107">When this occurs, the hierarchy descends to different levels for different drilldown paths.</span></span> <span data-ttu-id="64c40-108">在用戶端應用程式中，這會使得向下鑽研路徑變得很複雜。</span><span class="sxs-lookup"><span data-stu-id="64c40-108">In a client application, this can make drilldown paths unnecessarily complicated.</span></span>  
  
 <span data-ttu-id="64c40-109">用戶端應用程式在處理不完全階層的程度方面各有不同。</span><span class="sxs-lookup"><span data-stu-id="64c40-109">Client applications vary in how well they handle a ragged hierarchy.</span></span> <span data-ttu-id="64c40-110">如果您的模型中存在不完全階層，則需要執行一些額外的工作，才能取得預期的轉譯行為。</span><span class="sxs-lookup"><span data-stu-id="64c40-110">If ragged hierarchies exist in your model, be prepared to do a little extra work to get the rendering behavior you expect.</span></span>  
  
 <span data-ttu-id="64c40-111">第一個步驟是查看用戶端應用程式如何處理向下鑽研路徑。</span><span class="sxs-lookup"><span data-stu-id="64c40-111">As a first step, check the client application to see how it handles the drilldown path.</span></span> <span data-ttu-id="64c40-112">例如，Excel 會將父項名稱當做遺漏值的預留位置來重複。</span><span class="sxs-lookup"><span data-stu-id="64c40-112">For example, Excel repeats the parent names as placeholders for missing values.</span></span> <span data-ttu-id="64c40-113">若要自行查看這個行為，請在 Adventure Works 多維度模型中使用 Sales Territory 維度建置樞紐分析表。</span><span class="sxs-lookup"><span data-stu-id="64c40-113">To see this behavior yourself, build a PivotTable using the Sales Territory dimension in the Adventure Works multidimensional model.</span></span> <span data-ttu-id="64c40-114">在具有「銷售地區」屬性「群組」、「國家/地區」和「區域」的樞紐分析表中，您會看到遺漏區域值的國家/地區會取得預留位置，在本例中，會重複其父項 (國家/地區名稱)。</span><span class="sxs-lookup"><span data-stu-id="64c40-114">In a PivotTable having the Sales Territory attributes Group, Country, and Region, you will see that countries missing a region value will get a placeholder, in this case a repeat of the parent above it (Country name).</span></span> <span data-ttu-id="64c40-115">此行為衍生自 Excel 固有的連接字串屬性 MDX Compatibility=1。</span><span class="sxs-lookup"><span data-stu-id="64c40-115">This behavior derives from the MDX Compatibility=1 connection string property that is fixed within Excel.</span></span> <span data-ttu-id="64c40-116">如果用戶端未正常提供您所需的向下鑽研行為，您可以設定模型中的屬性，至少變更其中一些行為。</span><span class="sxs-lookup"><span data-stu-id="64c40-116">If the client does not naturally provide the drill-down behaviors you are looking for, you can set properties in the model to change at least some of those behaviors.</span></span>  
  
 <span data-ttu-id="64c40-117">本主題包含下列幾節：</span><span class="sxs-lookup"><span data-stu-id="64c40-117">This topic contains the following sections:</span></span>  
  
-   [<span data-ttu-id="64c40-118">在不完全階層中修改深入分級導覽的方法</span><span class="sxs-lookup"><span data-stu-id="64c40-118">Approaches for modifying drilldown navigation in a ragged hierarchy</span></span>](#bkmk_approach)  
  
-   [<span data-ttu-id="64c40-119">設定 HideMemberIf 以隱藏一般階層中的成員</span><span class="sxs-lookup"><span data-stu-id="64c40-119">Set HideMemberIf to hide members in a regular hierarchy</span></span>](#bkmk_Hide)  
  
-   [<span data-ttu-id="64c40-120">設定 MDX 相容性以決定如何在用戶端應用程式中表示預留位置</span><span class="sxs-lookup"><span data-stu-id="64c40-120">Set MDX Compatibility to determine how placeholders are represented in client applications</span></span>](#bkmk_Mdx)  
  
##  <a name="approaches-for-modifying-drilldown-navigation-in-a-ragged-hierarchy"></a><a name="bkmk_approach"></a> <span data-ttu-id="64c40-121">修改不完全階層中之向下鑽研導覽的方法</span><span class="sxs-lookup"><span data-stu-id="64c40-121">Approaches for modifying drilldown navigation in a ragged hierarchy</span></span>  
 <span data-ttu-id="64c40-122">向下鑽研導覽未傳回預期的值或視為使用不便時，不完全階層的存在將成為問題。</span><span class="sxs-lookup"><span data-stu-id="64c40-122">The presence of a ragged hierarchy becomes a problem when drilldown navigation does not return expected values or is perceived as awkward to use.</span></span> <span data-ttu-id="64c40-123">若要修正不完全階層所導致的問題，請考量以下選項：</span><span class="sxs-lookup"><span data-stu-id="64c40-123">To fix navigation problems that result from ragged hierarchies, consider these options:</span></span>  
  
-   <span data-ttu-id="64c40-124">使用一般階層，但是在每個層級上設定 `HideMemberIf` 屬性來指定使用者是否可看到遺漏的層級。</span><span class="sxs-lookup"><span data-stu-id="64c40-124">Use a regular hierarchy but set the `HideMemberIf` property on each level to specify whether a missing level is visualized to the user.</span></span> <span data-ttu-id="64c40-125">設定 `HideMemberIf` 時，您也應該在連接字串中設定 `MDXCompatibility` 以覆寫預設導覽行為。</span><span class="sxs-lookup"><span data-stu-id="64c40-125">When setting `HideMemberIf`, you should also set `MDXCompatibility` on the connection string to override default navigation behaviors.</span></span> <span data-ttu-id="64c40-126">本主題將提供設定這些屬性的指示。</span><span class="sxs-lookup"><span data-stu-id="64c40-126">Instructions for setting these properties are in this topic.</span></span>  
  
-   <span data-ttu-id="64c40-127">建立可以明確方式管理層級成員的父子式階層。</span><span class="sxs-lookup"><span data-stu-id="64c40-127">Create a parent-child hierarchy that explicitly manages the level members.</span></span> <span data-ttu-id="64c40-128">如需此技術的說明，請參閱 [Ragged Hierarchy in SSAS (blog post)](http://dwbi1.wordpress.com/2011/03/30/ragged-hierarchy-in-ssas/)(SSAS 中的不完全階層 (部落格文章))。</span><span class="sxs-lookup"><span data-stu-id="64c40-128">For an illustration of the technique, see [Ragged Hierarchy in SSAS (blog post)](http://dwbi1.wordpress.com/2011/03/30/ragged-hierarchy-in-ssas/).</span></span> <span data-ttu-id="64c40-129">如需《線上叢書》中的詳細資訊，請參閱[父子式](parent-child-dimension.md)階層。</span><span class="sxs-lookup"><span data-stu-id="64c40-129">For more information in Books Online, see [Parent-Child Hierarchy](parent-child-dimension.md).</span></span> <span data-ttu-id="64c40-130">建立父子式階層的缺點在於，每個維度只能有一個父子式階層，且當您計算中繼成員的彙總時，通常會導致效能降低。</span><span class="sxs-lookup"><span data-stu-id="64c40-130">Downsides to creating a parent-child hierarchy are that you can only have one per dimension, and you typically incur a performance penalty when calculating aggregations for intermediate members.</span></span>  
  
 <span data-ttu-id="64c40-131">如果您的維度包含多個不完全階層，您應該使用第一種方法：設定 `HideMemberIf`。</span><span class="sxs-lookup"><span data-stu-id="64c40-131">If your dimension contains more than one ragged hierarchy, you should use the first approach, setting `HideMemberIf`.</span></span> <span data-ttu-id="64c40-132">在使用不完全階層方面有實務經驗的 BI 開發人員，可進一步支援實體資料表中的其他變更，並建立每個層級的個別的資料表。</span><span class="sxs-lookup"><span data-stu-id="64c40-132">BI Developers with practical experience in working with ragged hierarchies go further in advocating for additional changes in the physical data tables, creating separate tables for each level.</span></span> <span data-ttu-id="64c40-133">如需這項技術的詳細資訊，請參閱[聖馬丁 Mason 的 SSAS 財務 Cube-第1A 層-不完全階層 (blog) ](http://martinmason.wordpress.com/2012/03/03/the-ssas-financial-cubepart-1aragged-hierarchies-cont/) 。</span><span class="sxs-lookup"><span data-stu-id="64c40-133">See [Martin Mason's the SSAS Financial Cube-Part 1a-Ragged Hierarchies (blog)](http://martinmason.wordpress.com/2012/03/03/the-ssas-financial-cubepart-1aragged-hierarchies-cont/) for details about this technique.</span></span>  
  
##  <a name="set-hidememberif-to-hide-members-in-a-regular-hierarchy"></a><a name="bkmk_Hide"></a> <span data-ttu-id="64c40-134">設定 HideMemberIf 以隱藏一般階層中的成員</span><span class="sxs-lookup"><span data-stu-id="64c40-134">Set HideMemberIf to hide members in a regular hierarchy</span></span>  
 <span data-ttu-id="64c40-135">在不完全維度的資料表中，在邏輯上遺漏的成員可以不同方式來表示。</span><span class="sxs-lookup"><span data-stu-id="64c40-135">In a ragged dimension's table, the logically missing members can be represented in different ways.</span></span> <span data-ttu-id="64c40-136">資料表資料格可包含 Null 或空字串，或者它們可以包含與它們父系相同的值以做為一個預留位置。</span><span class="sxs-lookup"><span data-stu-id="64c40-136">The table cells can contain nulls or empty strings, or they can contain the same value as their parent to serve as a placeholder.</span></span> <span data-ttu-id="64c40-137">預留位置的表示是由子成員的預留位置狀態 (如同 `HideMemberIf` 屬性所決定) 以及用戶端應用程式的 `MDX Compatibility` 連接字串屬性所決定。</span><span class="sxs-lookup"><span data-stu-id="64c40-137">The representation of placeholders is determined by the placeholder status of child members, as determined by the `HideMemberIf` property, and the `MDX Compatibility` connection string property for the client application.</span></span>  
  
 <span data-ttu-id="64c40-138">如果是支援不完全階層顯示的用戶端應用程式，您可以使用這些屬性來隱藏在邏輯上遺漏的成員。</span><span class="sxs-lookup"><span data-stu-id="64c40-138">For client applications that support the display of ragged hierarchies, you can use these properties to hide logically missing members.</span></span>  
  
1.  <span data-ttu-id="64c40-139">在 SSDT 中按兩下維度，在維度設計師中加以開啟。</span><span class="sxs-lookup"><span data-stu-id="64c40-139">In SSDT, double-click a dimension to open it in Dimension Designer.</span></span> <span data-ttu-id="64c40-140">第一個索引標籤 [維度結構] 會在 [階層] 窗格中顯示屬性階層。</span><span class="sxs-lookup"><span data-stu-id="64c40-140">The first tab, Dimension Structure, shows attribute hierarchies in the Hierarchies pane.</span></span>  
  
2.  <span data-ttu-id="64c40-141">以滑鼠右鍵按一下此階層中的成員，並選取 [屬性]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="64c40-141">Right-click a member within the hierarchy and select **Properties**.</span></span> <span data-ttu-id="64c40-142">將 `HideMemberIf` 設定為底下描述的其中一個值。</span><span class="sxs-lookup"><span data-stu-id="64c40-142">Set `HideMemberIf` to one of the values described below.</span></span>  
  
    |<span data-ttu-id="64c40-143">HideMemberIf 設定</span><span class="sxs-lookup"><span data-stu-id="64c40-143">HideMemberIf Setting</span></span>|<span data-ttu-id="64c40-144">描述</span><span class="sxs-lookup"><span data-stu-id="64c40-144">Description</span></span>|  
    |--------------------------|-----------------|  
    |`Never`|<span data-ttu-id="64c40-145">永不隱藏層級成員。</span><span class="sxs-lookup"><span data-stu-id="64c40-145">Level members are never hidden.</span></span> <span data-ttu-id="64c40-146">這是預設值。</span><span class="sxs-lookup"><span data-stu-id="64c40-146">This is the default value.</span></span>|  
    |<span data-ttu-id="64c40-147">**OnlyChildWithNoName**</span><span class="sxs-lookup"><span data-stu-id="64c40-147">**OnlyChildWithNoName**</span></span>|<span data-ttu-id="64c40-148">當層級成員是父系的唯一子系，且其名稱是 Null 或空白字串時，會隱藏層級成員。</span><span class="sxs-lookup"><span data-stu-id="64c40-148">A level member is hidden when it is the only child of its parent and its name is null or an empty string.</span></span>|  
    |<span data-ttu-id="64c40-149">**OnlyChildWithParentName**</span><span class="sxs-lookup"><span data-stu-id="64c40-149">**OnlyChildWithParentName**</span></span>|<span data-ttu-id="64c40-150">當層級成員是父系的唯一子系，且其名稱與其父系名稱相同時，會隱藏層級成員。</span><span class="sxs-lookup"><span data-stu-id="64c40-150">A level member is hidden when it is the only child of its parent and its name is the same as the name of its parent.</span></span>|  
    |<span data-ttu-id="64c40-151">**NoName**</span><span class="sxs-lookup"><span data-stu-id="64c40-151">**NoName**</span></span>|<span data-ttu-id="64c40-152">當層級成員名稱空白時，會隱藏層級成員。</span><span class="sxs-lookup"><span data-stu-id="64c40-152">A level member is hidden when its name is empty.</span></span>|  
    |<span data-ttu-id="64c40-153">**ParentName**</span><span class="sxs-lookup"><span data-stu-id="64c40-153">**ParentName**</span></span>|<span data-ttu-id="64c40-154">當層級成員名稱與其父系名稱相同時，會隱藏層級成員。</span><span class="sxs-lookup"><span data-stu-id="64c40-154">A level member is hidden when its name is identical to that of its parent.</span></span>|  
  
##  <a name="set-mdx-compatibility-to-determine-how-placeholders-are-represented-in-client-applications"></a><a name="bkmk_Mdx"></a><span data-ttu-id="64c40-155">設定 MDX 相容性以決定如何在用戶端應用程式中表示預留位置</span><span class="sxs-lookup"><span data-stu-id="64c40-155">Set MDX Compatibility to determine how placeholders are represented in client applications</span></span>  
 <span data-ttu-id="64c40-156">在階層層級上設定 `HideMemberIf` 之後，您也應該在從用戶端應用程式傳送的連接字串中設定 `MDX Compatibility` 屬性。</span><span class="sxs-lookup"><span data-stu-id="64c40-156">After setting `HideMemberIf` on a hierarchy level, you should also set the `MDX Compatibility` property in the connection string sent from the client application.</span></span> <span data-ttu-id="64c40-157">`MDX Compatibility` 設定會決定是否使用 `HideMemberIf`。</span><span class="sxs-lookup"><span data-stu-id="64c40-157">The `MDX Compatibility` setting determines whether the `HideMemberIf` is used.</span></span>  
  
|<span data-ttu-id="64c40-158">MDX 相容性設定</span><span class="sxs-lookup"><span data-stu-id="64c40-158">MDX Compatibility Setting</span></span>|<span data-ttu-id="64c40-159">描述</span><span class="sxs-lookup"><span data-stu-id="64c40-159">Description</span></span>|<span data-ttu-id="64c40-160">使用量</span><span class="sxs-lookup"><span data-stu-id="64c40-160">Usage</span></span>|  
|-------------------------------|-----------------|-----------|  
|<span data-ttu-id="64c40-161">**1**</span><span class="sxs-lookup"><span data-stu-id="64c40-161">**1**</span></span>|<span data-ttu-id="64c40-162">顯示預留位置的值。</span><span class="sxs-lookup"><span data-stu-id="64c40-162">Show a placeholder value.</span></span>|<span data-ttu-id="64c40-163">這是 Excel、SSDT 和 SSMS 使用的預設值。</span><span class="sxs-lookup"><span data-stu-id="64c40-163">This is the default used by Excel, SSDT, and SSMS.</span></span> <span data-ttu-id="64c40-164">它會指示伺服器在不完全階層中向下鑽研空的層級時，傳回預留位置的值。</span><span class="sxs-lookup"><span data-stu-id="64c40-164">It instructs the server to return placeholder values when drilling down empty levels in a ragged hierarchy.</span></span> <span data-ttu-id="64c40-165">如果您按一下預留位置的值，您可以繼續往下前往子節點 (分葉節點)。</span><span class="sxs-lookup"><span data-stu-id="64c40-165">If you click the placeholder value, you can continue down to get to the child (leaf) nodes.</span></span><br /><br /> <span data-ttu-id="64c40-166">Excel 擁有用來連接到 Analysis Services 的連接字串，而且它永遠都會針對每個新的連接將 `MDX Compatibility` 設定為 1。</span><span class="sxs-lookup"><span data-stu-id="64c40-166">Excel owns the connection string used to connect to Analysis Services, and it always sets `MDX Compatibility` to 1 on each new connection.</span></span> <span data-ttu-id="64c40-167">這個行為會保留回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="64c40-167">This behavior preserves backward compatibility.</span></span>|  
|<span data-ttu-id="64c40-168">**2**</span><span class="sxs-lookup"><span data-stu-id="64c40-168">**2**</span></span>|<span data-ttu-id="64c40-169">隱藏預留位置的值 (Null 值或父層級的重複)，但是會顯示具有相關值的其他層級和節點。</span><span class="sxs-lookup"><span data-stu-id="64c40-169">Hide a placeholder value (either a null value or a duplicate of the parent level), but show other levels and nodes having relevant values.</span></span>|<span data-ttu-id="64c40-170">就不完全階層而言，`MDX Compatibility`=2 通常會視為慣用設定。</span><span class="sxs-lookup"><span data-stu-id="64c40-170">`MDX Compatibility`=2 is typically viewed as the preferred setting in terms of ragged hierarchies.</span></span> <span data-ttu-id="64c40-171">[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表和某些協力廠商用戶端應用程式可以保留這項設定。</span><span class="sxs-lookup"><span data-stu-id="64c40-171">A [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] report and some third-party client applications can persist this setting.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="64c40-172">另請參閱</span><span class="sxs-lookup"><span data-stu-id="64c40-172">See Also</span></span>  
 <span data-ttu-id="64c40-173">[建立使用者定義階層](user-defined-hierarchies-create.md) </span><span class="sxs-lookup"><span data-stu-id="64c40-173">[Create User-Defined Hierarchies](user-defined-hierarchies-create.md) </span></span>  
 <span data-ttu-id="64c40-174">[使用者階層](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md) </span><span class="sxs-lookup"><span data-stu-id="64c40-174">[User Hierarchies](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md) </span></span>  
 <span data-ttu-id="64c40-175">[父子式階層](parent-child-dimension.md) </span><span class="sxs-lookup"><span data-stu-id="64c40-175">[Parent-Child Hierarchy](parent-child-dimension.md) </span></span>  
 [<span data-ttu-id="64c40-176">連接字串屬性 &#40;Analysis Services&#41;</span><span class="sxs-lookup"><span data-stu-id="64c40-176">Connection String Properties &#40;Analysis Services&#41;</span></span>](https://docs.microsoft.com/analysis-services/instances/connection-string-properties-analysis-services)  
  
  