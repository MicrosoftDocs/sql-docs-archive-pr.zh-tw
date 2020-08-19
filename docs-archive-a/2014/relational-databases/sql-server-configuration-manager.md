---
title: SQL Server 組態管理員 | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- protocols [SQL Server], managing
- network protocols [SQL Server], managing
- Client Network Utility
- accounts [SQL Server]
- SQL Server Configuration Manager
- Server Network Utility
- accounts [SQL Server], services
- services [SQL Server], managing
- tools [SQL Server], SQL Server Configuration Manager
- configuration manager [SQL Server]
ms.assetid: e6beaea4-164c-4078-95ae-b9e28b0aefe8
author: rothja
ms.author: jroth
ms.openlocfilehash: 53e2ce64c648edf389f9d003b06e993f29cb015c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597055"
---
# <a name="sql-server-configuration-manager"></a><span data-ttu-id="3f938-102">SQL Server 組態管理員</span><span class="sxs-lookup"><span data-stu-id="3f938-102">SQL Server Configuration Manager</span></span>
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] <span data-ttu-id="3f938-103">組態管理員是一個工具，用來管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的相關服務、設定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]所用的網路通訊協定，以及管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用戶端電腦的網路連接組態。</span><span class="sxs-lookup"><span data-stu-id="3f938-103">Configuration Manager is a tool to manage the services associated with [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], to configure the network protocols used by [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], and to manage the network connectivity configuration from [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] client computers.</span></span> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] <span data-ttu-id="3f938-104">組態管理員是一個 [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console 嵌入式管理單元，您可以從 [開始] 功能表存取它，也可以將它加入任何其他 [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console 顯示畫面中。</span><span class="sxs-lookup"><span data-stu-id="3f938-104">Configuration Manager is a [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console snap-in that is available from the Start menu, or can be added to any other [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console display.</span></span> [!INCLUDE[msCoName](../includes/msconame-md.md)]<span data-ttu-id="3f938-105">管理主控台 ( # A0) 會使用 Windows System32 資料夾中的 Sqlservermanager10.msc 來開啟 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager。</span><span class="sxs-lookup"><span data-stu-id="3f938-105">Management Console (mmc.exe) uses the SQLServerManager10.msc file in the Windows System32 folder to open [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager.</span></span>  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] <span data-ttu-id="3f938-106">組態管理員和 SQL Server Management Studio 利用 Window Management Instrumentation (WMI) 來檢視和變更部份伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="3f938-106">Configuration Manager and SQL Server Management Studio use Window Management Instrumentation (WMI) to view and change some server settings.</span></span> <span data-ttu-id="3f938-107">WMI 提供統一的方式來協助您連結管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工具所要求之登錄作業的 API 呼叫，在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員嵌入式管理單元元件的所選 SQL 服務上，它提供了增強的控制和操作功能。</span><span class="sxs-lookup"><span data-stu-id="3f938-107">WMI provides a unified way for interfacing with the API calls that manage the registry operations requested by the [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tools and to provide enhanced control and manipulation over the selected SQL services of the [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager snap-in component.</span></span> <span data-ttu-id="3f938-108">如需設定 WMI 相關權限的相關資訊，請參閱[設定 WMI 在 SQL Server 工具中顯示伺服器狀態](../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="3f938-108">For information about configuring permissions related to WMI, see [Configure WMI to Show Server Status in SQL Server Tools](../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md).</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="3f938-109">因為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員是 [!INCLUDE[msCoName](../includes/msconame-md.md)] 管理主控台程式的嵌入式管理單元，而不是獨立的程式，所以 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員在較新版本的 Windows 中不會作為應用程式出現。</span><span class="sxs-lookup"><span data-stu-id="3f938-109">Because [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager is a snap-in for the [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console program and not a stand-alone program, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager does not appear as an application in newer versions of Windows.</span></span>  
> 
>  -   <span data-ttu-id="3f938-110">**Windows 10**：</span><span class="sxs-lookup"><span data-stu-id="3f938-110">**Windows 10**:</span></span>  
>          <span data-ttu-id="3f938-111">若要開啟 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager，請在 [**開始] 頁面**上，輸入適用于) 的 sqlservermanager12.msc (。 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]</span><span class="sxs-lookup"><span data-stu-id="3f938-111">To open [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager, on the **Start Page**, type SQLServerManager12.msc (for [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]).</span></span> <span data-ttu-id="3f938-112">針對先前版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，以較小的數字取代 12。</span><span class="sxs-lookup"><span data-stu-id="3f938-112">For previous versions of [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] replace 12 with a smaller number.</span></span> <span data-ttu-id="3f938-113">按一下 SQLServerManager12.msc 即可開啟 Configuration Manager。</span><span class="sxs-lookup"><span data-stu-id="3f938-113">Clicking SQLServerManager12.msc opens the Configuration Manager.</span></span> <span data-ttu-id="3f938-114">若要將 Configuration Manager 釘選到起始頁或工作列，請在 [Sqlservermanager12.msc] 上按一下滑鼠右鍵，然後按一下 [**開啟檔案位置**]。</span><span class="sxs-lookup"><span data-stu-id="3f938-114">To pin the Configuration Manager to the Start Page or Task Bar, right-click SQLServerManager12.msc, and then click **Open file location**.</span></span> <span data-ttu-id="3f938-115">在 Windows 檔案瀏覽器中，以滑鼠右鍵按一下 [Sqlservermanager12.msc]，然後按一下 [**釘選到開始**] 或 [**釘選到工作列**]。</span><span class="sxs-lookup"><span data-stu-id="3f938-115">In the Windows File Explorer, right-click SQLServerManager12.msc, and then click **Pin to Start** or **Pin to taskbar**.</span></span>  
> -   <span data-ttu-id="3f938-116">**Windows 8**：</span><span class="sxs-lookup"><span data-stu-id="3f938-116">**Windows 8**:</span></span>  
>          <span data-ttu-id="3f938-117">若要開啟 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager，請在 [**搜尋**] 快速鍵的 [**應用程式**] 底下，輸入**SQLServerManager \<version> \*\* （例如 `SQLServerManager12.msc` ），然後按**enter\*\*。</span><span class="sxs-lookup"><span data-stu-id="3f938-117">To open [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager, in the **Search** charm, under **Apps**, type **SQLServerManager\<version>.msc** such as `SQLServerManager12.msc`, and then press **Enter**.</span></span>  
  
 <span data-ttu-id="3f938-118">若要利用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員來啟動、停止、暫停、繼續或設定另一部電腦中的服務，請參閱[連接至另一部電腦 &#40;SQL Server 組態管理員&#41;](../database-engine/configure-windows/scm-services-connect-to-another-computer.md)。</span><span class="sxs-lookup"><span data-stu-id="3f938-118">To start, stop, pause, resume, or configure services on another computer by using [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager, see [Connect to Another Computer &#40;SQL Server Configuration Manager&#41;](../database-engine/configure-windows/scm-services-connect-to-another-computer.md).</span></span>  
  
## <a name="managing-services"></a><span data-ttu-id="3f938-119">管理服務</span><span class="sxs-lookup"><span data-stu-id="3f938-119">Managing Services</span></span>  
 <span data-ttu-id="3f938-120">請利用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員來啟動、暫停、繼續或停止服務、檢視服務屬性，或變更服務屬性。</span><span class="sxs-lookup"><span data-stu-id="3f938-120">Use [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager to start, pause, resume, or stop the services, to view service properties, or to change service properties.</span></span>  
  
 <span data-ttu-id="3f938-121">使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員利用啟動參數來啟動 [!INCLUDE[ssDE](../includes/ssde-md.md)]。</span><span class="sxs-lookup"><span data-stu-id="3f938-121">Use [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager to start the [!INCLUDE[ssDE](../includes/ssde-md.md)] using startup parameters.</span></span>  <span data-ttu-id="3f938-122">如需詳細資訊，請參閱[設定伺服器啟動選項 &#40;SQL Server 組態管理員&#41;](../database-engine/configure-windows/scm-services-configure-server-startup-options.md)。</span><span class="sxs-lookup"><span data-stu-id="3f938-122">For more information, see [Configure Server Startup Options &#40;SQL Server Configuration Manager&#41;](../database-engine/configure-windows/scm-services-configure-server-startup-options.md).</span></span>  
  
## <a name="changing-the-accounts-used-by-the-services"></a><span data-ttu-id="3f938-123">變更服務所用的帳戶</span><span class="sxs-lookup"><span data-stu-id="3f938-123">Changing the Accounts Used by the Services</span></span>  
 <span data-ttu-id="3f938-124">利用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員來管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服務。</span><span class="sxs-lookup"><span data-stu-id="3f938-124">Manage the [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] services using [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager.</span></span>  
  
> [!IMPORTANT]  
>  <span data-ttu-id="3f938-125">請一律利用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工具 (如 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員) 來變更 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 服務所用的帳戶，或變更帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="3f938-125">Always use [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tools such as [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager to change the account used by the [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] or [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent services, or to change the password for the account.</span></span> <span data-ttu-id="3f938-126">除了變更帳戶名稱之外， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員也會執行其他組態，例如，設定 Windows 登錄中的權限，使新的帳戶能夠讀取 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 設定。</span><span class="sxs-lookup"><span data-stu-id="3f938-126">In addition to changing the account name, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager performs additional configuration such as setting permissions in the Windows Registry so that the new account can read the [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] settings.</span></span> <span data-ttu-id="3f938-127">其他工具，例如 Windows 服務控制管理員，也能夠變更帳戶名稱，但無法變更相關設定。</span><span class="sxs-lookup"><span data-stu-id="3f938-127">Other tools such as the Windows Services Control Manager can change the account name but do not change associated settings.</span></span> <span data-ttu-id="3f938-128">如果服務無法存取登錄的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 部份，服務可能無法適當啟動。</span><span class="sxs-lookup"><span data-stu-id="3f938-128">If the service cannot access the [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] portion of the registry the service may not start properly.</span></span>  
  
 <span data-ttu-id="3f938-129">利用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員、SMO 或 WMI 來變更密碼的另一個好處是，會立即生效，不需要重新啟動服務。</span><span class="sxs-lookup"><span data-stu-id="3f938-129">As an additional benefit, passwords changed using [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager, SMO, or WMI take affect immediately without restarting the service.</span></span>  
  
## <a name="manage-server--client-network-protocols"></a><span data-ttu-id="3f938-130">管理伺服器和用戶端網路通訊協定</span><span class="sxs-lookup"><span data-stu-id="3f938-130">Manage Server & Client Network Protocols</span></span>  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] <span data-ttu-id="3f938-131">組態管理員可讓您設定伺服器和用戶端網路通訊協定，以及連接選項。</span><span class="sxs-lookup"><span data-stu-id="3f938-131">Configuration Manager allows you to configure server and client network protocols, and connectivity options.</span></span> <span data-ttu-id="3f938-132">啟用正確的通訊協定之後，您通常不需要變更伺服器網路連接。</span><span class="sxs-lookup"><span data-stu-id="3f938-132">After the correct protocols are enabled, you usually do not need to change the server network connections.</span></span> <span data-ttu-id="3f938-133">不過，如果您需要重新設定伺服器連接，您可以利用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員，使 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 利用特定的網路通訊協定、埠或管道來接聽。</span><span class="sxs-lookup"><span data-stu-id="3f938-133">However, you can use [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager if you need to reconfigure the server connections so [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] listens on a particular network protocol, port, or pipe.</span></span> <span data-ttu-id="3f938-134">如需啟用通訊協定的詳細資訊，請參閱 [啟用或停用伺服器網路通訊協定](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)。</span><span class="sxs-lookup"><span data-stu-id="3f938-134">For more information about enabling protocols, see [Enable or Disable a Server Network Protocol](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md).</span></span> <span data-ttu-id="3f938-135">如需啟用透過防火牆存取通訊協定的相關資訊，請參閱 [設定 Windows 防火牆以允許 SQL Server 存取](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。</span><span class="sxs-lookup"><span data-stu-id="3f938-135">For information about enabling access to protocols through a firewall, see [Configure the Windows Firewall to Allow SQL Server Access](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).</span></span>  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] <span data-ttu-id="3f938-136">組態管理員可讓您管理伺服器和用戶端網路通訊協定，其中包括強迫加密通訊協定、檢視別名屬性，或啟用/停用通訊協定的功能。</span><span class="sxs-lookup"><span data-stu-id="3f938-136">Configuration Manager allows you to manage server and client network protocols, including the ability to force protocol encryption, view alias properties, or enable/disable a protocol.</span></span>  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] <span data-ttu-id="3f938-137">組態管理員可讓您建立或移除別名、變更通訊協定的使用順序，或檢視伺服器別名的屬性，其中包括：</span><span class="sxs-lookup"><span data-stu-id="3f938-137">Configuration Manager allows you to create or remove an alias, change the order in which protocols are uses, or view properties for a server alias, including:</span></span>  
  
-   <span data-ttu-id="3f938-138">伺服器別名 - 用戶端連接之電腦所用的伺服器別名。</span><span class="sxs-lookup"><span data-stu-id="3f938-138">Server Alias - The server alias used for the computer to which the client is connecting.</span></span>  
  
-   <span data-ttu-id="3f938-139">通訊協定 - 設定項目所用的網路通訊協定。</span><span class="sxs-lookup"><span data-stu-id="3f938-139">Protocol - The network protocol used for the configuration entry.</span></span>  
  
-   <span data-ttu-id="3f938-140">連接參數 - 網路通訊協定設定之連接位址的相關參數。</span><span class="sxs-lookup"><span data-stu-id="3f938-140">Connection Parameters - The parameters associated with the connection address for the network protocol configuration.</span></span>  
  
 <span data-ttu-id="3f938-141">另外， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員也可讓您檢視容錯移轉叢集執行個體的相關資訊，不過，部份啟動和停止服務之類的動作，應該使用叢集管理員。</span><span class="sxs-lookup"><span data-stu-id="3f938-141">The [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager also allows you to view information about failover cluster instances, though Cluster Administrator should be used for some actions such as starting and stopping the services.</span></span>  
  
### <a name="available-network-protocols"></a><span data-ttu-id="3f938-142">可用的網路通訊協定</span><span class="sxs-lookup"><span data-stu-id="3f938-142">Available Network Protocols</span></span>  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] <span data-ttu-id="3f938-143">支援共用記憶體、TCP/IP 與具名管道通訊協定。</span><span class="sxs-lookup"><span data-stu-id="3f938-143">supports Shared Memory, TCP/IP, and Named Pipes protocols.</span></span> <span data-ttu-id="3f938-144">如需有關選擇網路通訊協定的詳細資訊，請參閱＜ [Configure Client Protocols](../database-engine/configure-windows/configure-client-protocols.md)＞。</span><span class="sxs-lookup"><span data-stu-id="3f938-144">For information about choosing a network protocols, see [Configure Client Protocols](../database-engine/configure-windows/configure-client-protocols.md).</span></span> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] <span data-ttu-id="3f938-145">不支援 VIA、Banyan VINES Sequenced Packet Protocol (SPP)、多重通訊協定、AppleTalk 或 NWLink IPX/SPX 網路通訊協定。</span><span class="sxs-lookup"><span data-stu-id="3f938-145">does not support the VIA, Banyan VINES Sequenced Packet Protocol (SPP), Multiprotocol, AppleTalk, or NWLink IPX/SPX network protocols.</span></span> <span data-ttu-id="3f938-146">先前連接這些通訊協定的用戶端必須選取不同的通訊協定，才能連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。</span><span class="sxs-lookup"><span data-stu-id="3f938-146">Clients previously connecting with these protocols must select a different protocol to connect to [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="3f938-147">您不能利用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員來設定 WinSock Proxy。</span><span class="sxs-lookup"><span data-stu-id="3f938-147">You cannot use [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager to configure the WinSock proxy.</span></span> <span data-ttu-id="3f938-148">若要設定 WinSock Proxy，請參閱您的 ISA 伺服器文件集。</span><span class="sxs-lookup"><span data-stu-id="3f938-148">To configure the WinSock proxy, see your ISA Server documentation.</span></span>  
  
## <a name="related-tasks"></a><span data-ttu-id="3f938-149">相關工作</span><span class="sxs-lookup"><span data-stu-id="3f938-149">Related Tasks</span></span>  
 [<span data-ttu-id="3f938-150">管理服務的如何主題 &#40;SQL Server 組態管理員&#41;</span><span class="sxs-lookup"><span data-stu-id="3f938-150">Managing Services How-to Topics &#40;SQL Server Configuration Manager&#41;</span></span>](../database-engine/managing-services-how-to-topics-sql-server-configuration-manager.md)  
  
 [<span data-ttu-id="3f938-151">啟動、停止、暫停、繼續、重新啟動 Database Engine、SQL Server Agent 或 SQL Server Browser 服務</span><span class="sxs-lookup"><span data-stu-id="3f938-151">Start, Stop, Pause, Resume, Restart the Database Engine, SQL Server Agent, or SQL Server Browser Service</span></span>](../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
 [<span data-ttu-id="3f938-152">啟動、停止或暫停 SQL Server Agent 服務</span><span class="sxs-lookup"><span data-stu-id="3f938-152">Start, Stop, or Pause the SQL Server Agent Service</span></span>](../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
 [<span data-ttu-id="3f938-153">將 SQL Server 執行個體設定為自動啟動 &#40;SQL Server 組態管理員&#41;</span><span class="sxs-lookup"><span data-stu-id="3f938-153">Set an Instance of SQL Server to Start Automatically &#40;SQL Server Configuration Manager&#41;</span></span>](../database-engine/configure-windows/scm-services-set-an-instance-to-start-automatically.md)  
  
 [<span data-ttu-id="3f938-154">避免自動啟動 SQL Server 的執行個體 &#40;SQL Server 組態管理員&#41;</span><span class="sxs-lookup"><span data-stu-id="3f938-154">Prevent Automatic Startup of an Instance of SQL Server &#40;SQL Server Configuration Manager&#41;</span></span>](../database-engine/configure-windows/scm-services-prevent-automatic-startup-of-an-instance.md)  
  
  