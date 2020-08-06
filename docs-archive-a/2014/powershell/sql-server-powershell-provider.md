---
title: SQL Server PowerShell 提供者 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- PowerShell [SQL Server], provider
- PowerShell [SQL Server], SQL Server PowerShell Provider
- Providers [PowerShell]
- SMO [SQL Server], PowerShell
- PowerShell [SQL Server], SMO
- SQL Server Management Objects, PowerShell
ms.assetid: b97acc43-fcd2-4ae5-b218-e183bab916f9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 425c49fe8ebed1ea75c7872f9b99af5ea0f510ff
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87699874"
---
# <a name="sql-server-powershell-provider"></a><span data-ttu-id="79e05-102">SQL Server PowerShell 提供者</span><span class="sxs-lookup"><span data-stu-id="79e05-102">SQL Server PowerShell Provider</span></span>
  <span data-ttu-id="79e05-103">適用於 Windows PowerShell 的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者會公開類似於檔案系統路徑之路徑中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件階層。</span><span class="sxs-lookup"><span data-stu-id="79e05-103">The [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] provider for Windows PowerShell exposes the hierarchy of [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] objects in paths similar to file system paths.</span></span> <span data-ttu-id="79e05-104">您可以使用路徑來尋找物件，然後使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理物件 (SMO) 模型中的方法來針對物件執行動作。</span><span class="sxs-lookup"><span data-stu-id="79e05-104">You can use the paths to locate an object, and then use methods from the [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Object (SMO) models to perform actions on the objects.</span></span>  
  
## <a name="benefits-of-the-sql-server-powershell-provider"></a><span data-ttu-id="79e05-105">SQL Server PowerShell 提供者的優點</span><span class="sxs-lookup"><span data-stu-id="79e05-105">Benefits of the SQL Server PowerShell Provider</span></span>  
 <span data-ttu-id="79e05-106">[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者所實作的路徑可以輕鬆並以互動方式檢閱 SQL Server 執行個體中所有的物件。</span><span class="sxs-lookup"><span data-stu-id="79e05-106">The paths implemented by the [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] provider enable easily and interactively reviewing all of the objects in an instance of SQL Server.</span></span> <span data-ttu-id="79e05-107">您可以使用 Windows PowerShell 別名來導覽路徑，而別名類似於一般用來導覽檔案系統路徑的命令。</span><span class="sxs-lookup"><span data-stu-id="79e05-107">You can navigate the paths using Windows PowerShell aliases similar to the commands you typically use to navigate file system paths.</span></span>  
  
## <a name="the-sql-server-powershell-hierarchy"></a><span data-ttu-id="79e05-108">SQL Server PowerShell 階層</span><span class="sxs-lookup"><span data-stu-id="79e05-108">The SQL Server PowerShell Hierarchy</span></span>  
 <span data-ttu-id="79e05-109">可以在階層中表示資料或物件模型的產品會使用 Windows PowerShell 提供者來公開階層。</span><span class="sxs-lookup"><span data-stu-id="79e05-109">Products whose data or object models can be represented in a hierarchy use Windows PowerShell providers to expose the hierarchies.</span></span> <span data-ttu-id="79e05-110">這個階層是使用與 Windows 檔案系統所使用之磁碟機和路徑結構類似的結構公開。</span><span class="sxs-lookup"><span data-stu-id="79e05-110">The hierarchy is exposed by using a drive and path structure similar to what the Windows file system uses.</span></span>  
  
 <span data-ttu-id="79e05-111">每個 Windows PowerShell 提供者都會實作一或多個磁碟機，</span><span class="sxs-lookup"><span data-stu-id="79e05-111">Each Windows PowerShell provider implements one or more drives.</span></span> <span data-ttu-id="79e05-112">每一個磁碟機都是相關物件階層的根節點。</span><span class="sxs-lookup"><span data-stu-id="79e05-112">Each drive is the root node of a hierarchy of related objects.</span></span> <span data-ttu-id="79e05-113">[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者會實作 SQLSERVER: 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="79e05-113">The [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] provider implements a SQLSERVER: drive.</span></span> <span data-ttu-id="79e05-114">該提供者也會針對 SQLSERVER: 磁碟機定義一組主要資料夾。</span><span class="sxs-lookup"><span data-stu-id="79e05-114">The provider also defines a set of primary folders for the SQLSERVER: drive.</span></span> <span data-ttu-id="79e05-115">每個資料夾及其子資料夾都代表可使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理物件模型存取的一組物件。</span><span class="sxs-lookup"><span data-stu-id="79e05-115">Each folder and its subfolders represent the set of objects that can be accessed by using a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] management object model.</span></span> <span data-ttu-id="79e05-116">當您將焦點放在以其中一個主資料夾為開頭之路徑的子資料夾上時，就可以使用相關聯物件模型中的方法，針對此節點所表示的物件來執行動作。</span><span class="sxs-lookup"><span data-stu-id="79e05-116">When you are focused on a subfolder in a path that starts with one of these primary folders, you can use the methods from the associated object model to perform actions on the object that is represented by the node.</span></span> <span data-ttu-id="79e05-117">[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 提供者實作的 Windows PowerShell 資料夾列在下表中。</span><span class="sxs-lookup"><span data-stu-id="79e05-117">The Windows PowerShell folders implemented by the [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] provider are listed in the following table.</span></span>  
  
|<span data-ttu-id="79e05-118">資料夾</span><span class="sxs-lookup"><span data-stu-id="79e05-118">Folder</span></span>|<span data-ttu-id="79e05-119">SQL Server 物件模型命名空間</span><span class="sxs-lookup"><span data-stu-id="79e05-119">SQL Server object model namespace</span></span>|<span data-ttu-id="79e05-120">物件</span><span class="sxs-lookup"><span data-stu-id="79e05-120">Objects</span></span>|  
|------------|---------------------------------------|-------------|  
|<span data-ttu-id="79e05-121">SQLSERVER:\SQL</span><span class="sxs-lookup"><span data-stu-id="79e05-121">SQLSERVER:\SQL</span></span>|<xref:Microsoft.SqlServer.Management.Smo><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Agent><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Broker><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Mail>|<span data-ttu-id="79e05-122">資料庫物件，例如資料表、檢視表和預存程序。</span><span class="sxs-lookup"><span data-stu-id="79e05-122">Database objects, such as tables, views, and stored procedures.</span></span>|  
|<span data-ttu-id="79e05-123">SQLSERVER:\SQLPolicy</span><span class="sxs-lookup"><span data-stu-id="79e05-123">SQLSERVER:\SQLPolicy</span></span>|<xref:Microsoft.SqlServer.Management.Dmf><br /><br /> <xref:Microsoft.SqlServer.Management.Facets>|<span data-ttu-id="79e05-124">以原則為基礎的管理物件，例如原則和 Facet。</span><span class="sxs-lookup"><span data-stu-id="79e05-124">Policy-based management objects, such as policies and facets.</span></span>|  
|<span data-ttu-id="79e05-125">SQLSERVER:\SQLRegistration</span><span class="sxs-lookup"><span data-stu-id="79e05-125">SQLSERVER:\SQLRegistration</span></span>|<xref:Microsoft.SqlServer.Management.RegisteredServers><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.RegSvrEnum>|<span data-ttu-id="79e05-126">已註冊的伺服器物件，例如伺服器群組和已註冊的伺服器。</span><span class="sxs-lookup"><span data-stu-id="79e05-126">Registered server objects, such as server groups and registered servers.</span></span>|  
|<span data-ttu-id="79e05-127">SQLSERVER:\Utility</span><span class="sxs-lookup"><span data-stu-id="79e05-127">SQLSERVER:\Utility</span></span>|<xref:Microsoft.SqlServer.Management.Utility>|<span data-ttu-id="79e05-128">公用程式物件，例如， [!INCLUDE[ssDE](../includes/ssde-md.md)]的受管理的執行個體。</span><span class="sxs-lookup"><span data-stu-id="79e05-128">Utility objects, such as managed instances of the [!INCLUDE[ssDE](../includes/ssde-md.md)].</span></span>|  
|<span data-ttu-id="79e05-129">SQLSERVER:\DAC</span><span class="sxs-lookup"><span data-stu-id="79e05-129">SQLSERVER:\DAC</span></span>|[<span data-ttu-id="79e05-130">Microsoft. SqlServer. 管理 DAC</span><span class="sxs-lookup"><span data-stu-id="79e05-130">Microsoft.SqlServer.Management.DAC</span></span>](/dotnet/api/microsoft.sqlserver.management.utility.deployeddac)|<span data-ttu-id="79e05-131">資料層應用程式物件 (如 DAC 封裝) 與作業 (如部署 DAC)。</span><span class="sxs-lookup"><span data-stu-id="79e05-131">Data-tier application objects such as DAC packages, and operations such as deploying a DAC.</span></span>|  
|<span data-ttu-id="79e05-132">SQLSERVER:\DataCollection</span><span class="sxs-lookup"><span data-stu-id="79e05-132">SQLSERVER:\DataCollection</span></span>|<xref:Microsoft.SqlServer.Management.Collector>|<span data-ttu-id="79e05-133">資料收集器物件，例如收集組和組態存放區。</span><span class="sxs-lookup"><span data-stu-id="79e05-133">Data collector objects, such as collection sets and configuration stores.</span></span>|  
|<span data-ttu-id="79e05-134">SQLSERVER:\IntegrationServices</span><span class="sxs-lookup"><span data-stu-id="79e05-134">SQLSERVER:\IntegrationServices</span></span>|<xref:Microsoft.SqlServer.Management.IntegrationServices>|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] <span data-ttu-id="79e05-135">物件，例如專案、封裝和環境。</span><span class="sxs-lookup"><span data-stu-id="79e05-135">objects such as projects, packages, and environments.</span></span>|  
|<span data-ttu-id="79e05-136">SQLSERVER:\SQLAS</span><span class="sxs-lookup"><span data-stu-id="79e05-136">SQLSERVER:\SQLAS</span></span>|<xref:Microsoft.AnalysisServices>|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] <span data-ttu-id="79e05-137">物件，例如 Cube、彙總和維度。</span><span class="sxs-lookup"><span data-stu-id="79e05-137">objects such as cubes, aggregations, and dimensions.</span></span>|  
  
 <span data-ttu-id="79e05-138">例如，您可以使用 SQLSERVER:\SQL 資料夾來當做可代表 SMO 物件模型所支援之任何物件的路徑開頭。</span><span class="sxs-lookup"><span data-stu-id="79e05-138">For example, you can use the SQLSERVER:\SQL folder to start paths that can represent any object that is supported by the SMO object model.</span></span> <span data-ttu-id="79e05-139">Sqlserver： \ sql 路徑的前置部分是 sqlserver： \ sql \\ *ComputerName* \\ *InstanceName*。</span><span class="sxs-lookup"><span data-stu-id="79e05-139">The leading part of a SQLSERVER:\SQL path is SQLSERVER:\SQL\\*ComputerName*\\*InstanceName*.</span></span> <span data-ttu-id="79e05-140">執行個體名稱之後的節點會在物件集合 (例如「資料庫」\*\* 或「檢視」\*\*) 和物件名稱 (例如 AdventureWorks2012) 之間輪替。</span><span class="sxs-lookup"><span data-stu-id="79e05-140">The nodes after the instance name alternate between object collections (such as *Databases* or *Views*) and object names (such as AdventureWorks2012).</span></span> <span data-ttu-id="79e05-141">結構描述不會表示為物件類別。</span><span class="sxs-lookup"><span data-stu-id="79e05-141">Schemas are not represented as object classes.</span></span> <span data-ttu-id="79e05-142">當您在結構描述中指定最上層物件的節點 (如資料表或檢視表) 時，必須使用 *SchemaName.ObjectName*格式來指定物件名稱。</span><span class="sxs-lookup"><span data-stu-id="79e05-142">When you specify the node for a top-level object in a schema, such as a table or view, you must specify the object name in the format *SchemaName.ObjectName*.</span></span>  
  
 <span data-ttu-id="79e05-143">這是本機電腦上預設 [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體中 AdventureWorks2012 資料庫之 Purchasing 結構描述的 Vendor 資料表路徑：</span><span class="sxs-lookup"><span data-stu-id="79e05-143">This is the path of the Vendor table in the Purchasing schema of the AdventureWorks2012 database in a default instance of the [!INCLUDE[ssDE](../includes/ssde-md.md)] on the local computer:</span></span>  
  
```  
SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012\Tables\Purchasing.Vendor  
```  
  
 <span data-ttu-id="79e05-144">如需有關 SMO 物件模型階層的詳細資訊，請參閱 [SMO 物件模型圖表](../relational-databases/server-management-objects-smo/smo-object-model-diagram.md)。</span><span class="sxs-lookup"><span data-stu-id="79e05-144">For more information about the SMO object model hierarchy, see [SMO Object Model Diagram](../relational-databases/server-management-objects-smo/smo-object-model-diagram.md).</span></span>  
  
 <span data-ttu-id="79e05-145">路徑中的集合節點會與相關聯物件模型中的集合類別產生關聯。</span><span class="sxs-lookup"><span data-stu-id="79e05-145">Collection nodes in a path are associated with a collection class in the associated object model.</span></span> <span data-ttu-id="79e05-146">物件名稱節點會與相關聯物件模型中的物件類別產生關聯，如下表所示。</span><span class="sxs-lookup"><span data-stu-id="79e05-146">Object name nodes are associated with an object class in the associated object model, as in the following table.</span></span>  
  
|<span data-ttu-id="79e05-147">Path</span><span class="sxs-lookup"><span data-stu-id="79e05-147">Path</span></span>|<span data-ttu-id="79e05-148">SMO 類別</span><span class="sxs-lookup"><span data-stu-id="79e05-148">SMO class</span></span>|  
|----------|---------------|  
|<span data-ttu-id="79e05-149">SQLSERVER:\SQL\MyComputer\DEFAULT\Databases</span><span class="sxs-lookup"><span data-stu-id="79e05-149">SQLSERVER:\SQL\MyComputer\DEFAULT\Databases</span></span>|<xref:Microsoft.SqlServer.Management.Smo.DatabaseCollection>|  
|<span data-ttu-id="79e05-150">SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012</span><span class="sxs-lookup"><span data-stu-id="79e05-150">SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012</span></span>|<xref:Microsoft.SqlServer.Management.Smo.Database>|  
  
## <a name="sql-server-provider-tasks"></a><span data-ttu-id="79e05-151">SQL Server 提供者工作</span><span class="sxs-lookup"><span data-stu-id="79e05-151">SQL Server Provider Tasks</span></span>  
  
|<span data-ttu-id="79e05-152">工作描述</span><span class="sxs-lookup"><span data-stu-id="79e05-152">Task Description</span></span>|<span data-ttu-id="79e05-153">主題</span><span class="sxs-lookup"><span data-stu-id="79e05-153">Topic</span></span>|  
|----------------------|-----------|  
|<span data-ttu-id="79e05-154">描述如何使用 Windows PowerShell 指令程式導覽路徑中的節點，而且至少每個節點都會取得該節點的物件清單。</span><span class="sxs-lookup"><span data-stu-id="79e05-154">Describes how to use Windows PowerShell cmdlets to navigate through the nodes in a path, and at each node get a list of the objects at that node.</span></span>|[<span data-ttu-id="79e05-155">導覽 SQL Server PowerShell 路徑</span><span class="sxs-lookup"><span data-stu-id="79e05-155">Navigate SQL Server PowerShell Paths</span></span>](navigate-sql-server-powershell-paths.md)|  
|<span data-ttu-id="79e05-156">描述如何使用 SMO 方法和屬性，針對透過路徑中的節點所代表的物件來報告和執行工作。</span><span class="sxs-lookup"><span data-stu-id="79e05-156">Describes how to use the SMO methods and properties to report on and perform work on the object represented by a node in a path.</span></span> <span data-ttu-id="79e05-157">同時描述如何取得該節點的 SMO 方法和屬性清單。</span><span class="sxs-lookup"><span data-stu-id="79e05-157">Also describes how to get a list of the SMO methods and properties for that node.</span></span>|[<span data-ttu-id="79e05-158">使用 SQL Server PowerShell 路徑</span><span class="sxs-lookup"><span data-stu-id="79e05-158">Work With SQL Server PowerShell Paths</span></span>](work-with-sql-server-powershell-paths.md)|  
|<span data-ttu-id="79e05-159">描述如何將 SMO 統一資源名稱 (URN) 轉換為 SQL Server 提供者路徑。</span><span class="sxs-lookup"><span data-stu-id="79e05-159">Describes how to convert a SMO Uniform Resource Name (URN) to a SQL Server provider path.</span></span>|[<span data-ttu-id="79e05-160">將 URN 轉換成 SQL Server 提供者路徑</span><span class="sxs-lookup"><span data-stu-id="79e05-160">Convert URNs to SQL Server Provider Paths</span></span>](../database-engine/convert-urns-to-sql-server-provider-paths.md)|  
|<span data-ttu-id="79e05-161">描述如何使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者來開啟 SQL Server 驗證連接。</span><span class="sxs-lookup"><span data-stu-id="79e05-161">Describes how to open SQL Server Authentication connections by using the [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] provider.</span></span> <span data-ttu-id="79e05-162">提供者預設會使用的 Windows 驗證連接是使用執行 Windows PowerShell 工作階段之 Windows 帳戶的認證來進行。</span><span class="sxs-lookup"><span data-stu-id="79e05-162">By default, the provider uses Windows Authentication connections made using the credentials of the Windows account running the Windows PowerShell session.</span></span>|[<span data-ttu-id="79e05-163">管理 Database Engine PowerShell 中的驗證</span><span class="sxs-lookup"><span data-stu-id="79e05-163">Manage Authentication in Database Engine PowerShell</span></span>](manage-authentication-in-database-engine-powershell.md)|  
  
## <a name="see-also"></a><span data-ttu-id="79e05-164">另請參閱</span><span class="sxs-lookup"><span data-stu-id="79e05-164">See Also</span></span>  
 [<span data-ttu-id="79e05-165">SQL Server PowerShell</span><span class="sxs-lookup"><span data-stu-id="79e05-165">SQL Server PowerShell</span></span>](sql-server-powershell.md)  
  
  