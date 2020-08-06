---
title: SQL Server Browser 服務 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- services [SQL Server], security
- SQL Browser service (See SQL Server Browser Service)
- Browser Service
- SQL Server Browser service
ms.assetid: 3cc00d3a-487c-4cd9-a155-655f02485fa0
author: stevestein
ms.author: sstein
ms.openlocfilehash: df2edf99f05b9f579e480b2f482c574dc713efb9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705769"
---
# <a name="sql-server-browser-service"></a><span data-ttu-id="8c370-102">SQL Server Browser 服務</span><span class="sxs-lookup"><span data-stu-id="8c370-102">SQL Server Browser Service</span></span>
  <span data-ttu-id="8c370-103">[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser 程式會以 Windows 服務的方式執行。</span><span class="sxs-lookup"><span data-stu-id="8c370-103">The [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser program runs as a Windows service.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="8c370-104">Browser 會接聽 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源的內送要求，並提供有關在電腦上所安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資訊。</span><span class="sxs-lookup"><span data-stu-id="8c370-104">Browser listens for incoming requests for [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resources and provides information about [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instances installed on the computer.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="8c370-105">Browser 完成下列動作：</span><span class="sxs-lookup"><span data-stu-id="8c370-105">Browser contributes to the following actions:</span></span>  
  
-   <span data-ttu-id="8c370-106">瀏覽可用伺服器的清單</span><span class="sxs-lookup"><span data-stu-id="8c370-106">Browsing a list of available servers</span></span>  
  
-   <span data-ttu-id="8c370-107">連接到正確的伺服器執行個體</span><span class="sxs-lookup"><span data-stu-id="8c370-107">Connecting to the correct server instance</span></span>  
  
-   <span data-ttu-id="8c370-108">連接到專用管理員連接 (DAC) 端點</span><span class="sxs-lookup"><span data-stu-id="8c370-108">Connecting to dedicated administrator connection (DAC) endpoints</span></span>  
  
 <span data-ttu-id="8c370-109">對於 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 與 [!INCLUDE[ssAS](../../includes/ssas-md.md)]的每個執行個體， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務 (sqlbrowser) 會提供執行個體名稱與版本號碼。</span><span class="sxs-lookup"><span data-stu-id="8c370-109">For each instance of the [!INCLUDE[ssDE](../../includes/ssde-md.md)] and [!INCLUDE[ssAS](../../includes/ssas-md.md)], the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser service (sqlbrowser) provides the instance name and the version number.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="8c370-110">Browser 會與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]一起安裝。</span><span class="sxs-lookup"><span data-stu-id="8c370-110">Browser is installed with [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span>  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="8c370-111">組態管理員來設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser。</span><span class="sxs-lookup"><span data-stu-id="8c370-111">Browser can be configured during setup or by using [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.</span></span> <span data-ttu-id="8c370-112">根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務會在下列情況中自動啟動：</span><span class="sxs-lookup"><span data-stu-id="8c370-112">By default, the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser service starts automatically:</span></span>  
  
-   <span data-ttu-id="8c370-113">升級安裝時。</span><span class="sxs-lookup"><span data-stu-id="8c370-113">When upgrading an installation.</span></span>  
  
-   <span data-ttu-id="8c370-114">在叢集上安裝時。</span><span class="sxs-lookup"><span data-stu-id="8c370-114">When installing on a cluster.</span></span>  
  
-   <span data-ttu-id="8c370-115">安裝 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的具名執行個體並包括 SQL Server Express 的所有執行個體時。</span><span class="sxs-lookup"><span data-stu-id="8c370-115">When installing a named instance of the [!INCLUDE[ssDE](../../includes/ssde-md.md)] including all instances of SQL Server Express.</span></span>  
  
-   <span data-ttu-id="8c370-116">安裝 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的具名執行個體時。</span><span class="sxs-lookup"><span data-stu-id="8c370-116">When installing a named instance of [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].</span></span>  
  
## <a name="background"></a><span data-ttu-id="8c370-117">背景</span><span class="sxs-lookup"><span data-stu-id="8c370-117">Background</span></span>  
 <span data-ttu-id="8c370-118">在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]之前，電腦上只可以安裝一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="8c370-118">Prior to [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], only one instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] could be installed on a computer.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="8c370-119">接聽通訊埠 1433 內送的要求，該通訊埠是由 Internet Assigned Numbers Authority (IANA) 官方指派給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的。</span><span class="sxs-lookup"><span data-stu-id="8c370-119">listened for incoming requests on port 1433, assigned to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] by the official Internet Assigned Numbers Authority (IANA).</span></span> <span data-ttu-id="8c370-120">只有一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體可以使用通訊埠，因此當 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 推出支援多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的功能時，發展了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol (SSRP) 來接聽 UDP 通訊埠 1434。</span><span class="sxs-lookup"><span data-stu-id="8c370-120">Only one instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] can use a port, so when [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] introduced support for multiple instances of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol (SSRP) was developed to listen on UDP port 1434.</span></span> <span data-ttu-id="8c370-121">此接聽服務是以安裝的執行個體名稱，以及執行個體使用的通訊埠或具名管道來回應用戶端要求。</span><span class="sxs-lookup"><span data-stu-id="8c370-121">This listener service responded to client requests with the names of the installed instances, and the ports or named pipes used by the instance.</span></span> <span data-ttu-id="8c370-122">為了克服 SSRP 系統的限制， [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 引進 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務來取代 SSRP。</span><span class="sxs-lookup"><span data-stu-id="8c370-122">To resolve limitations of the SSRP system, [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introduced the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser service as a replacement for SSRP.</span></span>  
  
## <a name="how-sql-server-browser-works"></a><span data-ttu-id="8c370-123">SQL Server Browser 如何運作</span><span class="sxs-lookup"><span data-stu-id="8c370-123">How SQL Server Browser Works</span></span>  
 <span data-ttu-id="8c370-124">當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體啟動時，如果已為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]啟用 TCP/IP 通訊協定，則會指派 TCP/IP 通訊埠給伺服器。</span><span class="sxs-lookup"><span data-stu-id="8c370-124">When an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] starts, if the TCP/IP protocol is enabled for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], the server is assigned a TCP/IP port.</span></span> <span data-ttu-id="8c370-125">如果已啟用具名管道通訊協定，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會接聽特定的具名管道。</span><span class="sxs-lookup"><span data-stu-id="8c370-125">If the named pipes protocol is enabled, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] listens on a specific named pipe.</span></span> <span data-ttu-id="8c370-126">這個通訊埠或「管道」是由該特定執行個體使用，來與用戶端應用程式交換資料。</span><span class="sxs-lookup"><span data-stu-id="8c370-126">This port, or "pipe," is used by that specific instance to exchange data with client applications.</span></span> <span data-ttu-id="8c370-127">在安裝期間，TCP 通訊埠 1433 和管道 `\sql\query` 會指派給預設執行個體，但以後伺服器管理員可以使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」來變更它們。</span><span class="sxs-lookup"><span data-stu-id="8c370-127">During installation, TCP port 1433 and pipe `\sql\query` are assigned to the default instance, but those can be changed later by the server administrator using [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.</span></span> <span data-ttu-id="8c370-128">由於只有一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體可以使用通訊埠或管道，因此會指定不同的通訊埠編號和管道名稱給具名執行個體，包括 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]。</span><span class="sxs-lookup"><span data-stu-id="8c370-128">Because only one instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] can use a port or pipe, different port numbers and pipe names are assigned for named instances, including [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].</span></span> <span data-ttu-id="8c370-129">依預設，啟用之後，具名執行個體和 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 都設定為使用動態通訊埠，也就是說，當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動時會指派可用的通訊埠。</span><span class="sxs-lookup"><span data-stu-id="8c370-129">By default, when enabled, both named instances and [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] are configured to use dynamic ports, that is, an available port is assigned when [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] starts.</span></span> <span data-ttu-id="8c370-130">如果需要，也可以將特定通訊埠指派給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。</span><span class="sxs-lookup"><span data-stu-id="8c370-130">If you want, a specific port can be assigned to an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="8c370-131">在連接時，用戶端可以指定特定的通訊埠，但如果該通訊埠是動態指定，則每當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新啟動時，通訊埠編號可能變更，導致用戶端不知道正確的通訊埠編號。</span><span class="sxs-lookup"><span data-stu-id="8c370-131">When connecting, clients can specify a specific port; but if the port is dynamically assigned, the port number can change anytime [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is restarted, so the correct port number is unknown to the client.</span></span>  
  
 <span data-ttu-id="8c370-132">在啟動時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 會啟動並要求 UDP 通訊埠 1434。</span><span class="sxs-lookup"><span data-stu-id="8c370-132">Upon startup, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser starts and claims UDP port 1434.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="8c370-133">Browser 會讀取登錄項目、識別電腦上的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，並記下它們使用的通訊埠與具名管道。</span><span class="sxs-lookup"><span data-stu-id="8c370-133">Browser reads the registry, identifies all instances of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] on the computer, and notes the ports and named pipes that they use.</span></span> <span data-ttu-id="8c370-134">當伺服器擁有兩張或多張網路卡時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 會傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所遇到的第一個已啟用連接埠。</span><span class="sxs-lookup"><span data-stu-id="8c370-134">When a server has two or more network cards, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser returns the first enabled port it encounters for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="8c370-135">Browser 支援 ipv6 和 ipv4。</span><span class="sxs-lookup"><span data-stu-id="8c370-135">Browser support ipv6 and ipv4.</span></span>  
  
 <span data-ttu-id="8c370-136">當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端要求 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源時，用戶端網路程式庫會使用通訊埠 1434 傳送 UDP 訊息到伺服器。</span><span class="sxs-lookup"><span data-stu-id="8c370-136">When [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] clients request [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resources, the client network library sends a UDP message to the server using port 1434.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="8c370-137">瀏覽器回應要求之執行個體的 TCP/IP 通訊埠或具名管道。</span><span class="sxs-lookup"><span data-stu-id="8c370-137">Browser responds with the TCP/IP port or named pipe of the requested instance.</span></span> <span data-ttu-id="8c370-138">於是，用戶端應用程式上的網路程式庫會使用所要的執行個體的通訊埠或具名管道，將要求傳送至伺服器來完成連接。</span><span class="sxs-lookup"><span data-stu-id="8c370-138">The network library on the client application then completes the connection by sending a request to the server using the port or named pipe of the desired instance.</span></span>  
  
 <span data-ttu-id="8c370-139">如需有關啟動與停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 瀏覽器服務的詳細資訊，請參閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書。</span><span class="sxs-lookup"><span data-stu-id="8c370-139">For information about starting and stopping the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser service, see [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Online.</span></span>  
  
## <a name="using-sql-server-browser"></a><span data-ttu-id="8c370-140">使用 SQL Server Browser</span><span class="sxs-lookup"><span data-stu-id="8c370-140">Using SQL Server Browser</span></span>  
 <span data-ttu-id="8c370-141">如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務未執行，但您提供正確的通訊埠編號或具名管道，則仍然可以連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="8c370-141">If the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser service is not running, you are still able to connect to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] if you provide the correct port number or named pipe.</span></span> <span data-ttu-id="8c370-142">例如，您可以使用在通訊埠 1433 執行的 TCP/IP，來連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的預設執行個體。</span><span class="sxs-lookup"><span data-stu-id="8c370-142">For instance, you can connect to the default instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] with TCP/IP if it is running on port 1433.</span></span>  
  
 <span data-ttu-id="8c370-143">不過，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務未執行，則下列連接沒有作用：</span><span class="sxs-lookup"><span data-stu-id="8c370-143">However, if the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser service is not running, the following connections do not work:</span></span>  
  
