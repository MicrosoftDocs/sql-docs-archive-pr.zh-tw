---
title: 使用擴充保護連接至資料庫引擎 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- spoofing attacks
- service binding
- luring attacks
- Schannel
- channel binding
- Extended Protection
ms.assetid: ecfd783e-7dbb-4a6c-b5ab-c6c27d5dd57f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 718e5c9897f0883734d460e34ca26bba4f759a54
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597325"
---
# <a name="connect-to-the-database-engine-using-extended-protection"></a><span data-ttu-id="e4b4d-102">使用擴充保護連接至 Database Engine</span><span class="sxs-lookup"><span data-stu-id="e4b4d-102">Connect to the Database Engine Using Extended Protection</span></span>
  <span data-ttu-id="e4b4d-103">從 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 開始 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就支援 [擴充保護]。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-103">[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supports **Extended Protection** beginning with [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].</span></span> <span data-ttu-id="e4b4d-104">**驗證擴充保護** 是作業系統實作的網路元件功能。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-104">**Extended Protection for Authentication** is a feature of the network components implemented by the operating system.</span></span> <span data-ttu-id="e4b4d-105">Windows 7 和 Windows Server 2008 R2 上可支援 **[擴充保護]** 。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-105">**Extended Protection** is supported in Windows 7 and Windows Server 2008 R2.</span></span> <span data-ttu-id="e4b4d-106">Service Pack 中內含**擴充保護** ，可供舊版 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 作業系統使用。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-106">**Extended Protection** is included in service packs for older [!INCLUDE[msCoName](../../includes/msconame-md.md)] operating systems.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="e4b4d-107">在使用 **擴充保護**進行連接時較安全。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-107">is more secure when connections are made using **Extended Protection**.</span></span>  
  
