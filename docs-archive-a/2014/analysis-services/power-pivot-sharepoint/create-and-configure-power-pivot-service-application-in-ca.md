---
title: 在管理中心建立和設定 PowerPivot 服務應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b2e5693e-4af3-453f-83f3-07481ab1ac6a
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8becac1ecce25b6798dc727a00a3f5b0afed572c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688313"
---
# <a name="create-and-configure-a-powerpivot-service-application-in-central-administration"></a><span data-ttu-id="134de-102">在管理中心建立及設定 PowerPivot 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="134de-102">Create and Configure a PowerPivot Service Application in Central Administration</span></span>
  <span data-ttu-id="134de-103">PowerPivot 服務應用程式是 PowerPivot 系統服務的共用服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="134de-103">A PowerPivot service application is a shared service instance of the PowerPivot System Service.</span></span> <span data-ttu-id="134de-104">每一個服務應用程式都有它自己的應用程式識別、組態設定、屬性以及內部資料儲存位置。</span><span class="sxs-lookup"><span data-stu-id="134de-104">Each service application has its own application identity, configuration settings, properties, and internal data storage.</span></span>  
  
 <span data-ttu-id="134de-105">本主題包含下列幾節：</span><span class="sxs-lookup"><span data-stu-id="134de-105">This topic contains the following sections:</span></span>  
  
 [<span data-ttu-id="134de-106">決定是否要建立新 PowerPivot 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="134de-106">Determine whether to create a new PowerPivot Service Application</span></span>](#determine)  
  
 [<span data-ttu-id="134de-107">建立 PowerPivot 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="134de-107">Create a PowerPivot Service Application</span></span>](#CreateApp)  
  
 [<span data-ttu-id="134de-108">設定 PowerPivot 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="134de-108">Configure the PowerPivot Service Application</span></span>](#ConfigApp)  
  
 [<span data-ttu-id="134de-109">將 PowerPivot 服務應用程式指派給 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="134de-109">Assign a PowerPivot Service Application to a Web Application</span></span>](#AssignGSA)  
  
 [<span data-ttu-id="134de-110">編輯服務應用程式屬性</span><span class="sxs-lookup"><span data-stu-id="134de-110">Edit Service Application Properties</span></span>](#EditGSA)  
  
##  <a name="determine-whether-to-create-a-new-powerpivot-service-application"></a><a name="determine"></a><span data-ttu-id="134de-111">判斷是否要建立新的 PowerPivot 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="134de-111">Determine whether to create a new PowerPivot Service Application</span></span>  
 <span data-ttu-id="134de-112">PowerPivot for SharePoint 安裝必須在伺服陣列中至少有一個 PowerPivot 服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="134de-112">A PowerPivot for SharePoint installation must have at least one PowerPivot service application in the farm.</span></span> <span data-ttu-id="134de-113">如果您使用 PowerPivot 組態工具設定伺服器，便會自動建立服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="134de-113">A service application is created automatically if you used the PowerPivot Configuration Tool to configure the server.</span></span> <span data-ttu-id="134de-114">否則，您必須在管理中心手動建立 PowerPivot 服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="134de-114">Otherwise, you must create a PowerPivot service application manually in Central Administration.</span></span>  
  
 <span data-ttu-id="134de-115">建立服務應用程式可讓服務變成可用，並產生服務應用程式資料庫。</span><span class="sxs-lookup"><span data-stu-id="134de-115">Creating a service application makes the service available and generates the service application database.</span></span> <span data-ttu-id="134de-116">視建立服務應用程式時所選取的選項而定，會將 PowerPivot 服務連接加入預設的服務連接群組。</span><span class="sxs-lookup"><span data-stu-id="134de-116">Depending on options you select when creating the service application, a PowerPivot service connection is added to the default service connection group.</span></span> <span data-ttu-id="134de-117">所有訂閱預設服務連接群組的 SharePoint Web 應用程式，都會自動立即取得 PowerPivot 服務應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="134de-117">All SharePoint Web applications that subscribe to the default service connection group will get immediate access to the PowerPivot service application automatically.</span></span>  
  
 <span data-ttu-id="134de-118">您可以建立多個 PowerPivot 服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="134de-118">You can create multiple PowerPivot service applications.</span></span> <span data-ttu-id="134de-119">雖然一個服務應用程式即足以應付大部分的部署狀況，但是如果您的商務需求如下，即可考慮建立其他的 PowerPivot 服務應用程式：</span><span class="sxs-lookup"><span data-stu-id="134de-119">Although one service application is sufficient for most deployment scenarios, you might consider creating an additional PowerPivot service application if your business requirements include the following:</span></span>  
  
-   <span data-ttu-id="134de-120">針對每一個應用程式使用不同的自動 PowerPivot 資料重新整理帳戶。</span><span class="sxs-lookup"><span data-stu-id="134de-120">Using a different unattended PowerPivot data refresh account for each application.</span></span>  
  
-   <span data-ttu-id="134de-121">使用不同的逾時、使用量記錄和臨界值來進行查詢回覆報告。</span><span class="sxs-lookup"><span data-stu-id="134de-121">Using different timeouts, usage history, and thresholds for query response reporting.</span></span>  
  
-   <span data-ttu-id="134de-122">將服務管理委派給不同的人。</span><span class="sxs-lookup"><span data-stu-id="134de-122">Delegating service administration to different people.</span></span> <span data-ttu-id="134de-123">系統管理員只會看到他所管理之應用程式的資料重新整理記錄、使用量資料和其他屬性。</span><span class="sxs-lookup"><span data-stu-id="134de-123">An administrator will see data refresh history, usage data, and other properties only for the application he or she is administering.</span></span> <span data-ttu-id="134de-124">如果您需要隔離 SharePoint Web 應用程式 (例如，您的公司是一種主機服務，必須確保針對屬於不同客戶的 SharePoint Web 應用程式進行資料隔離)，則建立其他的 PowerPivot 服務應用程式可以幫助符合隔離需求，其方式是確保每一個服務管理員只會看到他所管理之應用程式的組態設定和屬性。</span><span class="sxs-lookup"><span data-stu-id="134de-124">If you are required to isolate SharePoint web applications (for example, if your company is a hosting service that must guarantee data isolation for the SharePoint Web applications that belong to different customers), creating separate PowerPivot service applications can help meet isolation requirements by ensuring each service administrator sees only the configuration settings and properties for the application he or she manages.</span></span>  
  
 <span data-ttu-id="134de-125">建立其他服務應用程式會引進管理服務關聯的新需求。</span><span class="sxs-lookup"><span data-stu-id="134de-125">Creating additional service application introduces new requirements for managing service associations.</span></span> <span data-ttu-id="134de-126">也就是說，它會要求您針對您所建立的每一個額外服務應用程式來建立及使用自訂服務關聯清單。</span><span class="sxs-lookup"><span data-stu-id="134de-126">Namely, it will require that you create and use custom service association lists for each additional service application that you create.</span></span>  
  
 <span data-ttu-id="134de-127">如果您沒有建立其他 PowerPivot 服務應用程式的特定理由，則應該為伺服陣列中的所有 Web 應用程式，使用單一的服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="134de-127">If you do not have a specific reason for creating additional PowerPivot service application, you should use a single service application for all of the Web applications in the farm.</span></span>  
  
##  <a name="create-a-powerpivot-service-application"></a><a name="CreateApp"></a><span data-ttu-id="134de-128">建立 PowerPivot 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="134de-128">Create a PowerPivot Service Application</span></span>  
  
1.  <span data-ttu-id="134de-129">在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]** 。</span><span class="sxs-lookup"><span data-stu-id="134de-129">In Central Administration, in Application Management, click **Manage service applications**.</span></span>  
  
2.  <span data-ttu-id="134de-130">在 **[服務應用程式]** 功能區中，按一下 **[新增]**。</span><span class="sxs-lookup"><span data-stu-id="134de-130">In the **Service Applications** ribbon, click **New**.</span></span>  
  
3.  <span data-ttu-id="134de-131">選取 [ **SQL Server PowerPivot 服務應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="134de-131">Select **SQL Server PowerPivot Service Application**.</span></span> <span data-ttu-id="134de-132">如果它沒有出現在清單中，表示 PowerPivot for SharePoint 未安裝或是未正確設定。</span><span class="sxs-lookup"><span data-stu-id="134de-132">If it does not appear in the list, PowerPivot for SharePoint is not installed or configured correctly.</span></span>  
  
4.  <span data-ttu-id="134de-133">在 [**建立新的 PowerPivot 服務應用程式**] 頁面中，輸入應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="134de-133">In the **Create New PowerPivot Service Application** page, enter a name for the application.</span></span> <span data-ttu-id="134de-134">預設值為 New-powerpivotserviceapplication \<number> 。</span><span class="sxs-lookup"><span data-stu-id="134de-134">The default is PowerPivotServiceApplication\<number>.</span></span> <span data-ttu-id="134de-135">如果您要建立多個 PowerPivot 服務應用程式，描述性名稱將可協助其他系統管理員，了解如何使用應用程式。</span><span class="sxs-lookup"><span data-stu-id="134de-135">If you are creating multiple PowerPivot service applications, a descriptive name will help other administrators understand how the application is used.</span></span>  
  
5.  <span data-ttu-id="134de-136">在 [應用程式集區] 中，針對此應用程式建立新的應用程式集區 (建議作法)。</span><span class="sxs-lookup"><span data-stu-id="134de-136">In Application Pool, create a new application pool for the application (recommended).</span></span> <span data-ttu-id="134de-137">請針對此應用程式集區選取或建立受管理的帳戶。</span><span class="sxs-lookup"><span data-stu-id="134de-137">Select or create a managed account for the application pool.</span></span> <span data-ttu-id="134de-138">請務必指定網域使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="134de-138">Be sure to specify a domain user account.</span></span> <span data-ttu-id="134de-139">網域使用者帳戶會啟用 SharePoint 的受管理帳戶功能，好讓您在一個地方更新密碼和帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="134de-139">A domain user account enables the use of SharePoint's managed account feature, which lets you update passwords and account information in one place.</span></span> <span data-ttu-id="134de-140">如果您計劃將部署向外延展，以包括將在相同識別下執行的其他服務執行個體，也需要網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="134de-140">Domain accounts are also required if you plan to scale out the deployment to include additional service instances that will run under the same identity.</span></span>  
  
6.  <span data-ttu-id="134de-141">在 **[資料庫伺服器]** 中，預設值是主控伺服陣列組態資料庫的 SQL Server Database Engine 執行個體。</span><span class="sxs-lookup"><span data-stu-id="134de-141">In **Database Server**, the default value is the SQL Server Database Engine instance that hosts the farm configuration databases.</span></span> <span data-ttu-id="134de-142">您可以使用這部伺服器，或選擇不同的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="134de-142">You can use this server or choose a different SQL Server.</span></span>  
  
7.  <span data-ttu-id="134de-143">在 [**資料庫名稱**] 中，預設值為 PowerPivotServiceApplication1_ \<guid> 。</span><span class="sxs-lookup"><span data-stu-id="134de-143">In **Database Name**, the default value is PowerPivotServiceApplication1_\<guid>.</span></span> <span data-ttu-id="134de-144">您必須針對每個 PowerPivot 服務應用程式，建立唯一的資料庫。</span><span class="sxs-lookup"><span data-stu-id="134de-144">You must create a unique database for each PowerPivot service application.</span></span> <span data-ttu-id="134de-145">預設的資料庫名稱會對應至服務應用程式的預設名稱。</span><span class="sxs-lookup"><span data-stu-id="134de-145">The default database name corresponds to the default name of the service application.</span></span> <span data-ttu-id="134de-146">如果您輸入唯一的服務應用程式名稱，請依照類似的命名慣例來命名資料庫名稱，以利同時管理它們。</span><span class="sxs-lookup"><span data-stu-id="134de-146">If you entered a unique service application name, follow a similar naming convention for your database name so that you can manage them together.</span></span>  
  
8.  <span data-ttu-id="134de-147">在 **[資料庫驗證]** 中，預設值是 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="134de-147">In **Database Authentication**, the default is Windows Authentication.</span></span> <span data-ttu-id="134de-148">如果您選擇 **[SQL 驗證]**，請參考 SharePoint 管理員指南，以了解有關如何在 SharePoint 部署中使用這個驗證類型的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="134de-148">If you choose **SQL Authentication**, refer to the SharePoint administrator guide for best practices on how to use this authentication type in a SharePoint deployment.</span></span>  
  
9. <span data-ttu-id="134de-149">（選擇性）選取 [**將這個 PowerPivot 服務應用程式的 Proxy 加入至伺服器陣列的預設 proxy 群組**] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="134de-149">Optionally, select the checkbox for **Add the proxy for this PowerPivot Service Application to the farm's default proxy group.**</span></span> <span data-ttu-id="134de-150">這會將服務應用程式連接加入到預設的服務連接群組。</span><span class="sxs-lookup"><span data-stu-id="134de-150">This adds the service application connection to the default service connection group.</span></span>  
  
     <span data-ttu-id="134de-151">如果您要建立第一個 PowerPivot 服務應用程式，則必須選取這個核取方塊。</span><span class="sxs-lookup"><span data-stu-id="134de-151">You must select this checkbox if you are creating your first PowerPivot service application.</span></span> <span data-ttu-id="134de-152">預設連接群組中必須有一個 PowerPivot 服務應用程式，才能讓 PowerPivot 管理儀表板能夠適當運作。</span><span class="sxs-lookup"><span data-stu-id="134de-152">There must be one PowerPivot service application in the default connection group in order for PowerPivot Management Dashboard to work properly.</span></span>  
  
     <span data-ttu-id="134de-153">如果已經有 PowerPivot 服務應用程式存在，請勿將 PowerPivot 服務應用程式加入到預設連接群組。</span><span class="sxs-lookup"><span data-stu-id="134de-153">Do not add the PowerPivot service application to the default connection group if one already exists.</span></span> <span data-ttu-id="134de-154">加入相同服務應用程式類型的多個項目並不是支援的組態，而且可能會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="134de-154">Adding multiple entries of the same service application type is not a supported configuration and might cause errors.</span></span> <span data-ttu-id="134de-155">如果您要建立其他服務應用程式，請將此應用程式加入到自訂清單，而不要加入到預設連接群組。</span><span class="sxs-lookup"><span data-stu-id="134de-155">If you are creating additional service applications, leave them out of the default connection group and add them to custom lists instead.</span></span>  
  
     <span data-ttu-id="134de-156">如需服務關聯的詳細資訊，請參閱[在管理中心將 PowerPivot 服務應用程式連接到 SharePoint Web 應用程式](connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)。</span><span class="sxs-lookup"><span data-stu-id="134de-156">For more information about service associations, see [Connect a PowerPivot Service Application to a SharePoint Web Application in Central Administration](connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md).</span></span>  
  
10. <span data-ttu-id="134de-157">按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="134de-157">Click **OK.**</span></span> <span data-ttu-id="134de-158">此服務將會與伺服器陣列服務應用程式清單中的其他受管理的服務一起顯示。</span><span class="sxs-lookup"><span data-stu-id="134de-158">The service will appear alongside other managed services in the farm's service application list.</span></span>  
  
##  <a name="configure-powerpivot-service-application"></a><a name="ConfigApp"></a><span data-ttu-id="134de-159">設定 PowerPivot 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="134de-159">Configure PowerPivot Service Application</span></span>  
 <span data-ttu-id="134de-160">使用預設組態建立 PowerPivot 服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="134de-160">A PowerPivot service application is created using a default configuration.</span></span> <span data-ttu-id="134de-161">在大部分的情況下建議使用預設值。</span><span class="sxs-lookup"><span data-stu-id="134de-161">The default settings are recommended for most scenarios.</span></span> <span data-ttu-id="134de-162">只有在您遇到回應時間變慢或連接已卸除時，或是如果您要改變特定 SharePoint Web 應用程式的 PowerPivot 服務組態時，才變更它們。</span><span class="sxs-lookup"><span data-stu-id="134de-162">Change them only if you encounter slow response time or dropped connections, or if you are varying PowerPivot service configuration for specific SharePoint Web applications.</span></span>  
  
1.  <span data-ttu-id="134de-163">在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]** 。</span><span class="sxs-lookup"><span data-stu-id="134de-163">In Central Administration, in Application Management, click **Manage service applications**.</span></span>  
  
     <span data-ttu-id="134de-164">在服務應用程式的清單中，您應該會看到剛才建立和命名的服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="134de-164">In the list of service applications, you should see the service application you just created and named.</span></span> <span data-ttu-id="134de-165">預設值是 **[PowerPivotServiceApplication1]**。</span><span class="sxs-lookup"><span data-stu-id="134de-165">The default is **PowerPivotServiceApplication1**.</span></span>  
  
2.  <span data-ttu-id="134de-166">按一下 PowerPivot 服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="134de-166">Click the PowerPivot service application.</span></span> <span data-ttu-id="134de-167">隨即開啟 PowerPivot 管理儀表板。</span><span class="sxs-lookup"><span data-stu-id="134de-167">This opens the PowerPivot Management Dashboard.</span></span>  
  
3.  <span data-ttu-id="134de-168">在儀表板右上角的 **[動作]** 清單中，按一下 **[設定服務應用程式設定]**。</span><span class="sxs-lookup"><span data-stu-id="134de-168">In the **Actions** list on the top right corner of the dashboard, click **Configure service application settings**.</span></span>  
  
4.  <span data-ttu-id="134de-169">在 [**資料庫載入超時**] 中，增加或減少值，以變更 powerpivot 服務等待 SQL Server Analysis Services 的回應， (powerpivot) 實例轉送載入資料要求的時間。</span><span class="sxs-lookup"><span data-stu-id="134de-169">In **Database Load Timeout**, increase or decrease the value to change how long the PowerPivot service waits for a response from the SQL Server Analysis Services (PowerPivot) instance to which it forwarded a load data request.</span></span> <span data-ttu-id="134de-170">因為非常大的資料集需要一些時間透過傳輸來移動，所以您必須允許 PowerPivot 服務執行個體有足夠的時間來擷取 Excel 活頁簿，並將 PowerPivot 資料移到 Analysis Services 執行個體，以進行查詢處理。</span><span class="sxs-lookup"><span data-stu-id="134de-170">Because very large datasets take time to move over the wire, you must allow sufficient time for the PowerPivot service instance to retrieve the Excel workbook and move the PowerPivot data to an Analysis Services instance for query processing.</span></span> <span data-ttu-id="134de-171">因為 PowerPivot 資料可能會非常大，預設值是 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="134de-171">Because PowerPivot data can be unusually large, the default value is 30 minutes.</span></span>  
  
5.  <span data-ttu-id="134de-172">在 **[連接集區逾時]** 中增加或減少值，以變更閒置的資料連接持續開啟的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="134de-172">In **Connection Pool Timeout**, increase or decrease the value to change how many minutes an idle data connection will remain open.</span></span> <span data-ttu-id="134de-173">預設值為 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="134de-173">The default value is 30 minutes.</span></span> <span data-ttu-id="134de-174">在這段期間，PowerPivot 服務將會針對來自相同 PowerPivot 資料之相同 SharePoint 使用者的唯讀要求，重複使用閒置資料連接。</span><span class="sxs-lookup"><span data-stu-id="134de-174">During this period, the PowerPivot service will reuse an idle data connection for read-only requests from the same SharePoint user for the same PowerPivot data.</span></span> <span data-ttu-id="134de-175">如果在指定的期間內沒有收到該資料的進一步要求，將會從集區移除該連接。</span><span class="sxs-lookup"><span data-stu-id="134de-175">If no further requests are received for that data during the period specified, the connection is removed from the pool.</span></span> <span data-ttu-id="134de-176">有效值為 1 到 3600 秒。</span><span class="sxs-lookup"><span data-stu-id="134de-176">Valid values are 1 to 3600 seconds.</span></span> <span data-ttu-id="134de-177">如需有關連接集區的詳細資訊，請參閱[設定 &#40;PowerPivot for SharePoint&#41;的參考](configuration-setting-reference-power-pivot-for-sharepoint.md)。</span><span class="sxs-lookup"><span data-stu-id="134de-177">For more information about connection pools, see [Configuration Setting Reference &#40;PowerPivot for SharePoint&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md).</span></span>  
  
6.  <span data-ttu-id="134de-178">在 [**最大使用者連接集區大小**] 中，增加或減少值，以變更 PowerPivot 服務將在每個 SharePoint 使用者、PowerPivot 資料集和版本組合的個別連接集區中建立的最大閒置連接數。</span><span class="sxs-lookup"><span data-stu-id="134de-178">In **Maximum User Connection Pool Size**, increase or decrease the value to change the maximum number of idle connections the PowerPivot service will create in individual connection pools for each SharePoint user, PowerPivot dataset, and version combinations.</span></span>  
  
     <span data-ttu-id="134de-179">預設值是 1000 個閒置連接。</span><span class="sxs-lookup"><span data-stu-id="134de-179">The default value is 1000 idle connections.</span></span> <span data-ttu-id="134de-180">有效值為 -1 (無限制)、0 (停用使用者連接共用)，或 1 至 10000。</span><span class="sxs-lookup"><span data-stu-id="134de-180">Valid values are -1 (unlimited), 0 (disables user connection pooling), or 1 to 10000.</span></span>  
  
     <span data-ttu-id="134de-181">這些連接集區可讓服務以更有效率的方式支援由相同使用者連至相同唯讀資料的持續連接。</span><span class="sxs-lookup"><span data-stu-id="134de-181">These connection pools enable the service to more efficiently support ongoing connections to the same read-only data by the same user.</span></span> <span data-ttu-id="134de-182">如果您停用連接共用，將會重新建立每一個連接。</span><span class="sxs-lookup"><span data-stu-id="134de-182">If you disable connection pooling, every connection will be created anew.</span></span>  
  
     <span data-ttu-id="134de-183">請注意，變更連接集區大小的限制 (包括將它設定為 0) 將不會導致卸除連接。</span><span class="sxs-lookup"><span data-stu-id="134de-183">Note that changing the limit on connection pool size, including setting it to 0, will not result in dropped connections.</span></span> <span data-ttu-id="134de-184">連接集區存在的目的是為了減少連接到資料的等候時間。</span><span class="sxs-lookup"><span data-stu-id="134de-184">Connection pools exist to reduce wait times when connecting to data.</span></span> <span data-ttu-id="134de-185">PowerPivot 服務永遠都不會拒絕以連接集區設定為基礎的連接。</span><span class="sxs-lookup"><span data-stu-id="134de-185">The PowerPivot service will never deny a connection based on connection pool settings.</span></span>  
  
7.  <span data-ttu-id="134de-186">在 [**最大管理連接集區大小**] 中，增加或減少值，以將針對 PowerPivot 服務連接所建立之連接集區中的開啟連接數目變更為 Analysis Services。</span><span class="sxs-lookup"><span data-stu-id="134de-186">In **Maximum Administrative Connection Pool Size**, increase or decrease the value to change the number of open connections in a connection pool created for a PowerPivot service connection to Analysis Services.</span></span> <span data-ttu-id="134de-187">每個 PowerPivot 服務執行個體都會在相同的電腦上開啟 Analysis Services 執行個體的個別管理連接。</span><span class="sxs-lookup"><span data-stu-id="134de-187">Each PowerPivot service instance opens a separate administrative connection to the Analysis Services instance on the same computer.</span></span> <span data-ttu-id="134de-188">PowerPivot 服務會建立不同的集區，以便基於檢查閒置連接和監視伺服器健全狀況的目的來重複使用管理連接。</span><span class="sxs-lookup"><span data-stu-id="134de-188">PowerPivot service creates a separate pool to reuse administrative connections for the purpose of checking for idle connections and monitoring server health.</span></span> <span data-ttu-id="134de-189">預設值是 200 個連接。</span><span class="sxs-lookup"><span data-stu-id="134de-189">The default value is 200 connections.</span></span> <span data-ttu-id="134de-190">有效值為 -1 (無限制)、0 (停用管理連接共用) 或 1 到 10000。</span><span class="sxs-lookup"><span data-stu-id="134de-190">Valid values are -1 (unlimited), 0 (disables administrative connection pooling), or 1 to 10000.</span></span> <span data-ttu-id="134de-191">如果您選取 0，將會重新建立每一個連接。</span><span class="sxs-lookup"><span data-stu-id="134de-191">If you select 0, every connection will be created anew.</span></span>  
  
8.  <span data-ttu-id="134de-192">在 [**配置方法**] 中，您可以指定負載平衡架構，讓 PowerPivot 系統服務用來選取特定的 PowerPivot 服務應用程式，以針對初始要求進行負載平衡。</span><span class="sxs-lookup"><span data-stu-id="134de-192">In **Allocation Method**, you can specify the load balancing schema that the PowerPivot System Service uses to select a specific PowerPivot service application for load balancing an initial request.</span></span> <span data-ttu-id="134de-193">預設值為 **[依據健全狀態]**，根據伺服器狀態來配置要求，這是以可用的記憶體及處理器使用量來衡量。</span><span class="sxs-lookup"><span data-stu-id="134de-193">The default is **Health Based**, which allocates requests based on server state, as measured by available memory and processor utilization.</span></span> <span data-ttu-id="134de-194">或者，您可以選擇 **[循環配置資源]** ，以相同的重複順序將要求配置到伺服器，而不論伺服器是忙碌或閒置。</span><span class="sxs-lookup"><span data-stu-id="134de-194">Alternatively, you can choose **Round Robin** to allocate requests to servers in the same repeating order, regardless of whether a server is busy or idle.</span></span>  
  
9. <span data-ttu-id="134de-195">在 [資料重新整理] 的 **[上班時間]** 中，您可以指定定義上班時間的小時範圍。</span><span class="sxs-lookup"><span data-stu-id="134de-195">In Data Refresh, in **Business Hours**, you can specify a range of hours that defines a business day.</span></span> <span data-ttu-id="134de-196">資料重新整理排程可以在下班後執行，以取得在正常上班時間所產生的交易資料。</span><span class="sxs-lookup"><span data-stu-id="134de-196">Data refresh schedules can run after the close of a business day to pick up transactional data that was generated during normal business hours.</span></span>  
  
10. <span data-ttu-id="134de-197">在**PowerPivot 無人看管的資料**重新整理帳戶中，您可以指定預先定義的 Secure Store Service 目標應用程式，以儲存預先定義的帳戶來執行 PowerPivot 資料重新整理作業。</span><span class="sxs-lookup"><span data-stu-id="134de-197">In **PowerPivot Unattended Data Refresh Account**, you can specify a predefined Secure Store Service target application that stores a predefined account for running PowerPivot data refresh jobs.</span></span> <span data-ttu-id="134de-198">請務必指定目標應用程式名稱，而非識別碼。</span><span class="sxs-lookup"><span data-stu-id="134de-198">Be sure to specify the target application name, and not the ID.</span></span> <span data-ttu-id="134de-199">如果您在 SQL Server 安裝程式中使用 [新的伺服器] 選項來安裝 PowerPivot for SharePoint，就會自動建立自動資料整理的目標應用程式。</span><span class="sxs-lookup"><span data-stu-id="134de-199">The target application for unattended data refresh is created automatically if you used the New Server option in SQL Server Setup to install PowerPivot for SharePoint.</span></span> <span data-ttu-id="134de-200">否則，您必須手動建立目標應用程式。</span><span class="sxs-lookup"><span data-stu-id="134de-200">Otherwise, you must create the target application manually.</span></span> <span data-ttu-id="134de-201">如需如何設定帳戶的指示，請參閱[設定 PowerPivot 無人看管的資料重新整理帳戶 &#40;PowerPivot for SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)。</span><span class="sxs-lookup"><span data-stu-id="134de-201">For instructions on how to configure the account, see [Configure the PowerPivot Unattended Data Refresh Account &#40;PowerPivot for SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md).</span></span>  
  
11. <span data-ttu-id="134de-202">在 **[允許使用者輸入自訂的 Windows 認證]** 中，您可以選取或清除可指定排程擁有者是否可以輸入任意 Windows 認證來執行資料重新整理排程的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="134de-202">In **Allow users to enter custom Windows credentials**, you can select or clear the checkbox to specify whether schedule owners can enter arbitrary Windows credentials to run a data refresh schedule.</span></span> <span data-ttu-id="134de-203">如果您選取這個核取方塊，PowerPivot 服務應用程式將會針對每組預存認證來建立及管理目標應用程式。</span><span class="sxs-lookup"><span data-stu-id="134de-203">If you select this checkbox, PowerPivot service application will create and manage a target application each set of stored credentials.</span></span> <span data-ttu-id="134de-204">如需詳細資訊，請參閱[設定 PowerPivot 資料重新整理的預存認證 &#40;PowerPivot for SharePoint&#41;](../configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)。</span><span class="sxs-lookup"><span data-stu-id="134de-204">For more information, see [Configure Stored Credentials for PowerPivot Data Refresh &#40;PowerPivot for SharePoint&#41;](../configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).</span></span>  
  
12. <span data-ttu-id="134de-205">在 **[最大處理記錄長度]** 中，您可以指定要保留資料重新整理處理的記錄多久。</span><span class="sxs-lookup"><span data-stu-id="134de-205">In **Maximum Processing History Length**, you can specify how long to retain a historical record of data refresh processing.</span></span> <span data-ttu-id="134de-206">此資訊會出現在資料重新整理記錄頁面中，這些頁面會針對使用資料重新整理的每個活頁簿而保留。</span><span class="sxs-lookup"><span data-stu-id="134de-206">This information appears in data refresh history pages that are kept for each workbook that uses data refresh.</span></span> <span data-ttu-id="134de-207">此資訊也會出現在 PowerPivot 管理儀表板中。</span><span class="sxs-lookup"><span data-stu-id="134de-207">It also appears in the PowerPivot Management Dashboard.</span></span>  
  
13. <span data-ttu-id="134de-208">在 [使用量資料收集] 的 **[查詢報告間隔]** 中，指定報告查詢統計資料的間隔時間。</span><span class="sxs-lookup"><span data-stu-id="134de-208">In Usage Data Collection, in **Query Reporting Interval**, specify an interval of time for reporting query statistics.</span></span> <span data-ttu-id="134de-209">查詢統計資料會報告成單一事件，以最小化伺服器對伺服器的通訊。</span><span class="sxs-lookup"><span data-stu-id="134de-209">Query statistics are reported as a single event to minimize server-to-server communication.</span></span>  
  
14. <span data-ttu-id="134de-210">在 [使用量資料記錄] 中，指定保留使用量資料歷程記錄的時間長度。</span><span class="sxs-lookup"><span data-stu-id="134de-210">In Usage Data History, specify how long to keep a historical record of usage data.</span></span> <span data-ttu-id="134de-211">使用量資訊也會出現在 PowerPivot 管理儀表板中。</span><span class="sxs-lookup"><span data-stu-id="134de-211">Usage information appears in the PowerPivot Management Dashboard.</span></span> <span data-ttu-id="134de-212">如果您為使用量資料記錄指定的值太低，報表將會比較沒有效率。</span><span class="sxs-lookup"><span data-stu-id="134de-212">The reports will be less effective if you specify too low a value for usage data history.</span></span>  
  
15. <span data-ttu-id="134de-213">在 [使用量資料收集] 的每個查詢回應臨界值中，指定可決定某個類別目錄停止且另一個類別目錄開始的上限。</span><span class="sxs-lookup"><span data-stu-id="134de-213">In Usage Data Collection, in each query response threshold, specify an upper limit that determines where one category stops and another begins.</span></span> <span data-ttu-id="134de-214">這些類別目錄會建立要針對哪一個查詢行為計算的基準。</span><span class="sxs-lookup"><span data-stu-id="134de-214">These categories establish a baseline against which query behavior is measured.</span></span> <span data-ttu-id="134de-215">您可以使用這些類別目錄來監視系統的查詢回應時間趨勢。</span><span class="sxs-lookup"><span data-stu-id="134de-215">You can use these categories to monitor trends in query response times for your system.</span></span> <span data-ttu-id="134de-216">此資訊也會出現在 PowerPivot 管理儀表板中。</span><span class="sxs-lookup"><span data-stu-id="134de-216">This information appears in the PowerPivot Management Dashboard.</span></span>  
  
16. <span data-ttu-id="134de-217">按一下 [確定]  以儲存變更。</span><span class="sxs-lookup"><span data-stu-id="134de-217">Click **OK** to save your changes.</span></span>  
  
     <span data-ttu-id="134de-218">對載入逾時或配置方法的變更只會套用至新的內送要求。</span><span class="sxs-lookup"><span data-stu-id="134de-218">Changes to the load timeout or allocation method are only applied to new incoming requests.</span></span> <span data-ttu-id="134de-219">已在進行中的要求受限於接收要求時生效的值。</span><span class="sxs-lookup"><span data-stu-id="134de-219">Requests that are already in progress are subject to the values that were in effect when the request was received.</span></span>  
  
##  <a name="assign-a-powerpivot-service-application-to-a-web-application"></a><a name="AssignGSA"></a><span data-ttu-id="134de-220">將 PowerPivot 服務應用程式指派給 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="134de-220">Assign a PowerPivot Service Application to a Web Application</span></span>  
 <span data-ttu-id="134de-221">設定 PowerPivot 服務應用程式後，即可將它指派給 Web 應用程式，其方法是將它加入該 Web 應用程式的服務應用程式連接清單。</span><span class="sxs-lookup"><span data-stu-id="134de-221">After you configure a PowerPivot service application, you can assign it to a Web application by adding it to the service application connection list for that Web application.</span></span> <span data-ttu-id="134de-222">作法有二：</span><span class="sxs-lookup"><span data-stu-id="134de-222">There are two ways to do this:</span></span>  
  
-   <span data-ttu-id="134de-223">將它加入 **預設** 連接群組。</span><span class="sxs-lookup"><span data-stu-id="134de-223">Add it to the **Default** connection group.</span></span> <span data-ttu-id="134de-224">*「預設連接群組」* (Default Connection Group) 是服務應用程式連接的集合，可供任何參考它的 Web 應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="134de-224">The *default connection group* is a collection of service application connections that are available to any Web application that references it.</span></span> <span data-ttu-id="134de-225">您必須將 PowerPivot 服務應用程式加入到這個清單中。</span><span class="sxs-lookup"><span data-stu-id="134de-225">You must add a PowerPivot service application to this list.</span></span>  
  
-   <span data-ttu-id="134de-226">為特定的 Web 應用程式建立 **[自訂]** 連接清單。</span><span class="sxs-lookup"><span data-stu-id="134de-226">Create a **Custom** connection list for a specific Web application.</span></span> <span data-ttu-id="134de-227">如果您建立了多個 PowerPivot 服務應用程式，則可以在自訂清單中選取要使用哪一個。</span><span class="sxs-lookup"><span data-stu-id="134de-227">If you created multiple PowerPivot service applications, you can choose which one to use by selecting it in a custom list.</span></span>  
  
 <span data-ttu-id="134de-228">預設的連接群組將可接受相同類型的多個服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="134de-228">The default connection group will accept more than one service application of the same type.</span></span> <span data-ttu-id="134de-229">不過請注意，將一個以上的 PowerPivot 服務應用程式加入到這個清單並不是支援的組態。</span><span class="sxs-lookup"><span data-stu-id="134de-229">Be aware, however, that adding more than one PowerPivot service applications to this list is not a supported configuration.</span></span>  
  
1.  <span data-ttu-id="134de-230">在 [管理中心] 的 **[應用程式管理]** 中，按一下 **[管理 Web 應用程式]**。</span><span class="sxs-lookup"><span data-stu-id="134de-230">In Central Administration, in **Application Management**, click **Manage web applications**.</span></span>  
  
2.  <span data-ttu-id="134de-231">選取您要指派連接的應用程式 (例如 SharePoint-80)。</span><span class="sxs-lookup"><span data-stu-id="134de-231">Select the application for which you want to assign a connection (for example, SharePoint -80).</span></span>  
  
3.  <span data-ttu-id="134de-232">按一下 **[服務連接]**。</span><span class="sxs-lookup"><span data-stu-id="134de-232">Click **Service Connections**.</span></span>  
  
4.  <span data-ttu-id="134de-233">在 [Edit the following group of associations (編輯下列關聯群組)]\*\*\*\* 中，選取 **default** 或 **[custom]**。</span><span class="sxs-lookup"><span data-stu-id="134de-233">In **Edit the following group of associations**, select **default** or **[custom]**.</span></span>  
  
5.  <span data-ttu-id="134de-234">針對 **[自訂]**，選取您想要使用之每個服務應用程式連線旁的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="134de-234">For **[custom]**, select the checkbox next to each service application connection you want to use.</span></span> <span data-ttu-id="134de-235">如果您具有多個 PowerPivot 服務應用程式 (由 [類型] 設定為 `PowerPivot Service Application Proxy` 來表示)，請務必只選擇一個。</span><span class="sxs-lookup"><span data-stu-id="134de-235">If you have multiple PowerPivot service applications (indicated by Type set to `PowerPivot Service Application Proxy`), be sure to choose just one.</span></span>  
  
6.  <span data-ttu-id="134de-236">按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="134de-236">Click **OK**.</span></span>  
  
##  <a name="edit-service-application-properties"></a><a name="EditGSA"></a><span data-ttu-id="134de-237">編輯服務應用程式屬性</span><span class="sxs-lookup"><span data-stu-id="134de-237">Edit Service Application Properties</span></span>  
 <span data-ttu-id="134de-238">使用下列指示來重新開啟屬性頁，以指定服務的應用程式名稱、應用程式集區、資料庫設定以及服務關聯。</span><span class="sxs-lookup"><span data-stu-id="134de-238">Use the following instructions to re-open the property page that specifies the service application name, application pool, database settings, and service associations.</span></span>  
  
1.  <span data-ttu-id="134de-239">在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]** 。</span><span class="sxs-lookup"><span data-stu-id="134de-239">In Central Administration, in Application Management, click **Manage service applications**.</span></span>  
  
2.  <span data-ttu-id="134de-240">選取 PowerPivot 服務應用程式，但是不要在上面按一下。</span><span class="sxs-lookup"><span data-stu-id="134de-240">Select, but do not click, the PowerPivot service application.</span></span> <span data-ttu-id="134de-241">您可以按一下類型名稱來選取整列。</span><span class="sxs-lookup"><span data-stu-id="134de-241">You can click the type name to select the entire row.</span></span>  
  
3.  <span data-ttu-id="134de-242">在功能區上按一下 **[屬性]** 。</span><span class="sxs-lookup"><span data-stu-id="134de-242">Click **Properties** on the ribbon.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="134de-243">另請參閱</span><span class="sxs-lookup"><span data-stu-id="134de-243">See Also</span></span>  
 [<span data-ttu-id="134de-244">管理中心的 PowerPivot 伺服器管理和設定</span><span class="sxs-lookup"><span data-stu-id="134de-244">PowerPivot Server Administration and Configuration in Central Administration</span></span>](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  