-   <span data-ttu-id="8c370-144">任何嘗試連接到具名執行個體卻未完整指定所有參數 (例如 TCP/IP 通訊埠或具名管道) 的元件。</span><span class="sxs-lookup"><span data-stu-id="8c370-144">Any component that tries to connect to a named instance without fully specifying all the parameters (such as the TCP/IP port or named pipe).</span></span>  
  
-   <span data-ttu-id="8c370-145">任何產生或傳遞伺服器/執行個體資訊的元件，稍後要重新連接的其他元件可使用此資訊。</span><span class="sxs-lookup"><span data-stu-id="8c370-145">Any component that generates or passes server\instance information that could later be used by other components to reconnect.</span></span>  
  
-   <span data-ttu-id="8c370-146">連接到具名執行個體但未提供通訊埠編號或管道。</span><span class="sxs-lookup"><span data-stu-id="8c370-146">Connecting to a named instance without providing the port number or pipe.</span></span>  
  
-   <span data-ttu-id="8c370-147">具名執行個體或預設執行個體 (若未使用 TCP/IP 通訊埠 1433) 的 DAC。</span><span class="sxs-lookup"><span data-stu-id="8c370-147">DAC to a named instance or the default instance if not using TCP/IP port 1433.</span></span>  
  
-   <span data-ttu-id="8c370-148">OLAP 重新導向程式服務。</span><span class="sxs-lookup"><span data-stu-id="8c370-148">The OLAP redirector service.</span></span>  
  
