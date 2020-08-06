---
title: Web 應用程式需求 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9455d3cf-c1b7-4d48-8aff-7dc636ed5dc3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: fc24095019d19ebcb656a2cccf86621dd78b30b4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706573"
---
# <a name="web-application-requirements-master-data-services"></a><span data-ttu-id="f8425-102">Web 應用程式需求 (Master Data Services)</span><span class="sxs-lookup"><span data-stu-id="f8425-102">Web Application Requirements (Master Data Services)</span></span>
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] <span data-ttu-id="f8425-103">是由 Internet Information Services (IIS) 裝載的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f8425-103">is a web application hosted by Internet Information Services (IIS).</span></span> [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] <span data-ttu-id="f8425-104">僅適用於 Internet Explorer (IE) 7 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f8425-104">works only in Internet Explorer (IE) 7 or later.</span></span> <span data-ttu-id="f8425-105">不支援 IE 7 及更新版本、Microsoft Edge 和 Chrome。</span><span class="sxs-lookup"><span data-stu-id="f8425-105">IE 7 and earlier versions, Microsoft Edge and Chrome are not supported.</span></span>  
  
 <span data-ttu-id="f8425-106">使用 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 可以建立及設定 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f8425-106">Use [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] to create and configure the [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] web application.</span></span> [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] <span data-ttu-id="f8425-107">會在本機電腦上設定 IIS，因此最適合用於初始 Web 組態工作。</span><span class="sxs-lookup"><span data-stu-id="f8425-107">configures IIS on the local computer, so it is best for initial web configuration tasks.</span></span> <span data-ttu-id="f8425-108">例如在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 環境中設定單一 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式，或在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]的向外延展部署中設定第一個 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f8425-108">For example, configure a [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] environment with a single [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] web application, or configure the first web application in a scale-out deployment of [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].</span></span> <span data-ttu-id="f8425-109">您可以使用 IIS 工具執行更複雜的工作，例如在向外延展部署中設定多部 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f8425-109">Use IIS tools to perform more complex tasks, such as configuring multiple web servers in a scale-out deployment.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="f8425-110">安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 元件的任何電腦都必須獲得授權。</span><span class="sxs-lookup"><span data-stu-id="f8425-110">Any computer on which you install components of [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] must be licensed.</span></span> <span data-ttu-id="f8425-111">如需詳細資訊，請參閱使用者授權合約 (EULA)。</span><span class="sxs-lookup"><span data-stu-id="f8425-111">For more information, refer to the End User License Agreement (EULA).</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="f8425-112">需求</span><span class="sxs-lookup"><span data-stu-id="f8425-112">Requirements</span></span>  
  
### <a name="operating-system"></a><span data-ttu-id="f8425-113">作業系統</span><span class="sxs-lookup"><span data-stu-id="f8425-113">Operating System</span></span>  
 <span data-ttu-id="f8425-114">下列 Windows 作業系統包含了 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web 應用程式及 Web 服務所需的 Internet Information Services (IIS) 功能。</span><span class="sxs-lookup"><span data-stu-id="f8425-114">The following Windows operating systems include the Internet Information Services (IIS) functionality required for the [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] web application and web service.</span></span>  
  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] <span data-ttu-id="f8425-115">Developer (64 位元) x64</span><span class="sxs-lookup"><span data-stu-id="f8425-115">Developer (64-bit) x64</span></span>|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] <span data-ttu-id="f8425-116">Enterprise (64 位元) x64</span><span class="sxs-lookup"><span data-stu-id="f8425-116">Enterprise (64-bit) x64</span></span>|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] <span data-ttu-id="f8425-117">Business Intelligence (64 位元) x64</span><span class="sxs-lookup"><span data-stu-id="f8425-117">Business Intelligence (64-bit) x64</span></span>|  
