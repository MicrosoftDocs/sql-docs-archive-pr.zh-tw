---
title: 為自訂資料處理延伸模組指定連線 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- custom data processing extensions [Reporting Services]
- IDbConnection interface, connection strings
- impersonation [Reporting Services]
- IDbConnectionExtension interface, connection strings
- data sources [Reporting Services], security
- connection strings [Reporting Services]
- credentials [Reporting Services]
- authentication [Reporting Services]
- external data sources [Reporting Services]
- data processing extensions [Reporting Services], connections
ms.assetid: 2cddc9ea-0e28-4350-80ae-332412908e47
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4f870baf84f3412fea0a217f034b6d74e7b6cb93
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706249"
---
# <a name="specify-connections-for-custom-data-processing-extensions"></a><span data-ttu-id="46035-102">為自訂資料處理延伸模組指定連接</span><span class="sxs-lookup"><span data-stu-id="46035-102">Specify Connections for Custom Data Processing Extensions</span></span>
  <span data-ttu-id="46035-103">您可以在報表伺服器中建立或使用協力廠商自訂資料處理延伸模組，以便強化支援之資料來源的資料處理功能，或支援預設 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝未提供的其他資料來源類型。</span><span class="sxs-lookup"><span data-stu-id="46035-103">You can create or use third-party custom data processing extensions on a report server to enhance the data processing capability of supported data sources, or to support additional types of data sources that are not available in a default [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installation.</span></span> <span data-ttu-id="46035-104">不同的實作，處理連接的方式也不同。</span><span class="sxs-lookup"><span data-stu-id="46035-104">Connections are handled differently depending on the implementation.</span></span> <span data-ttu-id="46035-105">下列實作適用於資料處理延伸模組：</span><span class="sxs-lookup"><span data-stu-id="46035-105">The following implementations are available for data processing extensions:</span></span>  
  
-   <span data-ttu-id="46035-106">自訂 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者 (若要從 DB2.NET、Oracle、ODP.NET 或 Teradata 資料來源存取資料，您可以使用自訂 .NET 資料提供者)</span><span class="sxs-lookup"><span data-stu-id="46035-106">Custom [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] data providers (if you are accessing data from DB2.NET, Oracle, ODP.NET, or Teradata data sources, you might be using a custom .NET data provider)</span></span>  
  
-   <span data-ttu-id="46035-107">支援 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection></span><span class="sxs-lookup"><span data-stu-id="46035-107">Custom data processing extensions that support <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection></span></span>  
  
-   <span data-ttu-id="46035-108">支援 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension></span><span class="sxs-lookup"><span data-stu-id="46035-108">Custom data processing extensions that support <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension></span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="46035-109">請洽詢協力廠商提供者，找出自訂資料處理延伸模組的實作方式。</span><span class="sxs-lookup"><span data-stu-id="46035-109">Check with your third-party provider to find out how your custom data processing extension is implemented.</span></span>  
  
## <a name="impersonation-and-custom-data-processing-extensions"></a><span data-ttu-id="46035-110">模擬與自訂資料處理延伸模組</span><span class="sxs-lookup"><span data-stu-id="46035-110">Impersonation and Custom Data Processing Extensions</span></span>  
 <span data-ttu-id="46035-111">如果自訂資料處理延伸模組利用模擬連接到資料來源，您必須在 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> 或 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> 介面使用 Open 方法來提出要求。</span><span class="sxs-lookup"><span data-stu-id="46035-111">If your custom data processing extension connects to data sources using impersonation, you must use the Open method on either the <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> or <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> interfaces to make the request.</span></span> <span data-ttu-id="46035-112">此外，您也可以先儲存使用者識別物件 (System.Security.Principal.WindowsIdentity)，然後在其他資料處理延伸模組 API 中重複使用它。</span><span class="sxs-lookup"><span data-stu-id="46035-112">Alternately, you can store the user identity object (System.Security.Principal.WindowsIdentity) and then reuse it in the other data processing extension APIs.</span></span>  
  
 <span data-ttu-id="46035-113">在舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，所有自訂資料處理延伸模組都是在使用者模擬下呼叫。</span><span class="sxs-lookup"><span data-stu-id="46035-113">In previous releases of [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], all custom data processing extensions were called under user impersonation.</span></span> <span data-ttu-id="46035-114">在此版本中，只有 Open 方法是在模擬使用者時呼叫。</span><span class="sxs-lookup"><span data-stu-id="46035-114">In this release, only the Open method will be called while impersonating the user.</span></span> <span data-ttu-id="46035-115">如果您有需要整合式安全性的現有資料處理延伸模組，則必須修改程式碼來使用 Open 方法或儲存使用者識別物件。</span><span class="sxs-lookup"><span data-stu-id="46035-115">If you have an existing data processing extension that requires integrated security, you must modify your code to use the Open method or store the user identity object.</span></span>  
  
## <a name="connections-for-custom-net-framework-data-providers"></a><span data-ttu-id="46035-116">自訂 .NET Framework 資料提供者的連接</span><span class="sxs-lookup"><span data-stu-id="46035-116">Connections for Custom .NET Framework Data Providers</span></span>  
 <span data-ttu-id="46035-117">設定報表來使用特定資料來源時，您必須設定屬性來判斷資料來源類型、連接字串，以及用於存取資料來源的認證。</span><span class="sxs-lookup"><span data-stu-id="46035-117">When configuring a report to use a specific data source, you set properties that determine the data source type, connection string, and credentials that are used to access the data source.</span></span> <span data-ttu-id="46035-118">下表描述 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者支援的認證類型。</span><span class="sxs-lookup"><span data-stu-id="46035-118">The following table describes the credential types that are supported for [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] data providers.</span></span> <span data-ttu-id="46035-119">如需設定報表資料來源屬性的詳細資訊，請參閱 [指定報表資料來源的認證及連接資訊](specify-credential-and-connection-information-for-report-data-sources.md)。</span><span class="sxs-lookup"><span data-stu-id="46035-119">For more information about setting report data source properties, see [Specify Credential and Connection Information for Report Data Sources](specify-credential-and-connection-information-for-report-data-sources.md).</span></span>  
  
|<span data-ttu-id="46035-120">認證</span><span class="sxs-lookup"><span data-stu-id="46035-120">Credentials</span></span>|<span data-ttu-id="46035-121">連接</span><span class="sxs-lookup"><span data-stu-id="46035-121">Connections</span></span>|  
|-----------------|-----------------|  
|<span data-ttu-id="46035-122">整合式安全性</span><span class="sxs-lookup"><span data-stu-id="46035-122">Integrated security</span></span>|<span data-ttu-id="46035-123">如果您的資料提供者支援它，您可以使用 Windows 整合式安全性。</span><span class="sxs-lookup"><span data-stu-id="46035-123">If your data provider supports it, you can use Windows integrated security.</span></span> <span data-ttu-id="46035-124">您可以利用目前使用者的認證來傳送要求。</span><span class="sxs-lookup"><span data-stu-id="46035-124">The request is sent using the credentials of the current user.</span></span><br /><br /> <span data-ttu-id="46035-125">定義連接字串時，請務必包含指定整合式安全性的引數 (例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源的連接可能在連接字串中包含 `Integrated Security=SSPI`)。</span><span class="sxs-lookup"><span data-stu-id="46035-125">When defining the connection string, be sure to include arguments that specify integrated security (for example, a connection to a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] data source might include `Integrated Security=SSPI` on the connection string).</span></span>|  
|<span data-ttu-id="46035-126">Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="46035-126">Windows Authentication</span></span>|<span data-ttu-id="46035-127">如果您的資料提供者支援它，您可以使用 Windows 網域使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="46035-127">If your data provider supports it, you can use a Windows domain user account.</span></span> <span data-ttu-id="46035-128">在呼叫資料處理延伸模組之前，報表伺服器會模擬使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="46035-128">The report server impersonates the user account before the data processing extension is called.</span></span><br /><br /> <span data-ttu-id="46035-129">定義連接字串時，請務必包含指定整合式安全性的引數 (例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源的連接可能在連接字串中包含 `Integrated Security=SSPI`)。</span><span class="sxs-lookup"><span data-stu-id="46035-129">When defining the connection string, be sure to include arguments that specify integrated security (for example, a connection to a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] data source might include `Integrated Security=SSPI` on the connection string).</span></span>|  
|<span data-ttu-id="46035-130">資料庫認證</span><span class="sxs-lookup"><span data-stu-id="46035-130">Database credentials</span></span>|<span data-ttu-id="46035-131">透過自訂 .NET 資料提供者進行的連接不支援資料庫驗證。</span><span class="sxs-lookup"><span data-stu-id="46035-131">Database authentication is not supported for connections made through a custom .NET data provider.</span></span> <span data-ttu-id="46035-132">在所有情況下，報表伺服器的連接都會失敗。</span><span class="sxs-lookup"><span data-stu-id="46035-132">The report server will fail the connection in all cases.</span></span>|  
|<span data-ttu-id="46035-133">無認證</span><span class="sxs-lookup"><span data-stu-id="46035-133">No credentials</span></span>|<span data-ttu-id="46035-134">您可以搭配自訂 .NET 資料提供者使用 [無認證] 選項。</span><span class="sxs-lookup"><span data-stu-id="46035-134">You can use the no credentials option with custom .NET data providers.</span></span> <span data-ttu-id="46035-135">如果指定自動執行帳戶，連接字串會判斷所使用的認證。</span><span class="sxs-lookup"><span data-stu-id="46035-135">If the unattended execution account is specified, the connection string determines the credentials that are used.</span></span> <span data-ttu-id="46035-136">報表伺服器會模擬自動執行帳戶來進行連接。</span><span class="sxs-lookup"><span data-stu-id="46035-136">The report server impersonates the unattended execution account to make the connection.</span></span><br /><br /> <span data-ttu-id="46035-137">如果未定義自動執行帳戶，報表伺服器的連接會失敗。</span><span class="sxs-lookup"><span data-stu-id="46035-137">If the unattended execution account is not defined, the report server will fail the connection.</span></span> <span data-ttu-id="46035-138">如需定義帳戶的詳細資訊，請參閱 [設定自動執行帳戶 &#40;SSRS 組態管理員&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="46035-138">For more information about defining the account, see [Configure the Unattended Execution Account &#40;SSRS Configuration Manager&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).</span></span>|  
  
## <a name="connections-for-idbconnection"></a><span data-ttu-id="46035-139">IDbConnection 的連接</span><span class="sxs-lookup"><span data-stu-id="46035-139">Connections for IDbConnection</span></span>  
 <span data-ttu-id="46035-140">如果您使用僅支援 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection>的自訂資料處理延伸模組，您必須以下列方式指定連接：</span><span class="sxs-lookup"><span data-stu-id="46035-140">If you are using a custom data processing extension that only supports <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection>, you must specify the connection in the following way:</span></span>  
  
1.  <span data-ttu-id="46035-141">設定自動執行帳戶。</span><span class="sxs-lookup"><span data-stu-id="46035-141">Configure the unattended execution account.</span></span> <span data-ttu-id="46035-142">若要利用 `IDbConnection` 來進行連接，則必須設定此帳戶。</span><span class="sxs-lookup"><span data-stu-id="46035-142">Configuring this account is required for connections made using `IDbConnection`.</span></span> <span data-ttu-id="46035-143">報表伺服器在進行連接時會模擬該帳戶。</span><span class="sxs-lookup"><span data-stu-id="46035-143">The report server impersonates the account when making the connection.</span></span>  
  
2.  <span data-ttu-id="46035-144">在報表中設定資料來源屬性來使用 **[無認證]** 。</span><span class="sxs-lookup"><span data-stu-id="46035-144">Configure the data source properties on the report to use **No credentials**.</span></span>  
  
3.  <span data-ttu-id="46035-145">將用於連接到資料來源的認證放在連接字串中。</span><span class="sxs-lookup"><span data-stu-id="46035-145">Put the credentials used to connect to the data source in the connection string.</span></span>  
  
 <span data-ttu-id="46035-146">使用 `IDbConnection` 時，不支援下列認證類型：整合式安全性、Windows 使用者帳戶和資料庫認證。</span><span class="sxs-lookup"><span data-stu-id="46035-146">When using `IDbConnection`, the following credential types are not supported: integrated security, Windows user accounts, and database credentials.</span></span> <span data-ttu-id="46035-147">如果資料來源連接使用這些選項，報表伺服器中的連接就會失敗。</span><span class="sxs-lookup"><span data-stu-id="46035-147">If a data source connection uses these options, the connection will fail on the report server.</span></span>  
  
## <a name="connections-for-idbconnectionextension"></a><span data-ttu-id="46035-148">IDbConnectionExtension 的連接</span><span class="sxs-lookup"><span data-stu-id="46035-148">Connections for IDbConnectionExtension</span></span>  
 <span data-ttu-id="46035-149">如果您使用的是自訂資料處理延伸模組和支援 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>，您必須以下列方式指定連接：</span><span class="sxs-lookup"><span data-stu-id="46035-149">If you are using a custom data processing extension and supports, <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>, you can specify the connection in the following ways:</span></span>  
  
|<span data-ttu-id="46035-150">認證</span><span class="sxs-lookup"><span data-stu-id="46035-150">Credentials</span></span>|<span data-ttu-id="46035-151">連接</span><span class="sxs-lookup"><span data-stu-id="46035-151">Connections</span></span>|  
|-----------------|-----------------|  
|<span data-ttu-id="46035-152">整合式安全性</span><span class="sxs-lookup"><span data-stu-id="46035-152">Integrated security</span></span>|<span data-ttu-id="46035-153">如果您的資料提供者支援它，您可以搭配使用 `IDbConnectionExtension` 的自訂資料處理延伸模組來使用 Windows 整合式安全性。</span><span class="sxs-lookup"><span data-stu-id="46035-153">If your data provider supports it, you can use Windows integrated security with custom data processing extensions that use `IDbConnectionExtension`.</span></span><br /><br /> <span data-ttu-id="46035-154">定義連接字串時，請務必包含指定整合式安全性的引數 (例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源的連接可能在連接字串中包含 `Integrated Security=SSPI`)。</span><span class="sxs-lookup"><span data-stu-id="46035-154">When defining the connection string, be sure to include arguments that specify integrated security (for example, a connection to a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] data source might include `Integrated Security=SSPI` on the connection string).</span></span>|  
|<span data-ttu-id="46035-155">Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="46035-155">Windows Authentication</span></span>|<span data-ttu-id="46035-156">如果您的資料提供者支援它，您可以將 Windows 網域使用者帳戶用於使用 `IDbConnectionExtension` 的自訂資料處理延伸模組。</span><span class="sxs-lookup"><span data-stu-id="46035-156">If your data provider supports it, you can use a Windows domain user account for custom data processing extensions that use `IDbConnectionExtension`.</span></span><br /><br /> <span data-ttu-id="46035-157">在呼叫資料處理延伸模組之前，報表伺服器會模擬使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="46035-157">The report server impersonates the user account before the data processing extension is called.</span></span> <span data-ttu-id="46035-158">定義連接字串時，請務必包含指定整合式安全性的引數 (例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源的連接可能在連接字串中包含 `Integrated Security=SSPI`)。</span><span class="sxs-lookup"><span data-stu-id="46035-158">When defining the connection string, be sure to include arguments that specify integrated security (for example, a connection to a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] data source might include `Integrated Security=SSPI` on the connection string).</span></span>|  
|<span data-ttu-id="46035-159">資料庫認證</span><span class="sxs-lookup"><span data-stu-id="46035-159">Database credentials</span></span>|<span data-ttu-id="46035-160">您可以利用資料庫驗證來設定使用 `IDbConnectionExtension` 之自訂資料處理延伸模組的連接。</span><span class="sxs-lookup"><span data-stu-id="46035-160">You can use database authentication to configure connections for custom data processing extensions that use `IDbConnectionExtension`.</span></span>|  
|<span data-ttu-id="46035-161">無認證</span><span class="sxs-lookup"><span data-stu-id="46035-161">No credentials</span></span>|<span data-ttu-id="46035-162">如果指定自動執行帳戶，連接字串會判斷所使用的認證。</span><span class="sxs-lookup"><span data-stu-id="46035-162">If the unattended execution account is specified, the connection string determines the credentials that are used.</span></span><br /><br /> <span data-ttu-id="46035-163">如果未定義自動執行帳戶，報表伺服器的連接會失敗。</span><span class="sxs-lookup"><span data-stu-id="46035-163">If the unattended execution account is not defined, the report server will fail the connection.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="46035-164">另請參閱</span><span class="sxs-lookup"><span data-stu-id="46035-164">See Also</span></span>  
 <span data-ttu-id="46035-165">[設定自動執行帳戶 &#40;SSRS 組態管理員&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) </span><span class="sxs-lookup"><span data-stu-id="46035-165">[Configure the Unattended Execution Account &#40;SSRS Configuration Manager&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) </span></span>  
 <span data-ttu-id="46035-166">[指定報表資料來源的認證及連接資訊](specify-credential-and-connection-information-for-report-data-sources.md) </span><span class="sxs-lookup"><span data-stu-id="46035-166">[Specify Credential and Connection Information for Report Data Sources](specify-credential-and-connection-information-for-report-data-sources.md) </span></span>  
 <span data-ttu-id="46035-167">[Reporting Services 中的資料連線、資料來源及連接字串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) </span><span class="sxs-lookup"><span data-stu-id="46035-167">[Data Connections, Data Sources, and Connection Strings in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) </span></span>  
 <span data-ttu-id="46035-168">[實作資料處理延伸模組](../extensions/data-processing/implementing-a-data-processing-extension.md) </span><span class="sxs-lookup"><span data-stu-id="46035-168">[Implementing a Data Processing Extension](../extensions/data-processing/implementing-a-data-processing-extension.md) </span></span>  
 <span data-ttu-id="46035-169">[報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md) </span><span class="sxs-lookup"><span data-stu-id="46035-169">[Report Manager  &#40;SSRS Native Mode&#41;](../report-manager-ssrs-native-mode.md) </span></span>  
 <span data-ttu-id="46035-170">[建立、刪除或修改共用資料來源 &#40;報表管理員&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md) </span><span class="sxs-lookup"><span data-stu-id="46035-170">[Create, Delete, or Modify a Shared Data Source &#40;Report Manager&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md) </span></span>  
 [<span data-ttu-id="46035-171">設定報表的資料來源屬性 &#40;報表管理員&#41;</span><span class="sxs-lookup"><span data-stu-id="46035-171">Configure Data Source Properties for a Report  &#40;Report Manager&#41;</span></span>](configure-data-source-properties-for-a-report-report-manager.md)  
  
  