-   <span data-ttu-id="8c370-149">列舉 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、Enterprise Manager 或 Query Analyzer 中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="8c370-149">Enumerating servers in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], Enterprise Manager, or Query Analyzer.</span></span>  
  
 <span data-ttu-id="8c370-150">如果您在主從式架構狀況中使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (例如，當應用程式透過網路上存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時)，且如果您停止或停用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務，則必須指派特定通訊埠編號給每一個執行個體，並將用戶端應用程式碼撰寫為永遠使用此通訊埠編號。</span><span class="sxs-lookup"><span data-stu-id="8c370-150">If you are using [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in a client-server scenario (for example, when your application is accessing [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] across a network), if you stop or disable the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser service, you must assign a specific port number to each instance and write your client application code to always use that port number.</span></span> <span data-ttu-id="8c370-151">此方式有下列問題：</span><span class="sxs-lookup"><span data-stu-id="8c370-151">This approach has the following problems:</span></span>  
  
-   <span data-ttu-id="8c370-152">您必須更新或維護用戶端應用程式碼，才能確保它是連接到正確的通訊埠。</span><span class="sxs-lookup"><span data-stu-id="8c370-152">You must update and maintain client application code to ensure it is connecting to the proper port.</span></span>  
  
-   <span data-ttu-id="8c370-153">您為每個執行個體選取的通訊埠可能正由該伺服器上的其他服務或應用程式使用中，導致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體無法使用。</span><span class="sxs-lookup"><span data-stu-id="8c370-153">The port you choose for each instance may be used by another service or application on the server, causing the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] to be unavailable.</span></span>  
  
