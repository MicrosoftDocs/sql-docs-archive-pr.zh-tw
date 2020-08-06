---
title: 商業智慧 SQL Server Management Studio 簡介 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio for Integration Services
- SQL Server Management Studio for Reporting Services
- SQL Server Management Studio for Analysis Services
ms.assetid: ffaa77b7-03d0-4d7a-aa42-c5091a4f2ceb
author: stevestein
ms.author: sstein
ms.openlocfilehash: fdb2a0645ad299fc355066d56b1cc371757f5b5a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87702297"
---
# <a name="introduction-to-sql-server-management-studio-for-business-intelligence"></a><span data-ttu-id="54696-102">適用於商業智慧的 SQL Server Management Studio 簡介</span><span class="sxs-lookup"><span data-stu-id="54696-102">Introduction to SQL Server Management Studio for Business Intelligence</span></span>
  <span data-ttu-id="54696-103">若要存取、設定及管理 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 和 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]，請使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。</span><span class="sxs-lookup"><span data-stu-id="54696-103">To access, configure, manage, and administer [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], and [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], use [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].</span></span> <span data-ttu-id="54696-104">雖然這三種商業智慧技術全都依賴 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，但是與每一項技術有關的管理工作則會有些微的差異。</span><span class="sxs-lookup"><span data-stu-id="54696-104">Although all three business intelligence technologies rely on [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], the administrative tasks associated with each of these technologies are slightly different.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="54696-105">若要建立及修改 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]和 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 解決方案，請使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，而不要使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。</span><span class="sxs-lookup"><span data-stu-id="54696-105">To create and modify [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], and [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] solutions, use [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], not [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].</span></span> [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] <span data-ttu-id="54696-106">是一個以 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[vsprvs](../includes/vsprvs-md.md)]為根據的開發環境。</span><span class="sxs-lookup"><span data-stu-id="54696-106">is a development environment that is based on [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[vsprvs](../includes/vsprvs-md.md)].</span></span>  
  