|-------------------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------|  
|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] <span data-ttu-id="f8425-118">SP2</span><span class="sxs-lookup"><span data-stu-id="f8425-118">SP2</span></span><br /><br /> <span data-ttu-id="f8425-119">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="f8425-119">Windows Server 2008 R2 SP1</span></span><br /><br /> <span data-ttu-id="f8425-120">Windows 7 專業版、企業版與旗艦版</span><span class="sxs-lookup"><span data-stu-id="f8425-120">Windows 7 Professional, Enterprise, and Ultimate</span></span><br /><br /> <span data-ttu-id="f8425-121">Windows 8.0 專業版、企業版與旗艦版</span><span class="sxs-lookup"><span data-stu-id="f8425-121">Windows 8.0 Professional, Enterprise, and Ultimate</span></span>|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] <span data-ttu-id="f8425-122">SP2</span><span class="sxs-lookup"><span data-stu-id="f8425-122">SP2</span></span><br /><br /> <span data-ttu-id="f8425-123">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="f8425-123">Windows Server 2008 R2 SP1</span></span><br /><br /> <span data-ttu-id="f8425-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="f8425-124">Windows Server 2012</span></span>|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] <span data-ttu-id="f8425-125">SP2</span><span class="sxs-lookup"><span data-stu-id="f8425-125">SP2</span></span><br /><br /> <span data-ttu-id="f8425-126">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="f8425-126">Windows Server 2008 R2 SP1</span></span><br /><br /> <span data-ttu-id="f8425-127">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="f8425-127">Windows Server 2012</span></span>|  
  
 <span data-ttu-id="f8425-128">如需版本所支援之 Windows 作業系統的完整清單 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請參閱[安裝 SQL Server 2014 的硬體和軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。</span><span class="sxs-lookup"><span data-stu-id="f8425-128">For a full list of the Windows operating systems that are supported for your edition of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], see [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).</span></span>  
  
