---
title: 選擇網路通訊協定 |Microsoft Docs
description: 比較和對比可用來連接到 SQL Server 資料庫引擎的網路通訊協定，例如共用記憶體、TCP/IP 和具名管道。
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
- Named Pipes [SQL Server]
- TCP [SQL Server]
- network protocols [SQL Server], choosing
- protocols [SQL Server], choosing
- NWLink IPX/SPX [SQL Server]
- client configuration [SQL Server], protocols
- VIA
- Multiprotocol Net-Library [SQL Server]
- IPX/SPX [SQL Server]
- Banyan VINES
- protocols [SQL Server], client configuration
ms.assetid: 6565fb7d-b076-4447-be90-e10d0dec359a
author: rothja
ms.author: jroth
ms.openlocfilehash: 13cbfbcbef54759a16729692e4f5a649f387d059
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87704593"
---
# <a name="choosing-a-network-protocol"></a><span data-ttu-id="9b376-103">選擇網路通訊協定</span><span class="sxs-lookup"><span data-stu-id="9b376-103">Choosing a Network Protocol</span></span>
  <span data-ttu-id="9b376-104">若要連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，必須啟用網路通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9b376-104">To connect to [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] you must have a network protocol enabled.</span></span> [!INCLUDE[msCoName](../../includes/msconame-md.md)]<span data-ttu-id="9b376-105">[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以同時服務數個通訊協定上的要求。</span><span class="sxs-lookup"><span data-stu-id="9b376-105">[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] can service requests on several protocols at the same time.</span></span> <span data-ttu-id="9b376-106">用戶端會使用單一通訊協定連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="9b376-106">Clients connect to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] with a single protocol.</span></span> <span data-ttu-id="9b376-107">如果用戶端程式不知道 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在接聽哪個通訊協定，請設定用戶端循序嘗試多個通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9b376-107">If the client program does not know which protocol [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is listening on, configure the client to sequentially try multiple protocols.</span></span> <span data-ttu-id="9b376-108">您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員來啟用、停用及設定網路通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9b376-108">Use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager to enable, disable, and configure network protocols.</span></span>  
  
## <a name="shared-memory"></a><span data-ttu-id="9b376-109">共用記憶體</span><span class="sxs-lookup"><span data-stu-id="9b376-109">Shared Memory</span></span>  
 <span data-ttu-id="9b376-110">共用記憶體是使用上最簡單的通訊協定，而且不用設定任何設定。</span><span class="sxs-lookup"><span data-stu-id="9b376-110">Shared memory is the simplest protocol to use and has no configurable settings.</span></span> <span data-ttu-id="9b376-111">因為使用共用記憶體通訊協定的用戶端，只能連接到在相同電腦上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，所以不適用於大部分資料庫活動。</span><span class="sxs-lookup"><span data-stu-id="9b376-111">Because clients using the shared memory protocol can only connect to a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance running on the same computer, it is not useful for most database activity.</span></span> <span data-ttu-id="9b376-112">當您懷疑其他通訊協定的設定不正確時，請使用共用記憶體通訊協定進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="9b376-112">Use the shared memory protocol for troubleshooting when you suspect the other protocols are configured incorrectly.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="9b376-113">使用 MDAC 2.8 或舊版的用戶端無法使用共用記憶體通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9b376-113">Clients that use MDAC 2.8 or earlier cannot use shared memory protocol.</span></span> <span data-ttu-id="9b376-114">即使這些使用者嘗試使用此通訊協定，還是會自動切換成具名管道通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9b376-114">If these clients try this, they are automatically switched to the named pipes protocol.</span></span>  
  
## <a name="tcpip"></a><span data-ttu-id="9b376-115">TCP/IP</span><span class="sxs-lookup"><span data-stu-id="9b376-115">TCP/IP</span></span>  
 <span data-ttu-id="9b376-116">TCP/IP 是網際網路廣泛使用的一般通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9b376-116">TCP/IP is a common protocol widely used over the Internet.</span></span> <span data-ttu-id="9b376-117">其可在具有各種硬體架構與不同作業系統之電腦的互連網路間通訊。</span><span class="sxs-lookup"><span data-stu-id="9b376-117">It communicates across interconnected networks of computers that have diverse hardware architectures and various operating systems.</span></span> <span data-ttu-id="9b376-118">TCP/IP 包括了路由網路傳輸量的標準，同時提供了進階安全性功能，</span><span class="sxs-lookup"><span data-stu-id="9b376-118">TCP/IP includes standards for routing network traffic and offers advanced security features.</span></span> <span data-ttu-id="9b376-119">為現今企業中最常用的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9b376-119">It is the most popular protocol that is used in business today.</span></span> <span data-ttu-id="9b376-120">設定電腦使用 TCP/IP 是一件很複雜的作業，但大部分網路電腦都已正確完成設定。</span><span class="sxs-lookup"><span data-stu-id="9b376-120">Configuring your computer to use TCP/IP can be complex, but most networked computers are already correctly configured.</span></span> <span data-ttu-id="9b376-121">若要設定「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」中未公開的 TCP/IP 設定，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 文件集。</span><span class="sxs-lookup"><span data-stu-id="9b376-121">To configure the TCP/IP settings that are not exposed in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, see the [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows documentation.</span></span>  
  
## <a name="named-pipes"></a><span data-ttu-id="9b376-122">具名管道</span><span class="sxs-lookup"><span data-stu-id="9b376-122">Named Pipes</span></span>  
 <span data-ttu-id="9b376-123">「具名管道」是為區域網路開發的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9b376-123">Named Pipes is a protocol developed for local area networks.</span></span> <span data-ttu-id="9b376-124">有一個處理序會使用部分記憶體將資訊傳遞給另一個處理序，如此該處理序的輸出會是另一個處理序的輸入。</span><span class="sxs-lookup"><span data-stu-id="9b376-124">A part of memory is used by one process to pass information to another process, so that the output of one is the input of the other.</span></span> <span data-ttu-id="9b376-125">第二個處理序可以在本機 (跟第一個處理序位於相同的電腦上) 或位於遠端 (在網路電腦上)。</span><span class="sxs-lookup"><span data-stu-id="9b376-125">The second process can be local (on the same computer as the first) or remote (on a networked computer).</span></span>  
  
## <a name="named-pipes-vs-tcpip-sockets"></a><span data-ttu-id="9b376-126">具名管道與TCP/IP 通訊端</span><span class="sxs-lookup"><span data-stu-id="9b376-126">Named Pipes vs. TCP/IP Sockets</span></span>  
 <span data-ttu-id="9b376-127">在速度快的區域網路 (LAN) 環境中，傳輸控制通訊協定/網際網路通訊協定 (TCP/IP) 通訊端與具名管道用戶端在效能方面可相互媲美。</span><span class="sxs-lookup"><span data-stu-id="9b376-127">In a fast local area network (LAN) environment, Transmission Control Protocol/Internet Protocol (TCP/IP) Sockets and Named Pipes clients are comparable with regard to performance.</span></span> <span data-ttu-id="9b376-128">但是，若使用速度較慢的網路，例如，廣域網路 (WAN) 或撥號網路，TCP/IP 通訊端與具名管道用戶端之間，在效能上的差異就顯而易見。</span><span class="sxs-lookup"><span data-stu-id="9b376-128">However, the performance difference between the TCP/IP Sockets and Named Pipes clients becomes apparent with slower networks, such as across wide area networks (WANs) or dial-up networks.</span></span> <span data-ttu-id="9b376-129">這是因為跨處理序通訊 (IPC) 機制，在對等端之間通訊的方式不同。</span><span class="sxs-lookup"><span data-stu-id="9b376-129">This is because of the different ways the interprocess communication (IPC) mechanisms communicate between peers.</span></span>  
  
 <span data-ttu-id="9b376-130">對於具名管道，網路通訊一般較為互動。</span><span class="sxs-lookup"><span data-stu-id="9b376-130">For named pipes, network communications are typically more interactive.</span></span> <span data-ttu-id="9b376-131">對等會等到另一個對等使用讀取命令，要求傳送資料時才會傳送。</span><span class="sxs-lookup"><span data-stu-id="9b376-131">A peer does not send data until another peer asks for it using a read command.</span></span> <span data-ttu-id="9b376-132">網路讀取動作在開始讀取資料之前，一般會涉及一連串的對等具名管道訊息。</span><span class="sxs-lookup"><span data-stu-id="9b376-132">A network read typically involves a series of peek named pipes messages before it starts to read the data.</span></span> <span data-ttu-id="9b376-133">這些在速度慢的網路中要付出的成本可能相當昂貴，而且會導致產生過多的網路傳輸量，而影響到其他網路用戶端。</span><span class="sxs-lookup"><span data-stu-id="9b376-133">These can be very costly in a slow network and cause excessive network traffic, which in turn affects other network clients.</span></span>  
  
 <span data-ttu-id="9b376-134">釐清您正在討論的是本機管道或網路管道也很重要。</span><span class="sxs-lookup"><span data-stu-id="9b376-134">It is also important to clarify if you are talking about local pipes or network pipes.</span></span> <span data-ttu-id="9b376-135">如果在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的電腦本機執行伺服器應用程式，則可以選擇本機的具名管道通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9b376-135">If the server application is running locally on the computer that is running an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], the local Named Pipes protocol is an option.</span></span> <span data-ttu-id="9b376-136">本機的具名管道會在核心模式下執行且執行速度會相當快。</span><span class="sxs-lookup"><span data-stu-id="9b376-136">Local named pipes runs in kernel mode and is very fast.</span></span>  
  
 <span data-ttu-id="9b376-137">對於 TCP/IP 通訊端，資料傳輸較為簡化而且負擔較輕。</span><span class="sxs-lookup"><span data-stu-id="9b376-137">For TCP/IP Sockets, data transmissions are more streamlined and have less overhead.</span></span> <span data-ttu-id="9b376-138">資料傳輸也可以得利於 TCP/IP 通訊端效能增強機制 (例如，視窗型、延遲的收條等等)，</span><span class="sxs-lookup"><span data-stu-id="9b376-138">Data transmissions can also take advantage of TCP/IP Sockets performance enhancement mechanisms such as windowing, delayed acknowledgements, and so on.</span></span> <span data-ttu-id="9b376-139">這對速度慢的網路非常有幫助。</span><span class="sxs-lookup"><span data-stu-id="9b376-139">This can be very helpful in a slow network.</span></span> <span data-ttu-id="9b376-140">視應用程式類型而定，效能差異可能十分顯著。</span><span class="sxs-lookup"><span data-stu-id="9b376-140">Depending on the type of applications, such performance differences can be significant.</span></span>  
  
 <span data-ttu-id="9b376-141">TCP/IP 通訊端也支援積存佇列，</span><span class="sxs-lookup"><span data-stu-id="9b376-141">TCP/IP Sockets also support a backlog queue.</span></span> <span data-ttu-id="9b376-142">跟在嘗試連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時可能會導致管道忙碌而產生錯誤的具名管道相比，可提供一些緩衝效果。</span><span class="sxs-lookup"><span data-stu-id="9b376-142">This can provide a limited smoothing effect compared to named pipes that could lead to pipe-busy errors when you are trying to connect to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span>  
  
 <span data-ttu-id="9b376-143">一般來說，速度慢的 LAN、WAN 或撥接網路會偏好使用 TCP/IP，而當不用擔心網路速度時，具名管道會是較佳的選擇，因為提供的功能較多、操作更為簡單，而且組態選項較多。</span><span class="sxs-lookup"><span data-stu-id="9b376-143">Generally, TCP/IP is preferred in a slow LAN, WAN, or dial-up network, whereas named pipes can be a better choice when network speed is not the issue, as it offers more functionality, ease of use, and configuration options.</span></span>  
  
## <a name="enabling-the-protocol"></a><span data-ttu-id="9b376-144">啟用通訊協定</span><span class="sxs-lookup"><span data-stu-id="9b376-144">Enabling the Protocol</span></span>  
 <span data-ttu-id="9b376-145">用戶端與伺服器兩者必須都啟用通訊協定，才能夠運作。</span><span class="sxs-lookup"><span data-stu-id="9b376-145">The protocol must be enabled on both the client and server to work.</span></span> <span data-ttu-id="9b376-146">伺服器可以同時接聽來自所有已啟用之通訊協定上的要求。</span><span class="sxs-lookup"><span data-stu-id="9b376-146">The server can listen for requests on all enabled protocols at the same time.</span></span> <span data-ttu-id="9b376-147">用戶端電腦可挑選一個通訊協定，或按 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員中列出的通訊協定依序嘗試。</span><span class="sxs-lookup"><span data-stu-id="9b376-147">Client computers can pick one, or try the protocols in the order listed in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.</span></span>  
  
 <span data-ttu-id="9b376-148">如需如何設定通訊協定並連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的簡要教學課程，請參閱 [教學課程：Database Engine 使用者入門](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)。</span><span class="sxs-lookup"><span data-stu-id="9b376-148">For a short tutorial about how to configure protocols and connect to the [!INCLUDE[ssDE](../../includes/ssde-md.md)], see [Tutorial: Getting Started with the Database Engine](../../relational-databases/tutorial-getting-started-with-the-database-engine.md).</span></span>  
  
  