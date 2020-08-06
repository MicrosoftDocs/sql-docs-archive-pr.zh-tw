---
title: 建立模型 (適用於 Excel 的 MDS 增益集) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 8ae26ec3-c5d5-4c4f-a810-2951a7454439
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f509fb81711d0eda5318fa2525e7f6e9e23485ba
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87698392"
---
# <a name="building-a-model-mds-add-in-for-excel"></a><span data-ttu-id="741e7-102">建立模型 (適用於 Excel 的 MDS 增益集)</span><span class="sxs-lookup"><span data-stu-id="741e7-102">Building a Model (MDS Add-in for Excel)</span></span>
  <span data-ttu-id="741e7-103">在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，系統管理員可以執行 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式中的管理功能子集。</span><span class="sxs-lookup"><span data-stu-id="741e7-103">In the [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], administrators can perform a subset of the administrative functions available in the [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] web application.</span></span>  
  
 <span data-ttu-id="741e7-104">系統管理員可在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 中執行的模型建立工作是：</span><span class="sxs-lookup"><span data-stu-id="741e7-104">The model building tasks administrators can do in the [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] are:</span></span>  
  
-   <span data-ttu-id="741e7-105">建立實體。</span><span class="sxs-lookup"><span data-stu-id="741e7-105">Create entities.</span></span> <span data-ttu-id="741e7-106">如需實體的詳細資訊，請參閱 [實體 &#40;Master Data Services&#41;](../entities-master-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="741e7-106">For more information about entities, see [Entities &#40;Master Data Services&#41;](../entities-master-data-services.md).</span></span>  
  
-   <span data-ttu-id="741e7-107">建立所有類型的屬性，包括網域屬性。</span><span class="sxs-lookup"><span data-stu-id="741e7-107">Create attributes of all types, including domain-based attributes.</span></span> <span data-ttu-id="741e7-108">如需屬性的詳細資訊，請參閱 [屬性 &#40;Master Data Services&#41;](../attributes-master-data-services.md) 和 [網域屬性 &#40;Master Data Services&#41;](../domain-based-attributes-master-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="741e7-108">For more information about attributes, see [Attributes &#40;Master Data Services&#41;](../attributes-master-data-services.md) and [Domain-Based Attributes &#40;Master Data Services&#41;](../domain-based-attributes-master-data-services.md).</span></span>  
  
 <span data-ttu-id="741e7-109">身為系統管理員，您必須透過使用 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式或 Web 服務來建立模型。</span><span class="sxs-lookup"><span data-stu-id="741e7-109">As an administrator, you must create the model by using the [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] web application or the web service.</span></span> <span data-ttu-id="741e7-110">然後您可以使用 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] ，在模型中建立實體和屬性。</span><span class="sxs-lookup"><span data-stu-id="741e7-110">Then you can use the [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] to create entities and attributes within the model.</span></span> <span data-ttu-id="741e7-111">如需模型物件的詳細資訊，請參閱 [模型 &#40;Master Data Services&#41;](../models-master-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="741e7-111">For more information about model objects, see [Models &#40;Master Data Services&#41;](../models-master-data-services.md).</span></span>  
  
## <a name="related-tasks"></a><span data-ttu-id="741e7-112">相關工作</span><span class="sxs-lookup"><span data-stu-id="741e7-112">Related Tasks</span></span>  
 <span data-ttu-id="741e7-113">大多數管理工作仍必須在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式中或透過使用 Web 服務來完成。</span><span class="sxs-lookup"><span data-stu-id="741e7-113">Most administrative tasks must still be done in the [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] web application or by using the web service.</span></span> <span data-ttu-id="741e7-114">下表顯示系統管理員可在 MDS 中使用哪些工具完成工作。</span><span class="sxs-lookup"><span data-stu-id="741e7-114">The following table shows which tools administrators can use to complete tasks in MDS.</span></span>  
  
|<span data-ttu-id="741e7-115">工作描述</span><span class="sxs-lookup"><span data-stu-id="741e7-115">Task Description</span></span>|<span data-ttu-id="741e7-116">工具</span><span class="sxs-lookup"><span data-stu-id="741e7-116">Tool</span></span>|<span data-ttu-id="741e7-117">主題</span><span class="sxs-lookup"><span data-stu-id="741e7-117">Topic</span></span>|  
|----------------------|----------|-----------|  
|<span data-ttu-id="741e7-118">建立模型。</span><span class="sxs-lookup"><span data-stu-id="741e7-118">Create models.</span></span>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] <span data-ttu-id="741e7-119">Web 應用程式或 Web 服務</span><span class="sxs-lookup"><span data-stu-id="741e7-119">web application or web service</span></span>|[<span data-ttu-id="741e7-120">建立模型 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-120">Create a Model &#40;Master Data Services&#41;</span></span>](../create-a-model-master-data-services.md)|  
|<span data-ttu-id="741e7-121">建立實體。</span><span class="sxs-lookup"><span data-stu-id="741e7-121">Create an entity.</span></span>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] <span data-ttu-id="741e7-122">Web 應用程式、Web 服務或 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]</span><span class="sxs-lookup"><span data-stu-id="741e7-122">web application, web service, or the [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]</span></span>|[<span data-ttu-id="741e7-123">建立實體 &#40;適用於 Excel 的 MDS 增益集&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-123">Create an Entity &#40;MDS Add-in for Excel&#41;</span></span>](create-an-entity-mds-add-in-for-excel.md)|  
|<span data-ttu-id="741e7-124">建立網域屬性。</span><span class="sxs-lookup"><span data-stu-id="741e7-124">Create a domain-based attribute.</span></span>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] <span data-ttu-id="741e7-125">Web 應用程式、Web 服務或 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]</span><span class="sxs-lookup"><span data-stu-id="741e7-125">web application, web service, or the [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]</span></span>|[<span data-ttu-id="741e7-126">建立網域屬性 &#40;適用於 Excel 的 MDS 增益集&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-126">Create a Domain-based Attribute &#40;MDS Add-in for Excel&#41;</span></span>](create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|<span data-ttu-id="741e7-127">建立屬性群組。</span><span class="sxs-lookup"><span data-stu-id="741e7-127">Create attribute groups.</span></span>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] <span data-ttu-id="741e7-128">Web 應用程式或 Web 服務</span><span class="sxs-lookup"><span data-stu-id="741e7-128">web application or web service</span></span>|[<span data-ttu-id="741e7-129">建立屬性群組 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-129">Create an Attribute Group &#40;Master Data Services&#41;</span></span>](../create-an-attribute-group-master-data-services.md)|  
|<span data-ttu-id="741e7-130">建立商務規則。</span><span class="sxs-lookup"><span data-stu-id="741e7-130">Create business rules.</span></span>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] <span data-ttu-id="741e7-131">Web 應用程式或 Web 服務</span><span class="sxs-lookup"><span data-stu-id="741e7-131">web application or web service</span></span>|[<span data-ttu-id="741e7-132">建立及發行商務規則 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-132">Create and Publish a Business Rule &#40;Master Data Services&#41;</span></span>](../create-and-publish-a-business-rule-master-data-services.md)|  
|<span data-ttu-id="741e7-133">建立訂閱檢視。</span><span class="sxs-lookup"><span data-stu-id="741e7-133">Create subscription views.</span></span>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] <span data-ttu-id="741e7-134">Web 應用程式或 Web 服務</span><span class="sxs-lookup"><span data-stu-id="741e7-134">web application or web service</span></span>|[<span data-ttu-id="741e7-135">建立訂閱視圖 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-135">Create a Subscription View &#40;Master Data Services&#41;</span></span>](../create-a-subscription-view-to-export-data-master-data-services.md)|  
|<span data-ttu-id="741e7-136">建立階層。</span><span class="sxs-lookup"><span data-stu-id="741e7-136">Create hierarchies.</span></span>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] <span data-ttu-id="741e7-137">Web 應用程式或 Web 服務</span><span class="sxs-lookup"><span data-stu-id="741e7-137">web application or web service</span></span>|[<span data-ttu-id="741e7-138">建立衍生階層 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-138">Create a Derived Hierarchy &#40;Master Data Services&#41;</span></span>](../create-a-derived-hierarchy-master-data-services.md)<br /><br /> [<span data-ttu-id="741e7-139">建立明確階層 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-139">Create an Explicit Hierarchy &#40;Master Data Services&#41;</span></span>](../create-an-explicit-hierarchy-master-data-services.md)|  
|<span data-ttu-id="741e7-140">建立集合。</span><span class="sxs-lookup"><span data-stu-id="741e7-140">Create collections.</span></span>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] <span data-ttu-id="741e7-141">Web 應用程式或 Web 服務</span><span class="sxs-lookup"><span data-stu-id="741e7-141">web application or web service</span></span>|[<span data-ttu-id="741e7-142">建立集合 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-142">Create a Collection &#40;Master Data Services&#41;</span></span>](../create-a-collection-master-data-services.md)|  
|<span data-ttu-id="741e7-143">建立資料的版本。</span><span class="sxs-lookup"><span data-stu-id="741e7-143">Create versions of data.</span></span>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] <span data-ttu-id="741e7-144">Web 應用程式或 Web 服務</span><span class="sxs-lookup"><span data-stu-id="741e7-144">web application or web service</span></span>|[<span data-ttu-id="741e7-145">鎖定版本 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-145">Lock a Version &#40;Master Data Services&#41;</span></span>](../lock-a-version-master-data-services.md)|  
|<span data-ttu-id="741e7-146">部署模型。</span><span class="sxs-lookup"><span data-stu-id="741e7-146">Deploy models.</span></span>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] <span data-ttu-id="741e7-147">Web 應用程式、Web 服務或 MDSModelDeploy 工具。</span><span class="sxs-lookup"><span data-stu-id="741e7-147">web application, web service, or MDSModelDeploy tool.</span></span>|[<span data-ttu-id="741e7-148">使用 MDSModelDeploy 建立模型部署封裝</span><span class="sxs-lookup"><span data-stu-id="741e7-148">Create a Model Deployment Package by Using MDSModelDeploy</span></span>](../create-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
  
## <a name="related-content"></a><span data-ttu-id="741e7-149">相關內容</span><span class="sxs-lookup"><span data-stu-id="741e7-149">Related Content</span></span>  
  
-   [<span data-ttu-id="741e7-150">模型 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-150">Models &#40;Master Data Services&#41;</span></span>](../models-master-data-services.md)  
  
-   [<span data-ttu-id="741e7-151">實體 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-151">Entities &#40;Master Data Services&#41;</span></span>](../entities-master-data-services.md)  
  
-   [<span data-ttu-id="741e7-152">屬性 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-152">Attributes &#40;Master Data Services&#41;</span></span>](../attributes-master-data-services.md)  
  
-   [<span data-ttu-id="741e7-153">網域屬性 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-153">Domain-Based Attributes &#40;Master Data Services&#41;</span></span>](../domain-based-attributes-master-data-services.md)  
  
-   [<span data-ttu-id="741e7-154">屬性群組 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-154">Attribute Groups &#40;Master Data Services&#41;</span></span>](../attribute-groups-master-data-services.md)  
  
-   [<span data-ttu-id="741e7-155">商務規則 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-155">Business Rules &#40;Master Data Services&#41;</span></span>](../business-rules-master-data-services.md)  
  
-   [<span data-ttu-id="741e7-156">將資料匯出 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-156">Exporting Data &#40;Master Data Services&#41;</span></span>](../overview-exporting-data-master-data-services.md)  
  
-   [<span data-ttu-id="741e7-157">階層 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-157">Hierarchies &#40;Master Data Services&#41;</span></span>](../hierarchies-master-data-services.md)  
  
-   [<span data-ttu-id="741e7-158">集合 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-158">Collections &#40;Master Data Services&#41;</span></span>](../collections-master-data-services.md)  
  
-   [<span data-ttu-id="741e7-159">版本 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-159">Versions &#40;Master Data Services&#41;</span></span>](../versions-master-data-services.md)  
  
-   [<span data-ttu-id="741e7-160">安全性 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-160">Security &#40;Master Data Services&#41;</span></span>](../security-master-data-services.md)  
  
-   [<span data-ttu-id="741e7-161">部署模型 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="741e7-161">Deploying Models &#40;Master Data Services&#41;</span></span>](../deploying-models-master-data-services.md)  
  
  