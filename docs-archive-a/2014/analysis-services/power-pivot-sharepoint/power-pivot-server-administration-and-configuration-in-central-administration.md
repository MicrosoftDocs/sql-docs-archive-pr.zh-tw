---
title: 管理中心的 PowerPivot 服務器管理和設定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2cdbfdc5-45a9-4000-a03d-318cc7ac8fe9
author: minewiskan
ms.author: owend
ms.openlocfilehash: ce5c06eda86fb8e8ac03803513c8767988a728eb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596325"
---
# <a name="powerpivot-server-administration-and-configuration-in-central-administration"></a><span data-ttu-id="38be9-102">管理中心的 PowerPivot 伺服器管理和組態</span><span class="sxs-lookup"><span data-stu-id="38be9-102">PowerPivot Server Administration and Configuration in Central Administration</span></span>
  <span data-ttu-id="38be9-103">PowerPivot 伺服器管理與組態是由 SharePoint 服務應用程式管理員使用 SharePoint 管理中心所執行。</span><span class="sxs-lookup"><span data-stu-id="38be9-103">PowerPivot server administration and configuration is performed by SharePoint service application administrators, using SharePoint Central Administration.</span></span>  
  
 <span data-ttu-id="38be9-104">您必須先設定 PowerPivot for SharePoint，然後才能使用。</span><span class="sxs-lookup"><span data-stu-id="38be9-104">PowerPivot for SharePoint must be configured before it can be used.</span></span> <span data-ttu-id="38be9-105">在您使用 SQL Server 安裝程式安裝 PowerPivot for SharePoint 之後，您可以使用下列任何方法加以設定：</span><span class="sxs-lookup"><span data-stu-id="38be9-105">After you install PowerPivot for SharePoint using SQL Server Setup, you can configure it using any of the following approaches:</span></span>  
  
-   <span data-ttu-id="38be9-106">PowerPivot 組態工具或 PowerPivot for SharePoint 2013 組態工具</span><span class="sxs-lookup"><span data-stu-id="38be9-106">PowerPivot Configuration Tool or PowerPivot for SharePoint 2013 Configuration tool</span></span>  
  
-   <span data-ttu-id="38be9-107">SharePoint 管理中心</span><span class="sxs-lookup"><span data-stu-id="38be9-107">SharePoint Central Administration</span></span>  
  
-   <span data-ttu-id="38be9-108">PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="38be9-108">PowerShell cmdlets</span></span>  
  
 <span data-ttu-id="38be9-109">這三種方法都提供完整設定的伺服器。</span><span class="sxs-lookup"><span data-stu-id="38be9-109">All three approaches deliver a fully configured server.</span></span>  
  
 <span data-ttu-id="38be9-110">本節包含使用管理中心設定軟體的工作。</span><span class="sxs-lookup"><span data-stu-id="38be9-110">This section includes tasks for configuring the software using Central Administration.</span></span> <span data-ttu-id="38be9-111">您至少必須執行底下清單所列的所有三個必要組態工作。</span><span class="sxs-lookup"><span data-stu-id="38be9-111">At a minimum, you must perform all three of the required configuration tasks noted in the list below.</span></span>  
  
> [!IMPORTANT]  
>  <span data-ttu-id="38be9-112">如果是 SharePoint 2010，您必須先安裝 SharePoint 2010 Service Pack 1 (SP1)，才可設定 PowerPivot for SharePoint 或使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 資料庫伺服器的 SharePoint 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="38be9-112">For SharePoint 2010, SharePoint 2010 Service Pack 1 (SP1) must be installed before you can configure either PowerPivot for SharePoint, or a SharePoint farm that uses a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] database server.</span></span> <span data-ttu-id="38be9-113">如果您尚未安裝該 Service Pack，請在開始設定伺服器之前先加以安裝。</span><span class="sxs-lookup"><span data-stu-id="38be9-113">If you have not yet installed the service pack, do so now before you begin configuring the server.</span></span>  
  
