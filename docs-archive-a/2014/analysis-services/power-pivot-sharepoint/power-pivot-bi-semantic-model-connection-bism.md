---
title: PowerPivot BI 語義模型連接 (. bism) |Microsoft Docs
ms.custom: ''
ms.date: 04/19/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 08828eec-4f8c-4f34-a145-e442f7b7031d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 14a30128986a5ba23cb093be771c036c94fa25ce
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599213"
---
# <a name="powerpivot-bi-semantic-model-connection-bism"></a><span data-ttu-id="fd5ad-102">PowerPivot BI 語意模型連接 (.bism)</span><span class="sxs-lookup"><span data-stu-id="fd5ad-102">PowerPivot BI Semantic Model Connection (.bism)</span></span>
  <span data-ttu-id="fd5ad-103">BI 語意模型連接 (.bism) 是可攜式連接，用於將 Excel 或 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 報表連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格式 model 資料庫或處於多維度模式下的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-103">A BI semantic model connection (.bism) is a portable connection that connects Excel or [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] reports to an [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tabular model database or an [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instance in multidimensional mode.</span></span> <span data-ttu-id="fd5ad-104">如果您熟悉 Office 資料連接 (.odc) 檔案，您會注意到定義和使用 .bism 連接檔案之方式的相似性。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-104">If you are familiar with office data connection (.odc) files, you will notice a similarity in how a .bism connection file is defined and used.</span></span>  
  
 <span data-ttu-id="fd5ad-105">BI 語意模型連接是透過 SharePoint 來建立和存取。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-105">A BI semantic model connection is created and accessed via SharePoint.</span></span> <span data-ttu-id="fd5ad-106">建立 BI 語意模型連接會針對程式庫中的 BI 語意模型連接啟用命令。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-106">Creating BI semantic model connections enables quick launch commands on a BI semantic model connection in a library.</span></span> <span data-ttu-id="fd5ad-107">快速啟動命令會開啟新的 Excel 活頁簿或是編輯連接檔案的選項。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-107">Quick launch commands open a new Excel workbook or options for editing the connection file.</span></span> <span data-ttu-id="fd5ad-108">如果已安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，您也會看到可建立 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 報表的命令。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-108">If [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] is installed, you will also see a command to create a [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] report.</span></span>  
  
 <span data-ttu-id="fd5ad-109">![BISM 快速啟動命令的螢幕擷取畫面](../media/ssas-bism-quicklaunch.gif "BISM 快速啟動命令的螢幕擷取畫面")</span><span class="sxs-lookup"><span data-stu-id="fd5ad-109">![Screenshot of BISM quick launch command](../media/ssas-bism-quicklaunch.gif "Screenshot of BISM quick launch command")</span></span>  
  
##  <a name="supported-databases"></a><a name="bkmk_prereq"></a> <span data-ttu-id="fd5ad-110">支援的資料庫</span><span class="sxs-lookup"><span data-stu-id="fd5ad-110">Supported databases</span></span>  
 <span data-ttu-id="fd5ad-111">BI 語意模型連接指向表格式模型資料庫。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-111">A BI semantic model connection points to tabular model data.</span></span> <span data-ttu-id="fd5ad-112">這個資料有三個來源：</span><span class="sxs-lookup"><span data-stu-id="fd5ad-112">There are three sources for this data:</span></span>  
  
-   <span data-ttu-id="fd5ad-113">在表格式伺服器模式中於獨立 Analysis Services 執行個體上執行的表格式模型資料庫。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-113">A tabular model database running on a standalone Analysis Services instance in tabular server mode.</span></span> <span data-ttu-id="fd5ad-114">獨立 Analysis Services 執行個體的部署來自伺服陣列外部。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-114">A deployment of a standalone Analysis Services instance is external to the farm.</span></span> <span data-ttu-id="fd5ad-115">存取伺服陣列外部的資料來源需要額外的權限，您可以在這個主題中閱讀詳細資訊：＜ [Create a BI Semantic Model Connection to a Tabular Model Database](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)＞。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-115">Accessing data sources off the farm requires additional permissions, which you can read about in this topic: [Create a BI Semantic Model Connection to a Tabular Model Database](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md).</span></span>  
  
