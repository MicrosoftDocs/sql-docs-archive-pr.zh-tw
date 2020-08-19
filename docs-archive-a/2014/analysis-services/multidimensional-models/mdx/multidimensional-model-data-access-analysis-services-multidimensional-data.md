---
title: 多維度模型資料存取 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SSAS, data access interfaces
- objects [Analysis Services], data access interfaces
- Analysis Services data access interfaces
- data retrieval [Analysis Services]
- retrieving data
- metadata [Analysis Services]
- data access interfaces [Analysis Services]
- manipulating objects [Analysis Services]
- Analysis Services data access interfaces, about data access interfaces
ms.assetid: 46388efb-3c78-47a2-b5c9-5a69ff394d03
author: minewiskan
ms.author: owend
ms.openlocfilehash: 721cfbe160bf65c04462fca28f3b5261c1f1b00c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598612"
---
# <a name="multidimensional-model-data-access-analysis-services---multidimensional-data"></a><span data-ttu-id="a881c-102">多維度模型資料存取 (Analysis Services - 多維度資料)</span><span class="sxs-lookup"><span data-stu-id="a881c-102">Multidimensional Model Data Access (Analysis Services - Multidimensional Data)</span></span>
  <span data-ttu-id="a881c-103">使用本主題中的資訊了解如何使用程式設計方法、指令碼或用戶端應用程式 (其中包含的內建支援可連接至網路上的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器) 存取 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 多維度資料。</span><span class="sxs-lookup"><span data-stu-id="a881c-103">Use the information in this topic to learn how to access [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] multidimensional data using programmatic methods, script, or client applications that include built-in support for connecting to an [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] server on your network.</span></span>  
  
 <span data-ttu-id="a881c-104">本主題包含下列幾節：</span><span class="sxs-lookup"><span data-stu-id="a881c-104">This topic contains the following sections:</span></span>  
  
 [<span data-ttu-id="a881c-105">用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="a881c-105">Client Applications</span></span>](#bkmk_clientapps)  
  
 [<span data-ttu-id="a881c-106">查詢語言</span><span class="sxs-lookup"><span data-stu-id="a881c-106">Query Languages</span></span>](#bkmk_querylang)  
  
 [<span data-ttu-id="a881c-107">程式設計介面</span><span class="sxs-lookup"><span data-stu-id="a881c-107">Programmatic Interfaces</span></span>](#bkmk_api)  
  
##  <a name="client-applications"></a><a name="bkmk_clientapps"></a><span data-ttu-id="a881c-108">用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="a881c-108">Client Applications</span></span>  
 <span data-ttu-id="a881c-109">雖然 Analysis Services 提供的介面可讓您使用程式設計方式建立或整合多維度資料庫，但更常見的方法是使用 Microsoft 以及對 Analysis Services 資料擁有內建資料存取之其他軟體廠商所提供的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="a881c-109">Although Analysis Services provides interfaces that let you build or integrate multidimensional databases programmatically, a more common approach is to use existing client applications from Microsoft and other software vendors that have built-in data access to Analysis Services data.</span></span>  
  
 <span data-ttu-id="a881c-110">下列 Microsoft 應用程式支援多維度資料的原生連接。</span><span class="sxs-lookup"><span data-stu-id="a881c-110">The following Microsoft applications support native connections to multidimensional data.</span></span>  
  
### <a name="excel"></a><span data-ttu-id="a881c-111">Excel</span><span class="sxs-lookup"><span data-stu-id="a881c-111">Excel</span></span>  
 <span data-ttu-id="a881c-112">Analysis Services 多維度資料通常是使用 Excel 活頁簿中的樞紐分析表和樞紐分析圖控制項呈現。</span><span class="sxs-lookup"><span data-stu-id="a881c-112">Analysis Services multidimensional data is often presented using pivot tables and pivot chart controls in an Excel workbook.</span></span> <span data-ttu-id="a881c-113">樞紐分析表適用於多維度資料，因為模型中的階層、彙總與導覽建構函式與樞紐分析表的資料摘要功能是絕配。</span><span class="sxs-lookup"><span data-stu-id="a881c-113">PivotTables are suited to multidimensional data because the hierarchies, aggregations, and navigational constructs in the model pair well with the data summary features of a PivotTable.</span></span> <span data-ttu-id="a881c-114">Analysis Services OLE DB 資料提供者包含在 Excel 安裝中，可以讓資料連接的設定更為容易。</span><span class="sxs-lookup"><span data-stu-id="a881c-114">An Analysis Services OLE DB data provider is included in an Excel installation to make setting up data connections easier.</span></span> <span data-ttu-id="a881c-115">如需詳細資訊，請參閱＜ [連接到 SQL Server Analysis Services 或是從中匯入資料](https://go.microsoft.com/fwlink/?linkID=215150)＞。</span><span class="sxs-lookup"><span data-stu-id="a881c-115">For more information, see [Connect to or import data from SQL Server Analysis Services](https://go.microsoft.com/fwlink/?linkID=215150).</span></span>  
  
### <a name="reporting-services-reports"></a><span data-ttu-id="a881c-116">Reporting Services 報表</span><span class="sxs-lookup"><span data-stu-id="a881c-116">Reporting Services Reports</span></span>  
 <span data-ttu-id="a881c-117">您可以使用報表產生器或報表設計師建立取用包含分析資料之 Analysis Services 資料庫的報表。</span><span class="sxs-lookup"><span data-stu-id="a881c-117">You can use Report Builder or Report Designer to create reports that consume Analysis Services databases that contain analytical data.</span></span> <span data-ttu-id="a881c-118">報表產生器和報表設計師都包含一個 MDX 查詢設計工具，您可以使用此查詢設計工具輸入或設計從可用資料來源擷取的 MDX 陳述式。</span><span class="sxs-lookup"><span data-stu-id="a881c-118">Both Report Builder and Report Designer include an MDX query designer that you can use to type or design MDX statements that retrieve data from an available data source.</span></span> <span data-ttu-id="a881c-119">如需詳細資訊，請參閱 [Reporting Services 支援的資料來源 &#40;SSRS&#41;](../../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md) 和 [MDX 的 Analysis Services 連接類型 &#40;SSRS&#41;](../../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)。</span><span class="sxs-lookup"><span data-stu-id="a881c-119">For more information, see [Data Sources Supported by Reporting Services &#40;SSRS&#41;](../../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md) and [Analysis Services Connection Type for MDX &#40;SSRS&#41;](../../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md).</span></span>  
  
### <a name="performancepoint-dashboards"></a><span data-ttu-id="a881c-120">PerformancePoint 儀表板</span><span class="sxs-lookup"><span data-stu-id="a881c-120">PerformancePoint Dashboards</span></span>  
 <span data-ttu-id="a881c-121">PerformancePoint 儀表板用來在 SharePoint 中建立計分卡，這些計分卡會根據預先定義的量值，傳達商務效能。</span><span class="sxs-lookup"><span data-stu-id="a881c-121">PerformancePoint Dashboards are used to create scorecards in SharePoint that communicate business performance against predefined measures.</span></span> <span data-ttu-id="a881c-122">PerformancePoint 包含 Analysis Services 多維度資料的資料連接支援。</span><span class="sxs-lookup"><span data-stu-id="a881c-122">PerformancePoint includes support for data connections to Analysis Services multidimensional data.</span></span> <span data-ttu-id="a881c-123">如需詳細資訊，請參閱 [建立 Analysis Services 資料連接 (PerformancePoint Services)](https://go.microsoft.com/fwlink/?linkid=232471)。</span><span class="sxs-lookup"><span data-stu-id="a881c-123">For more information, [Create an Analysis Services data connection (PerformancePoint Services)](https://go.microsoft.com/fwlink/?linkid=232471).</span></span>  
  
### <a name="sql-server-data-tools"></a><span data-ttu-id="a881c-124">SQL Server Data Tools</span><span class="sxs-lookup"><span data-stu-id="a881c-124">SQL Server Data Tools</span></span>  
 <span data-ttu-id="a881c-125">模型和報表設計師使用 SQL Server Data Tools 建立包含多維度模型的方案。</span><span class="sxs-lookup"><span data-stu-id="a881c-125">Model and report designers use SQL Server Data Tools to build solutions that include multidimensional models.</span></span> <span data-ttu-id="a881c-126">將方案部署至 Analysis Services 執行個體就是建立您之後從 Excel、Reporting Services 以及其他商業智慧用戶端應用程式連接之資料庫的程序。</span><span class="sxs-lookup"><span data-stu-id="a881c-126">Deploying the solution to an Analysis Services instance is what creates the database that you subsequently connect to from Excel, Reporting Services, and other business intelligence client applications.</span></span>  
  
 <span data-ttu-id="a881c-127">SQL Server Data Tools 建立在 Visual Studio Shell 之上，並使用專案組織與包含模型。</span><span class="sxs-lookup"><span data-stu-id="a881c-127">SQL Server Data Tools is built on a Visual Studio shell and uses projects to organize and contain the model.</span></span> <span data-ttu-id="a881c-128">如需詳細資訊，請參閱[使用 SQL Server 資料工具建立多維度模型 &#40;SSDT&#41;](../creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)。</span><span class="sxs-lookup"><span data-stu-id="a881c-128">For more information, see [Creating Multidimensional Models Using SQL Server Data Tools &#40;SSDT&#41;](../creating-multidimensional-models-using-sql-server-data-tools-ssdt.md).</span></span>  
  
### <a name="sql-server-management-studio"></a><span data-ttu-id="a881c-129">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="a881c-129">SQL Server Management Studio</span></span>  
 <span data-ttu-id="a881c-130">對於資料庫管理員，SQL Server Management Studio 是一個整合式的環境，可用來管理 SQL Server 執行個體，包括 Analysis Services 的執行個體與多維度資料庫。</span><span class="sxs-lookup"><span data-stu-id="a881c-130">For database administrators, SQL Server Management Studio is an integrated environment for managing your SQL Server instances, including instances of Analysis Services and multidimensional databases.</span></span> <span data-ttu-id="a881c-131">如需詳細資訊，請參閱 [SQL Server Management Studio](../../../ssms/sql-server-management-studio-ssms.md) 和 [連接到 Analysis Services](../../instances/connect-to-analysis-services.md)。</span><span class="sxs-lookup"><span data-stu-id="a881c-131">For more information, see [SQL Server Management Studio](../../../ssms/sql-server-management-studio-ssms.md) and [Connect to Analysis Services](../../instances/connect-to-analysis-services.md).</span></span>  
  
##  <a name="query-languages"></a><a name="bkmk_querylang"></a><span data-ttu-id="a881c-132">查詢語言</span><span class="sxs-lookup"><span data-stu-id="a881c-132">Query Languages</span></span>  
 <span data-ttu-id="a881c-133">MDX 是一個業界標準查詢與計算語言，可用來擷取 OLAP 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="a881c-133">MDX is an industry standard query and calculation language used to retrieve data from OLAP databases.</span></span> <span data-ttu-id="a881c-134">在 Analysis Services 中，MDX 是用來擷取資料的查詢語言，但也支援資料定義與資料操作。</span><span class="sxs-lookup"><span data-stu-id="a881c-134">In Analysis Services, MDX is the query language used to retrieve data, but also supports data definition and data manipulation.</span></span> <span data-ttu-id="a881c-135">MDX 編輯器內建在 SQL Server Management Studio、Reporting Services 和 SQL Server Data Tools 中。</span><span class="sxs-lookup"><span data-stu-id="a881c-135">MDX editors are built into SQL Server Management Studio, Reporting Services, and SQL Server Data Tools.</span></span> <span data-ttu-id="a881c-136">您可以使用 MDX 編輯器建立特定查詢或可重複使用的指令碼 (如果是可重複的資料作業)。</span><span class="sxs-lookup"><span data-stu-id="a881c-136">You can use the MDX editors to create ad hoc queries or reusable script if the data operation is repeatable.</span></span>  
  
 <span data-ttu-id="a881c-137">有些工具和應用程式 (例如 Excel) 在內部使用 MDX 建構函式來查詢 Analysis Services 資料來源。</span><span class="sxs-lookup"><span data-stu-id="a881c-137">Some tools and applications, such as Excel, use MDX constructs internally to query an Analysis Services data source.</span></span> <span data-ttu-id="a881c-138">您也可以在程式設計上使用 MDX，只要將 MDX 陳述式包含在 XMLA Execute 要求中即可。</span><span class="sxs-lookup"><span data-stu-id="a881c-138">You can also use MDX programmatically, by enclosing MDX statement in an XMLA Execute request.</span></span>  
  
 <span data-ttu-id="a881c-139">下列連結提供有關 MDX 的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="a881c-139">The following links provide more information about MDX:</span></span>  
  
 [<span data-ttu-id="a881c-140">使用 MDX 查詢多維度資料</span><span class="sxs-lookup"><span data-stu-id="a881c-140">Querying Multidimensional Data with MDX</span></span>](querying-multidimensional-data-with-mdx.md)  
  
 [<span data-ttu-id="a881c-141">MDX 的關鍵概念 &#40;Analysis Services&#41;</span><span class="sxs-lookup"><span data-stu-id="a881c-141">Key Concepts in MDX &#40;Analysis Services&#41;</span></span>](../key-concepts-in-mdx-analysis-services.md)  
  
 [<span data-ttu-id="a881c-142">MDX 查詢基礎觀念 &#40;Analysis Services&#41;</span><span class="sxs-lookup"><span data-stu-id="a881c-142">MDX Query Fundamentals &#40;Analysis Services&#41;</span></span>](mdx-query-fundamentals-analysis-services.md)  
  
 [<span data-ttu-id="a881c-143">MDX 指令碼基礎觀念 &#40;Analysis Services&#41;</span><span class="sxs-lookup"><span data-stu-id="a881c-143">MDX Scripting Fundamentals &#40;Analysis Services&#41;</span></span>](mdx-scripting-fundamentals-analysis-services.md)  
  
##  <a name="programmatic-interfaces"></a><a name="bkmk_api"></a><span data-ttu-id="a881c-144">程式設計介面</span><span class="sxs-lookup"><span data-stu-id="a881c-144">Programmatic Interfaces</span></span>  
 <span data-ttu-id="a881c-145">如果您要建立使用多維度資料的自訂應用程式，您存取資料的方法最有可能分成下列其中一個類別：</span><span class="sxs-lookup"><span data-stu-id="a881c-145">If you are building a custom application that uses multidimensional data, your approach for accessing the data will most likely fall into one of the following categories:</span></span>  
  
-   <span data-ttu-id="a881c-146">**XMLA**。</span><span class="sxs-lookup"><span data-stu-id="a881c-146">**XMLA**.</span></span> <span data-ttu-id="a881c-147">當您需要與多種作業系統和通訊協定相容時，請使用 XMLA。</span><span class="sxs-lookup"><span data-stu-id="a881c-147">Use XMLA when you require compatibility with a wide variety of operating systems and protocols.</span></span> <span data-ttu-id="a881c-148">XMLA 提供最大的彈性，但代價是犧牲提升的效能與程式設計的簡易性。</span><span class="sxs-lookup"><span data-stu-id="a881c-148">XMLA offers the greatest flexibility, but often at the cost of improved performance and ease of programming.</span></span>  
  
-   <span data-ttu-id="a881c-149">**用戶端程式庫**。</span><span class="sxs-lookup"><span data-stu-id="a881c-149">**Client libraries**.</span></span> <span data-ttu-id="a881c-150">當您想要從在 Microsoft Windows 作業系統上執行的用戶端程式使用程式設計方式存取資料時，請使用 Analysis Services 用戶端程式庫 (例如 ADOMD.NET、AMO 和 OLE DB)。</span><span class="sxs-lookup"><span data-stu-id="a881c-150">Use Analysis Services client libraries, such as ADOMD.NET, AMO, and OLE DB when you want to access data programmatically from client applications that run on a Microsoft Windows operating system.</span></span> <span data-ttu-id="a881c-151">用戶端應用程式會使用提供更好效能的物件模型與最佳化包裝 XMLA。</span><span class="sxs-lookup"><span data-stu-id="a881c-151">The client libraries wrap XMLA with an object model and optimizations that provide better performance.</span></span>  
  
     <span data-ttu-id="a881c-152">ADOMD.NET 和 AMO 用戶端程式庫則供使用 Managed 程式碼撰寫的應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="a881c-152">ADOMD.NET and AMO client libraries are for applications written in managed code.</span></span> <span data-ttu-id="a881c-153">如果您的應用程式是以原生程式碼撰寫，請使用 OLE DB for Analysis Services。</span><span class="sxs-lookup"><span data-stu-id="a881c-153">Use OLE DB for Analysis Services if your application is written in native code.</span></span>  
  
 <span data-ttu-id="a881c-154">下表提供連接 Analysis Services 與自訂應用程式所使用之用戶端程式庫的其他詳細資料和連結。</span><span class="sxs-lookup"><span data-stu-id="a881c-154">The following table provides additional detail and links about the client libraries used for connecting Analysis Services to a custom application.</span></span>  
  
|<span data-ttu-id="a881c-155">介面</span><span class="sxs-lookup"><span data-stu-id="a881c-155">Interface</span></span>|<span data-ttu-id="a881c-156">描述</span><span class="sxs-lookup"><span data-stu-id="a881c-156">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="a881c-157">Analysis Services 管理物件 (AMO)</span><span class="sxs-lookup"><span data-stu-id="a881c-157">Analysis Services Management Objects (AMO)</span></span>|<span data-ttu-id="a881c-158">AMO 是在程式碼中管理 Analysis Services 執行個體與多維度資料庫的主要物件模型。</span><span class="sxs-lookup"><span data-stu-id="a881c-158">AMO is the primary object model for administering Analysis Services instances and multidimensional databases in code.</span></span> <span data-ttu-id="a881c-159">例如，SQL Server Management Studio 使用 AMO 支援伺服器與資料庫管理。</span><span class="sxs-lookup"><span data-stu-id="a881c-159">For example, SQL Server Management Studio uses AMO to support server and database administration.</span></span> <span data-ttu-id="a881c-160">如需詳細資訊，請參閱[使用分析管理物件 &#40;AMO&#41; 來開發](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)。</span><span class="sxs-lookup"><span data-stu-id="a881c-160">For more information, see [Developing with Analysis Management Objects &#40;AMO&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo).</span></span>|  
|<span data-ttu-id="a881c-161">ADOMD.NET</span><span class="sxs-lookup"><span data-stu-id="a881c-161">ADOMD.NET</span></span>|<span data-ttu-id="a881c-162">ADOMD.NET 是在自訂應用程式中建立與存取多維度資料的主要物件模型。</span><span class="sxs-lookup"><span data-stu-id="a881c-162">ADOMD.NET is the primary object model creating and accessing multidimensional data in custom applications.</span></span> <span data-ttu-id="a881c-163">您可以使用通用的 Microsoft .NET Framework 資料存取介面，在 Managed 用戶端應用程式中使用 ADOMD.NET 來擷取 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資訊。</span><span class="sxs-lookup"><span data-stu-id="a881c-163">You can use ADOMD.NET in a managed client application to retrieve [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] information using common Microsoft .NET Framework data access interfaces.</span></span> <span data-ttu-id="a881c-164">如需詳細資訊，請參閱 [使用 ADOMD.NET 來開發](https://docs.microsoft.com/bi-reference/adomd/developing-with-adomd-net) 和 [ADOMD.NET 用戶端程式設計](https://docs.microsoft.com/analysis-services/adomd/multidimensional-models-adomd-net-client/adomd-net-client-programming)。</span><span class="sxs-lookup"><span data-stu-id="a881c-164">For more information, see [Developing with ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/developing-with-adomd-net) and [ADOMD.NET Client Programming](https://docs.microsoft.com/analysis-services/adomd/multidimensional-models-adomd-net-client/adomd-net-client-programming).</span></span>|  
|<span data-ttu-id="a881c-165">Analysis Services OLE DB 提供者 (MSOLAP.dll)</span><span class="sxs-lookup"><span data-stu-id="a881c-165">Analysis Services OLE DB Provider (MSOLAP.dll)</span></span>|<span data-ttu-id="a881c-166">您可以使用原生 OLE DB 提供者，使用程式設計方式從 Unmanaged API 存取 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="a881c-166">You can use the native OLE DB provider to access [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] programmatically from a non-managed API.</span></span> <span data-ttu-id="a881c-167">如需詳細資訊，請參閱 [Analysis Services OLE DB 提供者 &#40;Analysis Services - 多維度資料&#41;](../../dev-guide/analysis-services-ole-db-provider-analysis-services-multidimensional-data.md)。</span><span class="sxs-lookup"><span data-stu-id="a881c-167">For more information, see [Analysis Services OLE DB Provider &#40;Analysis Services - Multidimensional Data&#41;](../../dev-guide/analysis-services-ole-db-provider-analysis-services-multidimensional-data.md).</span></span>|  
|<span data-ttu-id="a881c-168">結構描述資料列集</span><span class="sxs-lookup"><span data-stu-id="a881c-168">Schema Rowsets</span></span>|<span data-ttu-id="a881c-169">結構描述資料列集資料表是一種資料結構，其中包含有關在伺服器上部署之多維度模型的描述性資訊，以及有關伺服器上目前活動的資訊。</span><span class="sxs-lookup"><span data-stu-id="a881c-169">Schema rowset tables are data structures that contain descriptive information about a multidimensional model that is deployed on the server, as well as information about current activity on the server.</span></span> <span data-ttu-id="a881c-170">身為程式設計人員，您可以在用戶端應用程式中查詢結構描述資料列集資料表，以檢查儲存在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體上的中繼資料，並從其擷取支援和監視資訊。</span><span class="sxs-lookup"><span data-stu-id="a881c-170">As a programmer, you can query schema rowset tables in client applications to examine metadata stored on, and retrieve support and monitoring information from, an [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instance.</span></span> <span data-ttu-id="a881c-171">您可以搭配這些程式設計介面使用結構描述資料列集：OLE DB、OLE DB for Analysis Services、OLE DB for Data Mining 或 XMLA。</span><span class="sxs-lookup"><span data-stu-id="a881c-171">You can use schema rowsets with these programmatic interfaces: OLE DB, OLE DB for Analysis Services, OLE DB for Data Mining, or XMLA.</span></span> <span data-ttu-id="a881c-172">如需詳細資訊，請參閱 [Analysis Services 結構描述資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/analysis-services-schema-rowsets)。</span><span class="sxs-lookup"><span data-stu-id="a881c-172">For more information, see [Analysis Services Schema Rowsets](https://docs.microsoft.com/bi-reference/schema-rowsets/analysis-services-schema-rowsets).</span></span><br /><br /> <span data-ttu-id="a881c-173">以下清單說明使用結構描述資料列集的數個方法：</span><span class="sxs-lookup"><span data-stu-id="a881c-173">The following list explains several approaches for using schema rowsets:</span></span><br /><br /> <span data-ttu-id="a881c-174">在 SQL Server Management Studio 或自訂報表中執行 DMV 查詢，以便使用 SQL 語法存取結構描述資料列集。</span><span class="sxs-lookup"><span data-stu-id="a881c-174">Run DMV queries in SQL Server Management Studio or in custom reports to access schema rowsets using SQL syntax.</span></span> <span data-ttu-id="a881c-175">如需詳細資訊，請參閱[使用動態管理檢視 &#40;DMV&#41; 監視 Analysis Services](../../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)。</span><span class="sxs-lookup"><span data-stu-id="a881c-175">For more information, see [Use Dynamic Management Views &#40;DMVs&#41; to Monitor Analysis Services](../../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md).</span></span><br /><br /> <span data-ttu-id="a881c-176">撰寫呼叫結構描述資料列集的 ADOMD.NET 程式碼。</span><span class="sxs-lookup"><span data-stu-id="a881c-176">Write ADOMD.NET code that calls a schema rowset.</span></span><br /><br /> <span data-ttu-id="a881c-177">直接針對 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體執行 XMLA `Discover` 方法，以擷取結構描述資料列集資訊。</span><span class="sxs-lookup"><span data-stu-id="a881c-177">Run the XMLA `Discover` method directly against an [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instance to retrieve schema rowset information.</span></span> <span data-ttu-id="a881c-178">如需詳細資訊，請參閱 [Discover 方法 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)。</span><span class="sxs-lookup"><span data-stu-id="a881c-178">For more information, see [Discover Method &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover).</span></span>|  
|<span data-ttu-id="a881c-179">XMLA</span><span class="sxs-lookup"><span data-stu-id="a881c-179">XMLA</span></span>|<span data-ttu-id="a881c-180">XMLA 是提供給 Analysis Services 程式設計人員的最低層級 API，也是做為所有 Analysis Services 資料存取方法的共同分母。</span><span class="sxs-lookup"><span data-stu-id="a881c-180">XMLA is the lowest level API available to an Analysis Services programmer, and is the common denominator that underlies all Analysis Services data access methodologies.</span></span> <span data-ttu-id="a881c-181">XMLA 是一種業界標準，SOAP 以 XML 通訊協定為基礎，支援通用資料透過 HTTP 連接，對於任何可用之標準多維度資料來源的存取。</span><span class="sxs-lookup"><span data-stu-id="a881c-181">XMLA is an industry standard, SOAP based XML protocol that supports universal data access to any standard multidimensional data source available over an HTTP connection.</span></span> <span data-ttu-id="a881c-182">它會使用 SOAP 編寫用於多維度資料的要求和回應。</span><span class="sxs-lookup"><span data-stu-id="a881c-182">It uses SOAP to formulate requests and responses for multidimensional data.</span></span> <span data-ttu-id="a881c-183">如果您的應用程式在非 Windows 平台上執行，可以使用 XMLA 存取在網路上的 Windows 伺服器上執行的多維度資料庫。</span><span class="sxs-lookup"><span data-stu-id="a881c-183">If your application runs on a non-Windows platform, you can use XMLA to access a multidimensional database that is running on a Windows server on your network.</span></span> <span data-ttu-id="a881c-184">如需詳細資訊，請參閱 [在 Analysis Services 中使用 XMLA 進行開發](../../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)。</span><span class="sxs-lookup"><span data-stu-id="a881c-184">For more information, see [Developing with XMLA in Analysis Services](../../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md).</span></span>|  
|<span data-ttu-id="a881c-185">Analysis Services 指令碼語言 (ASSL)</span><span class="sxs-lookup"><span data-stu-id="a881c-185">Analysis Services Scripting Language (ASSL)</span></span>|<span data-ttu-id="a881c-186">ASSL 是一個適用於 XMLA 通訊協定之 Analysis Services 延伸模組的描述性詞彙。</span><span class="sxs-lookup"><span data-stu-id="a881c-186">ASSL is a descriptive term that applies to Analysis Services extensions of the XMLA protocol.</span></span> <span data-ttu-id="a881c-187">ASSL 延伸模組可讓 Analysis Services 使用超出通訊協定基本提供範圍的 XMLA 建構函式，以增加資料定義、資料操作以及資料控制支援。</span><span class="sxs-lookup"><span data-stu-id="a881c-187">ASSL extensions enable Analysis Services to use XMLA constructs beyond the basic provisions of the protocol, adding data definition, data manipulation, and data control support.</span></span>  <span data-ttu-id="a881c-188">由於 Execute 和 Discover 方法是由 XMLA 通訊協定所描述，因此 ASSL 會加入下列功能：</span><span class="sxs-lookup"><span data-stu-id="a881c-188">Whereas the Execute and Discover methods are described by the XMLA protocol, ASSL adds the following capability:</span></span><br /><br /> <span data-ttu-id="a881c-189">XMLA 指令碼</span><span class="sxs-lookup"><span data-stu-id="a881c-189">XMLA script</span></span><br /><br /> <span data-ttu-id="a881c-190">XMLA 物件定義</span><span class="sxs-lookup"><span data-stu-id="a881c-190">XMLA object definitions</span></span><br /><br /> <span data-ttu-id="a881c-191">XMLA 命令</span><span class="sxs-lookup"><span data-stu-id="a881c-191">XMLA commands</span></span><br /><br /> <br /><br /> <span data-ttu-id="a881c-192">如需詳細資訊，請參閱＜ [使用 Analysis Services 指令碼語言 &#40;ASSL&#41; 開發](../scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)＞。</span><span class="sxs-lookup"><span data-stu-id="a881c-192">For more information, see [Developing with Analysis Services Scripting Language &#40;ASSL&#41;](../scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="a881c-193">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a881c-193">See Also</span></span>  
 <span data-ttu-id="a881c-194">[連接到 Analysis Services](../../instances/connect-to-analysis-services.md) </span><span class="sxs-lookup"><span data-stu-id="a881c-194">[Connect to Analysis Services](../../instances/connect-to-analysis-services.md) </span></span>  
 <span data-ttu-id="a881c-195">[使用 Analysis Services 指令碼語言進行開發 &#40;ASSL&#41;](../scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md) </span><span class="sxs-lookup"><span data-stu-id="a881c-195">[Developing with Analysis Services Scripting Language &#40;ASSL&#41;](../scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md) </span></span>  
 <span data-ttu-id="a881c-196">[在 Analysis Services 中使用 XMLA 進行開發](../../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md) </span><span class="sxs-lookup"><span data-stu-id="a881c-196">[Developing with XMLA in Analysis Services](../../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md) </span></span>  
 [<span data-ttu-id="a881c-197">表格式模型資料存取</span><span class="sxs-lookup"><span data-stu-id="a881c-197">Tabular Model Data Access</span></span>](../../tabular-models/tabular-model-data-access.md)  
  
  