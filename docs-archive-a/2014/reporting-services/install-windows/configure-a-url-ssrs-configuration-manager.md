---
title: 設定 URL (SSRS 設定管理員) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], syntax
ms.assetid: 851e163a-ad2a-491e-bc1e-4df92327092f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7bebded7acc39c3cf98a082130594a4712068620
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708918"
---
# <a name="configure-a-url--ssrs-configuration-manager"></a><span data-ttu-id="930f5-102">設定 URL (SSRS 組態管理員)</span><span class="sxs-lookup"><span data-stu-id="930f5-102">Configure a URL  (SSRS Configuration Manager)</span></span>
  <span data-ttu-id="930f5-103">使用報表管理員或報表伺服器 Web 服務之前，您至少必須為每一個應用程式設定一個 URL。</span><span class="sxs-lookup"><span data-stu-id="930f5-103">Before you can use Report Manager or the Report Server Web service, you must configure at least one URL for each application.</span></span> <span data-ttu-id="930f5-104">如果您在「僅限檔案」模式下安裝了 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (意即在安裝精靈的 [報表伺服器安裝選項] 頁面中選取 [安裝但不設定伺服器]  選項)，就一定要設定 URL。</span><span class="sxs-lookup"><span data-stu-id="930f5-104">Configuring the URLs is mandatory if you installed [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in "files-only" mode (that is, by selecting the **Install but do not configure the server** option on the Report Server Installation Options page in the Installation Wizard).</span></span> <span data-ttu-id="930f5-105">如果您在預設組態中安裝了 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，就表示已經為每一個應用程式設定了 URL。</span><span class="sxs-lookup"><span data-stu-id="930f5-105">If you installed [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in the default configuration, URLs are already configured for each application.</span></span> <span data-ttu-id="930f5-106">如果您擁有一個設定成使用 SharePoint 整合模式的報表伺服器，而且您使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來更新報表伺服器 Web 服務 URL，也必須在 SharePoint 管理中心內更新此 URL。</span><span class="sxs-lookup"><span data-stu-id="930f5-106">If you have a report server that is configured to use SharePoint Integrated mode and you update the Report Server Web Service URL by using the [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration tool, you must also update the URL in SharePoint Central Administration.</span></span>  
  
 <span data-ttu-id="930f5-107">使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具可設定 URL，</span><span class="sxs-lookup"><span data-stu-id="930f5-107">Use the [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration tool to configure the URLs.</span></span> <span data-ttu-id="930f5-108">URL 的所有部分都會定義在這個工具中。</span><span class="sxs-lookup"><span data-stu-id="930f5-108">All parts of the URL are defined in this tool.</span></span> <span data-ttu-id="930f5-109">與舊版不同的是，Internet Information Services (IIS) 網站不再提供 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和更新版本中 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="930f5-109">Unlike earlier releases, Internet Information Services (IIS) Web sites no longer provide access to [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] applications in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] and later versions.</span></span>  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] <span data-ttu-id="930f5-110">會提供可在大多數部署狀況下順利運作的預設值，包括與其他 Web 服務和應用程式的並存部署。</span><span class="sxs-lookup"><span data-stu-id="930f5-110">provides default values that work well in most deployment scenarios, including side-by-side deployments with other Web services and applications.</span></span> <span data-ttu-id="930f5-111">預設 URL 會併入執行個體名稱，好讓在相同電腦上執行多個報表伺服器執行個體時的 URL 衝突風險降到最低。</span><span class="sxs-lookup"><span data-stu-id="930f5-111">Default URLs incorporate instance names, minimizing the risk of URL conflicts if you run multiple report server instances on the same computer.</span></span>  
  
 <span data-ttu-id="930f5-112">本主題提供下列工作的指示：</span><span class="sxs-lookup"><span data-stu-id="930f5-112">This topic provides instructions for the following tasks:</span></span>  
  
-   <span data-ttu-id="930f5-113">為報表伺服器 Web 服務建立 URL。</span><span class="sxs-lookup"><span data-stu-id="930f5-113">Create a URL for the Report Server Web service.</span></span>  
  
-   <span data-ttu-id="930f5-114">為報表管理員建立 URL。</span><span class="sxs-lookup"><span data-stu-id="930f5-114">Create a URL for Report Manager.</span></span>  
  
-   <span data-ttu-id="930f5-115">設定進階的 URL 屬性，以定義其他 URL。</span><span class="sxs-lookup"><span data-stu-id="930f5-115">Set advanced URL properties to define additional URLs.</span></span>  
  
 <span data-ttu-id="930f5-116">如需有關如何儲存及維護 Url 或互通性問題的詳細資訊，請參閱[關於 Url 保留專案和註冊 &#40;ssrs Configuration Manager&#41;](about-url-reservations-and-registration-ssrs-configuration-manager.md)和安裝 Reporting Services 和 Internet Information Services 《線上叢書》中[的並行 &#40;Ssrs 原生模式](install-reporting-and-internet-information-services-side-by-side.md)&#41;[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="930f5-116">For more information about how URLs are stored and maintained or interoperability issues, see [About URL Reservations and Registration  &#40;SSRS Configuration Manager&#41;](about-url-reservations-and-registration-ssrs-configuration-manager.md) and [Install Reporting Services and Internet Information Services Side-by-Side &#40;SSRS Native Mode&#41;](install-reporting-and-internet-information-services-side-by-side.md)in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Online.</span></span> <span data-ttu-id="930f5-117">若要檢閱 Reporting Services 安裝中常用的 URL 範例，請參閱本主題的＜ [URL 範例](#URLExamples) ＞。</span><span class="sxs-lookup"><span data-stu-id="930f5-117">To review examples of URLs often used in a Reporting Services installation, see [Examples of URLs](#URLExamples) in this topic.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="930f5-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="930f5-118">Prerequisites</span></span>  
 <span data-ttu-id="930f5-119">在您建立或修改 URL 之前，請記住以下要點：</span><span class="sxs-lookup"><span data-stu-id="930f5-119">Before you create or modify a URL, remember the following points:</span></span>  
  
-   <span data-ttu-id="930f5-120">您在報表伺服器電腦上必須是本機管理員群組的成員。</span><span class="sxs-lookup"><span data-stu-id="930f5-120">You must be a member of the local Administrators group on the report server computer.</span></span>  
  
-   <span data-ttu-id="930f5-121">如果相同電腦上安裝了 IIS 6.0 或 7.0，請檢查使用通訊埠 80 之任何網站上的虛擬目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="930f5-121">If IIS 6.0 or 7.0 is installed on the same computer, check the names of virtual directories on any Web site that uses port 80.</span></span> <span data-ttu-id="930f5-122">如果您看到任何虛擬目錄使用預設 Reporting Services 虛擬目錄名稱 (意即 "Reports" 和 "ReportServer")，請為您設定的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 選擇不同的虛擬目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="930f5-122">If you see any virtual directories that use the default Reporting Services virtual directory names (that is, "Reports" and "ReportServer"), choose different virtual directory names for the [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URLs that you configure.</span></span>  
  
-   <span data-ttu-id="930f5-123">您必須使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來設定 URL，</span><span class="sxs-lookup"><span data-stu-id="930f5-123">You must use the [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration tool to configure the URL.</span></span> <span data-ttu-id="930f5-124">請勿使用系統公用程式。</span><span class="sxs-lookup"><span data-stu-id="930f5-124">Do not use a system utility.</span></span> <span data-ttu-id="930f5-125">絕對不要直接在 RSReportServer.config 檔案的 `URLReservations` 區段中修改 URL 保留項目。</span><span class="sxs-lookup"><span data-stu-id="930f5-125">Never modify URL reservations in the `URLReservations` section of the RSReportServer.config file directly.</span></span> <span data-ttu-id="930f5-126">若要更新儲存於內部的基礎 URL 保留項目以及同步處理 RSReportServer.config 檔案中儲存的 URL 設定，必須要使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具。</span><span class="sxs-lookup"><span data-stu-id="930f5-126">Using the [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration tool is necessary to update both the underlying URL reservation that is stored internally and synchronize the URL settings stored in the RSReportServer.config file.</span></span>  
  
-   <span data-ttu-id="930f5-127">請選擇具有低報表活動的時間。</span><span class="sxs-lookup"><span data-stu-id="930f5-127">Choose a time that has low report activity.</span></span> <span data-ttu-id="930f5-128">每當 URL 保留項目變更時，您就可以預期報表伺服器 Web 服務和報表管理員的應用程式定義域可能會回收使用。</span><span class="sxs-lookup"><span data-stu-id="930f5-128">Each time the URL reservation changes, you can expect that the application domains for Report Server Web service and Report Manager might be recycled.</span></span>  
  
-   <span data-ttu-id="930f5-129">如需 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]URL 建構和使用方式的概觀，請參閱 [設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](configure-report-server-urls-ssrs-configuration-manager.md)建立 URL。</span><span class="sxs-lookup"><span data-stu-id="930f5-129">For an overview of URL construction and usage in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], see [Configure Report Server URLs  &#40;SSRS Configuration Manager&#41;](configure-report-server-urls-ssrs-configuration-manager.md).</span></span>  
  
### <a name="to-configure-a-url-for-the-report-server-web-service"></a><span data-ttu-id="930f5-130">為報表伺服器 Web 服務設定 URL</span><span class="sxs-lookup"><span data-stu-id="930f5-130">To configure a URL for the Report Server Web service</span></span>  
  
1.  <span data-ttu-id="930f5-131">啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並連接到本機報表伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="930f5-131">Start the [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration tool and connect to a local report server instance.</span></span>  
  
2.  <span data-ttu-id="930f5-132">按一下 **[Web 服務 URL]** 。</span><span class="sxs-lookup"><span data-stu-id="930f5-132">Click **Web Service URL**.</span></span>  
  
3.  <span data-ttu-id="930f5-133">指定虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="930f5-133">Specify the virtual directory.</span></span> <span data-ttu-id="930f5-134">此虛擬目錄名稱會識別哪一個應用程式將接收要求。</span><span class="sxs-lookup"><span data-stu-id="930f5-134">The virtual directory name identifies which application receives the request.</span></span> <span data-ttu-id="930f5-135">由於 IP 位址和通訊埠可由多個應用程式共用，所以此虛擬目錄名稱會指定哪一個應用程式要接收要求。</span><span class="sxs-lookup"><span data-stu-id="930f5-135">Because an IP address and port can be shared by multiple applications, the virtual directory name specifies which application receives the request.</span></span>  
  
     <span data-ttu-id="930f5-136">這個值必須是唯一的，以確保此要求可送到所要的目的地。</span><span class="sxs-lookup"><span data-stu-id="930f5-136">This value must be unique to ensure that the request reaches its intended destination.</span></span> <span data-ttu-id="930f5-137">這是必要的值。</span><span class="sxs-lookup"><span data-stu-id="930f5-137">This value is required.</span></span> <span data-ttu-id="930f5-138">而且不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="930f5-138">It is case-insensitive.</span></span> <span data-ttu-id="930f5-139">虛擬目錄名稱與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式的執行個體之間為一對一的對應關係。</span><span class="sxs-lookup"><span data-stu-id="930f5-139">There is a one-to-one correspondence between a virtual directory name and an instance of a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] application.</span></span> <span data-ttu-id="930f5-140">如果您對相同的應用程式執行個體建立多個 URL，必須在為此應用程式執行個體定義的所有 URL 中使用相同的虛擬目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="930f5-140">If you create multiple URLs to the same application instance, you must use the same virtual directory name in all of the URLs you define for this application instance.</span></span>  
  
     <span data-ttu-id="930f5-141">如果是報表伺服器 Web 服務，預設虛擬目錄名稱會是 **ReportServer**。</span><span class="sxs-lookup"><span data-stu-id="930f5-141">For the Report Server Web service, the default virtual directory name is **ReportServer**.</span></span>  
  
4.  <span data-ttu-id="930f5-142">指定可唯一識別網路上之報表伺服器電腦的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="930f5-142">Specify the IP address that uniquely identifies the report server computer on the network.</span></span> <span data-ttu-id="930f5-143">如果您想要指定主機標頭，或針對相同的應用程式執行個體定義其他 URL，您必須按一下 **[進階]** 。</span><span class="sxs-lookup"><span data-stu-id="930f5-143">If you want to specify a host header or define additional URLs for the same application instance, you must click **Advanced**.</span></span> <span data-ttu-id="930f5-144">如需有關如何針對 URL 設定進階屬性的指示，請參閱本主題稍後的指示。</span><span class="sxs-lookup"><span data-stu-id="930f5-144">For instructions on how to set advanced properties on the URL, see the instructions later in this topic.</span></span> <span data-ttu-id="930f5-145">否則，請使用 **[Web 服務 URL]** 頁面，從下列值當中選取：</span><span class="sxs-lookup"><span data-stu-id="930f5-145">Otherwise, use the **Web Service URL** page to select from the following values:</span></span>  
  
    -   <span data-ttu-id="930f5-146">**[全部指派]** 會指定指派給電腦的任何一個 IP 位址都可以用於指向報表伺服器應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="930f5-146">**All Assigned** specifies that any of the IP addresses that are assigned to the computer can be used in a URL that points to a report server application.</span></span> <span data-ttu-id="930f5-147">這個值也包含易記主機名稱 (如電腦名稱)，網域名稱伺服器可將該名稱解析為指派給電腦的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="930f5-147">This value also encompasses friendly host names (such as computer names) that can be resolved by a domain name server to an IP address that is assigned to the computer.</span></span> <span data-ttu-id="930f5-148">這是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 的預設值。</span><span class="sxs-lookup"><span data-stu-id="930f5-148">This is the default value for a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL.</span></span>  
  
    -   <span data-ttu-id="930f5-149">**[全未指派]** 會指定報表伺服器將會接收另一個應用程式尚未處理的任何要求。</span><span class="sxs-lookup"><span data-stu-id="930f5-149">**All Unassigned** specifies that the report server will receive any request that has not been handled by another application.</span></span> <span data-ttu-id="930f5-150">建議您避免使用這個選項。</span><span class="sxs-lookup"><span data-stu-id="930f5-150">We recommend that you avoid this option.</span></span> <span data-ttu-id="930f5-151">如果您選取這個選項，則另一個具有更強式 URL 保留項目的應用程式就可能會攔截要送給報表伺服器的要求。</span><span class="sxs-lookup"><span data-stu-id="930f5-151">If you select this option, it becomes possible for another application that has a stronger URL reservation to intercept requests intended for the report server.</span></span>  
  
    -   <span data-ttu-id="930f5-152">**[127.0.0.1]** 是用來存取 localhost 的 IPv4 位址，</span><span class="sxs-lookup"><span data-stu-id="930f5-152">**127.0.0.1** is the IPv4 address used to access to localhost.</span></span> <span data-ttu-id="930f5-153">它可支援報表伺服器電腦上的本機管理。</span><span class="sxs-lookup"><span data-stu-id="930f5-153">It supports local administration on the report server computer.</span></span> <span data-ttu-id="930f5-154">如果您只選取這個值，則只有在本機登入報表伺服器電腦的使用者才會擁有此應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="930f5-154">If you select only this value, only users who are logged on locally to the report server computer will have access to the application.</span></span>  
  
    -   <span data-ttu-id="930f5-155">**[::1]** 是 IPv6 格式的回送位址。</span><span class="sxs-lookup"><span data-stu-id="930f5-155">**::1** is the loopback address in IPv6 format.</span></span>  
  
    -   <span data-ttu-id="930f5-156">特定的 IP 位址也會出現在這個清單中。</span><span class="sxs-lookup"><span data-stu-id="930f5-156">Specific IP addresses also appear in this list.</span></span> <span data-ttu-id="930f5-157">IP 位址可以採用 IPv4 和 IPv6 格式。</span><span class="sxs-lookup"><span data-stu-id="930f5-157">IP addresses can be in IPv4 and IPv6 formats.</span></span> <span data-ttu-id="930f5-158">*Nnn.nnn.nnn.nnn* 是電腦網路介面卡的 32 位元 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="930f5-158">*Nnn.nnn.nnn.nnn* is the 32-bit IPv4 address of a network adapter card on your computer.</span></span> <span data-ttu-id="930f5-159">IPv6 位址為128位，具有八個4位元組的欄位，並以冒號分隔： \<prefix> ：*nnnn： nnnn： nnnn： nnnn： nnnn： nnnn*</span><span class="sxs-lookup"><span data-stu-id="930f5-159">IPv6 addresses are 128-bit, with eight 4-byte fields separated by colons: \<prefix>:*nnnn:nnnn:nnnn:nnnn:nnnn:nnnn*</span></span>  
  
         <span data-ttu-id="930f5-160">如果您有多張網路介面卡或是您的網路同時支援 IPv4 和 IPv6 位址，您將會看到多個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="930f5-160">If you have multiple cards or if your network supports both IPv4 and IPv6 addresses, you will see multiple IP addresses.</span></span> <span data-ttu-id="930f5-161">如果您只選取一個 IP 位址，它會將應用程式存取限制為只有該 IP 位址 (以及網域名稱伺服器對應至該位址的任何主機名稱)。</span><span class="sxs-lookup"><span data-stu-id="930f5-161">If you select only one IP address, it will limit application access to the just the IP address (and any host name that a domain name server maps to that address).</span></span> <span data-ttu-id="930f5-162">您無法使用 localhost 來存取報表伺服器，而且也不能使用安裝於報表伺服器電腦上之其他網路卡的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="930f5-162">You cannot use localhost to access a report server, and you cannot use the IP addresses of other network adapter cards that are installed on the report server computer.</span></span> <span data-ttu-id="930f5-163">一般來說，如果您選取這個值，這是因為您正在設定多個同時也指定明確 IP 位址或主機名稱的 URL 保留項目 (例如，一個項目用於內部網路連接的網路介面卡，另一個項目用於外部網路連接)。</span><span class="sxs-lookup"><span data-stu-id="930f5-163">Typically, if you select this value, it is because you are configuring multiple URL reservations that also specify explicit IP addresses or host names (for example, one for a network adapter card used for intranet connections and a second one used for extranet connections).</span></span>  
  
5.  <span data-ttu-id="930f5-164">指定通訊埠。</span><span class="sxs-lookup"><span data-stu-id="930f5-164">Specify the port.</span></span> <span data-ttu-id="930f5-165">在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 Windows Server 2008 上，通訊埠 80 是 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] 的預設值，因為它可以與其他應用程式共用。</span><span class="sxs-lookup"><span data-stu-id="930f5-165">Port 80 is the default for [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] on [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] and Windows Server 2008 because it can be shared with other applications.</span></span> <span data-ttu-id="930f5-166">如果您想要使用自訂通訊埠編號，請記得一定要在用來存取報表伺服器的 URL 中指定它。</span><span class="sxs-lookup"><span data-stu-id="930f5-166">If you want to use a custom port number, remember that you will have to always specify it in the URL used to access the report server.</span></span> <span data-ttu-id="930f5-167">您可以使用下列方法來尋找可用的通訊埠：</span><span class="sxs-lookup"><span data-stu-id="930f5-167">You can use the following techniques to find an available port:</span></span>  
  
    -   <span data-ttu-id="930f5-168">從命令提示字元輸入下列命令，以傳回所使用的 TCP 通訊埠清單：</span><span class="sxs-lookup"><span data-stu-id="930f5-168">From a command prompt, type the following command to return a list of TCP ports that are being used:</span></span>  
  
         `netstat -a -n -p tcp`  
  
    -   <span data-ttu-id="930f5-169">請檢閱 Microsoft 技術支援文件 [TCP/IP 連接埠指派資訊](https://support.microsoft.com/kb/174904)，以閱讀有關 TCP 通訊埠指派以及已知通訊埠 (0 到 1023)、已註冊的通訊埠 (1024 到 49151) 和動態或私人通訊埠 (49152 到 65535) 之間差異的資訊。</span><span class="sxs-lookup"><span data-stu-id="930f5-169">Review the Microsoft Support article, [Information about TCP/IP port assignments](https://support.microsoft.com/kb/174904), to read about TCP port assignments and the differences between Well Known Ports (0 through 1023), Registered Ports (1024 through 49151), and Dynamic or Private Ports (49152 through 65535).</span></span>  
  
    -   <span data-ttu-id="930f5-170">如果您正在使用 Windows 防火牆，您必須開啟此通訊埠。</span><span class="sxs-lookup"><span data-stu-id="930f5-170">If you are using Windows Firewall, you must open the port.</span></span> <span data-ttu-id="930f5-171">如需指示，請參閱 [Configure a Firewall for Report Server Access](../report-server/configure-a-firewall-for-report-server-access.md)。</span><span class="sxs-lookup"><span data-stu-id="930f5-171">For instructions, see [Configure a Firewall for Report Server Access](../report-server/configure-a-firewall-for-report-server-access.md).</span></span>  
  
6.  <span data-ttu-id="930f5-172">如果您尚未這樣做，請確認 IIS (如果已安裝) 並沒有與您打算使用之名稱相同的虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="930f5-172">If you have not done so already, verify that IIS (if it is installed) does not have virtual directory with the same name you plan to use.</span></span>  
  
7.  <span data-ttu-id="930f5-173">如果您安裝了 SSL 憑證，您可以現在選取它，以便將此 URL 繫結至電腦上所安裝的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="930f5-173">If you installed an SSL certificate, you can select it now to bind the URL to the SSL certificate that is installed on your computer.</span></span>  
  
8.  <span data-ttu-id="930f5-174">如果您選擇性地選取 SSL 憑證，您就可以指定自訂通訊埠。</span><span class="sxs-lookup"><span data-stu-id="930f5-174">Optionally, if you select an SSL certificate, you can specify a custom port.</span></span> <span data-ttu-id="930f5-175">預設值是 443，但是您可以使用任何可用的通訊埠。</span><span class="sxs-lookup"><span data-stu-id="930f5-175">The default is 443 but you can use any port that is available.</span></span>  
  
9. <span data-ttu-id="930f5-176">按一下 **[套用]** ，即可建立此 URL。</span><span class="sxs-lookup"><span data-stu-id="930f5-176">Click **Apply** to create the URL.</span></span>  
  
10. <span data-ttu-id="930f5-177">按一下頁面 **[URL]** 區段中的連結來測試此 URL。</span><span class="sxs-lookup"><span data-stu-id="930f5-177">Test the URL by clicking the link in the **URLs** section of page.</span></span> <span data-ttu-id="930f5-178">請注意，在您可以測試此 URL 之前，必須先建立及設定報表伺服器資料庫。</span><span class="sxs-lookup"><span data-stu-id="930f5-178">Note that the report server database must be created and configured before you can test the URL.</span></span> <span data-ttu-id="930f5-179">如需指示，請參閱[建立原生模式報表伺服器資料庫 &#40;SSRS 設定管理員&#41;](ssrs-report-server-create-a-native-mode-report-server-database.md)。</span><span class="sxs-lookup"><span data-stu-id="930f5-179">For instructions, see [Create a Native Mode Report Server Database  &#40;SSRS Configuration Manager&#41;](ssrs-report-server-create-a-native-mode-report-server-database.md).</span></span>  
  
11. <span data-ttu-id="930f5-180">此外，如果您的報表伺服器設定成使用 SharePoint 整合模式，請在 SharePoint 管理中心內設定報表伺服器 Web 服務 URL。</span><span class="sxs-lookup"><span data-stu-id="930f5-180">Additionally, if your report server is configured to use SharePoint Integrated mode, configure the Report Server Web service URL in SharePoint Central Administration.</span></span> <span data-ttu-id="930f5-181">如需如何在 SharePoint 管理中心內更新報表伺服器 Web 服務 URL 的詳細資訊，請參閱設定[和管理報表伺服器 &#40;Reporting Services Sharepoint 模式&#41;](../configure-administer-report-server-reporting-services-sharepoint-mode.md)和[Reporting Services 報表伺服器 &#40;sharepoint 模式&#41;](../reporting-services-report-server-sharepoint-mode.md)。</span><span class="sxs-lookup"><span data-stu-id="930f5-181">For more information about how to update the Report Server Web service URL in SharePoint Central Administration, see [Configuration and Administration of a Report Server &#40;Reporting Services SharePoint Mode&#41;](../configure-administer-report-server-reporting-services-sharepoint-mode.md) and [Reporting Services Report Server &#40;SharePoint Mode&#41;](../reporting-services-report-server-sharepoint-mode.md).</span></span>  
  
### <a name="to-create-a-url-reservation-for-report-manager"></a><span data-ttu-id="930f5-182">為報表管理員建立 URL 保留項目</span><span class="sxs-lookup"><span data-stu-id="930f5-182">To create a URL reservation for Report Manager</span></span>  
  
1.  <span data-ttu-id="930f5-183">啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並連接到報表伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="930f5-183">Start the [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration tool and connect to the report server instance.</span></span>  
  
2.  <span data-ttu-id="930f5-184">按一下 **[報表管理員 URL]**。</span><span class="sxs-lookup"><span data-stu-id="930f5-184">Click **Report Manager URL**.</span></span>  
  
3.  <span data-ttu-id="930f5-185">指定虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="930f5-185">Specify the virtual directory.</span></span> <span data-ttu-id="930f5-186">報表管理員會接聽與報表伺服器 Web 服務相同的 IP 位址和通訊埠。</span><span class="sxs-lookup"><span data-stu-id="930f5-186">Report Manager listens on the same IP address and port as the Report Server Web service.</span></span> <span data-ttu-id="930f5-187">如果您設定報表管理員指向不同的報表伺服器 Web 服務，您必須修改 RSReportServer.config 檔案中的報表管理員 URL 設定。</span><span class="sxs-lookup"><span data-stu-id="930f5-187">If you configured Report Manager to point to a different Report Server Web service, you must modify the Report Manager URL settings in the RSReportServer.config file.</span></span> <span data-ttu-id="930f5-188">如需指示，請參閱《線上叢書》中的[設定 &#40;原生模式&#41;報表管理員](../report-server/configure-web-portal.md) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="930f5-188">For instructions, see [Configure Report Manager &#40;Native Mode&#41;](../report-server/configure-web-portal.md) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Online.</span></span>  
  
4.  <span data-ttu-id="930f5-189">如果您安裝了 SSL 憑證，就可以選取它，以便要求送給報表管理員的所有要求都透過 HTTPS 路由傳送。</span><span class="sxs-lookup"><span data-stu-id="930f5-189">If you installed an SSL certificate, you can select it to require that all requests to Report Manager are routed over HTTPS.</span></span>  
  
     <span data-ttu-id="930f5-190">如果您選擇性地選取 SSL 憑證，您就可以指定自訂通訊埠。</span><span class="sxs-lookup"><span data-stu-id="930f5-190">Optionally, if you select an SSL certificate, you can specify a custom port.</span></span> <span data-ttu-id="930f5-191">預設值是 443，但是您可以使用任何可用的通訊埠。</span><span class="sxs-lookup"><span data-stu-id="930f5-191">The default is 443 but you can use any port that is available.</span></span>  
  
5.  <span data-ttu-id="930f5-192">按一下 **[套用]** ，即可建立此 URL。</span><span class="sxs-lookup"><span data-stu-id="930f5-192">Click **Apply** to create the URL.</span></span>  
  
6.  <span data-ttu-id="930f5-193">按一下頁面 **[URL]** 區段中的連結來測試此 URL。</span><span class="sxs-lookup"><span data-stu-id="930f5-193">Test the URL by clicking the link in the **URLs** section of page.</span></span>  
  
## <a name="setting-advanced-properties-to-specify-additional-urls"></a><span data-ttu-id="930f5-194">設定進階屬性來指定其他 URL</span><span class="sxs-lookup"><span data-stu-id="930f5-194">Setting Advanced Properties to Specify Additional URLs</span></span>  
 <span data-ttu-id="930f5-195">您可以藉由指定不同的通訊埠或主機名稱，為報表伺服器 Web 服務或報表管理員保留多個 URL (可以是 IP 位址，或是網域名稱伺服器可解析為指派給電腦之 IP 位址的主機標頭名稱)。</span><span class="sxs-lookup"><span data-stu-id="930f5-195">You can reserve multiple URLs for the Report Server Web service or Report Manager by specifying different ports or host names (either an IP address or a host header name that a domain name server can resolve to an IP address assigned to the computer).</span></span> <span data-ttu-id="930f5-196">您可以藉由建立多個 URL，設定對相同報表伺服器執行個體的不同存取路徑。</span><span class="sxs-lookup"><span data-stu-id="930f5-196">By creating multiple URLs, you can set up different access paths to the same report server instance.</span></span> <span data-ttu-id="930f5-197">例如，若要啟用對報表伺服器的內部網路和外部網路存取，您可能會使用預設 URL 來存取內部網路，並使用額外的完整主機名稱來存取外部網路：</span><span class="sxs-lookup"><span data-stu-id="930f5-197">For example, to enable intranet and extranet access to a report server, you might use the default URL for access across the intranet, and an additional fully qualified host name for extranet access:</span></span>  
  
-   `http://myserver01/reportserver`
  
-   `http://www.adventure-works.com/reportserver`  
  
 <span data-ttu-id="930f5-198">您不能為相同的應用程式執行個體設定多個虛擬目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="930f5-198">You cannot set multiple virtual directory names for the same application instance.</span></span> <span data-ttu-id="930f5-199">每一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式執行個體都會對應到單一虛擬目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="930f5-199">Each [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] application instance is mapped to a single virtual directory name.</span></span> <span data-ttu-id="930f5-200">如果您在相同電腦上有多個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體，應用程式的虛擬目錄名稱應該包含此執行個體名稱，以確保每一個要求都會到達所要的目標。</span><span class="sxs-lookup"><span data-stu-id="930f5-200">If you have multiple instances of [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] on the same computer, the virtual directory name for an application should include the instance name to ensure that each request reaches its intended target.</span></span>  
  
#### <a name="to-set-advanced-properties-on-a-url"></a><span data-ttu-id="930f5-201">設定 URL 的進階屬性</span><span class="sxs-lookup"><span data-stu-id="930f5-201">To set advanced properties on a URL</span></span>  
  
1.  <span data-ttu-id="930f5-202">在 **[Web 服務 URL]** 或 **[報表管理員 URL]** 頁面上，按一下 **[進階]**。</span><span class="sxs-lookup"><span data-stu-id="930f5-202">On either the **Web Service URL** or **Report Manager URL** page, click **Advanced**.</span></span>  
  
2.  <span data-ttu-id="930f5-203">按一下 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="930f5-203">Click **Add**.</span></span>  
  
3.  <span data-ttu-id="930f5-204">按一下 IP 位址或主機標頭名稱。</span><span class="sxs-lookup"><span data-stu-id="930f5-204">Click IP Address or Host Header Name.</span></span> <span data-ttu-id="930f5-205">如果您指定主機標頭，請務必指定 DNS 服務可以解析的名稱。</span><span class="sxs-lookup"><span data-stu-id="930f5-205">If you specify a host header, be sure to specify a name that the DNS service can resolve.</span></span> <span data-ttu-id="930f5-206">如果您要指定公開可用的網域名稱，請包含整個 URL，包括 http://www 在內。</span><span class="sxs-lookup"><span data-stu-id="930f5-206">If you are specifying publicly available domain name, include the whole URL, including http://www.</span></span>  
  
4.  <span data-ttu-id="930f5-207">指定通訊埠。</span><span class="sxs-lookup"><span data-stu-id="930f5-207">Specify the port.</span></span> <span data-ttu-id="930f5-208">如果您指定自訂通訊埠，應用程式的 URL 一定要包含通訊埠編號。</span><span class="sxs-lookup"><span data-stu-id="930f5-208">If you specify a custom port, the URL to the application must always include the port number.</span></span>  
  
5.  <span data-ttu-id="930f5-209">按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="930f5-209">Click **OK**.</span></span>  
  
6.  <span data-ttu-id="930f5-210">開啟瀏覽器視窗，並輸入此 URL 加以測試。</span><span class="sxs-lookup"><span data-stu-id="930f5-210">Test the URL by opening a browser window and entering the URL.</span></span>  
  
## <a name="urls-for-multiple-report-server-instances-on-the-same-computer"></a><span data-ttu-id="930f5-211">相同電腦上多個報表伺服器執行個體的 URL</span><span class="sxs-lookup"><span data-stu-id="930f5-211">URLs for Multiple Report Server Instances on the Same Computer</span></span>  
 <span data-ttu-id="930f5-212">如果您為多個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]執行個體保留 URL，您應該遵循命名慣例，好讓您可以避免命名衝突。</span><span class="sxs-lookup"><span data-stu-id="930f5-212">If you are reserving URLs for multiple instances of [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], you should follow naming conventions so that you can avoid naming conflicts.</span></span> <span data-ttu-id="930f5-213">如需詳細資訊，請參閱[多重執行個體報表伺服器部署的 URL 保留項目 &#40;SSRS 組態管理員&#41;](url-reservations-for-multi-instance-report-server-deployments.md)。</span><span class="sxs-lookup"><span data-stu-id="930f5-213">For more information, see [URL Reservations for Multi-Instance Report Server Deployments  &#40;SSRS Configuration Manager&#41;](url-reservations-for-multi-instance-report-server-deployments.md).</span></span>  
  
##  <a name="examples-of-url-configurations"></a><a name="URLExamples"></a> <span data-ttu-id="930f5-214">URL 組態的範例</span><span class="sxs-lookup"><span data-stu-id="930f5-214">Examples of URL Configurations</span></span>  
 <span data-ttu-id="930f5-215">下列清單顯示一些報表伺服器 URL 的範例：</span><span class="sxs-lookup"><span data-stu-id="930f5-215">The following list shows some examples of what a report server URL might resemble:</span></span>  
  
-   http://localhost/reportserver  
  
-   http://localhost/reportserver_SQLEXPRESS  
  
-   http://sales01/reportserver  
  
-   http://sales01:8080/reportserver  
  
-   `https://sales.adventure-works.com/reportserver`  
  
-   `https://www.adventure-works.com:8080/reportserver01`  
  
 <span data-ttu-id="930f5-216">您用以存取報表管理員的 URL 共用類似的格式，而且通常建立在主控報表伺服器的相同網站之下。</span><span class="sxs-lookup"><span data-stu-id="930f5-216">URLs that you use to access Report Manager share a similar format and are typically created under the same Web site that hosts the report server.</span></span> <span data-ttu-id="930f5-217">唯一不同的是虛擬目錄名稱 (在這個範例中為 **reports** ，但是您可以將它設定成想要使用的任何名稱)：</span><span class="sxs-lookup"><span data-stu-id="930f5-217">The only difference is the virtual directory name (in this case, it is **reports** but you can configure it to use whatever name that you want):</span></span>  
  
-   http://localhost/reports  
  
-   http://localhost/reports_SQLEXPRESS  
  
-   http://sales01/reports  
  
-   http://sales01:8080/reports  
  
-   `https://sales.adventure-works.com/reports`  
  
-   `https://www.adventure-works.com:8080/reports`  
  
## <a name="see-also"></a><span data-ttu-id="930f5-218">另請參閱</span><span class="sxs-lookup"><span data-stu-id="930f5-218">See Also</span></span>  
 <span data-ttu-id="930f5-219">[Reporting Services 組態管理員 &#40;原生模式&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md) </span><span class="sxs-lookup"><span data-stu-id="930f5-219">[Reporting Services Configuration Manager &#40;Native Mode&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md) </span></span>  
 [<span data-ttu-id="930f5-220">設定報表伺服器 URL &#40;SSRS 組態管理員&#41;</span><span class="sxs-lookup"><span data-stu-id="930f5-220">Configure Report Server URLs  &#40;SSRS Configuration Manager&#41;</span></span>](configure-report-server-urls-ssrs-configuration-manager.md)  
  
  