## <a name="managing-analysis-services-solutions-using-sql-server-management-studio"></a><span data-ttu-id="54696-107">使用 SQL Server Management Studio 管理 Analysis Services 解決方案</span><span class="sxs-lookup"><span data-stu-id="54696-107">Managing Analysis Services Solutions Using SQL Server Management Studio</span></span>  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] <span data-ttu-id="54696-108">可讓您管理 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件，例如執行備份及處理物件。</span><span class="sxs-lookup"><span data-stu-id="54696-108">enables you to manage [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] objects, such as performing back-ups and processing objects.</span></span>  
  
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] <span data-ttu-id="54696-109">會提供一個 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 指令碼專案，您可在其中開發及儲存使用多維度運算式 (MDX)、資料採礦延伸模組 (DMX) 和 XML for Analysis (XMLA) 所撰寫的指令碼。</span><span class="sxs-lookup"><span data-stu-id="54696-109">provides an [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Script project in which you develop and save scripts written in Multidimensional Expressions (MDX), Data Mining Extensions (DMX), and XML for Analysis (XMLA).</span></span> <span data-ttu-id="54696-110">您可以使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 指令碼專案來執行管理工作或是在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體上重新建立物件，例如資料庫和 Cube。</span><span class="sxs-lookup"><span data-stu-id="54696-110">You use [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Scripts projects to perform management tasks or re-create objects, such as database and cubes, on [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instances.</span></span> <span data-ttu-id="54696-111">例如，您可以在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 指令碼專案中開發 XMLA 指令碼，該指令碼會直接在現有的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體上建立新的物件。</span><span class="sxs-lookup"><span data-stu-id="54696-111">For example, you can develop an XMLA script in an [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Script project that creates new objects directly on an existing [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instance.</span></span> <span data-ttu-id="54696-112">[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 指令碼專案可儲存成為方案的一部分，並與原始程式碼控制整合。</span><span class="sxs-lookup"><span data-stu-id="54696-112">The [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Scripts projects can be saved as part of a solution and integrated with source code control.</span></span>  
  
 <span data-ttu-id="54696-113">如需如何使用的詳細資訊 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ，請參閱[SQL Server Management Studio 中的 Analysis Services 腳本專案](https://docs.microsoft.com/analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio)。</span><span class="sxs-lookup"><span data-stu-id="54696-113">For more information about how to use [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], see [Analysis Services Scripts Project in SQL Server Management Studio](https://docs.microsoft.com/analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio).</span></span>  
  
## <a name="managing-integration-services-solutions-using-sql-server-management-studio"></a><span data-ttu-id="54696-114">使用 SQL Server Management Studio 管理 Integration Services 解決方案</span><span class="sxs-lookup"><span data-stu-id="54696-114">Managing Integration Services Solutions Using SQL Server Management Studio</span></span>  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] <span data-ttu-id="54696-115">可讓您使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務來管理套件及監視執行中的套件。</span><span class="sxs-lookup"><span data-stu-id="54696-115">enables you to use the [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] service to manage packages and monitor running packages.</span></span> <span data-ttu-id="54696-116">您也可以使用 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 將封裝組織成資料夾、執行封裝、匯入及匯出封裝、移轉 Data Transformation Services (DTS) 封裝及升級 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。</span><span class="sxs-lookup"><span data-stu-id="54696-116">You can also use [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] to organize packages into folders, run packages, import and export packages, migrate Data Transformation Services (DTS) packages, and upgrade [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] packages.</span></span>  
  
## <a name="managing-reporting-services-projects-using-sql-server-management-studio"></a><span data-ttu-id="54696-117">使用 SQL Server Management Studio 來管理 Reporting Services 專案</span><span class="sxs-lookup"><span data-stu-id="54696-117">Managing Reporting Services Projects Using SQL Server Management Studio</span></span>  
 <span data-ttu-id="54696-118">使用 SQL Server Management Studio 可啟用 Reporting Services 功能、管理服務和資料庫，以及管理角色和作業。</span><span class="sxs-lookup"><span data-stu-id="54696-118">Use SQL Server Management Studio to enable Reporting Services features, administer the server and databases, and manage roles and jobs.</span></span>  
  
 <span data-ttu-id="54696-119">您可使用 [共用排程] 資料夾來管理共用排程，並管理報表伺服器資料庫 (ReportServer、ReportServerTempdb)。</span><span class="sxs-lookup"><span data-stu-id="54696-119">You manage shared schedules by using the Shared Schedules folder, and manage report server databases (ReportServer, ReportServerTempdb).</span></span> <span data-ttu-id="54696-120">當您將報表伺服器資料庫移到新的或不同的 SQL Server 資料庫引擎 () 時，您也會在 Master 系統資料庫中建立 RSExecRole [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="54696-120">You also create a RSExecRole in the Master system database when you move a report server database to a new or different SQL Server Database Engine ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]).</span></span> <span data-ttu-id="54696-121">如需有關這些工作的詳細資訊，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="54696-121">For more information about these tasks, see the following topics:</span></span>  
  
-   [<span data-ttu-id="54696-122">SQL Server Management Studio 中的 Reporting Services &#40;SSRS&#41;</span><span class="sxs-lookup"><span data-stu-id="54696-122">Reporting Services in SQL Server Management Studio &#40;SSRS&#41;</span></span>](../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)  
  
-   [<span data-ttu-id="54696-123">管理報表伺服器資料庫 &#40;SSRS 原生模式&#41;</span><span class="sxs-lookup"><span data-stu-id="54696-123">Administer a Report Server Database &#40;SSRS Native Mode&#41;</span></span>](../reporting-services/report-server/report-server-database-ssrs-native-mode.md)  
  
-   [<span data-ttu-id="54696-124">建立 RSExecRole</span><span class="sxs-lookup"><span data-stu-id="54696-124">Create the RSExecRole</span></span>](../reporting-services/security/create-the-rsexecrole.md)  
  
 <span data-ttu-id="54696-125">您也可以透過以下方式來管理伺服器：啟用及設定各種功能、設定伺服器預設值及管理角色和作業。</span><span class="sxs-lookup"><span data-stu-id="54696-125">You also manage the server by enabling and configuring various features, setting server defaults, and managing roles and jobs.</span></span> <span data-ttu-id="54696-126">如需有關這些工作的詳細資訊，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="54696-126">For more information about these tasks, see the following topics:</span></span>  
  
-   [<span data-ttu-id="54696-127">設定報表伺服器屬性 &#40;Management Studio&#41;</span><span class="sxs-lookup"><span data-stu-id="54696-127">Set Report Server Properties &#40;Management Studio&#41;</span></span>](../reporting-services/tools/set-report-server-properties-management-studio.md)  
  
-   [<span data-ttu-id="54696-128">建立、刪除或修改角色 &#40;Management Studio&#41;</span><span class="sxs-lookup"><span data-stu-id="54696-128">Create, Delete, or Modify a Role &#40;Management Studio&#41;</span></span>](../reporting-services/security/role-definitions-create-delete-or-modify.md)  
  
-   [<span data-ttu-id="54696-129">啟用和停用 Reporting Services 的用戶端列印功能</span><span class="sxs-lookup"><span data-stu-id="54696-129">Enable and Disable Client-Side Printing for Reporting Services</span></span>](../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)  
  
## <a name="see-also"></a><span data-ttu-id="54696-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="54696-130">See Also</span></span>  
 <span data-ttu-id="54696-131">[使用 SQL Server Data Tools &#40;SSDT&#41;建立多維度模型](https://docs.microsoft.com/analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt) </span><span class="sxs-lookup"><span data-stu-id="54696-131">[Creating Multidimensional Models Using SQL Server Data Tools &#40;SSDT&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt) </span></span>  
 [<span data-ttu-id="54696-132">SQL Server Data Tools &#40;SSDT 中的 Reporting Services&#41;</span><span class="sxs-lookup"><span data-stu-id="54696-132">Reporting Services in SQL Server Data Tools &#40;SSDT&#41;</span></span>](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)  
  
  