## <a name="benefits-of-configuring-powerpivot-for-sharepoint-using-central-administration"></a><span data-ttu-id="38be9-114">使用管理中心設定 PowerPivot for SharePoint 的優點</span><span class="sxs-lookup"><span data-stu-id="38be9-114">Benefits of Configuring PowerPivot for SharePoint Using Central Administration</span></span>  
 <span data-ttu-id="38be9-115">SharePoint 管理中心是 SharePoint 伺服器陣列的管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="38be9-115">SharePoint Central Administration is the administrative application of a SharePoint farm.</span></span> <span data-ttu-id="38be9-116">如果您是伺服器陣列管理員，當您將 PowerPivot for SharePoint 執行個體加入至伺服器陣列時，可能會偏好使用熟悉的工具。</span><span class="sxs-lookup"><span data-stu-id="38be9-116">If you are farm administrator, you might prefer to use a familiar tool when adding a PowerPivot for SharePoint instance to your farm.</span></span>  
  
 <span data-ttu-id="38be9-117">管理中心所提供的頁面會完整指定當您設定應用程式或伺服器時可能設定的所有選項，與 PowerPivot 組態工具或 PowerShell 指令程式相反。</span><span class="sxs-lookup"><span data-stu-id="38be9-117">In contrast with the PowerPivot Configuration Tools or PowerShell cmdlets, Central Administration provides pages that fully specify all of the options you might set when configuring an application or server.</span></span> <span data-ttu-id="38be9-118">其他方法會將組態工作流程濃縮成較少的步驟，或者需要事先了解如何使用 PowerShell 設定 SharePoint 伺服器。</span><span class="sxs-lookup"><span data-stu-id="38be9-118">Other approaches either condense the configuration workflow into a fewer number of steps, or require prior knowledge of how to configure a SharePoint server using PowerShell.</span></span>  
  
## <a name="related-content"></a><span data-ttu-id="38be9-119">相關內容</span><span class="sxs-lookup"><span data-stu-id="38be9-119">Related Content</span></span>  
 [<span data-ttu-id="38be9-120">使用 Windows PowerShell 的 PowerPivot 設定</span><span class="sxs-lookup"><span data-stu-id="38be9-120">PowerPivot Configuration using Windows PowerShell</span></span>](power-pivot-configuration-using-windows-powershell.md)  
  
 [<span data-ttu-id="38be9-121">PowerPivot 設定工具</span><span class="sxs-lookup"><span data-stu-id="38be9-121">PowerPivot Configuration Tools</span></span>](power-pivot-configuration-tools.md)  
  
## <a name="related-tasks"></a><span data-ttu-id="38be9-122">相關工作</span><span class="sxs-lookup"><span data-stu-id="38be9-122">Related Tasks</span></span>  
  
