---
title: PowerPivot 可用性和嚴重損壞修復 (SQL Server 2014) |Microsoft Docs
ms.custom: ''
ms.date: 03/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4aaf008c-3bcb-4dbf-862c-65747d1a668c
author: minewiskan
ms.author: owend
ms.openlocfilehash: 51a48470887f83515ddee8d01c1bb209dfa94008
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687261"
---
# <a name="powerpivot-availability-and-disaster-recovery-sql-server-2014"></a><span data-ttu-id="8d9eb-102">PowerPivot 高可用性及災害復原 (SQL Server 2014)</span><span class="sxs-lookup"><span data-stu-id="8d9eb-102">PowerPivot Availability and Disaster Recovery (SQL Server 2014)</span></span>
  <span data-ttu-id="8d9eb-103">[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 的可用性和災害復原計畫主要取決於您的 SharePoint 伺服器陣列的設計、不同元件可接受的停機時間以及針對 SharePoint 可用性所實作的工具和最佳作法。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-103">Availability and disaster recovery plans for [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] depend primarily on the design of your SharePoint farm, the amount of downtime acceptable for different components, and the tools and best practices you implement for SharePoint availability.</span></span> <span data-ttu-id="8d9eb-104">本主題摘要說明技術，並包含在規劃部署的可用性和嚴重損壞修復時所要考慮的範例拓撲圖表 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-104">This topic summarizes technologies and includes example topology diagrams to consider when planning availability and disaster recovery for a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] deployment.</span></span>

||
|-|
|<span data-ttu-id="8d9eb-105">**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010</span><span class="sxs-lookup"><span data-stu-id="8d9eb-105">**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010</span></span>|

 <span data-ttu-id="8d9eb-106">**本主題內容：**</span><span class="sxs-lookup"><span data-stu-id="8d9eb-106">**In this topic:**</span></span>

