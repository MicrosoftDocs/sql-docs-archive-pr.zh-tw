---
title: 登入 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server, logging in
- services [SQL Server], logging in
- TCP connection string
- connecting to the Database Engine
- logins [SQL Server], about logging in
- named pipe connection string
- log ins [SQL Server]
- shared memory connection string
- logging in [SQL Server]
- logins [SQL Server]
ms.assetid: 77158a9a-d638-4818-90a1-cb2eb57df514
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: dfe8aa5373c3aafe423f52c04b73c5b11d283c6a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687157"
---
# <a name="logging-in-to-sql-server"></a><span data-ttu-id="bdef0-102">登入 SQL Server</span><span class="sxs-lookup"><span data-stu-id="bdef0-102">Logging In to SQL Server</span></span>
  <span data-ttu-id="bdef0-103">您可以使用任何圖形化管理工具，或是從命令提示字元登入 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。</span><span class="sxs-lookup"><span data-stu-id="bdef0-103">You can log in to an instance of [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] by using any of the graphical administration tools or from a command prompt.</span></span>  
  
 <span data-ttu-id="bdef0-104">當您利用圖形化管理工具 (例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ) 登入 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]執行個體時，必要時會提示您輸入伺服器名稱、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和密碼。</span><span class="sxs-lookup"><span data-stu-id="bdef0-104">When you log in to an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] by using a graphical administration tool such as [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], you are prompted to supply the server name, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login, and a password, if necessary.</span></span> <span data-ttu-id="bdef0-105">若使用「Windows 驗證」登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則不需要在每次存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體時提供 SQL Server 登入。</span><span class="sxs-lookup"><span data-stu-id="bdef0-105">If you log in to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] using Windows Authentication, you do not have to provide a SQL Server login each time you access an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="bdef0-106">相反地， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會利用您的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶自動將您登入。</span><span class="sxs-lookup"><span data-stu-id="bdef0-106">Instead, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uses your [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows account to log you in automatically.</span></span> <span data-ttu-id="bdef0-107">如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是以混合模式驗證 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 驗證模式) 執行，且您選擇使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證」來登入，則必須提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和密碼。</span><span class="sxs-lookup"><span data-stu-id="bdef0-107">If [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is running in mixed mode authentication ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] and Windows Authentication Mode), and you choose to log in using [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentication, you must provide a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login and password.</span></span> <span data-ttu-id="bdef0-108">盡可能使用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="bdef0-108">When possible, use Windows Authentication.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="bdef0-109">安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時若使用區分大小寫的定序， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入也會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="bdef0-109">If you selected a case-sensitive collation when you installed [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], your [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login is also case sensitive.</span></span>  
  
## <a name="format-for-specifying-the-name-of-sql-server"></a><span data-ttu-id="bdef0-110">指定 SQL Server 名稱的格式</span><span class="sxs-lookup"><span data-stu-id="bdef0-110">Format for Specifying the Name of SQL Server</span></span>  
 <span data-ttu-id="bdef0-111">連接至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體時，必須指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="bdef0-111">When connecting to an instance of the [!INCLUDE[ssDE](../../includes/ssde-md.md)] you must specify the name of the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="bdef0-112">如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體是預設執行個體 (未命名的執行個體)，請指定已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦名稱，或電腦的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="bdef0-112">If the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is the default instance (an unnamed instance), then specify the name of the computer where [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is installed, or the IP address of the computer.</span></span> <span data-ttu-id="bdef0-113">如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體是具名執行個體 (例如 SQLEXPRESS)，請指定已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦名稱，或電腦的 IP 位址，並加入斜線和執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="bdef0-113">If the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is a named instance (such as SQLEXPRESS), then specify the name of the computer where [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is installed, or the IP address of the computer, and add a slash and the instance name.</span></span>  
  
 <span data-ttu-id="bdef0-114">下列範例連接至 APPHOST 電腦上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。</span><span class="sxs-lookup"><span data-stu-id="bdef0-114">The following examples connect to an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] running on a computer named APPHOST.</span></span> <span data-ttu-id="bdef0-115">指定具名執行個體時，範例會使用執行個體名稱 SQLEXPRESS。</span><span class="sxs-lookup"><span data-stu-id="bdef0-115">When specifying a named instance, the examples use an instance name SQLEXPRESS.</span></span>  
  
 <span data-ttu-id="bdef0-116">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bdef0-116">**Examples:**</span></span>  
  
|<span data-ttu-id="bdef0-117">執行個體類型</span><span class="sxs-lookup"><span data-stu-id="bdef0-117">Type of Instance</span></span>|<span data-ttu-id="bdef0-118">伺服器名稱的項目</span><span class="sxs-lookup"><span data-stu-id="bdef0-118">Entry for the server name</span></span>|  
|----------------------|-------------------------------|  
|<span data-ttu-id="bdef0-119">使用預設通訊協定連接至預設執行個體</span><span class="sxs-lookup"><span data-stu-id="bdef0-119">Connection to a default instance using the default protocol.</span></span> <span data-ttu-id="bdef0-120">(這是預設執行個體的建議項目)。</span><span class="sxs-lookup"><span data-stu-id="bdef0-120">(This is the recommended entry for a default instance.)</span></span>|<span data-ttu-id="bdef0-121">APPHOST</span><span class="sxs-lookup"><span data-stu-id="bdef0-121">APPHOST</span></span>|  
|<span data-ttu-id="bdef0-122">使用預設通訊協定連接至具名執行個體</span><span class="sxs-lookup"><span data-stu-id="bdef0-122">Connection to a named instance using the default protocol.</span></span> <span data-ttu-id="bdef0-123">(這是具名執行個體的建議項目)。</span><span class="sxs-lookup"><span data-stu-id="bdef0-123">(This is the recommended entry for a named instance.)</span></span>|<span data-ttu-id="bdef0-124">APPHOST\SQLEXPRESS</span><span class="sxs-lookup"><span data-stu-id="bdef0-124">APPHOST\SQLEXPRESS</span></span>|  
|<span data-ttu-id="bdef0-125">使用句號連接至同一部電腦上的預設執行個體，指出執行個體是在本機電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="bdef0-125">Connection to a default instance on the same computer using a period to indicate that the instance is running on the local computer.</span></span>|<span data-ttu-id="bdef0-126">。</span><span class="sxs-lookup"><span data-stu-id="bdef0-126">.</span></span>|  
|<span data-ttu-id="bdef0-127">使用句號連接至同一部電腦上的具名執行個體，指出執行個體是在本機電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="bdef0-127">Connection to a named instance on the same computer using a period to indicate that the instance is running on the local computer.</span></span>|<span data-ttu-id="bdef0-128">.\SQLEXPRESS</span><span class="sxs-lookup"><span data-stu-id="bdef0-128">.\SQLEXPRESS</span></span>|  
|<span data-ttu-id="bdef0-129">使用 localhost 連接至同一部電腦上的預設執行個體，指出執行個體是在本機電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="bdef0-129">Connection to a default instance on the same computer using localhost to indicate that the instance is running on the local computer.</span></span>|<span data-ttu-id="bdef0-130">localhost</span><span class="sxs-lookup"><span data-stu-id="bdef0-130">localhost</span></span>|  
|<span data-ttu-id="bdef0-131">使用 localhost 連接至同一部電腦上的具名執行個體，指出執行個體是在本機電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="bdef0-131">Connection to a named instance on the same computer using localhost to indicate that the instance is running on the local computer.</span></span>|<span data-ttu-id="bdef0-132">localhost\SQLEXPRESS</span><span class="sxs-lookup"><span data-stu-id="bdef0-132">localhost\SQLEXPRESS</span></span>|  
|<span data-ttu-id="bdef0-133">使用 (local) 連接至同一部電腦上的預設執行個體，指出執行個體是在本機電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="bdef0-133">Connection to a default instance on the same computer using (local) to indicate that the instance is running on the local computer.</span></span>|<span data-ttu-id="bdef0-134">(local)</span><span class="sxs-lookup"><span data-stu-id="bdef0-134">(local)</span></span>|  
|<span data-ttu-id="bdef0-135">使用 (local) 連接至同一部電腦上的具名執行個體，指出執行個體是在本機電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="bdef0-135">Connection to a named instance on the same computer using (local) to indicate that the instance is running on the local computer.</span></span>|<span data-ttu-id="bdef0-136">(local)\SQLEXPRESS</span><span class="sxs-lookup"><span data-stu-id="bdef0-136">(local)\SQLEXPRESS</span></span>|  
|<span data-ttu-id="bdef0-137">連接至同一部電腦上的預設執行個體，會強制進行共用記憶體連線。</span><span class="sxs-lookup"><span data-stu-id="bdef0-137">Connection to a default instance on the same computer forcing a shared memory connection.</span></span>|<span data-ttu-id="bdef0-138">lpc:APPHOST</span><span class="sxs-lookup"><span data-stu-id="bdef0-138">lpc:APPHOST</span></span>|  
|<span data-ttu-id="bdef0-139">連接至同一部電腦上的具名執行個體，會強制進行共用記憶體連接。</span><span class="sxs-lookup"><span data-stu-id="bdef0-139">Connection to a named instance on the same computer forcing a shared memory connection.</span></span>|<span data-ttu-id="bdef0-140">lpc:APPHOST\SQLEXPRESS</span><span class="sxs-lookup"><span data-stu-id="bdef0-140">lpc:APPHOST\SQLEXPRESS</span></span>|  
|<span data-ttu-id="bdef0-141">使用 IP 位址，連接至接聽 TCP 位址 192.168.17.28 的預設執行個體。</span><span class="sxs-lookup"><span data-stu-id="bdef0-141">Connection to a default instance listening on TCP address 192.168.17.28 using an IP address.</span></span>|<span data-ttu-id="bdef0-142">192.168.17.28</span><span class="sxs-lookup"><span data-stu-id="bdef0-142">192.168.17.28</span></span>|  
|<span data-ttu-id="bdef0-143">使用 IP 位址，連接至接聽 TCP 位址 192.168.17.28 的具名執行個體。</span><span class="sxs-lookup"><span data-stu-id="bdef0-143">Connection to a named instance listening on TCP address 192.168.17.28 using an IP address.</span></span>|<span data-ttu-id="bdef0-144">192.168.17.28\SQLEXPRESS</span><span class="sxs-lookup"><span data-stu-id="bdef0-144">192.168.17.28\SQLEXPRESS</span></span>|  
|<span data-ttu-id="bdef0-145">指定正在使用的通訊埠 (在此情況下，是 2828)，以連接至未接聽預設 TCP 通訊埠的預設執行個體</span><span class="sxs-lookup"><span data-stu-id="bdef0-145">Connection to a default instance that is not listening on the default TCP port, by specifying the port that is being used, in this case 2828.</span></span> <span data-ttu-id="bdef0-146">(如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 接聽預設通訊埠 (1433)，則不需要進行此作業)。</span><span class="sxs-lookup"><span data-stu-id="bdef0-146">(This is not necessary if the [!INCLUDE[ssDE](../../includes/ssde-md.md)] is listening on the default port (1433).)</span></span>|<span data-ttu-id="bdef0-147">APPHOST,2828</span><span class="sxs-lookup"><span data-stu-id="bdef0-147">APPHOST,2828</span></span>|  
|<span data-ttu-id="bdef0-148">連接至所指定 TCP 通訊埠 (在此情況下，是 2828) 的具名執行個體</span><span class="sxs-lookup"><span data-stu-id="bdef0-148">Connection to a named instance on a designated TCP port, in this case 2828.</span></span> <span data-ttu-id="bdef0-149">(如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務不是在主機電腦上執行，通常會需要進行此作業)。</span><span class="sxs-lookup"><span data-stu-id="bdef0-149">(This is often necessary if the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser service is not running on the host computer.)</span></span>|<span data-ttu-id="bdef0-150">APPHOST,2828</span><span class="sxs-lookup"><span data-stu-id="bdef0-150">APPHOST,2828</span></span>|  
|<span data-ttu-id="bdef0-151">指定正在使用的 IP 位址和 TCP 通訊埠 (在此情況下，是 2828)，以連接至未接聽預設 TCP 通訊埠的預設執行個體。</span><span class="sxs-lookup"><span data-stu-id="bdef0-151">Connection to a default instance that is not listening on the default TCP port, by specifying both the IP address and the TCP port that is being used, in this case 2828.</span></span>|<span data-ttu-id="bdef0-152">192.168.17.28,2828</span><span class="sxs-lookup"><span data-stu-id="bdef0-152">192.168.17.28,2828</span></span>|  
|<span data-ttu-id="bdef0-153">指定正在使用的 IP 位址和 TCP 通訊埠 (在此情況下，是 2828)，以連接至具名執行個體。</span><span class="sxs-lookup"><span data-stu-id="bdef0-153">Connection to a named instance by specifying both the IP address and the TCP port that is being used, in this case 2828.</span></span>|<span data-ttu-id="bdef0-154">192.168.17.28,2828</span><span class="sxs-lookup"><span data-stu-id="bdef0-154">192.168.17.28,2828</span></span>|  
|<span data-ttu-id="bdef0-155">依名稱連接至預設執行個體，強制進行 TCP 連接。</span><span class="sxs-lookup"><span data-stu-id="bdef0-155">Connecting to default instance by name, forcing a TCP connection.</span></span>|<span data-ttu-id="bdef0-156">tcp:APPHOST</span><span class="sxs-lookup"><span data-stu-id="bdef0-156">tcp:APPHOST</span></span>|  
|<span data-ttu-id="bdef0-157">依名稱連接至具名執行個體，強制進行 TCP 連接。</span><span class="sxs-lookup"><span data-stu-id="bdef0-157">Connecting to named instance by name, forcing a TCP connection.</span></span>|<span data-ttu-id="bdef0-158">tcp:APPHOST\SQLEXPRESS</span><span class="sxs-lookup"><span data-stu-id="bdef0-158">tcp:APPHOST\SQLEXPRESS</span></span>|  
|<span data-ttu-id="bdef0-159">指定具名管道名稱，以連接至預設執行個體。</span><span class="sxs-lookup"><span data-stu-id="bdef0-159">Connecting to a default instance by specifying a named pipe name.</span></span>|<span data-ttu-id="bdef0-160">\\\APPHOST\pipe\unit\app</span><span class="sxs-lookup"><span data-stu-id="bdef0-160">\\\APPHOST\pipe\unit\app</span></span>|  
|<span data-ttu-id="bdef0-161">指定具名管道名稱，以連接至具名執行個體。</span><span class="sxs-lookup"><span data-stu-id="bdef0-161">Connecting to a named instance by specifying a named pipe name.</span></span>|<span data-ttu-id="bdef0-162">\\\APPHOST\pipe\MSSQL$SQLEXPRESS\SQL\query</span><span class="sxs-lookup"><span data-stu-id="bdef0-162">\\\APPHOST\pipe\MSSQL$SQLEXPRESS\SQL\query</span></span>|  
|<span data-ttu-id="bdef0-163">依名稱連接至預設執行個體，強制進行具名管道連接。</span><span class="sxs-lookup"><span data-stu-id="bdef0-163">Connecting to default instance by name, forcing a named pipes connection.</span></span>|<span data-ttu-id="bdef0-164">np:APPHOST</span><span class="sxs-lookup"><span data-stu-id="bdef0-164">np:APPHOST</span></span>|  
|<span data-ttu-id="bdef0-165">依名稱連接至具名執行個體，強制進行具名管道連接。</span><span class="sxs-lookup"><span data-stu-id="bdef0-165">Connecting to named instance by name, forcing a named pipes connection.</span></span>|<span data-ttu-id="bdef0-166">np:APPHOST\SQLEXPRESS</span><span class="sxs-lookup"><span data-stu-id="bdef0-166">np:APPHOST\SQLEXPRESS</span></span>|  
  
## <a name="verifying-your-connection-protocol"></a><span data-ttu-id="bdef0-167">驗證您的連接通訊協定</span><span class="sxs-lookup"><span data-stu-id="bdef0-167">Verifying your Connection Protocol</span></span>  
 <span data-ttu-id="bdef0-168">連接至 [!INCLUDE[ssDE](../../includes/ssde-md.md)]時，下列查詢會傳回用於目前連接的通訊協定和驗證方法 (NTLM 或 Kerberos)，並指出是否加密連接。</span><span class="sxs-lookup"><span data-stu-id="bdef0-168">When connected to the [!INCLUDE[ssDE](../../includes/ssde-md.md)], the following query will return the protocol  used for the current connection, along with the authentication method (NTLM or Kerberos), and will indicate if the connection is encrypted.</span></span>  
  
```sql  
SELECT net_transport, auth_scheme, encrypt_option   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
```  
  
## <a name="related-tasks"></a><span data-ttu-id="bdef0-169">相關工作</span><span class="sxs-lookup"><span data-stu-id="bdef0-169">Related Tasks</span></span>  
 [<span data-ttu-id="bdef0-170">登入 SQL Server 的執行個體 &#40;命令提示字元&#41;</span><span class="sxs-lookup"><span data-stu-id="bdef0-170">Log In to an Instance of SQL Server &#40;Command Prompt&#41;</span></span>](log-in-to-an-instance-of-sql-server-command-prompt.md)  
  
 <span data-ttu-id="bdef0-171">下列資源可協助您疑難排解連接問題。</span><span class="sxs-lookup"><span data-stu-id="bdef0-171">The following resources can help you troubleshoot a connection problem.</span></span>  
  
-   [<span data-ttu-id="bdef0-172">如何疑難排解與 SQL Server Database Engine 的連接</span><span class="sxs-lookup"><span data-stu-id="bdef0-172">How to Troubleshoot Connecting to the SQL Server Database Engine</span></span>](https://social.technet.microsoft.com/wiki/contents/articles/how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)  
  
-   [<span data-ttu-id="bdef0-173">疑難排解 SQL 連接性問題的步驟</span><span class="sxs-lookup"><span data-stu-id="bdef0-173">Steps to troubleshoot SQL connectivity issues</span></span>](https://docs.microsoft.com/archive/blogs/sql_protocols/steps-to-troubleshoot-sql-connectivity-issues)  
  
## <a name="related-content"></a><span data-ttu-id="bdef0-174">相關內容</span><span class="sxs-lookup"><span data-stu-id="bdef0-174">Related Content</span></span>  
 [<span data-ttu-id="bdef0-175">選擇驗證模式</span><span class="sxs-lookup"><span data-stu-id="bdef0-175">Choose an Authentication Mode</span></span>](../../relational-databases/security/choose-an-authentication-mode.md)  
  
 [<span data-ttu-id="bdef0-176">使用 sqlcmd 公用程式</span><span class="sxs-lookup"><span data-stu-id="bdef0-176">Use the sqlcmd Utility</span></span>](../../relational-databases/scripting/sqlcmd-use-the-utility.md)  
  
 [<span data-ttu-id="bdef0-177">建立登入</span><span class="sxs-lookup"><span data-stu-id="bdef0-177">Creating a Login</span></span>](../../t-sql/lesson-2-1-creating-a-login.md)  
  
  