> [!IMPORTANT]  
>  <span data-ttu-id="e4b4d-108">Windows 預設不會啟用 **[擴充保護]** 。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-108">Windows does not enable **Extended Protection** by default.</span></span> <span data-ttu-id="e4b4d-109">如需有關如何在 Windows 中啟用 **[擴充保護]** 的詳細資訊，請參閱 [驗證擴充保護](https://support.microsoft.com/kb/968389)。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-109">For information about how to enable **Extended Protection** in Windows, see [Extended Protection for Authentication](https://support.microsoft.com/kb/968389).</span></span>  
  
## <a name="description-of-extended-protection"></a><span data-ttu-id="e4b4d-110">擴充保護的描述</span><span class="sxs-lookup"><span data-stu-id="e4b4d-110">Description of Extended Protection</span></span>  
 <span data-ttu-id="e4b4d-111">**[擴充保護]** 會使用服務繫結與通道繫結來避免驗證轉送攻擊。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-111">**Extended Protection** uses service binding and channel binding to help prevent an authentication relay attack.</span></span> <span data-ttu-id="e4b4d-112">在驗證轉送攻擊中，可以執行 NTLM 驗證的用戶端 (如 Windows 檔案總管、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Outlook、.NET SqlClient 應用程式等) 會連接到攻擊者 (如惡意 CIFS 檔案伺服器)。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-112">In an authentication relay attack, a client that can perform NTLM authentication (for example, Windows Explorer, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Outlook, a .NET SqlClient application, etc.), connects to an attacker (for example, a malicious CIFS file server).</span></span> <span data-ttu-id="e4b4d-113">攻擊者會使用用戶端的認證來偽裝成用戶端，並向服務驗證 (例如，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務的執行個體)。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-113">The attacker uses the client's credentials to masquerade as the client and authenticate to a service (for example, an instance of the [!INCLUDE[ssDE](../../includes/ssde-md.md)] service).</span></span>  
  
 <span data-ttu-id="e4b4d-114">這種攻擊有兩種變化：</span><span class="sxs-lookup"><span data-stu-id="e4b4d-114">There are two variations of this attack:</span></span>  
  
-   <span data-ttu-id="e4b4d-115">在引誘攻擊中引誘用戶端自願連接到攻擊者。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-115">In a luring attack, the client is lured to voluntarily connect to the attacker.</span></span>  
  
-   <span data-ttu-id="e4b4d-116">在詐騙攻擊中，用戶端打算連接到有效的服務，但沒有注意到 DNS 和 IP 路由的其中一個或兩者已被侵害，所以連接會重新導向攻擊者。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-116">In a spoofing attack, the client intends to connect to a valid service, but is unaware that one or both of DNS and IP routing are poisoned to redirect the connection to the attacker instead.</span></span>  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="e4b4d-117">支援服務繫結與通道繫結，以減少 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的這些攻擊。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-117">supports service binding and channel binding to help reduce these attacks on [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instances.</span></span>  
  
### <a name="service-binding"></a><span data-ttu-id="e4b4d-118">服務繫結</span><span class="sxs-lookup"><span data-stu-id="e4b4d-118">Service Binding</span></span>  
 <span data-ttu-id="e4b4d-119">服務繫結位址引誘攻擊的方式，是要求用戶端傳送用戶端打算連接之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的已簽署服務主要名稱 (SPN)。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-119">Service binding addresses luring attacks by requiring a client to send a signed service principal name (SPN) of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] service that the client intends to connect to.</span></span> <span data-ttu-id="e4b4d-120">在驗證回應的過程中，該服務會驗證封包中收到的 SPN 與它自己的 SPN 相符。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-120">As part of the authentication response, the service validates that the SPN received in the packet matches its own SPN.</span></span> <span data-ttu-id="e4b4d-121">如果用戶端被引誘連接到攻擊者，用戶端將會包含攻擊者的已簽署 SPN。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-121">If a client is lured to connect to an attacker, the client will include the signed SPN of the attacker.</span></span> <span data-ttu-id="e4b4d-122">攻擊者無法轉送封包來向真正的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務驗證為用戶端，因為其中包含攻擊者的 SPN。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-122">The attacker cannot relay the packet to authenticate to the real [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] service as the client, because it would include the SPN of the attacker.</span></span> <span data-ttu-id="e4b4d-123">服務繫結會產生單次可忽略的成本，但是並不會處理詐騙攻擊。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-123">Service binding incurs a one-time, negligible cost, but it does not address spoofing attacks.</span></span> <span data-ttu-id="e4b4d-124">當用戶端應用程式沒有使用加密來連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，系統就會進行服務繫結。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-124">Service Binding occurs when a client application does not use encryption to connect to the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span>  
  
### <a name="channel-binding"></a><span data-ttu-id="e4b4d-125">通道繫結</span><span class="sxs-lookup"><span data-stu-id="e4b4d-125">Channel Binding</span></span>  
 <span data-ttu-id="e4b4d-126">通道繫結會在用戶端與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的執行個體之間建立安全通道 (Schannel)。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-126">Channel binding establishes a secure channel (Schannel) between a client and an instance of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] service.</span></span> <span data-ttu-id="e4b4d-127">此服務會驗證用戶端的真實性，其方式是比較該通道特定用戶端通道繫結權杖 (CBT) 與它自己的 CBT。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-127">The service verifies the authenticity of the client by comparing the client's channel binding token (CBT) specific to that channel, with its own CBT.</span></span> <span data-ttu-id="e4b4d-128">通道繫結會處理引誘和詐騙這兩種攻擊。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-128">Channel binding addresses both luring and spoofing attacks.</span></span> <span data-ttu-id="e4b4d-129">但是，它會發生較大的執行階段成本，因為它需要所有工作階段流量的傳輸層安全性 (TLS) 加密。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-129">However, it incurs a larger runtime cost, because it requires Transport Layer Security (TLS) encryption of all the session traffic.</span></span> <span data-ttu-id="e4b4d-130">用戶端應用程式使用加密連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時會發生通道繫結，與加密由用戶端還是伺服器強制無關。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-130">Channel Binding occurs when a client application uses encryption to connect to the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], regardless of whether encryption is enforced by the client or by the server.</span></span>  
  
> [!WARNING]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="e4b4d-131">的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 資料提供者支援 TLS 1.0 和 SSL 3.0。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-131">and [!INCLUDE[msCoName](../../includes/msconame-md.md)] data providers for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] support TLS 1.0 and SSL 3.0.</span></span> <span data-ttu-id="e4b4d-132">如果您以在作業系統 SChannel 層級中進行變更的方式，強制執行不同的通訊協定 (例如 TLS 1.1 或 TLS 1.2)，您與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的連線可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-132">If you enforce a different protocol (such as TLS 1.1 or TLS 1.2) by making changes in the operating system SChannel layer, your connections to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] might fail.</span></span>  
  
### <a name="operating-system-support"></a><span data-ttu-id="e4b4d-133">作業系統支援</span><span class="sxs-lookup"><span data-stu-id="e4b4d-133">Operating System Support</span></span>  
 <span data-ttu-id="e4b4d-134">下列連結提供有關 Windows 如何支援 **[擴充保護]** 的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="e4b4d-134">The following links provide more information about how Windows supports **Extended Protection**:</span></span>  
  
-   [<span data-ttu-id="e4b4d-135">具有擴充保護的整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="e4b4d-135">Integrated Windows Authentication with Extended Protection</span></span>](https://msdn.microsoft.com/library/dd639324.aspx)  
  
-   [<span data-ttu-id="e4b4d-136">Microsoft 安全性摘要報告 (973811)，驗證擴充保護</span><span class="sxs-lookup"><span data-stu-id="e4b4d-136">Microsoft Security Advisory (973811), Extended Protection for Authentication</span></span>](https://support.microsoft.com//help/973811/microsoft-security-advisory-extended-protection-for-authentication)  
  
## <a name="settings"></a><span data-ttu-id="e4b4d-137">設定</span><span class="sxs-lookup"><span data-stu-id="e4b4d-137">Settings</span></span>  
 <span data-ttu-id="e4b4d-138">有三個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接設定會影響服務繫結與通道繫結。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-138">There are three [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] connection settings that affect service binding and channel binding.</span></span> <span data-ttu-id="e4b4d-139">這些設定可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員或 WMI 加以設定，而且可以使用原則型式管理中的 **[伺服器通訊協定設定]** Facet 加以檢視。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-139">The settings can be configured by using the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, or by using WMI, and can by viewed by using the **Server Protocol Settings** facet of Policy Based Management.</span></span>  
  
-   <span data-ttu-id="e4b4d-140">**強制加密**</span><span class="sxs-lookup"><span data-stu-id="e4b4d-140">**Force Encryption**</span></span>  
  
     <span data-ttu-id="e4b4d-141">可能的值是 **[開啟]** 和 **[關閉]** 。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-141">Possible values are **On** and **Off**.</span></span> <span data-ttu-id="e4b4d-142">若要使用通道繫結，[ **強制加密** ] 必須設定為 [ **開啟**]，而所有用戶端將會強制加密。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-142">To use channel binding, **Force Encryption** must be set to **On**, and all clients will be forced to encrypt.</span></span> <span data-ttu-id="e4b4d-143">如果設定為 **[關閉]** ，則只會保證服務繫結。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-143">If it is **Off**, only service binding is guaranteed.</span></span> <span data-ttu-id="e4b4d-144">**[強制加密]** 位於 **組態管理員的** [MSSQLSERVER 的通訊協定屬性] ([旗標] 索引標籤) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-144">**Force Encryption** is on the **Protocols for MSSQLSERVER Properties (Flags Tab)** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.</span></span>  
  
-   <span data-ttu-id="e4b4d-145">**擴充保護**</span><span class="sxs-lookup"><span data-stu-id="e4b4d-145">**Extended Protection**</span></span>  
  
     <span data-ttu-id="e4b4d-146">可能的值是 **[關閉]** 、 **[允許]** 和 **[必要]** 。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-146">Possible values are **Off**, **Allowed**, and **Required**.</span></span> <span data-ttu-id="e4b4d-147">**[擴充保護]** 變數可讓使用者設定每個 **執行個體的** 擴充保護層級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-147">The **Extended Protection** variable lets users configure the **Extended Protection** level for each [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance.</span></span> <span data-ttu-id="e4b4d-148">**[擴充保護]** 位於 **組態管理員的** [MSSQLSERVER 的通訊協定屬性] ([進階] 索引標籤) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-148">**Extended Protection** is on the **Protocols for MSSQLSERVER Properties (Advanced Tab)** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.</span></span>  
  
    -   <span data-ttu-id="e4b4d-149">當設定為 **[關閉]** 時，便會停用 **[擴充保護]** 。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-149">When set to **Off**, **Extended Protection** is disabled.</span></span> <span data-ttu-id="e4b4d-150">[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體將會接受來自任何用戶端的連接，不論用戶端是否受到保護。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-150">The instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] will accept connections from any client regardless of whether the client is protected or not.</span></span> <span data-ttu-id="e4b4d-151">**[關閉]** 與舊版及未修補的作業系統相容，但是比較不安全。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-151">**Off** is compatible with older and unpatched operating systems, but is less secure.</span></span> <span data-ttu-id="e4b4d-152">當您知道用戶端作業系統不支援擴充保護時，請使用這個設定。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-152">Use this setting when you know that the client operating systems do not support extended protection.</span></span>  
  
    -   <span data-ttu-id="e4b4d-153">當設定為 **[允許]** 時，支援 **[擴充保護]** 之作業系統的連接便需要 **[擴充保護]** 。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-153">When set to **Allowed**, **Extended Protection** is required for connections from operating systems that support **Extended Protection**.</span></span> <span data-ttu-id="e4b4d-154">如果是不支援 **[擴充保護]** 之作業系統所做的連接，便會忽略 **[擴充保護]** 。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-154">**Extended Protection** is ignored for connections from operating systems that do not support **Extended Protection**.</span></span> <span data-ttu-id="e4b4d-155">如果未受保護的用戶端應用程式在受保護的用戶端作業系統上執行，則會拒絕來自該應用程式的連接。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-155">Connections from unprotected client applications that are running on protected client operating systems are rejected.</span></span> <span data-ttu-id="e4b4d-156">這個設定要比 **[關閉]** 安全，但不是最安全的設定。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-156">This setting is more secure than **Off**, but is not the most secure setting.</span></span> <span data-ttu-id="e4b4d-157">請在某些作業系統支援 **[擴充保護]** 但某些不支援的混合式環境中使用這個設定。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-157">Use this setting in mixed environments, where some operating systems support **Extended Protection** and some do not.</span></span>  
  
    -   <span data-ttu-id="e4b4d-158">當設定為 **[必要]** 時，只會接受來自受保護之作業系統上的受保護應用程式的連接。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-158">When set to **Required**, only connections from protected applications on protected operating systems are accepted.</span></span> <span data-ttu-id="e4b4d-159">這個設定最安全，但是不支援 **[擴充保護]** 之作業系統或應用程式的連接將無法連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-159">This setting is the most secure but connections from operating systems or applications that do not support **Extended Protection** will not be able to connect to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span>  
  
-   <span data-ttu-id="e4b4d-160">**接受的 NTLM SPN**</span><span class="sxs-lookup"><span data-stu-id="e4b4d-160">**Accepted NTLM SPNs**</span></span>  
  
     <span data-ttu-id="e4b4d-161">當一個以上的 SPN 知道伺服器時，便需要 **[接受的 NTLM SPN]** 變數。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-161">The **Accepted NTLM SPNs** variable is needed when a server is known by more than one SPN.</span></span> <span data-ttu-id="e4b4d-162">當用戶端嘗試使用伺服器不知道的有效 SPN 連接到伺服器時，服務繫結將會失敗。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-162">When a client attempts to connect to the server by using a valid SPN that the server does not know, service binding will fail.</span></span> <span data-ttu-id="e4b4d-163">若要避免這個問題，使用者可以使用 **[接受的 NTLM SPN]** 來指定代表伺服器的數個 SPN。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-163">To avoid this problem, users can specify several SPNs that represent the server by using **Accepted NTLM SPNs**.</span></span> <span data-ttu-id="e4b4d-164">**[接受的 NTLM SPN]** 是以分號分隔的一系列 SPN。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-164">**Accepted NTLM SPNs** is a series of SPNs separated my semicolons.</span></span> <span data-ttu-id="e4b4d-165">例如，若要允許 SPN **MSSQLSvc/ HostName1.Contoso.com** 和 **MSSQLSvc/ HostName2.Contoso.com**，請在 **[接受的 NTLM SPN]** 方塊中輸入 **MSSQLSvc/HostName1.Contoso.com;MSSQLSvc/HostName2.Contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-165">For example, to allow the SPNs **MSSQLSvc/ HostName1.Contoso.com** and **MSSQLSvc/ HostName2.Contoso.com**, type **MSSQLSvc/HostName1.Contoso.com;MSSQLSvc/HostName2.Contoso.com** in the **Accepted NTLM SPNs** box.</span></span> <span data-ttu-id="e4b4d-166">此變數的最大長度為 2,048 個字元。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-166">The variable has a maximum length of 2,048 characters.</span></span> <span data-ttu-id="e4b4d-167">**[接受的 NTLM SPN]** 位於 **組態管理員的** [MSSQLSERVER 的通訊協定屬性] ([進階] 索引標籤) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-167">**Accepted NTLM SPNs** is on the **Protocols for MSSQLSERVER Properties (Advanced Tab)** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.</span></span>  
  
## <a name="enabling-extended-protection-for-the-database-engine"></a><span data-ttu-id="e4b4d-168">啟用 Database Engine 的擴充保護</span><span class="sxs-lookup"><span data-stu-id="e4b4d-168">Enabling Extended Protection for the Database Engine</span></span>  
 <span data-ttu-id="e4b4d-169">若要使用 **[擴充保護]** ，伺服器和用戶端都必須擁有支援 **[擴充保護]** 的作業系統，而且必須在作業系統上啟用 **[擴充保護]** 。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-169">To use **Extended Protection**, both the server and the client must have an operating system on that supports **Extended Protection**, and **Extended Protection** must be enabled on the operating system.</span></span> <span data-ttu-id="e4b4d-170">如需有關如何針對作業系統啟用 **[擴充保護]** 的詳細資訊，請參閱 [驗證擴充保護](https://support.microsoft.com/kb/968389)。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-170">For more information about how to enable **Extended Protection** for the operating system, see [Extended Protection for Authentication](https://support.microsoft.com/kb/968389).</span></span>  
  
 <span data-ttu-id="e4b4d-171">從 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 開始 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就支援 [擴充保護]。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-171">[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supports **Extended Protection** beginning with [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].</span></span> <span data-ttu-id="e4b4d-172">某些舊版**的未來更新中將可以使用** [擴充保護] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-172">**Extended Protection** for some earlier versions of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] will be made available in future updates.</span></span> <span data-ttu-id="e4b4d-173">在伺服器電腦上啟用 **[擴充保護]** 之後，請使用下列步驟來啟用 **[擴充保護]** ：</span><span class="sxs-lookup"><span data-stu-id="e4b4d-173">After enabling **Extended Protection** on the server computer, use the following steps to enable **Extended Protection**:</span></span>  
  
1.  <span data-ttu-id="e4b4d-174">在 **[開始]** 功能表上，選擇 **[所有程式]** ，指向 **[Microsoft SQL Server]** ，然後按一下 **[SQL Server 組態管理員]** 。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-174">On the **Start** menu, choose **All Programs**, point to **Microsoft SQL Server** and then click **SQL Server Configuration Manager**.</span></span>  
  
2.  <span data-ttu-id="e4b4d-175">展開 [ **SQL Server 網路**設定]，然後在 [**通訊協定**] 上按一下滑鼠右鍵 *\<*InstanceName*>* ，然後按一下 [內容]。 **Properties**</span><span class="sxs-lookup"><span data-stu-id="e4b4d-175">Expand **SQL Server Network Configuration**, and then right-click **Protocols for** *\<*InstanceName*>*, and then click **Properties**.</span></span>  
  
3.  <span data-ttu-id="e4b4d-176">針對通道繫結和服務繫結，在 **[進階]** 索引標籤上將 **[擴充保護]** 設定為適當的設定值。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-176">For both channel binding and service binding, on the **Advanced** tab, set **Extended Protection** to the appropriate setting.</span></span>  
  
4.  <span data-ttu-id="e4b4d-177">當一個以上的 SPN 知道伺服器時，您也可以選擇在 **[進階]** 索引標籤上設定 **[接受的 NTLM SPN]** 欄位，如＜設定＞一節所述。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-177">Optionally, when a server is known by more than one SPN, on the **Advanced** tab configure the **Accepted NTLM SPNs** field as described in the "Settings" section.</span></span>  
  
5.  <span data-ttu-id="e4b4d-178">如果是通道繫結，請在 **[旗標]** 索引標籤上將 **[強制加密]** 設定為 **[開啟]** 。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-178">For channel binding, on the **Flags** tab, set **Force Encryption** to **On**.</span></span>  
  
6.  <span data-ttu-id="e4b4d-179">重新啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-179">Restart the [!INCLUDE[ssDE](../../includes/ssde-md.md)] service.</span></span>  
  
## <a name="configuring-other-sql-server-components"></a><span data-ttu-id="e4b4d-180">設定其他 SQL Server 元件</span><span class="sxs-lookup"><span data-stu-id="e4b4d-180">Configuring Other SQL Server Components</span></span>  
 <span data-ttu-id="e4b4d-181">如需如何設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的詳細資訊，請參閱 [含有 Reporting Services 的驗證擴充保護](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-181">For more information about how to configure [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], see [Extended Protection for Authentication with Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md).</span></span>  
  
 <span data-ttu-id="e4b4d-182">當使用 IIS 來透過 HTTP 或 HTTPs 連接存取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可以充分利用 IIS 所提供的擴充保護。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-182">When using IIS to access [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] data using an HTTP or HTTPs connection, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] can take advantage of Extended Protection provided by IIS.</span></span> <span data-ttu-id="e4b4d-183">如需有關如何設定 IIS 使用擴充保護的詳細資訊，請參閱 [在 IIS 7.5 中設定擴充保護](https://go.microsoft.com/fwlink/?LinkId=181105)。</span><span class="sxs-lookup"><span data-stu-id="e4b4d-183">For more information about how to configure IIS to use Extended Protection, see [Configure Extended Protection in IIS 7.5](https://go.microsoft.com/fwlink/?LinkId=181105).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e4b4d-184">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e4b4d-184">See Also</span></span>  
 <span data-ttu-id="e4b4d-185">[伺服器網路組態](server-network-configuration.md) </span><span class="sxs-lookup"><span data-stu-id="e4b4d-185">[Server Network Configuration](server-network-configuration.md) </span></span>  
 <span data-ttu-id="e4b4d-186">[用戶端網路組態](client-network-configuration.md) </span><span class="sxs-lookup"><span data-stu-id="e4b4d-186">[Client Network Configuration](client-network-configuration.md) </span></span>  
 <span data-ttu-id="e4b4d-187">[驗證擴充保護概觀](https://go.microsoft.com/fwlink/?LinkID=177943) </span><span class="sxs-lookup"><span data-stu-id="e4b4d-187">[Extended Protection for Authentication Overview](https://go.microsoft.com/fwlink/?LinkID=177943) </span></span>  
 [<span data-ttu-id="e4b4d-188">具有擴充保護的整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="e4b4d-188">Integrated Windows Authentication with Extended Protection</span></span>](https://go.microsoft.com/fwlink/?LinkId=179922)  
  
  