-   <span data-ttu-id="fd5ad-116">儲存到 SharePoint 中的 PowerPivot 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-116">PowerPivot workbooks saved to SharePoint.</span></span> <span data-ttu-id="fd5ad-117">Excel 活頁簿內部的內嵌 PowerPivot 資料庫相當於在獨立 Analysis Services 表格式模式伺服器上執行的表格式模型資料庫。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-117">Embedded PowerPivot databases inside Excel workbooks are equivalent to tabular model databases that run on a standalone Analysis Services tabular mode server.</span></span> <span data-ttu-id="fd5ad-118">如果您已經使用 PowerPivot for Excel 和 PowerPivot for SharePoint，可以在 SharePoint 文件庫中定義指向 PowerPivot 活頁簿的 BI 語意模型連接，並使用現有的 PowerPivot 資料建立 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 報表。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-118">If you already use PowerPivot for Excel and PowerPivot for SharePoint, you can define a BI semantic model connection that points to PowerPivot workbooks in a SharePoint library and build [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] reports using existing PowerPivot data.</span></span>  <span data-ttu-id="fd5ad-119">您可以使用在 SQL Server 2008 R2 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版本的 PowerPivot for Excel 中建立的活頁簿。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-119">You can use workbooks created in either SQL Server 2008 R2 or [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] versions of PowerPivot for Excel.</span></span>  
  