## <a name="clustering"></a><span data-ttu-id="8c370-154">叢集</span><span class="sxs-lookup"><span data-stu-id="8c370-154">Clustering</span></span>  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="8c370-155">Browser 不是群集資源，不支援一個叢集節點容錯移轉到另一個叢集節點。</span><span class="sxs-lookup"><span data-stu-id="8c370-155">Browser is not a clustered resource and does not support failover from one cluster node to the other.</span></span> <span data-ttu-id="8c370-156">因此，以群集的情況而言，應該要為群集的每一個節點安裝及開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser。</span><span class="sxs-lookup"><span data-stu-id="8c370-156">Therefore, in the case of a cluster, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser should be installed and turned on for each node of the cluster.</span></span> <span data-ttu-id="8c370-157">在群集上， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 會接聽 IP_ANY。</span><span class="sxs-lookup"><span data-stu-id="8c370-157">On clusters, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser listens on IP_ANY.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="8c370-158">接聽 IP_ANY 時，若您啟用的是接聽特定 IP，則使用者必須在每一個 IP 上設定相同的 TCP 通訊埠，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 會傳回它發現的第一個 IP/通訊埠組合。</span><span class="sxs-lookup"><span data-stu-id="8c370-158">When listening on IP_ANY, when you enable listening on specific IPs, the user must configure the same TCP port on each IP, because [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser returns the first IP/port pair that it encounters.</span></span>  
  