### <a name="microsoft-silverlight"></a><span data-ttu-id="f8425-129">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="f8425-129">Microsoft Silverlight</span></span>  
 <span data-ttu-id="f8425-130">若要在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式中工作，用戶端電腦必須安裝 Silverlight 5。</span><span class="sxs-lookup"><span data-stu-id="f8425-130">To work in the [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] web application, Silverlight 5 must be installed on the client computer.</span></span> <span data-ttu-id="f8425-131">如果您沒有必要的 Silverlight 版本，系統將會在您導覽至需要 Silverlight 的 Web 應用程式區域時提示安裝 Silverlight。</span><span class="sxs-lookup"><span data-stu-id="f8425-131">If you do not have the required version of Silverlight, you will be prompted to install it when you navigate to an area of the web application that requires it.</span></span> <span data-ttu-id="f8425-132">您可以從[這裡](https://go.microsoft.com/fwlink/?LinkId=243096)安裝 Silverlight 5。</span><span class="sxs-lookup"><span data-stu-id="f8425-132">You can install Silverlight 5 from [here](https://go.microsoft.com/fwlink/?LinkId=243096).</span></span>  
  
### <a name="role-and-role-services-windows-server-2008-or-windows-server-2008-r2-windows-7-operating-systems"></a><span data-ttu-id="f8425-133">角色和角色服務 (Windows Server 2008 或 Windows Server 2008 R2、Windows 7 作業系統)</span><span class="sxs-lookup"><span data-stu-id="f8425-133">Role and Role Services (Windows Server 2008 or Windows Server 2008 R2, Windows 7 operating systems)</span></span>  
 <span data-ttu-id="f8425-134">在 Windows Server 2008 R2 上，您可以使用 Microsoft Management Console (MMC) 中所提供的 **[伺服器管理員]**，以安裝 **[網頁伺服器 (IIS)]** 角色及下列必要的角色服務。</span><span class="sxs-lookup"><span data-stu-id="f8425-134">On Windows Server 2008 R2, you can use **Server Manager**, which is available in the Microsoft Management Console (MMC), to install the **Web Server (IIS)** role and the following required role services.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="f8425-135">在 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 和 Windows 7 作業系統上，使用 [控制台] 內的 **[程式和功能]** ，在 **[Windows 功能]** 對話方塊中啟用這些選項。</span><span class="sxs-lookup"><span data-stu-id="f8425-135">On [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] and Windows 7 operating systems, use **Programs and Features** in Control Panel to enable these options in the **Windows Features** dialog box.</span></span>  
  
||  
|-|  
|<span data-ttu-id="f8425-136">Web 伺服器</span><span class="sxs-lookup"><span data-stu-id="f8425-136">Web Server</span></span><br /><br /> <span data-ttu-id="f8425-137">一般 HTTP 功能</span><span class="sxs-lookup"><span data-stu-id="f8425-137">Common HTTP Features</span></span><br /><br /> <span data-ttu-id="f8425-138">靜態內容</span><span class="sxs-lookup"><span data-stu-id="f8425-138">Static Content</span></span><br /><br /> <span data-ttu-id="f8425-139">預設文件</span><span class="sxs-lookup"><span data-stu-id="f8425-139">Default Document</span></span><br /><br /> <span data-ttu-id="f8425-140">瀏覽目錄</span><span class="sxs-lookup"><span data-stu-id="f8425-140">Directory Browsing</span></span><br /><br /> <span data-ttu-id="f8425-141">HTTP 錯誤</span><span class="sxs-lookup"><span data-stu-id="f8425-141">HTTP Errors</span></span><br /><br /> <span data-ttu-id="f8425-142">應用程式開發</span><span class="sxs-lookup"><span data-stu-id="f8425-142">Application Development</span></span><br /><br /> <span data-ttu-id="f8425-143">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f8425-143">ASP.NET</span></span><br /><br /> <span data-ttu-id="f8425-144">.NET 擴充性</span><span class="sxs-lookup"><span data-stu-id="f8425-144">.NET Extensibility</span></span><br /><br /> <span data-ttu-id="f8425-145">ISAPI 擴充功能</span><span class="sxs-lookup"><span data-stu-id="f8425-145">ISAPI Extensions</span></span><br /><br /> <span data-ttu-id="f8425-146">ISAPI 篩選</span><span class="sxs-lookup"><span data-stu-id="f8425-146">ISAPI Filters</span></span><br /><br /> <span data-ttu-id="f8425-147">健康情況及診斷</span><span class="sxs-lookup"><span data-stu-id="f8425-147">Health and Diagnostics</span></span><br /><br /> <span data-ttu-id="f8425-148">HTTP 記錄</span><span class="sxs-lookup"><span data-stu-id="f8425-148">HTTP Logging</span></span><br /><br /> <span data-ttu-id="f8425-149">要求監視器</span><span class="sxs-lookup"><span data-stu-id="f8425-149">Request Monitor</span></span><br /><br /> <span data-ttu-id="f8425-150">安全性</span><span class="sxs-lookup"><span data-stu-id="f8425-150">Security</span></span><br /><br /> <span data-ttu-id="f8425-151">Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="f8425-151">Windows Authentication</span></span><br /><br /> <span data-ttu-id="f8425-152">要求篩選</span><span class="sxs-lookup"><span data-stu-id="f8425-152">Request Filtering</span></span><br /><br /> <span data-ttu-id="f8425-153">效能</span><span class="sxs-lookup"><span data-stu-id="f8425-153">Performance</span></span><br /><br /> <span data-ttu-id="f8425-154">靜態內容壓縮</span><span class="sxs-lookup"><span data-stu-id="f8425-154">Static Content Compression</span></span><br /><br /> <span data-ttu-id="f8425-155">管理工具</span><span class="sxs-lookup"><span data-stu-id="f8425-155">Management Tools</span></span><br /><br /> <span data-ttu-id="f8425-156">IIS 管理主控台</span><span class="sxs-lookup"><span data-stu-id="f8425-156">IIS Management Console</span></span>|  
  
### <a name="role-and-role-services-windows-server-2012-or-windows-8-operating-systems"></a><span data-ttu-id="f8425-157">角色和角色服務 (Windows Server 2012 或 Windows 8 作業系統)</span><span class="sxs-lookup"><span data-stu-id="f8425-157">Role and Role Services (Windows Server 2012 or Windows 8 operating systems)</span></span>  
 <span data-ttu-id="f8425-158">在 Windows Server 2012 上，您可以使用 Microsoft Management Console (MMC) 中所提供的 **[伺服器管理員]** 來安裝 **[網頁伺服器 (IIS)]** 角色及下列必要的角色服務。</span><span class="sxs-lookup"><span data-stu-id="f8425-158">On Windows Server 2012, you can use **Server Manager**, which is available in the Microsoft Management Console (MMC), to install the **Web Server (IIS)** role and the following required role services.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="f8425-159">在 Windows 8 作業系統上，請使用 [控制台] 內的 **[程式和功能]** ，在 **[Windows 功能]** 對話方塊中啟用這些選項。</span><span class="sxs-lookup"><span data-stu-id="f8425-159">On the Windows 8 operating system, use **Programs and Features** in Control Panel to enable these options in the **Windows Features** dialog box.</span></span>  
  
||  
|-|  
|<span data-ttu-id="f8425-160">Internet Information Services</span><span class="sxs-lookup"><span data-stu-id="f8425-160">Internet Information Services</span></span><br /><br /> <span data-ttu-id="f8425-161">Web 管理工具</span><span class="sxs-lookup"><span data-stu-id="f8425-161">Web Management Tools</span></span><br /><br /> <span data-ttu-id="f8425-162">IIS 管理主控台</span><span class="sxs-lookup"><span data-stu-id="f8425-162">IIS Management Console</span></span><br /><br /> <span data-ttu-id="f8425-163">World Wide Web 服務</span><span class="sxs-lookup"><span data-stu-id="f8425-163">World Wide Web Services</span></span><br /><br /> <span data-ttu-id="f8425-164">應用程式開發</span><span class="sxs-lookup"><span data-stu-id="f8425-164">Application Development</span></span><br /><br /> <span data-ttu-id="f8425-165">.NET 擴充性 3.5</span><span class="sxs-lookup"><span data-stu-id="f8425-165">.NET Extensibility 3.5</span></span><br /><br /> <span data-ttu-id="f8425-166">.NET 擴充性 4.5</span><span class="sxs-lookup"><span data-stu-id="f8425-166">.NET Extensibility 4.5</span></span><br /><br /> <span data-ttu-id="f8425-167">ASP.NET 3.5</span><span class="sxs-lookup"><span data-stu-id="f8425-167">ASP.NET 3.5</span></span><br /><br /> <span data-ttu-id="f8425-168">ASP.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="f8425-168">ASP.NET 4.5</span></span><br /><br /> <span data-ttu-id="f8425-169">ISAPI 擴充功能</span><span class="sxs-lookup"><span data-stu-id="f8425-169">ISAPI Extensions</span></span><br /><br /> <span data-ttu-id="f8425-170">ISAPI 篩選</span><span class="sxs-lookup"><span data-stu-id="f8425-170">ISAPI Filters</span></span><br /><br /> <span data-ttu-id="f8425-171">一般 HTTP 功能</span><span class="sxs-lookup"><span data-stu-id="f8425-171">Common HTTP Features</span></span><br /><br /> <span data-ttu-id="f8425-172">預設文件</span><span class="sxs-lookup"><span data-stu-id="f8425-172">Default Document</span></span><br /><br /> <span data-ttu-id="f8425-173">瀏覽目錄</span><span class="sxs-lookup"><span data-stu-id="f8425-173">Directory Browsing</span></span><br /><br /> <span data-ttu-id="f8425-174">HTTP 錯誤</span><span class="sxs-lookup"><span data-stu-id="f8425-174">HTTP Errors</span></span><br /><br /> <span data-ttu-id="f8425-175">靜態內容</span><span class="sxs-lookup"><span data-stu-id="f8425-175">Static Content</span></span><br /><br /> <span data-ttu-id="f8425-176">[注意：請勿安裝 WebDAV 發行]</span><span class="sxs-lookup"><span data-stu-id="f8425-176">[Note: Do not install WebDAV Publishing]</span></span><br /><br /> <span data-ttu-id="f8425-177">健康情況及診斷</span><span class="sxs-lookup"><span data-stu-id="f8425-177">Health and Diagnostics</span></span><br /><br /> <span data-ttu-id="f8425-178">HTTP 記錄</span><span class="sxs-lookup"><span data-stu-id="f8425-178">HTTP Logging</span></span><br /><br /> <span data-ttu-id="f8425-179">要求監視器</span><span class="sxs-lookup"><span data-stu-id="f8425-179">Request Monitor</span></span><br /><br /> <span data-ttu-id="f8425-180">效能</span><span class="sxs-lookup"><span data-stu-id="f8425-180">Performance</span></span><br /><br /> <span data-ttu-id="f8425-181">靜態內容壓縮</span><span class="sxs-lookup"><span data-stu-id="f8425-181">Static Content Compression</span></span><br /><br /> <span data-ttu-id="f8425-182">安全性</span><span class="sxs-lookup"><span data-stu-id="f8425-182">Security</span></span><br /><br /> <span data-ttu-id="f8425-183">要求篩選</span><span class="sxs-lookup"><span data-stu-id="f8425-183">Request Filtering</span></span><br /><br /> <span data-ttu-id="f8425-184">Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="f8425-184">Windows Authentication</span></span>|  
  
### <a name="features-windows-server-2008-or-windows-server-2008-r2-windows-7-operating-systems"></a><span data-ttu-id="f8425-185">功能 (Windows Server 2008 或 Windows Server 2008 R2、Windows 7 作業系統)</span><span class="sxs-lookup"><span data-stu-id="f8425-185">Features (Windows Server 2008 or Windows Server 2008 R2, Windows 7 operating systems)</span></span>  
 <span data-ttu-id="f8425-186">在 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 或 Windows Server 2008 R2 上，您可以使用 **[伺服器管理員]** 來安裝下列必要的功能。</span><span class="sxs-lookup"><span data-stu-id="f8425-186">On [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] or Windows Server 2008 R2, you can use **Server Manager** to install the following required features.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="f8425-187">在 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 和 Windows 7 作業系統上，使用 [控制台] 內的 **[程式和功能]** ，在 **[Windows 功能]** 對話方塊中啟用這些選項。</span><span class="sxs-lookup"><span data-stu-id="f8425-187">On [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] and Windows 7 operating systems, use **Programs and Features** in Control Panel to enable these options in the **Windows Features** dialog box.</span></span>  
  
||  
|-|  
|<span data-ttu-id="f8425-188">.NET Framework 3.0 功能</span><span class="sxs-lookup"><span data-stu-id="f8425-188">.NET Framework 3.0 Features</span></span><br /><br /> <span data-ttu-id="f8425-189">WCF 啟用</span><span class="sxs-lookup"><span data-stu-id="f8425-189">WCF Activation</span></span><br /><br /> <span data-ttu-id="f8425-190">HTTP 啟用</span><span class="sxs-lookup"><span data-stu-id="f8425-190">HTTP Activation</span></span><br /><br /> <span data-ttu-id="f8425-191">非 HTTP 啟用</span><span class="sxs-lookup"><span data-stu-id="f8425-191">Non-HTTP Activation</span></span><br /><br /> <span data-ttu-id="f8425-192">Windows 處理序啟用服務</span><span class="sxs-lookup"><span data-stu-id="f8425-192">Windows Process Activation Service</span></span><br /><br /> <span data-ttu-id="f8425-193">處理序模型</span><span class="sxs-lookup"><span data-stu-id="f8425-193">Process Model</span></span><br /><br /> <span data-ttu-id="f8425-194">.NET 環境</span><span class="sxs-lookup"><span data-stu-id="f8425-194">.NET Environment</span></span><br /><br /> <span data-ttu-id="f8425-195">設定 API</span><span class="sxs-lookup"><span data-stu-id="f8425-195">Configuration APIs</span></span>|  
  
### <a name="features-windows-server-2012-or-windows-8-operating-systems"></a><span data-ttu-id="f8425-196">功能 (Windows Server 2012 或 Windows 8 作業系統)</span><span class="sxs-lookup"><span data-stu-id="f8425-196">Features (Windows Server 2012 or Windows 8 operating systems)</span></span>  
 <span data-ttu-id="f8425-197">在 Windows Server 2012 上，您可以使用 **[伺服器管理員]** 來安裝下列必要的功能。</span><span class="sxs-lookup"><span data-stu-id="f8425-197">On Windows Server 2012, you can use **Server Manager** to install the following required features.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="f8425-198">在 Windows 8 作業系統上，請使用 [控制台] 內的 **[程式和功能]** ，在 **[Windows 功能]** 對話方塊中啟用這些選項。</span><span class="sxs-lookup"><span data-stu-id="f8425-198">On the Windows 8 operating system, use **Programs and Features** in Control Panel to enable these options in the **Windows Features** dialog box.</span></span>  
  
||  
|-|  
|<span data-ttu-id="f8425-199">.NET Framework 3.5 (包括 .NET 2.0 和 3.0)</span><span class="sxs-lookup"><span data-stu-id="f8425-199">.NET Framework 3.5 (includes .NET 2.0 and 3.0)</span></span><br /><br /> <span data-ttu-id="f8425-200">.NET Framework 4.5 進階服務</span><span class="sxs-lookup"><span data-stu-id="f8425-200">.NET Framework 4.5 Advanced Services</span></span><br /><br /> <span data-ttu-id="f8425-201">ASP.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="f8425-201">ASP.NET 4.5</span></span><br /><br /> <span data-ttu-id="f8425-202">WCF Services</span><span class="sxs-lookup"><span data-stu-id="f8425-202">WCF Services</span></span><br /><br /> <span data-ttu-id="f8425-203">HTTP 啟用 [注意：這是必要項。]</span><span class="sxs-lookup"><span data-stu-id="f8425-203">HTTP Activation [Note: This is required.]</span></span><br /><br /> <span data-ttu-id="f8425-204">TCP 連接埠共用</span><span class="sxs-lookup"><span data-stu-id="f8425-204">TCP Port Sharing</span></span><br /><br /> <span data-ttu-id="f8425-205">Windows 處理序啟用服務</span><span class="sxs-lookup"><span data-stu-id="f8425-205">Windows Process Activation Service</span></span><br /><br /> <span data-ttu-id="f8425-206">處理序模型</span><span class="sxs-lookup"><span data-stu-id="f8425-206">Process Model</span></span><br /><br /> <span data-ttu-id="f8425-207">.NET 環境</span><span class="sxs-lookup"><span data-stu-id="f8425-207">.NET Environment</span></span><br /><br /> <span data-ttu-id="f8425-208">設定 API</span><span class="sxs-lookup"><span data-stu-id="f8425-208">Configuration APIs</span></span>|  
  
### <a name="accounts-and-permissions"></a><span data-ttu-id="f8425-209">帳戶和權限</span><span class="sxs-lookup"><span data-stu-id="f8425-209">Accounts and Permissions</span></span>  
  
|<span data-ttu-id="f8425-210">類型</span><span class="sxs-lookup"><span data-stu-id="f8425-210">Type</span></span>|<span data-ttu-id="f8425-211">描述</span><span class="sxs-lookup"><span data-stu-id="f8425-211">Description</span></span>|  
|----------|-----------------|  
|<span data-ttu-id="f8425-212">Windows 帳戶</span><span class="sxs-lookup"><span data-stu-id="f8425-212">Windows account</span></span>|<span data-ttu-id="f8425-213">您必須使用具備設定 Windows 角色、角色服務與功能，以及在本機電腦之 IIS 中建立與管理應用程式集區、網站與 Web 應用程式的 Windows 帳戶登入 Web 伺服器電腦。</span><span class="sxs-lookup"><span data-stu-id="f8425-213">You must log on to the web server computer with a Windows account that has permission to configure Windows roles, role services, and features, and to create and manage application pools, web sites, and web applications in IIS on the local computer.</span></span>|  
|<span data-ttu-id="f8425-214">服務帳戶</span><span class="sxs-lookup"><span data-stu-id="f8425-214">Service account</span></span>|<span data-ttu-id="f8425-215">建立 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 中的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]Web 應用程式時，必須為應用程式執行所在之應用程式集區指定識別。</span><span class="sxs-lookup"><span data-stu-id="f8425-215">When you create the [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] web application in [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)], you must specify an identity for the application pool that the application runs in.</span></span> <span data-ttu-id="f8425-216">此帳戶可能與建立 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫時所指定的服務帳戶不同。</span><span class="sxs-lookup"><span data-stu-id="f8425-216">This account can be different from the service account that was specified when the [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] database was created.</span></span><br /><br /> <span data-ttu-id="f8425-217">這個識別必須是網域使用者帳戶，而且加入至 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫的 mds_exec 資料庫角色來進行資料庫存取。</span><span class="sxs-lookup"><span data-stu-id="f8425-217">This identity must be a domain user account, and it is added to the mds_exec database role in the [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] database for database access.</span></span> <span data-ttu-id="f8425-218">如需詳細資訊，請參閱[資料庫登入、使用者和角色 &#40;Master Data Services&#41;](../database-logins-users-and-roles-master-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="f8425-218">For more information, see [Database Logins, Users, and Roles &#40;Master Data Services&#41;](../database-logins-users-and-roles-master-data-services.md).</span></span> <span data-ttu-id="f8425-219">這個帳戶也會加入 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Windows 群組 **MDS_ServiceAccounts**，而這個群組在檔案系統中已被授與暫存編譯目錄 **MDSTempDir**的權限。</span><span class="sxs-lookup"><span data-stu-id="f8425-219">This account is also added to a [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Windows group, **MDS_ServiceAccounts**, which is granted permission to the temporary compilation directory, **MDSTempDir**, in the file system.</span></span> <span data-ttu-id="f8425-220">如需詳細資訊，請參閱[資料夾和檔案的權限 &#40;Master Data Services&#41;](../folder-and-file-permissions-master-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="f8425-220">For more information, see [Folder and File Permissions &#40;Master Data Services&#41;](../folder-and-file-permissions-master-data-services.md).</span></span><br /><br /> <span data-ttu-id="f8425-221">應用程式集區帳戶需要 VIEW SERVER STATE 權限，以避免發生伺服器錯誤。</span><span class="sxs-lookup"><span data-stu-id="f8425-221">The application pool account needs the VIEW SERVER STATE permission, to avoid server errors.</span></span> <span data-ttu-id="f8425-222">例如，MDS 驗證版本命令因伺服器錯誤而失敗。</span><span class="sxs-lookup"><span data-stu-id="f8425-222">For example, the MDS Validate Version command fails with a server error.</span></span> <span data-ttu-id="f8425-223">如需詳細資訊，請參閱 [MDS 驗證版本命令因 SQL Server 2012 和 SQL Server 2014 伺服器錯誤而失敗](https://go.microsoft.com/fwlink/p/?LinkId=526304)</span><span class="sxs-lookup"><span data-stu-id="f8425-223">For more information, see [MDS Validate Version command fails with a server error in SQL Server 2012 and SQL Server 2014](https://go.microsoft.com/fwlink/p/?LinkId=526304)</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="f8425-224">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f8425-224">See Also</span></span>  
 <span data-ttu-id="f8425-225">[安裝 Master Data Services](install-master-data-services.md) </span><span class="sxs-lookup"><span data-stu-id="f8425-225">[Install Master Data Services](install-master-data-services.md) </span></span>  
 <span data-ttu-id="f8425-226">[建立主資料管理員 Web 應用程式 &#40;Master Data Services&#41;](create-a-master-data-manager-web-application-master-data-services.md) </span><span class="sxs-lookup"><span data-stu-id="f8425-226">[Create a Master Data Manager Web Application &#40;Master Data Services&#41;](create-a-master-data-manager-web-application-master-data-services.md) </span></span>  
 [<span data-ttu-id="f8425-227">Web 組態頁面 &#40;Master Data Services 組態管理員&#41;</span><span class="sxs-lookup"><span data-stu-id="f8425-227">Web Configuration Page &#40;Master Data Services Configuration Manager&#41;</span></span>](../web-configuration-page-master-data-services-configuration-manager.md)  
  
  