-   [<span data-ttu-id="8d9eb-107">PowerPivot 高可用性的 SharePoint 2013 拓撲範例</span><span class="sxs-lookup"><span data-stu-id="8d9eb-107">Example SharePoint 2013 topology for PowerPivot high availability</span></span>](#bkmk_sharepoint2013)

-   [<span data-ttu-id="8d9eb-108">PowerPivot 高可用性的 SharePoint 2010 拓撲範例</span><span class="sxs-lookup"><span data-stu-id="8d9eb-108">Example SharePoint 2010 topology for PowerPivot high availability</span></span>](#bkmk_sharepoint2010)

-   [<span data-ttu-id="8d9eb-109">PowerPivot 服務應用程式資料庫及 SQL Server 可用性和復原技術</span><span class="sxs-lookup"><span data-stu-id="8d9eb-109">PowerPivot service application database and SQL Server availability and recovery technologies</span></span>](#bkmk_sql_server_technologies)

-   [<span data-ttu-id="8d9eb-110">詳細資訊連結</span><span class="sxs-lookup"><span data-stu-id="8d9eb-110">Links to more information</span></span>](#bkmk_more_resources)

##  <a name="example-sharepoint-2013-topology-for-powerpivot-high-availability"></a><a name="bkmk_sharepoint2013"></a><span data-ttu-id="8d9eb-111">PowerPivot 高可用性的 SharePoint 2013 拓撲範例</span><span class="sxs-lookup"><span data-stu-id="8d9eb-111">Example SharePoint 2013 topology for PowerPivot high availability</span></span>
 <span data-ttu-id="8d9eb-112">在 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 部署中，您設計 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 可用性的方式有更大的彈性。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-112">In a [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 deployment there is more flexibility in how you design [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] availability.</span></span> <span data-ttu-id="8d9eb-113">在 SharePoint 2013 中，以 SharePoint 模式部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體 (也稱為 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 伺服器) 會在 SharePoint 伺服器陣列外部執行，而且可以安裝在不同的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-113">In SharePoint 2013, the [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instance deployed in SharePoint mode, also referred to as the [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] server, runs outside the SharePoint farm and can be installed on separate servers.</span></span> <span data-ttu-id="8d9eb-114">SharePoint 模式下的每個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體都會向 Excel Services 註冊。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-114">Each instance of [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in SharePoint mode is registered with Excel Services.</span></span> <span data-ttu-id="8d9eb-115">[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 共用服務和服務應用程式會在 SharePoint 應用程式伺服器上執行。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-115">The [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] shared service and service application run on SharePoint application servers.</span></span>

 <span data-ttu-id="8d9eb-116">下圖描述 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 部署範例。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-116">The following diagram illustrates an example [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 deployment.</span></span> <span data-ttu-id="8d9eb-117">這個範例支援 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 服務的正常可用性，並假設資料庫會定期備份。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-117">This example supports good availability of the [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] services and assumes the databases are backed up on a regular basis.</span></span>

 <span data-ttu-id="8d9eb-118">![2013 中的 powerpivot 可用性](../media/ssas-powerpivot-services-2013.png "2013 中的 powerpivot 可用性")</span><span class="sxs-lookup"><span data-stu-id="8d9eb-118">![powerpivot availability in 2013](../media/ssas-powerpivot-services-2013.png "powerpivot availability in 2013")</span></span>

-   <span data-ttu-id="8d9eb-119">**(1)** Web 前端伺服器。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-119">**(1)** The Web front-end servers.</span></span> <span data-ttu-id="8d9eb-120">使用 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 增益集，將資料提供者安裝在每部伺服器上。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-120">Use the [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 Add-in to install the data providers on each server.</span></span> <span data-ttu-id="8d9eb-121">如需詳細資訊，請參閱[安裝或卸載 PowerPivot for SharePoint 增益集 &#40;SharePoint 2013&#41;](../instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-121">For more information, see [Install or Uninstall the PowerPivot for SharePoint Add-in &#40;SharePoint 2013&#41;](../instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).</span></span>

-   <span data-ttu-id="8d9eb-122">**(2)**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 共用服務會在 **每部** 應用程式伺服器上執行，並允許服務應用程式 **跨** 應用程式伺服器來執行。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-122">**(2)** The [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] shared service runs **on each** application server and allows the service application to run **across** application servers.</span></span> <span data-ttu-id="8d9eb-123">因此，如果單一應用程式伺服器離線， [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 應用程式依然可以使用。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-123">Therefore if a single application server goes offline, the [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] application will still be available.</span></span>

-   <span data-ttu-id="8d9eb-124">**(3)** Excel Calculation Services 會在每部應用程式伺服器上執行，並允許服務應用程式跨應用程式伺服器來執行。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-124">**(3)** Excel Calculation Services runs one each application server and allows the service application to run across application servers.</span></span> <span data-ttu-id="8d9eb-125">因此，如果單一應用程式伺服器離線，Excel Calculation Services 依然可以使用。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-125">Therefore if a single application server goes offline, Excel Calculation Services will still be available.</span></span>

-   <span data-ttu-id="8d9eb-126">\*\* (4) **和** (6) **的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ins 實例 sharepoint 模式會在 sharepoint 伺服器陣列外部的伺服器上執行，這包括 Windows 服務**SQL Server Analysis Services (POWERPIVOT) \*\*。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-126">**(4)** and **(6)** Instances of [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ins SharePoint mode run on servers outside the SharePoint farm, this includes the Windows Service **SQL Server Analysis Services (POWERPIVOT)**.</span></span> <span data-ttu-id="8d9eb-127">這些執行個體都會向 Excel Services 註冊 **(3)**。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-127">Each of these instances is registered with Excel Services **(3)**.</span></span> <span data-ttu-id="8d9eb-128">Excel Services 會管理傳送給 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 伺服器之要求的負載平衡。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-128">Excel Services manages load balancing of requests to the [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] servers.</span></span> <span data-ttu-id="8d9eb-129">[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 架構可讓您擁有 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 適用的多部伺服器，好讓您可以視需要輕鬆地加入更多執行個體。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-129">The [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 architecture enables you to have multiple servers for [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] so you can easily add more instances as needed.</span></span> <span data-ttu-id="8d9eb-130">如需詳細資訊，請參閱 [Manage Excel Services data model settings (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780\(v=office.15\).aspx)(管理 Excel Services 資料模型設定 (SharePoint Server 2013))。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-130">For more information, see [Manage Excel Services data model settings (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780\(v=office.15\).aspx).</span></span>

-   <span data-ttu-id="8d9eb-131">**(5)** 用於內容、組態和應用程式資料庫的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-131">**(5)** The SQL Server databases used for content, configuration, and application databases.</span></span> <span data-ttu-id="8d9eb-132">其中包括 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式資料庫。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-132">This includes the [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] service application database.</span></span> <span data-ttu-id="8d9eb-133">您的 DR 計畫應該包括資料庫層。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-133">Your DR plan should include the database layer.</span></span> <span data-ttu-id="8d9eb-134">在此設計中，資料庫會在其中一個 **執行個體上與** (4) [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 相同的伺服器上執行。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-134">In this design the databases run on the same server as **(4)** one of the [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] instances.</span></span> <span data-ttu-id="8d9eb-135">**(4)** 和 **(5)** 也可能會在不同的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-135">**(4)** and **(5)** could also be on different servers.</span></span>

-   <span data-ttu-id="8d9eb-136">**(7)** 某個形式的 SQL Server 資料庫備份或備援。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-136">**(7)** Some form of SQL Server database backup or redundancy.</span></span>

##  <a name="example-sharepoint-2010-topology-for-powerpivot-high-availability"></a><a name="bkmk_sharepoint2010"></a><span data-ttu-id="8d9eb-137">PowerPivot 高可用性的 SharePoint 2010 拓撲範例</span><span class="sxs-lookup"><span data-stu-id="8d9eb-137">Example SharePoint 2010 topology for PowerPivot high availability</span></span>
 <span data-ttu-id="8d9eb-138">[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 架構要求所有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 元件都在相同的 SharePoint 應用程式伺服器上執行。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-138">The [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 architecture requires all [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] components run on the same SharePoint application servers.</span></span> <span data-ttu-id="8d9eb-139">其中包括在 SharePoint 模式中部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體以及兩個共用服務 (相較於 SharePoint 2013 部署則只有一個)。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-139">This includes the [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instance deployed in SharePoint mode and two shared services compared to only one in a SharePoint 2013 deployment.</span></span>

 <span data-ttu-id="8d9eb-140">下圖描述 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 部署範例。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-140">The following diagram illustrates an example [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 deployment.</span></span> <span data-ttu-id="8d9eb-141">這個範例支援 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 服務的正常可用性，並假設資料庫會定期備份。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-141">This example supports good availability of the [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] services and assumes the databases are backed up on a regular basis.</span></span>

 <span data-ttu-id="8d9eb-142">![sharepoint 2010 中的 powerpivot 可用性](../media/ssas-powerpivot-services-2010.png "sharepoint 2010 中的 powerpivot 可用性")</span><span class="sxs-lookup"><span data-stu-id="8d9eb-142">![powerpivot availability in sharepoint 2010](../media/ssas-powerpivot-services-2010.png "powerpivot availability in sharepoint 2010")</span></span>

-   <span data-ttu-id="8d9eb-143">**(1)** Web 前端伺服器。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-143">**(1)** The Web front-end servers.</span></span> <span data-ttu-id="8d9eb-144">在每部伺服器上安裝資料提供者。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-144">Install the data providers on each server.</span></span> <span data-ttu-id="8d9eb-145">如需詳細資訊，請參閱 [在 SharePoint 伺服器上安裝 Analysis Services OLE DB 提供者](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-145">For more information, see [Install the Analysis Services OLE DB Provider on SharePoint Servers](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md).</span></span>

-   <span data-ttu-id="8d9eb-146">\*\* (2) **在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] SharePoint 應用程式伺服器上安裝的兩個共用服務和** (4) \*\* Windows 服務\*\*SQL Server Analysis Services (POWERPIVOT) \*\* 。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-146">**(2)** The two [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] shared services and **(4)** the Windows Service **SQL Server Analysis Services (POWERPIVOT)** are installed on the SharePoint application servers.</span></span>

     <span data-ttu-id="8d9eb-147">[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務會在 **每部** 應用程式伺服器上執行，並允許服務應用程式 **跨** 應用程式伺服器來執行。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-147">The [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service runs **on each** application server and allows the service application to run **across** application servers.</span></span> <span data-ttu-id="8d9eb-148">如果單一應用程式伺服器離線， [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 服務應用程式依然可以使用。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-148">If a single application server goes offline, the [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] service application will still be available.</span></span>

     <span data-ttu-id="8d9eb-149">若要提高 SharePoint 2010 中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 容量，請部署更多 SharePoint 應用程式伺服器來執行 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-149">To increase [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] capacity in a SharePoint 2010, deploy more SharePoint application servers running the [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service.</span></span>

-   <span data-ttu-id="8d9eb-150">**(3)** Excel Calculation Services 會在每部應用程式伺服器上執行，並允許服務應用程式跨應用程式伺服器來執行。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-150">**(3)** Excel Calculation Services runs on each application server and allows the service application to run across application servers.</span></span> <span data-ttu-id="8d9eb-151">因此，如果單一應用程式伺服器離線，Excel Calculation Services 依然可以使用。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-151">Therefore if a single application server goes offline, Excel Calculation Services will still be available.</span></span>

-   <span data-ttu-id="8d9eb-152">**(5)** 用於內容、組態和應用程式資料庫的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-152">**(5)** The SQL Server databases used for content, configuration, and application databases.</span></span> <span data-ttu-id="8d9eb-153">其中包括 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式資料庫。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-153">This includes the [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] service application database.</span></span> <span data-ttu-id="8d9eb-154">您的 DR 計畫應該包括資料庫層。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-154">Your DR plan should include the database layer.</span></span>

-   <span data-ttu-id="8d9eb-155">**(6)** 某個形式的 SQL Server 資料庫備份或備援。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-155">**(6)** Some form of SQL Server database backup or redundancy.</span></span>

##  <a name="powerpivot-service-application-database-and-sql-server-availability-and-recovery-technologies"></a><a name="bkmk_sql_server_technologies"></a><span data-ttu-id="8d9eb-156">PowerPivot 服務應用程式資料庫和 SQL Server 可用性和修復技術</span><span class="sxs-lookup"><span data-stu-id="8d9eb-156">PowerPivot service application database and SQL Server availability and recovery technologies</span></span>
 <span data-ttu-id="8d9eb-157">在您的 SharePoint 高可用性規劃中包含 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 服務應用程式資料庫。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-157">Include the [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] service application database in you SharePoint high availability planning.</span></span> <span data-ttu-id="8d9eb-158">這個資料庫的預設名稱為 `DefaultPowerPivotServiceApplicationDB-<GUID>`。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-158">The default name of the database is `DefaultPowerPivotServiceApplicationDB-<GUID>`.</span></span> <span data-ttu-id="8d9eb-159">以下是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可用性技術的摘要和搭配使用 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 資料庫時的建議。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-159">The following is a summary of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] availability technologies and recommendations when used with the [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] database.</span></span> <span data-ttu-id="8d9eb-160">如需詳細資訊，請參閱 [Supported high availability and disaster recovery options for SharePoint databases (SharePoint 2013)](https://technet.microsoft.com/library/jj841106.aspx)(SharePoint 資料庫支援的高可用性和災害復原選項 (SharePoint 2013))。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-160">For more information, see [Supported high availability and disaster recovery options for SharePoint databases (SharePoint 2013)](https://technet.microsoft.com/library/jj841106.aspx).</span></span>

||<span data-ttu-id="8d9eb-161">註解</span><span class="sxs-lookup"><span data-stu-id="8d9eb-161">Comments</span></span>|
|-|--------------|
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] <span data-ttu-id="8d9eb-162">和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 同步鏡像的可用性。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-162">and [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] synchronous mirroring in a farm for availability.</span></span>|<span data-ttu-id="8d9eb-163">支援，但不建議使用。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-163">Supported but not recommended.</span></span> <span data-ttu-id="8d9eb-164">建議在同步認可模式中使用 AlwaysOn。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-164">The recommendation is to use AlwaysOn in Synchronous - commit mode.</span></span>|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<span data-ttu-id="8d9eb-165">[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]在同步認可模式中</span><span class="sxs-lookup"><span data-stu-id="8d9eb-165">[!INCLUDE[ssHADR](../../includes/sshadr-md.md)] in Synchronous-Commit mode</span></span>|<span data-ttu-id="8d9eb-166">支援和建議。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-166">Supported and recommended.</span></span>|
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] <span data-ttu-id="8d9eb-167">非同步鏡像或記錄傳送至另一個伺服器陣列以進行災害復原。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-167">asynchronous mirroring or log-shipping to another farm for disaster recovery.</span></span>|<span data-ttu-id="8d9eb-168">支援。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-168">Supported.</span></span>|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<span data-ttu-id="8d9eb-169">[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]針對嚴重損壞修復進行非同步認可</span><span class="sxs-lookup"><span data-stu-id="8d9eb-169">[!INCLUDE[ssHADR](../../includes/sshadr-md.md)] with asynchronous-commit for disaster recovery</span></span>|<span data-ttu-id="8d9eb-170">支援</span><span class="sxs-lookup"><span data-stu-id="8d9eb-170">Supported</span></span>|

-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]

-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="8d9eb-171">記錄傳送</span><span class="sxs-lookup"><span data-stu-id="8d9eb-171">Log Shipping</span></span>

 <span data-ttu-id="8d9eb-172">如需有關如何使用 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]規劃冷待命案例的詳細資訊，請參閱＜ [PowerPivot 災害復原](https://social.technet.microsoft.com/wiki/contents/articles/22137.sharepoint-powerpivot-disaster-recovery.aspx)＞。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-172">For more information on how to plan a cold standby scenario with [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], see [PowerPivot Disaster Recovery](https://social.technet.microsoft.com/wiki/contents/articles/22137.sharepoint-powerpivot-disaster-recovery.aspx).</span></span>

## <a name="verification"></a><span data-ttu-id="8d9eb-173">驗證</span><span class="sxs-lookup"><span data-stu-id="8d9eb-173">Verification</span></span>
 <span data-ttu-id="8d9eb-174">如需指引和腳本，協助您在嚴重損壞 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 修復週期前後驗證部署，請參閱[檢查清單：使用 PowerShell 驗證 PowerPivot for SharePoint](../instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint.md)。</span><span class="sxs-lookup"><span data-stu-id="8d9eb-174">For guidance and scripts to help you verify a [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] deployment before and after a disaster recovery cycle, see [CheckList: Use PowerShell to Verify PowerPivot for SharePoint](../instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint.md).</span></span>

##  <a name="links-to-more-information"></a><a name="bkmk_more_resources"></a><span data-ttu-id="8d9eb-175">詳細資訊的連結</span><span class="sxs-lookup"><span data-stu-id="8d9eb-175">Links to more information</span></span>

-   [<span data-ttu-id="8d9eb-176">Supported high availability and disaster recovery options for SharePoint databases (SharePoint 2013)</span><span class="sxs-lookup"><span data-stu-id="8d9eb-176">Supported high availability and disaster recovery options for SharePoint databases (SharePoint 2013)</span></span>](https://technet.microsoft.com/library/jj841106.aspx)

-   <span data-ttu-id="8d9eb-177">[規劃嚴重損壞修復 (SharePoint Server 2010)](https://technet.microsoft.com/library/ff628971\(v=office.14\).aspx)</span><span class="sxs-lookup"><span data-stu-id="8d9eb-177">[Plan for disaster recovery (SharePoint Server 2010)](https://technet.microsoft.com/library/ff628971\(v=office.14\).aspx)</span></span>