## <a name="installing-uninstalling-and-running-from-the-command-line"></a><span data-ttu-id="8c370-159">從命令列安裝、解除安裝和執行</span><span class="sxs-lookup"><span data-stu-id="8c370-159">Installing, Uninstalling, and Running from the Command Line</span></span>  
 <span data-ttu-id="8c370-160">依預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 程式會安裝在 C:\Program Files (x86)\Microsoft SQL Server\90\Shared\sqlbrowser.exe。</span><span class="sxs-lookup"><span data-stu-id="8c370-160">By default, the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser program is installed at C:\Program Files (x86)\Microsoft SQL Server\90\Shared\sqlbrowser.exe.</span></span>  
  
 <span data-ttu-id="8c370-161">移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的最後一個執行個體之後，就會解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務。</span><span class="sxs-lookup"><span data-stu-id="8c370-161">The [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser service is uninstalled when the last instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is removed.</span></span>  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="8c370-162">利用 **-c** 參數，可從命令提示字元啟動瀏覽器來進行疑難排解：</span><span class="sxs-lookup"><span data-stu-id="8c370-162">Browser can be started from the command prompt for troubleshooting, by using the **-c** switch:</span></span>  
  
```  
<drive>\<path>\sqlbrowser.exe -c  
```  
  
## <a name="security"></a><span data-ttu-id="8c370-163">安全性</span><span class="sxs-lookup"><span data-stu-id="8c370-163">Security</span></span>  
  
### <a name="account-privileges"></a><span data-ttu-id="8c370-164">帳戶權限</span><span class="sxs-lookup"><span data-stu-id="8c370-164">Account Privileges</span></span>  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="8c370-165">瀏覽器會接聽 UDP 通訊埠，並接受使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol (SSRP) 的未驗證要求。</span><span class="sxs-lookup"><span data-stu-id="8c370-165">Browser listens on a UDP port and accepts unauthenticated requests by using [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol (SSRP).</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="8c370-166">Browser，以降低遭受惡意攻擊的機會。</span><span class="sxs-lookup"><span data-stu-id="8c370-166">Browser should be run in the security context of a low privileged user to minimize exposure to a malicious attack.</span></span> <span data-ttu-id="8c370-167">可利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員來變更登入帳戶。</span><span class="sxs-lookup"><span data-stu-id="8c370-167">The logon account can be changed by using the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.</span></span> <span data-ttu-id="8c370-168">[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 所需的最低使用者權限如下：</span><span class="sxs-lookup"><span data-stu-id="8c370-168">The minimum user rights for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser are the following:</span></span>  
  
-   <span data-ttu-id="8c370-169">拒絕從網路存取這部電腦</span><span class="sxs-lookup"><span data-stu-id="8c370-169">Deny access to this computer from the network</span></span>  
  
-   <span data-ttu-id="8c370-170">拒絕本機登入</span><span class="sxs-lookup"><span data-stu-id="8c370-170">Deny logon locally</span></span>  
  
-   <span data-ttu-id="8c370-171">拒絕以批次作業登入</span><span class="sxs-lookup"><span data-stu-id="8c370-171">Deny Log on as a batch job</span></span>  
  
-   <span data-ttu-id="8c370-172">拒絕透過終端機服務登入</span><span class="sxs-lookup"><span data-stu-id="8c370-172">Deny Log On Through Terminal Services</span></span>  
  
-   <span data-ttu-id="8c370-173">登入為服務</span><span class="sxs-lookup"><span data-stu-id="8c370-173">Log on as a service</span></span>  
  
-   <span data-ttu-id="8c370-174">讀寫與網路通訊 (通訊埠和管道) 有關的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登錄機碼。</span><span class="sxs-lookup"><span data-stu-id="8c370-174">Read and write the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registry keys related to network communication (ports and pipes)</span></span>  
  
### <a name="default-account"></a><span data-ttu-id="8c370-175">預設帳戶</span><span class="sxs-lookup"><span data-stu-id="8c370-175">Default Account</span></span>  
 <span data-ttu-id="8c370-176">在安裝過程中，安裝程式會設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 使用此帳戶來啟動服務。</span><span class="sxs-lookup"><span data-stu-id="8c370-176">Setup configures [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser to use the account selected for services during setup.</span></span> <span data-ttu-id="8c370-177">其他可能的帳戶包括下列各項：</span><span class="sxs-lookup"><span data-stu-id="8c370-177">Other possible accounts include the following:</span></span>  
  
-   <span data-ttu-id="8c370-178">任何 **網域\本機** 帳戶</span><span class="sxs-lookup"><span data-stu-id="8c370-178">Any **domain\local** account</span></span>  
  
-   <span data-ttu-id="8c370-179">**[本機服務]** 帳戶</span><span class="sxs-lookup"><span data-stu-id="8c370-179">The **local service** account</span></span>  
  
-   <span data-ttu-id="8c370-180">**本機系統** 帳戶 (不建議使用，因為有不必要的權限)</span><span class="sxs-lookup"><span data-stu-id="8c370-180">The **local system** account (not recommended as has unnecessary privileges)</span></span>  
  
### <a name="hiding-sql-server"></a><span data-ttu-id="8c370-181">隱藏 SQL Server</span><span class="sxs-lookup"><span data-stu-id="8c370-181">Hiding SQL Server</span></span>  
 <span data-ttu-id="8c370-182">隱藏的執行個體是只支援共用記憶體連接的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。</span><span class="sxs-lookup"><span data-stu-id="8c370-182">Hidden instances are instances of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] that support only shared memory connections.</span></span> <span data-ttu-id="8c370-183">對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請設定 `HideInstance` 旗標以指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 不應使用關於此伺服器執行個體的資訊來回應。</span><span class="sxs-lookup"><span data-stu-id="8c370-183">For [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], set the `HideInstance` flag to indicate that [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser should not respond with information about this server instance.</span></span>  
  
### <a name="using-a-firewall"></a><span data-ttu-id="8c370-184">使用防火牆</span><span class="sxs-lookup"><span data-stu-id="8c370-184">Using a Firewall</span></span>  
 <span data-ttu-id="8c370-185">若要與位於防火牆後面之伺服器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務進行通訊，除了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的 TCP 通訊埠 (例如 1433) 之外，請開啟 UDP 通訊埠 1434。</span><span class="sxs-lookup"><span data-stu-id="8c370-185">To communicate with the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser service on a server behind a firewall, open UDP port 1434, in addition to the TCP port used by [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (e.g., 1433).</span></span> <span data-ttu-id="8c370-186">如需有關使用防火牆的詳細資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜如何：設定防火牆供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取＞。</span><span class="sxs-lookup"><span data-stu-id="8c370-186">For information about working with a firewall, see "How to: Configure a Firewall for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Access" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Online.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8c370-187">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8c370-187">See Also</span></span>  
 [<span data-ttu-id="8c370-188">網路通訊協定和網路程式庫</span><span class="sxs-lookup"><span data-stu-id="8c370-188">Network Protocols and Network Libraries</span></span>](../../../2014/sql-server/install/network-protocols-and-network-libraries.md)  
  
  