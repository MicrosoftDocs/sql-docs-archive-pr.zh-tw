---
title: MSReportServer_ConfigurationSetting 屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- MSReportServer_ConfigurationSetting Properties
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: e75fe1e5-197b-4c65-859b-370821cad003
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5bb3b57b34919748cb982a548b9640ae77ae7d9d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87702366"
---
# <a name="msreportserver_configurationsetting-properties"></a><span data-ttu-id="50265-102">MSReportServer_ConfigurationSetting 屬性</span><span class="sxs-lookup"><span data-stu-id="50265-102">MSReportServer_ConfigurationSetting Properties</span></span>
  <span data-ttu-id="50265-103">MSReportServer_ConfigurationSetting 類別代表報表伺服器執行個體的安裝與執行階段參數。</span><span class="sxs-lookup"><span data-stu-id="50265-103">The MSReportServer_ConfigurationSetting class represents the installation and runtime parameters of a report server instance.</span></span> <span data-ttu-id="50265-104">這些設定儲存在 RSReportServer.config 組態檔中。</span><span class="sxs-lookup"><span data-stu-id="50265-104">These settings are stored in the RSReportServer.config configuration file.</span></span>  
  
## <a name="public-properties"></a><span data-ttu-id="50265-105">公用屬性</span><span class="sxs-lookup"><span data-stu-id="50265-105">Public Properties</span></span>  
  
