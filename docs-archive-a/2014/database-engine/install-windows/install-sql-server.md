---
title: 安裝 SQL Server 2014 |Microsoft Docs
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c4cb6275fa2ba10ad1fd4b200949efe25f7b522f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688153"
---
# <a name="install-sql-server-2014"></a><span data-ttu-id="1a371-102">安裝 SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="1a371-102">Install SQL Server 2014</span></span>
## <a name="download-sql-server-2014-express"></a>[<span data-ttu-id="1a371-103">下載 SQL Server 2014 Express</span><span class="sxs-lookup"><span data-stu-id="1a371-103">Download SQL Server 2014 Express</span></span>](http://www.hanselman.com/blog/DownloadSQLServerExpress.aspx)
  <span data-ttu-id="1a371-104">**感謝[Scott Hanselman](http://www.hanselman.com/)在一處收集所有安裝程式套件連結！**</span><span class="sxs-lookup"><span data-stu-id="1a371-104">**Thank you to [Scott Hanselman](http://www.hanselman.com/) for collecting all of the installer package links in one place!**</span></span>
  
 <span data-ttu-id="1a371-105">本主題提供可以用於安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 之不同安裝選項的概觀。</span><span class="sxs-lookup"><span data-stu-id="1a371-105">This topic provides an overview of different installation options we have for installing [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].</span></span> <span data-ttu-id="1a371-106">如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需可安裝之各種元件和安裝程式的詳細資訊，請參閱[SQL Server 2014 的安裝](installation-for-sql-server.md)。</span><span class="sxs-lookup"><span data-stu-id="1a371-106">For more information about the various [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] components that can be installed, and the installation process, see [Installation for SQL Server 2014](installation-for-sql-server.md).</span></span>  
> <span data-ttu-id="1a371-107">**注意：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在32位和64位版本中都有提供。</span><span class="sxs-lookup"><span data-stu-id="1a371-107">**NOTE:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is available in 32-bit and 64-bit editions.</span></span> <span data-ttu-id="1a371-108">64 位元和 32 位元版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是透過安裝精靈或命令提示字元來安裝。</span><span class="sxs-lookup"><span data-stu-id="1a371-108">The 64-bit and 32-bit editions of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] are installed either through the Installation Wizard, or at a command prompt.</span></span> <span data-ttu-id="1a371-109">如需元件的詳細資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請參閱[SQL Server 2014 的版本和元件](../../sql-server/editions-and-components-of-sql-server-2016.md)和[SQL Server 2014 版本所支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。</span><span class="sxs-lookup"><span data-stu-id="1a371-109">For more information about [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] components, see [Editions and Components of SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md) and [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).</span></span>  
  
 <span data-ttu-id="1a371-110">根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程序中不會安裝範例資料庫和範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="1a371-110">By default, sample databases and sample code are not installed as part of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup.</span></span> <span data-ttu-id="1a371-111">若要針對非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express Edition 安裝範例資料庫和範例程式碼，請參閱 [CodePlex 網站](https://go.microsoft.com/fwlink/?LinkId=87843)。</span><span class="sxs-lookup"><span data-stu-id="1a371-111">To install sample databases and sample code for non-Express editions of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], see the [CodePlex Web site](https://go.microsoft.com/fwlink/?LinkId=87843).</span></span> <span data-ttu-id="1a371-112">如需查閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]範例資料庫及範例程式碼的支援資訊，請參閱＜ [資料庫及範例概觀](https://go.microsoft.com/fwlink/?LinkId=110391)＞。</span><span class="sxs-lookup"><span data-stu-id="1a371-112">To read about support for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sample databases and sample code for [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], see [Databases and Samples Overview](https://go.microsoft.com/fwlink/?LinkId=110391).</span></span>  
  
 <span data-ttu-id="1a371-113">安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，請先檢閱安裝需求、系統組態檢查與安全性考量。</span><span class="sxs-lookup"><span data-stu-id="1a371-113">Before you install [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], review installation requirements, system configuration checks, and security considerations.</span></span> <span data-ttu-id="1a371-114">如需詳細資訊，請參閱 [Planning a SQL Server Installation](../../sql-server/install/planning-a-sql-server-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="1a371-114">For more information, see [Planning a SQL Server Installation](../../sql-server/install/planning-a-sql-server-installation.md).</span></span> <span data-ttu-id="1a371-115">如需有關不同 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝案例的詳細資訊，請參閱下節中的主題。</span><span class="sxs-lookup"><span data-stu-id="1a371-115">Review the topics in the next section for information about various installation scenarios for [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].</span></span>  
  
  
## <a name="install-sscurrent-components"></a><span data-ttu-id="1a371-116">安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 元件</span><span class="sxs-lookup"><span data-stu-id="1a371-116">Install [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Components</span></span>  
  
|<span data-ttu-id="1a371-117">主題</span><span class="sxs-lookup"><span data-stu-id="1a371-117">Topic</span></span>|<span data-ttu-id="1a371-118">描述</span><span class="sxs-lookup"><span data-stu-id="1a371-118">Description</span></span>|  
|-----------|-----------------|  
|[<span data-ttu-id="1a371-119">關於 SQL Server Database Engine</span><span class="sxs-lookup"><span data-stu-id="1a371-119">About the SQL Server Database Engine</span></span>](../sql-server-database-engine-overview.md)|<span data-ttu-id="1a371-120">描述如何安裝及設定 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。</span><span class="sxs-lookup"><span data-stu-id="1a371-120">Describes how to install and configure the [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].</span></span>|  
|[<span data-ttu-id="1a371-121">安裝 SQL Server 複寫</span><span class="sxs-lookup"><span data-stu-id="1a371-121">Install SQL Server Replication</span></span>](install-sql-server-replication.md)|<span data-ttu-id="1a371-122">描述如何安裝及設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication。</span><span class="sxs-lookup"><span data-stu-id="1a371-122">Describes how to install and configure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication.</span></span>|  
|[<span data-ttu-id="1a371-123">安裝 Distributed Replay</span><span class="sxs-lookup"><span data-stu-id="1a371-123">Install Distributed Replay</span></span>](../../tools/distributed-replay/install-distributed-replay-overview.md)|<span data-ttu-id="1a371-124">列出安裝 Distributed Replay 功能的主題。</span><span class="sxs-lookup"><span data-stu-id="1a371-124">Lists down the topics to install the Distributed Replay feature.</span></span>|  
|[<span data-ttu-id="1a371-125">安裝 SQL Server 管理工具</span><span class="sxs-lookup"><span data-stu-id="1a371-125">Install SQL Server Management Tools</span></span>](../../sql-server/install/install-sql-server-management-tools.md)|<span data-ttu-id="1a371-126">描述如何安裝及設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理工具。</span><span class="sxs-lookup"><span data-stu-id="1a371-126">Describes how to install and configure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] management tools.</span></span>|  
|[<span data-ttu-id="1a371-127">安裝 SQL Server PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a371-127">Install SQL Server PowerShell</span></span>](install-sql-server-powershell.md)|<span data-ttu-id="1a371-128">描述安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 元件時的考量。</span><span class="sxs-lookup"><span data-stu-id="1a371-128">Describes the considerations for installing [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell components.</span></span>|  
  
## <a name="how-to-install-sscurrent"></a><span data-ttu-id="1a371-129">如何安裝[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]</span><span class="sxs-lookup"><span data-stu-id="1a371-129">How to Install [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]</span></span>  
  
|<span data-ttu-id="1a371-130">Title</span><span class="sxs-lookup"><span data-stu-id="1a371-130">Title</span></span>|<span data-ttu-id="1a371-131">描述</span><span class="sxs-lookup"><span data-stu-id="1a371-131">Description</span></span>|  
|-----------|-----------------|  
|[<span data-ttu-id="1a371-132">安裝的使用說明主題</span><span class="sxs-lookup"><span data-stu-id="1a371-132">Installation How-to Topics</span></span>](../../sql-server/install/installation-how-to-topics.md)|<span data-ttu-id="1a371-133">提供如何從安裝精靈、從命令提示字元、使用組態檔及使用 SysPrep 安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的程序性主題連結。</span><span class="sxs-lookup"><span data-stu-id="1a371-133">Provides links to procedural topics for installing [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] from the installation wizard, from the command prompt, by using configuration files, and by using SysPrep.</span></span>|  
|[<span data-ttu-id="1a371-134">在 Server Core 上安裝 SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="1a371-134">Install SQL Server 2014 on Server Core</span></span>](install-sql-server-on-server-core.md)|<span data-ttu-id="1a371-135">檢閱本主題了解如何在 Windows Server Core 上安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="1a371-135">Review this topic to install [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] on Windows Server Core.</span></span>|  
|[<span data-ttu-id="1a371-136">驗證 SQL Server 安裝</span><span class="sxs-lookup"><span data-stu-id="1a371-136">Validate a SQL Server Installation</span></span>](validate-a-sql-server-installation.md)|<span data-ttu-id="1a371-137">檢閱 SQL 探索報告的使用狀況，以驗證電腦上所安裝之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。</span><span class="sxs-lookup"><span data-stu-id="1a371-137">Review the use of the SQL Discovery report to verify the version of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] and the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] features installed on the computer.</span></span>|  
|[<span data-ttu-id="1a371-138">檢查 System Configuration Checker 的參數</span><span class="sxs-lookup"><span data-stu-id="1a371-138">Check Parameters for the System Configuration Checker</span></span>](check-parameters-for-the-system-configuration-checker.md)|<span data-ttu-id="1a371-139">討論系統組態檢查 (SCC) 的功能。</span><span class="sxs-lookup"><span data-stu-id="1a371-139">Discusses the function of the System Configuration Checker (SCC).</span></span>|  
  
## <a name="configuration"></a><span data-ttu-id="1a371-140">組態</span><span class="sxs-lookup"><span data-stu-id="1a371-140">Configuration</span></span>  
  
|<span data-ttu-id="1a371-141">主題</span><span class="sxs-lookup"><span data-stu-id="1a371-141">Topic</span></span>|<span data-ttu-id="1a371-142">描述</span><span class="sxs-lookup"><span data-stu-id="1a371-142">Description</span></span>|  
|-----------|-----------------|  
|[<span data-ttu-id="1a371-143">設定 Windows 防火牆以允許 SQL Server 存取</span><span class="sxs-lookup"><span data-stu-id="1a371-143">Configure the Windows Firewall to Allow SQL Server Access</span></span>](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|<span data-ttu-id="1a371-144">本主題提供防火牆組態及如何設定 Windows 防火牆的概觀。</span><span class="sxs-lookup"><span data-stu-id="1a371-144">This topic provides an overview of firewall configuration and how to configure the Windows firewall.</span></span>|  
|[<span data-ttu-id="1a371-145">設定多重主目錄電腦進行 SQL Server 存取</span><span class="sxs-lookup"><span data-stu-id="1a371-145">Configure a Multi-Homed Computer for SQL Server Access</span></span>](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|<span data-ttu-id="1a371-146">此主題描述如何設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和具有進階安全性的 Windows 防火牆，以便在多重主目錄環境中提供給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的網路連接。</span><span class="sxs-lookup"><span data-stu-id="1a371-146">This topic describes how to configure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] and Windows Firewall with Advanced Security to provide for network connections to an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in a multi-homed environment.</span></span>|  
|[<span data-ttu-id="1a371-147">設定 Windows 防火牆以允許 Analysis Services 存取</span><span class="sxs-lookup"><span data-stu-id="1a371-147">Configure the Windows Firewall to Allow Analysis Services Access</span></span>](https://docs.microsoft.com/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)|<span data-ttu-id="1a371-148">您可以遵循本主題所提供的步驟，設定通訊埠和防火牆設定，以允許存取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 PowerPivot for SharePoint。</span><span class="sxs-lookup"><span data-stu-id="1a371-148">You can follow the steps provided in this topic to configure both port and firewall settings to allow access to [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] or PowerPivot for SharePoint.</span></span>|  
  
## <a name="related-sections"></a><span data-ttu-id="1a371-149">相關章節</span><span class="sxs-lookup"><span data-stu-id="1a371-149">Related Sections</span></span>  
 [<span data-ttu-id="1a371-150">安裝 SQL Server 2014 BI 功能</span><span class="sxs-lookup"><span data-stu-id="1a371-150">Install SQL Server 2014 BI Features</span></span>](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 <span data-ttu-id="1a371-151">屬於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] BI 平台的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 功能包括 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]，以及數種用來建立或處理分析資料的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="1a371-151">[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] features that are part of the [!INCLUDE[msCoName](../../includes/msconame-md.md)] BI platform include [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)], and several client applications used for creating or working with analytical data.</span></span> <span data-ttu-id="1a371-152">[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式文件集中的這一節將說明如何安裝 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]、[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] 及 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。</span><span class="sxs-lookup"><span data-stu-id="1a371-152">This section of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup documentation explains how to install [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)], and [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].</span></span>  
  
 [<span data-ttu-id="1a371-153">SQL Server 容錯移轉叢集安裝</span><span class="sxs-lookup"><span data-stu-id="1a371-153">SQL Server Failover Cluster Installation</span></span>](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 <span data-ttu-id="1a371-154">[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式文件集中的這一節將說明如何安裝及設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="1a371-154">This section of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup documentation explains how to install, and configure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] failover cluster.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1a371-155">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1a371-155">See Also</span></span>  
 <span data-ttu-id="1a371-156">[規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md) </span><span class="sxs-lookup"><span data-stu-id="1a371-156">[Planning a SQL Server Installation](../../sql-server/install/planning-a-sql-server-installation.md) </span></span>  
 <span data-ttu-id="1a371-157">[升級至 SQL Server 2014](upgrade-sql-server.md) </span><span class="sxs-lookup"><span data-stu-id="1a371-157">[Upgrade to SQL Server 2014](upgrade-sql-server.md) </span></span>  
 <span data-ttu-id="1a371-158">[卸載 SQL Server 2014](../../sql-server/install/uninstall-sql-server.md) </span><span class="sxs-lookup"><span data-stu-id="1a371-158">[Uninstall SQL Server 2014](../../sql-server/install/uninstall-sql-server.md) </span></span>  
 [<span data-ttu-id="1a371-159">高可用性解決方案 &#40;SQL Server&#41;</span><span class="sxs-lookup"><span data-stu-id="1a371-159">High Availability Solutions &#40;SQL Server&#41;</span></span>](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  