-   <span data-ttu-id="fd5ad-120">[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上的多維度資料模型。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-120">A multidimensional data model on an [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instance.</span></span>  
  
 <span data-ttu-id="fd5ad-121">如需資料來源的比較，請參閱「 [瞭解 SQL Server 2012 BI 語義模型 (BISM) ](http://www.mssqltips.com/sqlservertip/2818/understanding-the-sql-server-2012-bi-semantic-model-bism/)的「社區內容」。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-121">For a comparison of the data sources, see the community  content [Understanding the SQL Server 2012 BI Semantic Model (BISM)](http://www.mssqltips.com/sqlservertip/2818/understanding-the-sql-server-2012-bi-semantic-model-bism/).</span></span>  
  
## <a name="understanding-the-connection-sequence-for-bi-semantic-connections"></a><span data-ttu-id="fd5ad-122">了解 BI 語意連接的連接順序</span><span class="sxs-lookup"><span data-stu-id="fd5ad-122">Understanding the Connection Sequence for BI Semantic Connections</span></span>  
 <span data-ttu-id="fd5ad-123">本節說明各種用戶端應用程式 (例如 Excel 桌面應用程式或 SharePoint 上的 Power View 報表用戶端) 和 SharePoint 伺服器陣列內部或外部表格式模型資料庫之間的連接行為。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-123">This section explains the connection behavior between various client applications, such as the Excel desktop application or the Power View reporting client on SharePoint, and a tabular model database inside or outside the SharePoint farm.</span></span>  
  
 <span data-ttu-id="fd5ad-124">表格式模型資料庫的所有連接都是使用要求資料之使用者的認證來建立。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-124">All connections to a tabular model database are made using the credentials of the user who is requesting the data.</span></span> <span data-ttu-id="fd5ad-125">不過，根據連接是伺服器陣列內部連接、單躍點或雙躍點連接，以及 Kerberos 是否啟用，連接機制將會有所不同。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-125">However, the mechanics of that connection will vary depending on whether the connection is an in-farm connection, a single or double-hop connection, and whether Kerberos is enabled.</span></span> <span data-ttu-id="fd5ad-126">如需 SharePoint 與後端資料來源之間驗證連接的詳細資訊，請參閱 [雙躍點驗證：NTLM 失敗與 Kerberos 成功的原因](https://go.microsoft.com/fwlink/?LinkId=237137)。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-126">For more information about authenticated connections between SharePoint and backend data sources, see [Double-hop authentication: Why NTLM fails and Kerberos works](https://go.microsoft.com/fwlink/?LinkId=237137).</span></span>  
  
 <span data-ttu-id="fd5ad-127">**從 Excel 連接到網路上的表格式資料**</span><span class="sxs-lookup"><span data-stu-id="fd5ad-127">**Connecting from Excel to tabular data on a network**</span></span>  
  
 <span data-ttu-id="fd5ad-128">當 Excel 使用者指定 BI 語意模型連接做為資料來源時，.bism 檔案內部的連接資訊會下載至用戶端應用程式，然後用戶端應用程式會將它自己的直接要求發出至 Analysis Services 上的表格式模型資料庫。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-128">When an Excel user specifies a BI semantic model connection as a data source, the connection information inside the .bism file is downloaded to the client application, which then issues its own direct request to the tabular model database on Analysis Services.</span></span> <span data-ttu-id="fd5ad-129">若要存取 .bism 連接，Excel 使用者必須是具有 .bism 連接檔案讀取權限的 SharePoint 使用者。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-129">To access the .bism connection, the Excel user must be a SharePoint user with read permissions on the .bism connection file.</span></span> <span data-ttu-id="fd5ad-130">下載連接資訊之後，所有後續連接都會略過 SharePoint，直接從 Excel 流向後端表格式模型資料庫。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-130">Once the connection information is downloaded, all subsequent connections bypass SharePoint, flowing directly from Excel to the backend tabular model database.</span></span>  
  
 <span data-ttu-id="fd5ad-131">下圖顯示此連接順序。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-131">The following illustration shows this connection sequence.</span></span> <span data-ttu-id="fd5ad-132">一開始是 .bism 連接的要求，接著將連接資訊下載至用戶端，最後是資料庫的單躍點連接。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-132">It starts with a request for the .bism connection, followed by the download of connection information to the client, and finally the single-hop connection to the database.</span></span> <span data-ttu-id="fd5ad-133">連接是使用具有 Analysis Services 資料庫讀取權限之 Excel 使用者的 Windows 認證來建立。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-133">The connection is made using the Windows credentials of the Excel user, who has read permissions on the Analysis Services database.</span></span> <span data-ttu-id="fd5ad-134">它是單躍點，因此不需要 Kerberos，即使啟用此設定也一樣。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-134">It is a single hop, so even if Kerberos is enabled, it is not required for this scenario.</span></span>  
  
 <span data-ttu-id="fd5ad-135">![從 Excel 連接到表格式模型資料庫](../media/ssas-powerpivotbismconnection-1.gif "從 Excel 連接到表格式模型資料庫")</span><span class="sxs-lookup"><span data-stu-id="fd5ad-135">![Connections from Excel to tabular model database](../media/ssas-powerpivotbismconnection-1.gif "Connections from Excel to tabular model database")</span></span>  
  
 <span data-ttu-id="fd5ad-136">**從 Power View 連接到網路上的表格式資料**</span><span class="sxs-lookup"><span data-stu-id="fd5ad-136">**Connecting from Power View to tabular data on a network**</span></span>  
  
 <span data-ttu-id="fd5ad-137">當 SharePoint 使用者按一下文件庫中的 BI 語意連接時，Power View (如果已安裝) 會立即啟動並開啟表格式模型資料庫的連接。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-137">When a SharePoint user clicks on a BI semantic connection in a document library, Power View (if it is installed), starts immediately and opens a connection to the tabular model database.</span></span>  
  
 <span data-ttu-id="fd5ad-138">Power View 和表格式模型資料庫之間的連接依循雙躍點驗證順序，其中使用者識別會從用戶端流向 SharePoint，然後再從 SharePoint 流向伺服器陣列外部執行的後端 Analysis Services 表格式模型資料庫。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-138">Connections between Power View and a tabular model database follow a double-hop authentication sequence where the user identity is flowed from the client to SharePoint, and then from SharePoint to a back-end Analysis Services tabular model database that runs outside of the farm.</span></span> <span data-ttu-id="fd5ad-139">處理連接要求的 ADOMD.NET 用戶端程式庫在初次嘗試時一定會嘗試 Kerberos。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-139">The ADOMD.NET client library that handles the connection request always tries Kerberos on the first attempt.</span></span> <span data-ttu-id="fd5ad-140">如果設定 Kerberos，表格式模型資料庫的連接上會模擬使用者識別，而且連接會成功。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-140">If Kerberos is configured, the user identity is impersonated on the connection to the tabular model database, and the connection succeeds.</span></span>  
  
 <span data-ttu-id="fd5ad-141">如果未設定 Kerberos，而且要求失敗，Reporting Services 會進行第二次嘗試。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-141">If Kerberos is not configured and the request fails, Reporting Services makes a second attempt.</span></span> <span data-ttu-id="fd5ad-142">在這種情況下，用戶端程式庫會使用 Reporting Services 服務識別和 NTLM 驗證連接到 Analysis Services。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-142">Under this scenario, the client library connects to Analysis Services using the Reporting Services service identity and NTLM authentication.</span></span> <span data-ttu-id="fd5ad-143">Power View 使用者的識別是透過使用 `effectiveusername` 參數的連接字串來傳遞。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-143">The identity of the Power View user is passed on the connection string using the `effectiveusername` parameter.</span></span>  
  
 <span data-ttu-id="fd5ad-144">僅 Analysis Services 執行個體的系統管理員角色成員有權使用 `effectiveusername` 參數建立連接以及模擬伺服器執行個體上的另一個使用者。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-144">Only a member of the system administrator role on the Analysis Services instance has permission to make a connection using the `effectiveusername` parameter and impersonate another user on the server instance.</span></span> <span data-ttu-id="fd5ad-145">因此，Reporting Services 共用服務的執行帳戶必須有 Analysis Services 執行個體的管理權限。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-145">For this reason, the execution account of the Reporting Services shared service must have administrative rights on the Analysis Services instance.</span></span>  <span data-ttu-id="fd5ad-146">[建立與表格式模型資料庫的 BI 語意模型連接](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)主題中提供有關授與管理權限給服務帳戶的指示。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-146">Instructions for granting administrative permissions to the service account is provided in this topic, [Create a BI Semantic Model Connection to a Tabular Model Database](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md).</span></span>  
  
 <span data-ttu-id="fd5ad-147">下圖顯示每個連接都使用相同 Windows 使用者識別的連接順序。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-147">The following illustration shows a connection sequence that uses the same Windows user identity for each connection.</span></span> <span data-ttu-id="fd5ad-148">最後一個 Analysis Services 連接上，連接是透過 Reporting Services 服務應用程式識別，使用 `effectiveusername` 傳遞 Windows 使用者識別來建立。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-148">On the last connection to Analysis Services, the connection is made by the Reporting Services service application identity, passing the Windows user identity using `effectiveusername`.</span></span>  
  
 <span data-ttu-id="fd5ad-149">![與表格式資料庫之間的模擬連接](../media/ssas-powerpivotbismconnection-2.gif "與表格式資料庫之間的模擬連接")</span><span class="sxs-lookup"><span data-stu-id="fd5ad-149">![Imersonated connection to tabular db](../media/ssas-powerpivotbismconnection-2.gif "Imersonated connection to tabular db")</span></span>  
  
 <span data-ttu-id="fd5ad-150">**從 Power View 連接到 SharePoint 中的 PowerPivot 資料**</span><span class="sxs-lookup"><span data-stu-id="fd5ad-150">**Connecting from Power View to PowerPivot data in SharePoint**</span></span>  
  
 <span data-ttu-id="fd5ad-151">當 SharePoint 使用者按一下 BI 語意連接，而解析為相同伺服器陣列中的 PowerPivot 活頁簿時，該連接會在 SharePoint 環境的內容中發生。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-151">When a SharePoint user clicks on a BI semantic connection that resolves to a PowerPivot workbook in the same farm, the connections occur within the context of the SharePoint environment.</span></span> <span data-ttu-id="fd5ad-152">PowerPivot 服務應用程式會處理連接要求，將它轉送到同一部電腦上的 Analysis Services 執行個體。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-152">A PowerPivot service application handles the connection request, which it forwards to the Analysis Services instance on the same computer.</span></span> <span data-ttu-id="fd5ad-153">Analysis Services 執行個體會從活頁簿擷取並載入 PowerPivot 資料。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-153">The Analysis Services instance extracts the PowerPivot data from the workbook and loads it.</span></span> <span data-ttu-id="fd5ad-154">所有後續連接都是由伺服器陣列中的 PowerPivot 服務應用程式管理。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-154">All subsequent connections are managed by PowerPivot service applications in the farm.</span></span>  
  
 <span data-ttu-id="fd5ad-155">在這種情況下，所有連接都是在相同伺服器陣列中發生，因此不需要 Kerberos 或受條件約束的委派。</span><span class="sxs-lookup"><span data-stu-id="fd5ad-155">In this scenario, all connections occur within the same farm, so there is no requirement for Kerberos or constrained delegation.</span></span>  
  
##  <a name="related-tasks"></a><a name="bkmk_rel"></a> <span data-ttu-id="fd5ad-156">相關工作</span><span class="sxs-lookup"><span data-stu-id="fd5ad-156">Related Tasks</span></span>  
 [<span data-ttu-id="fd5ad-157">將 BI 語義模型線上內容類型新增至程式庫 &#40;PowerPivot for SharePoint&#41;</span><span class="sxs-lookup"><span data-stu-id="fd5ad-157">Add a BI Semantic Model Connection Content Type to a Library &#40;PowerPivot for SharePoint&#41;</span></span>](add-bi-semantic-model-connection-content-type-to-library.md)  
  
 [<span data-ttu-id="fd5ad-158">建立與 PowerPivot 活頁簿的 BI 語意模型連接</span><span class="sxs-lookup"><span data-stu-id="fd5ad-158">Create a BI Semantic Model Connection to a PowerPivot Workbook</span></span>](create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)  
  
 [<span data-ttu-id="fd5ad-159">建立與表格式模型資料庫的 BI 語義模型連接</span><span class="sxs-lookup"><span data-stu-id="fd5ad-159">Create a BI Semantic Model Connection to a Tabular Model Database</span></span>](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)  
  
 [<span data-ttu-id="fd5ad-160">在 Excel 或 Reporting Services 使用 BI 語意模型連接</span><span class="sxs-lookup"><span data-stu-id="fd5ad-160">Use a BI Semantic Model Connection in Excel or Reporting Services</span></span>](use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)  
  
## <a name="see-also"></a><span data-ttu-id="fd5ad-161">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fd5ad-161">See Also</span></span>  
 <span data-ttu-id="fd5ad-162">[判斷 Analysis Services 實例的伺服器模式](../instances/determine-the-server-mode-of-an-analysis-services-instance.md) </span><span class="sxs-lookup"><span data-stu-id="fd5ad-162">[Determine the Server Mode of an Analysis Services Instance](../instances/determine-the-server-mode-of-an-analysis-services-instance.md) </span></span>  
 [<span data-ttu-id="fd5ad-163">連接到 Analysis Services</span><span class="sxs-lookup"><span data-stu-id="fd5ad-163">Connect to Analysis Services</span></span>](../instances/connect-to-analysis-services.md)  
  
  