|||  
|-|-|  
|[<span data-ttu-id="50265-106">ConnectionPoolSize</span><span class="sxs-lookup"><span data-stu-id="50265-106">ConnectionPoolSize</span></span>](configurationsetting-property-connectionpoolsize.md)|<span data-ttu-id="50265-107">傳回報表伺服器用來與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體 (其主控報表伺服器資料庫) 進行通訊的連接集區大小。</span><span class="sxs-lookup"><span data-stu-id="50265-107">Returns the connection pool size used by the report server to communicate with the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] instance that hosts the report server database.</span></span> <span data-ttu-id="50265-108">唯讀。</span><span class="sxs-lookup"><span data-stu-id="50265-108">Read-only.</span></span>|  
|[<span data-ttu-id="50265-109">DatabaseLogonAccount</span><span class="sxs-lookup"><span data-stu-id="50265-109">DatabaseLogonAccount</span></span>](configurationsetting-property-databaselogonaccount.md)|<span data-ttu-id="50265-110">指定報表伺服器用來連線至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體 (其主控報表伺服器資料庫) 的登入帳戶。</span><span class="sxs-lookup"><span data-stu-id="50265-110">Specifies the logon account used by the report server to connect to the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] instance that hosts the report server database.</span></span> <span data-ttu-id="50265-111">唯讀。</span><span class="sxs-lookup"><span data-stu-id="50265-111">Read-only.</span></span>|  
|[<span data-ttu-id="50265-112">DatabaseLogonTimeout</span><span class="sxs-lookup"><span data-stu-id="50265-112">DatabaseLogonTimeout</span></span>](configurationsetting-property-databaselogontimeout.md)|<span data-ttu-id="50265-113">指定嘗試登入報表伺服器資料庫失敗之前等候的秒數。</span><span class="sxs-lookup"><span data-stu-id="50265-113">Specifies the number of seconds to wait before an attempt to log on to the report server database fails.</span></span> <span data-ttu-id="50265-114">唯讀。</span><span class="sxs-lookup"><span data-stu-id="50265-114">Read-only.</span></span>|  
|[<span data-ttu-id="50265-115">DatabaseLogonType</span><span class="sxs-lookup"><span data-stu-id="50265-115">DatabaseLogonType</span></span>](configurationsetting-property-databaselogontype.md)|<span data-ttu-id="50265-116">指定報表伺服器會使用 Windows 服務帳戶、Windows 使用者帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入來存取報表伺服器資料庫。</span><span class="sxs-lookup"><span data-stu-id="50265-116">Specifies whether the report server uses a Windows service account, a Windows user account, or a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login to access the report server database.</span></span> <span data-ttu-id="50265-117">唯讀。</span><span class="sxs-lookup"><span data-stu-id="50265-117">Read-only.</span></span>|  
|[<span data-ttu-id="50265-118">DatabaseName</span><span class="sxs-lookup"><span data-stu-id="50265-118">DatabaseName</span></span>](configurationsetting-property-databasename.md)|<span data-ttu-id="50265-119">指定主控報表伺服器資料庫之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="50265-119">Specifies the name of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance that hosts the report server database.</span></span>|  
|[<span data-ttu-id="50265-120">DatabaseQueryTimeout</span><span class="sxs-lookup"><span data-stu-id="50265-120">DatabaseQueryTimeout</span></span>](configurationsetting-property-databasequerytimeout.md)|<span data-ttu-id="50265-121">指定此命令失敗或逾時之前必須經過的秒數。報表伺服器會針對 SQL Server 目錄 (而非報表的資料來源) 進行處理序計時。</span><span class="sxs-lookup"><span data-stu-id="50265-121">Specifies the number of seconds that must elapse before the command fails or times out. The report server is timing the process against the SQL Server catalog, not a data source for the report.</span></span>|  
|[<span data-ttu-id="50265-122">DatabaseServerName</span><span class="sxs-lookup"><span data-stu-id="50265-122">DatabaseServerName</span></span>](configurationsetting-property-databaseservername.md)|<span data-ttu-id="50265-123">指定安裝報表伺服器資料庫之伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="50265-123">Specifies the name of the server on which the report server database is installed.</span></span>|  
|[<span data-ttu-id="50265-124">InstallationID 屬性</span><span class="sxs-lookup"><span data-stu-id="50265-124">InstallationID Property</span></span>](configurationsetting-property-installationid.md)|<span data-ttu-id="50265-125">傳回特定報表伺服器執行個體的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="50265-125">Returns a unique identifier for a specific report server instance.</span></span>|  
|[<span data-ttu-id="50265-126">InstanceName</span><span class="sxs-lookup"><span data-stu-id="50265-126">InstanceName</span></span>](configurationsetting-property-instancename.md)|<span data-ttu-id="50265-127">指定特定電腦上報表伺服器執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="50265-127">Specifies the name of a report server instance on a specific computer.</span></span>|  
|[<span data-ttu-id="50265-128">IsInitialized</span><span class="sxs-lookup"><span data-stu-id="50265-128">IsInitialized</span></span>](configurationsetting-property-isinitialized.md)|<span data-ttu-id="50265-129">指出報表伺服器執行個體是否已初始化。</span><span class="sxs-lookup"><span data-stu-id="50265-129">Indicates whether the report server instance is initialized.</span></span>  <span data-ttu-id="50265-130">唯讀。</span><span class="sxs-lookup"><span data-stu-id="50265-130">Read-only.</span></span>|  
|[<span data-ttu-id="50265-131">IsSharePointIntegrated</span><span class="sxs-lookup"><span data-stu-id="50265-131">IsSharePointIntegrated</span></span>](configurationsetting-property-issharepointintegrated.md)|<span data-ttu-id="50265-132">指出報表伺服器是否設定為 SharePoint 整合模式。</span><span class="sxs-lookup"><span data-stu-id="50265-132">Indicates whether the report server is configured for SharePoint integrated mode.</span></span>|  
|[<span data-ttu-id="50265-133">IsWebServiceEnabled</span><span class="sxs-lookup"><span data-stu-id="50265-133">IsWebServiceEnabled</span></span>](configurationsetting-property-iswebserviceenabled.md)|<span data-ttu-id="50265-134">指出報表伺服器 Web 服務是否已啟用。</span><span class="sxs-lookup"><span data-stu-id="50265-134">Indicates whether the Report Server Web service is enabled.</span></span> <span data-ttu-id="50265-135">唯讀。</span><span class="sxs-lookup"><span data-stu-id="50265-135">Read-only.</span></span>|  
|[<span data-ttu-id="50265-136">IsWindowsServiceEnabled</span><span class="sxs-lookup"><span data-stu-id="50265-136">IsWindowsServiceEnabled</span></span>](configurationsetting-property-iswindowsserviceenabled.md)|<span data-ttu-id="50265-137">指出是否已啟用報表伺服器 Windows 服務。</span><span class="sxs-lookup"><span data-stu-id="50265-137">Indicates whether the Report Server Windows service is enabled.</span></span> <span data-ttu-id="50265-138">唯讀。</span><span class="sxs-lookup"><span data-stu-id="50265-138">Read-only.</span></span>|  
|[<span data-ttu-id="50265-139">MachineAccountIdentity 屬性 &#40;WMI&#41;</span><span class="sxs-lookup"><span data-stu-id="50265-139">MachineAccountIdentity Property &#40;WMI&#41;</span></span>](configurationsetting-property-machineaccountidentity.md)|<span data-ttu-id="50265-140">取得安裝報表伺服器的電腦帳戶識別。</span><span class="sxs-lookup"><span data-stu-id="50265-140">Gets the machine account identity of the computer that the report server is installed on.</span></span>|  
|[<span data-ttu-id="50265-141">PathName</span><span class="sxs-lookup"><span data-stu-id="50265-141">PathName</span></span>](configurationsetting-property-pathname.md)|<span data-ttu-id="50265-142">指定報表伺服器執行個體的安裝路徑。</span><span class="sxs-lookup"><span data-stu-id="50265-142">Specifies the installation path to a report server instance.</span></span>|  
|[<span data-ttu-id="50265-143">SecureConnectionLevel</span><span class="sxs-lookup"><span data-stu-id="50265-143">SecureConnectionLevel</span></span>](configurationsetting-property-secureconnectionlevel.md)|<span data-ttu-id="50265-144">傳回 RSReportServer.config 檔案中指定的安全連接層級。</span><span class="sxs-lookup"><span data-stu-id="50265-144">Returns the secure connection level specified in the RSReportServer.config file.</span></span>|  
|[<span data-ttu-id="50265-145">SenderEmailAddress</span><span class="sxs-lookup"><span data-stu-id="50265-145">SenderEmailAddress</span></span>](configurationsetting-property-senderemailaddress.md)|<span data-ttu-id="50265-146">取得用以從報表伺服器傳送電子郵件的位址。</span><span class="sxs-lookup"><span data-stu-id="50265-146">Gets the address used to send e-mail from the report server.</span></span> <span data-ttu-id="50265-147">唯讀。</span><span class="sxs-lookup"><span data-stu-id="50265-147">Read-only.</span></span>|  
|[<span data-ttu-id="50265-148">SendUsingSMTPServer</span><span class="sxs-lookup"><span data-stu-id="50265-148">SendUsingSMTPServer</span></span>](configurationsetting-property-sendusingsmtpserver.md)|<span data-ttu-id="50265-149">指定電子郵件組態中的 SendUsing 屬性是否設定為 TRUE。</span><span class="sxs-lookup"><span data-stu-id="50265-149">Specifies whether the SendUsing property in the e-mail configuration is set to TRUE.</span></span>|  
|[<span data-ttu-id="50265-150">SMTPServer</span><span class="sxs-lookup"><span data-stu-id="50265-150">SMTPServer</span></span>](configurationsetting-property-smtpserver.md)|<span data-ttu-id="50265-151">從 RSReportServer.config 檔案中取得 SMTP 伺服器屬性。</span><span class="sxs-lookup"><span data-stu-id="50265-151">Gets the SMTP server property from the RSReportServer.config file.</span></span> <span data-ttu-id="50265-152">唯讀。</span><span class="sxs-lookup"><span data-stu-id="50265-152">Read-only.</span></span>|  
|[<span data-ttu-id="50265-153">UnattendedExecutionAccount</span><span class="sxs-lookup"><span data-stu-id="50265-153">UnattendedExecutionAccount</span></span>](configurationsetting-property-unattendedexecutionaccount.md)|<span data-ttu-id="50265-154">指定自動執行報表時報表伺服器所模擬的登入使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="50265-154">Specifies the login user account that the report server impersonates when running reports unattended.</span></span> <span data-ttu-id="50265-155">唯讀。</span><span class="sxs-lookup"><span data-stu-id="50265-155">Read-only.</span></span>|  
|[<span data-ttu-id="50265-156">版本</span><span class="sxs-lookup"><span data-stu-id="50265-156">Version</span></span>](configurationsetting-property-version.md)|<span data-ttu-id="50265-157">傳回報表伺服器的版本。</span><span class="sxs-lookup"><span data-stu-id="50265-157">Returns the version of the report server.</span></span>|  
|[<span data-ttu-id="50265-158">VirtualDirectoryReportManager 屬性 &#40;WMI MSReportServer_ConfigurationSetting&#41;</span><span class="sxs-lookup"><span data-stu-id="50265-158">VirtualDirectoryReportManager Property &#40;WMI MSReportServer_ConfigurationSetting&#41;</span></span>](configurationsetting-property-virtualdirectoryreportmanager.md)|<span data-ttu-id="50265-159">傳回報表管理員應用程式的虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="50265-159">Returns the virtual directory for the report manager application</span></span>|  
|[<span data-ttu-id="50265-160">VirtualDirectoryReportServer 屬性 &#40;WMI MSReportServer_ConfigurationSetting&#41;</span><span class="sxs-lookup"><span data-stu-id="50265-160">VirtualDirectoryReportServer Property &#40;WMI MSReportServer_ConfigurationSetting&#41;</span></span>](configurationsetting-property-virtualdirectoryreportserver.md)|<span data-ttu-id="50265-161">傳回報表伺服器 Web 服務應用程式的虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="50265-161">Returns the Virtual directory for the report server web service application.</span></span>|  
|[<span data-ttu-id="50265-162">WindowsServiceIdentityActual</span><span class="sxs-lookup"><span data-stu-id="50265-162">WindowsServiceIdentityActual</span></span>](configurationsetting-property-windowsserviceidentityactual.md)|<span data-ttu-id="50265-163">傳回實際執行報表伺服器 Windows 服務所使用的識別。</span><span class="sxs-lookup"><span data-stu-id="50265-163">Returns the identity that the Report Server Windows service is actually running under.</span></span> <span data-ttu-id="50265-164">唯讀。</span><span class="sxs-lookup"><span data-stu-id="50265-164">Read-only.</span></span>|  
|[<span data-ttu-id="50265-165">WindowsServiceIdentityConfigured</span><span class="sxs-lookup"><span data-stu-id="50265-165">WindowsServiceIdentityConfigured</span></span>](windowsserviceidentityconfigured-property.md)|<span data-ttu-id="50265-166">傳回上次設定報表伺服器 Windows 服務執行時所使用的識別。</span><span class="sxs-lookup"><span data-stu-id="50265-166">Returns the identity that the Report Server Windows service was last configured to run under.</span></span> <span data-ttu-id="50265-167">唯讀。</span><span class="sxs-lookup"><span data-stu-id="50265-167">Read-only.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="50265-168">另請參閱</span><span class="sxs-lookup"><span data-stu-id="50265-168">See Also</span></span>  
 [<span data-ttu-id="50265-169">MSReportServer_ConfigurationSetting 成員</span><span class="sxs-lookup"><span data-stu-id="50265-169">MSReportServer_ConfigurationSetting Members</span></span>](msreportserver-configurationsetting-members.md)  
  
  