|<span data-ttu-id="38be9-123">連結</span><span class="sxs-lookup"><span data-stu-id="38be9-123">Link</span></span>|<span data-ttu-id="38be9-124">類型</span><span class="sxs-lookup"><span data-stu-id="38be9-124">Type</span></span>|<span data-ttu-id="38be9-125">工作描述</span><span class="sxs-lookup"><span data-stu-id="38be9-125">Task Description</span></span>|  
|----------|----------|----------------------|  
|[<span data-ttu-id="38be9-126">將 PowerPivot 方案部署到 SharePoint</span><span class="sxs-lookup"><span data-stu-id="38be9-126">Deploy PowerPivot Solutions to SharePoint</span></span>](deploy-power-pivot-solutions-to-sharepoint.md)|<span data-ttu-id="38be9-127">必要</span><span class="sxs-lookup"><span data-stu-id="38be9-127">Required</span></span>|<span data-ttu-id="38be9-128">這個步驟會安裝方案檔，這些檔案會將程式檔和應用程式頁面加入至伺服器陣列和網站集合。</span><span class="sxs-lookup"><span data-stu-id="38be9-128">This step installs the solution files that add program files and application pages to the farm and to site collections.</span></span>|  
|[<span data-ttu-id="38be9-129">在管理中心建立及設定 PowerPivot 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="38be9-129">Create and Configure a PowerPivot Service Application in Central Administration</span></span>](create-and-configure-power-pivot-service-application-in-ca.md)|<span data-ttu-id="38be9-130">必要</span><span class="sxs-lookup"><span data-stu-id="38be9-130">Required</span></span>|<span data-ttu-id="38be9-131">這個步驟會佈建 PowerPivot 系統服務。</span><span class="sxs-lookup"><span data-stu-id="38be9-131">This step provisions the PowerPivot System Service.</span></span>|  
|[<span data-ttu-id="38be9-132">在管理中心為網站集合啟用 PowerPivot 功能整合</span><span class="sxs-lookup"><span data-stu-id="38be9-132">Activate PowerPivot Feature Integration for Site Collections in Central Administration</span></span>](activate-power-pivot-integration-for-site-collections-in-ca.md)|<span data-ttu-id="38be9-133">必要</span><span class="sxs-lookup"><span data-stu-id="38be9-133">Required</span></span>|<span data-ttu-id="38be9-134">這個步驟會在網站集合層級開啟 PowerPivot 功能。</span><span class="sxs-lookup"><span data-stu-id="38be9-134">This step turns on PowerPivot features at the site collection level.</span></span>|  
|[<span data-ttu-id="38be9-135">加入 MSOLAP.5 做為 Excel Services 中受信任的資料提供者</span><span class="sxs-lookup"><span data-stu-id="38be9-135">Add MSOLAP.5 as a Trusted Data Provider in Excel Services</span></span>](add-msolap-5-as-a-trusted-data-provider-in-excel-services.md)|<span data-ttu-id="38be9-136">必要</span><span class="sxs-lookup"><span data-stu-id="38be9-136">Required</span></span>|<span data-ttu-id="38be9-137">此步驟會加入 Analysis Services OLE DB 提供者做為 Excel Services 中受信任的提供者。</span><span class="sxs-lookup"><span data-stu-id="38be9-137">This step adds the Analysis Services OLE DB provider as a trusted provider in Excel Services.</span></span>|  
|[<span data-ttu-id="38be9-138">SharePoint 2010 中的 PowerPivot 資料重新整理</span><span class="sxs-lookup"><span data-stu-id="38be9-138">PowerPivot Data Refresh with SharePoint 2010</span></span>](../powerpivot-data-refresh-with-sharepoint-2010.md)|<span data-ttu-id="38be9-139">建議</span><span class="sxs-lookup"><span data-stu-id="38be9-139">Recommended</span></span>|<span data-ttu-id="38be9-140">資料重新整理為選擇性，但是建議使用它。</span><span class="sxs-lookup"><span data-stu-id="38be9-140">Data refresh is optional but recommended.</span></span> <span data-ttu-id="38be9-141">它可讓您將自動更新排程到已發行之 Excel 活頁簿中的 PowerPivot 資料。</span><span class="sxs-lookup"><span data-stu-id="38be9-141">It allows you to schedule unattended updates to the PowerPivot data in published Excel workbooks.</span></span>|  
|[<span data-ttu-id="38be9-142">設定 PowerPivot 無人看管的資料重新整理帳戶 &#40;PowerPivot for SharePoint&#41;</span><span class="sxs-lookup"><span data-stu-id="38be9-142">Configure the PowerPivot Unattended Data Refresh Account &#40;PowerPivot for SharePoint&#41;</span></span>](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)|<span data-ttu-id="38be9-143">建議</span><span class="sxs-lookup"><span data-stu-id="38be9-143">Recommended</span></span>|<span data-ttu-id="38be9-144">這個步驟會佈建特殊目的的帳戶，此帳戶可在伺服器上用來執行資料重新整理作業。</span><span class="sxs-lookup"><span data-stu-id="38be9-144">This step provisions a special-purpose account that can be used to run data refresh jobs on the server.</span></span>|  
|[<span data-ttu-id="38be9-145">設定 &#40;PowerPivot for SharePoint 的使用量資料收集</span><span class="sxs-lookup"><span data-stu-id="38be9-145">Configure Usage Data Collection for &#40;PowerPivot for SharePoint</span></span>](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)|<span data-ttu-id="38be9-146">選擇性</span><span class="sxs-lookup"><span data-stu-id="38be9-146">Optional</span></span>|<span data-ttu-id="38be9-147">預設會設定使用量資料收集。</span><span class="sxs-lookup"><span data-stu-id="38be9-147">Usage data collection is configured by default.</span></span> <span data-ttu-id="38be9-148">您可以使用這些步驟來修改預設值。</span><span class="sxs-lookup"><span data-stu-id="38be9-148">You can use these steps to modify the default settings.</span></span>|  
|[<span data-ttu-id="38be9-149">設定專用的資料重新整理或僅查詢處理 &#40;PowerPivot for SharePoint&#41;</span><span class="sxs-lookup"><span data-stu-id="38be9-149">Configure Dedicated Data Refresh or Query-Only Processing &#40;PowerPivot for SharePoint&#41;</span></span>](../configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)|<span data-ttu-id="38be9-150">選擇性</span><span class="sxs-lookup"><span data-stu-id="38be9-150">Optional</span></span>|<span data-ttu-id="38be9-151">PowerPivot 執行個體可以專門處理資料重新整理作業或查詢。</span><span class="sxs-lookup"><span data-stu-id="38be9-151">A PowerPivot instance can be dedicated to just data refresh jobs or queries.</span></span> <span data-ttu-id="38be9-152">此外，您也可以修改平行資料重新整理作業的預設值。</span><span class="sxs-lookup"><span data-stu-id="38be9-152">In addition, you can modify default settings for parallel data refresh jobs.</span></span>|  
|[<span data-ttu-id="38be9-153">設定 PowerPivot 服務帳戶</span><span class="sxs-lookup"><span data-stu-id="38be9-153">Configure PowerPivot Service Accounts</span></span>](configure-power-pivot-service-accounts.md)|<span data-ttu-id="38be9-154">選擇性</span><span class="sxs-lookup"><span data-stu-id="38be9-154">Optional</span></span>|<span data-ttu-id="38be9-155">說明如何更新密碼或變更服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="38be9-155">Explains how to update passwords or change service accounts.</span></span>|  
|[<span data-ttu-id="38be9-156">在管理中心將 PowerPivot 服務應用程式連接到 SharePoint Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="38be9-156">Connect a PowerPivot Service Application to a SharePoint Web Application in Central Administration</span></span>](connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)|<span data-ttu-id="38be9-157">選擇性</span><span class="sxs-lookup"><span data-stu-id="38be9-157">Optional</span></span>|<span data-ttu-id="38be9-158">說明如何修改服務關聯。</span><span class="sxs-lookup"><span data-stu-id="38be9-158">Explains how to modify service associations.</span></span>|  
|[<span data-ttu-id="38be9-159">Create a trusted location for PowerPivot sites in Central Administration</span><span class="sxs-lookup"><span data-stu-id="38be9-159">Create a trusted location for PowerPivot sites in Central Administration</span></span>](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)|<span data-ttu-id="38be9-160">選擇性</span><span class="sxs-lookup"><span data-stu-id="38be9-160">Optional</span></span>|<span data-ttu-id="38be9-161">說明如何將 PowerPivot 圖庫當做信任的位置加入。</span><span class="sxs-lookup"><span data-stu-id="38be9-161">Explains how to add the PowerPivot Gallery as a trusted location.</span></span>|  
|[<span data-ttu-id="38be9-162">設定及查看 SharePoint 記錄檔和診斷記錄 &#40;PowerPivot for SharePoint&#41;</span><span class="sxs-lookup"><span data-stu-id="38be9-162">Configure and View SharePoint Log Files  and Diagnostic Logging &#40;PowerPivot for SharePoint&#41;</span></span>](configure-and-view-sharepoint-and-diagnostic-logging.md)|<span data-ttu-id="38be9-163">選擇性</span><span class="sxs-lookup"><span data-stu-id="38be9-163">Optional</span></span>|<span data-ttu-id="38be9-164">預設會設定事件記錄。</span><span class="sxs-lookup"><span data-stu-id="38be9-164">Event logging is configured by default.</span></span> <span data-ttu-id="38be9-165">您可以使用這些步驟來修改預設值。</span><span class="sxs-lookup"><span data-stu-id="38be9-165">You can use these steps to modify the default settings.</span></span>|  
|[<span data-ttu-id="38be9-166">PowerPivot 健全狀況規則 - 設定</span><span class="sxs-lookup"><span data-stu-id="38be9-166">PowerPivot Health Rules - Configure</span></span>](configure-power-pivot-health-rules.md)|<span data-ttu-id="38be9-167">選擇性</span><span class="sxs-lookup"><span data-stu-id="38be9-167">Optional</span></span>|<span data-ttu-id="38be9-168">預設會設定伺服器健全狀況規則。</span><span class="sxs-lookup"><span data-stu-id="38be9-168">Server health rules are configured by default.</span></span> <span data-ttu-id="38be9-169">您可以使用這些步驟來修改某些預設值。</span><span class="sxs-lookup"><span data-stu-id="38be9-169">You can use these steps to modify some of the default settings.</span></span>|  
|[<span data-ttu-id="38be9-170">建立及自訂 PowerPivot 圖庫</span><span class="sxs-lookup"><span data-stu-id="38be9-170">Create and Customize PowerPivot Gallery</span></span>](create-and-customize-power-pivot-gallery.md)|<span data-ttu-id="38be9-171">選擇性</span><span class="sxs-lookup"><span data-stu-id="38be9-171">Optional</span></span>|<span data-ttu-id="38be9-172">如果是手動設定的安裝，這個程序會說明如何建立 PowerPivot 圖庫，以顯示其中所包含之 PowerPivot 活頁簿的影像縮圖。</span><span class="sxs-lookup"><span data-stu-id="38be9-172">For installations that you are configuring manually, this procedure explains how to create a PowerPivot Gallery library that shows image thumbnails of the PowerPivot workbooks it contains.</span></span>|  
|[<span data-ttu-id="38be9-173">將 BI 語義模型連接內容類型新增至程式庫 &#40;PowerPivot for SharePoint&#41;</span><span class="sxs-lookup"><span data-stu-id="38be9-173">Add a BI Semantic Model Connection Content Type to a Library &#40;PowerPivot for SharePoint&#41;</span></span>](add-bi-semantic-model-connection-content-type-to-library.md)|<span data-ttu-id="38be9-174">選擇性</span><span class="sxs-lookup"><span data-stu-id="38be9-174">Optional</span></span>|<span data-ttu-id="38be9-175">說明如何擴充文件庫來支援 BI 語意模型連接檔案的建立。</span><span class="sxs-lookup"><span data-stu-id="38be9-175">Explains how to extend a document library to support the creation of BI semantic model connection files.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="38be9-176">另請參閱</span><span class="sxs-lookup"><span data-stu-id="38be9-176">See Also</span></span>  
 <span data-ttu-id="38be9-177">[PowerPivot for SharePoint 2010 安裝](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md) </span><span class="sxs-lookup"><span data-stu-id="38be9-177">[PowerPivot for SharePoint 2010 Installation](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md) </span></span>  
 <span data-ttu-id="38be9-178">[設定參考 &#40;PowerPivot for SharePoint&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md) </span><span class="sxs-lookup"><span data-stu-id="38be9-178">[Configuration Setting Reference &#40;PowerPivot for SharePoint&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md) </span></span>  
 [<span data-ttu-id="38be9-179">PowerPivot for SharePoint 災害復原</span><span class="sxs-lookup"><span data-stu-id="38be9-179">Disaster Recovery for PowerPivot for SharePoint</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  