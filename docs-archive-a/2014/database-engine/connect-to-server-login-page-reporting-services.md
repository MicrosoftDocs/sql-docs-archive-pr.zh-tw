---
title: 連線到伺服器 (登入頁面) Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttors.login.f1
helpviewer_keywords:
- Connect to Server dialog box, Reporting Services
ms.assetid: d312c740-19d7-4931-84a2-88b805ec8439
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 16c1a4f8b5560e2d49d9eb13ca3bdd5594461517
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707817"
---
# <a name="connect-to-server-login-page-reporting-services"></a><span data-ttu-id="5adf6-102">連線到伺服器 (登入頁面) Reporting Services</span><span class="sxs-lookup"><span data-stu-id="5adf6-102">Connect to Server (Login Page) Reporting Services</span></span>
  <span data-ttu-id="5adf6-103">連接到時，使用此索引標籤來查看或指定下列選項 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="5adf6-103">Use this tab to view or specify the following options when connecting to [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].</span></span>  
  
## <a name="options"></a><span data-ttu-id="5adf6-104">選項。</span><span class="sxs-lookup"><span data-stu-id="5adf6-104">Options</span></span>  
 <span data-ttu-id="5adf6-105">**伺服器類型**</span><span class="sxs-lookup"><span data-stu-id="5adf6-105">**Server type**</span></span>  
 <span data-ttu-id="5adf6-106">從 [物件總管] 註冊伺服器時，選取要連接的伺服器類型： [!INCLUDE[ssDE](../includes/ssde-md.md)]、Analysis Services、Reporting Services 或 Integration Services。</span><span class="sxs-lookup"><span data-stu-id="5adf6-106">When registering a server from Object Explorer, select the type of server to connect to: [!INCLUDE[ssDE](../includes/ssde-md.md)], Analysis Services, Reporting Services, or Integration Services.</span></span> <span data-ttu-id="5adf6-107">對話方塊的其他部分僅會顯示適用於所選取伺服器類型的選項。</span><span class="sxs-lookup"><span data-stu-id="5adf6-107">The rest of the dialog shows only the options that apply to the selected server type.</span></span> <span data-ttu-id="5adf6-108">從 [已註冊的伺服器] 註冊伺服器時，[伺服器類型]  方塊是唯讀的，且會與 [已註冊的伺服器] 元件中所顯示的伺服器類型相符。</span><span class="sxs-lookup"><span data-stu-id="5adf6-108">When registering a server from Registered Servers, the **Server type** box is read-only, and matches the type of server displayed in the Registered Servers component.</span></span> <span data-ttu-id="5adf6-109">若要註冊不同類型的伺服器，請先從 [已註冊的伺服器] 工具列中選取 [[!INCLUDE[ssDE](../includes/ssde-md.md)]]、[Analysis Services]、[Reporting Services] 或 [Integration Services]，再開始註冊新的伺服器。</span><span class="sxs-lookup"><span data-stu-id="5adf6-109">To register a different type of server, select [!INCLUDE[ssDE](../includes/ssde-md.md)], Analysis Services, Reporting Services, or Integration Services from the Registered Servers toolbar before starting to register a new server.</span></span>  
  
 <span data-ttu-id="5adf6-110">**伺服器名稱**</span><span class="sxs-lookup"><span data-stu-id="5adf6-110">**Server name**</span></span>  
 <span data-ttu-id="5adf6-111">您要連接之報表伺服器執行個體的伺服器模式會決定您必須輸入的值。</span><span class="sxs-lookup"><span data-stu-id="5adf6-111">The server mode of the report server instance you are connecting to determines the value you must enter.</span></span>  
  
 <span data-ttu-id="5adf6-112">若為以原生模式執行的報表伺服器，請指定要連接的報表伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="5adf6-112">For a report server that runs in native mode, specify the report server instance to connect to.</span></span> <span data-ttu-id="5adf6-113">如果您正使用預設執行個體，此伺服器名稱通常就是電腦的名稱。</span><span class="sxs-lookup"><span data-stu-id="5adf6-113">If you are using the default instance, the server name is typically the name of the computer.</span></span> <span data-ttu-id="5adf6-114">如果您安裝了已命名的實例，請使用下列格式將實例名稱附加到伺服器名稱： \<servername> \\<InstanceName \> 。</span><span class="sxs-lookup"><span data-stu-id="5adf6-114">If you installed a named instance, append the instance name to the server name in this format: \<servername>\\<InstanceName\>.</span></span> <span data-ttu-id="5adf6-115">Reporting Services 會使用反斜線字元來分隔執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="5adf6-115">Reporting Services uses the backslash character to delimit the instance name.</span></span>  
  
 <span data-ttu-id="5adf6-116">若為以 SharePoint 整合模式執行的報表伺服器，您就必須指定 SharePoint 網站。</span><span class="sxs-lookup"><span data-stu-id="5adf6-116">For a report server that runs in SharePoint integrated mode, you must specify a SharePoint site.</span></span> <span data-ttu-id="5adf6-117">您可以在網站集合中指定與 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]整合的任何網站。</span><span class="sxs-lookup"><span data-stu-id="5adf6-117">You can specify any site in a site collection that is integrated with [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].</span></span> <span data-ttu-id="5adf6-118">您所提供的 URL 必須包含 HTTP 或 HTTPS 前置詞。</span><span class="sxs-lookup"><span data-stu-id="5adf6-118">The URL that you provide must include the HTTP or HTTPS prefix.</span></span> <span data-ttu-id="5adf6-119">您必須擁有存取 SharePoint 網站的權限，才能在 Management Studio 中連接至此網站。</span><span class="sxs-lookup"><span data-stu-id="5adf6-119">You must have permission to access the SharePoint site in order to connect to it in Management Studio.</span></span> <span data-ttu-id="5adf6-120">您被指派的權限等級將會決定您可以檢視和管理的項目。</span><span class="sxs-lookup"><span data-stu-id="5adf6-120">The permission level you are assigned to will determine which items you can view and manage.</span></span> <span data-ttu-id="5adf6-121">如需詳細資訊，請參閱 [Connect to a Report Server in Management Studio](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md) (連線至 Management Studio 中的報表伺服器)。</span><span class="sxs-lookup"><span data-stu-id="5adf6-121">For more information, see [Connect to a Report Server in Management Studio](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md).</span></span>  
  
 <span data-ttu-id="5adf6-122">**驗證**</span><span class="sxs-lookup"><span data-stu-id="5adf6-122">**Authentication**</span></span>  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] <span data-ttu-id="5adf6-123">可設定為接受由您提供之自訂驗證延伸模組處理的 Windows 驗證要求或表單驗證要求。</span><span class="sxs-lookup"><span data-stu-id="5adf6-123">can be configured to accept Windows Authentication requests or Forms authentication requests that are handled by a custom authentication extension that you provide.</span></span> <span data-ttu-id="5adf6-124">連接到 Reporting Services 時，請選取下列其中一種驗證模式：</span><span class="sxs-lookup"><span data-stu-id="5adf6-124">Select from one of the following authentication modes when connecting to Reporting Services:</span></span>  
  
 <span data-ttu-id="5adf6-125">**Windows 驗證模式 (Windows 驗證)**</span><span class="sxs-lookup"><span data-stu-id="5adf6-125">**Windows Authentication Mode (Windows Authentication)**</span></span>  
 <span data-ttu-id="5adf6-126">使用您的 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 認證連接到報表伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="5adf6-126">Connect to the report server instance using your [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows credentials.</span></span>  
  
 <span data-ttu-id="5adf6-127">**基本驗證**</span><span class="sxs-lookup"><span data-stu-id="5adf6-127">**Basic Authentication**</span></span>  
 <span data-ttu-id="5adf6-128">如果您的 Reporting Services 安裝設定為使用基本驗證，請使用 [基本驗證]\*\*\*\* 來連接。</span><span class="sxs-lookup"><span data-stu-id="5adf6-128">Connect using **Basic Authentication** if your Reporting Services installation is configured to use Basic Authentication.</span></span>  
  
 <span data-ttu-id="5adf6-129">**表單驗證**</span><span class="sxs-lookup"><span data-stu-id="5adf6-129">**Forms Authentication**</span></span>  
 <span data-ttu-id="5adf6-130">如果您的 Reporting Services 安裝設定為使用自訂驗證延伸模組，請使用 [表單驗證]\*\*\*\* 來連接。</span><span class="sxs-lookup"><span data-stu-id="5adf6-130">Connect using **Forms Authentication** if your Reporting Services installation is configured to use a custom authentication extension.</span></span>  
  
 <span data-ttu-id="5adf6-131">**使用者名稱**</span><span class="sxs-lookup"><span data-stu-id="5adf6-131">**User Name**</span></span>  
 <span data-ttu-id="5adf6-132">請輸入連接將使用的登入名稱。</span><span class="sxs-lookup"><span data-stu-id="5adf6-132">Enter the login name to use for the connection.</span></span> <span data-ttu-id="5adf6-133">唯有選取 **[基本驗證]** 或 **[表單驗證]** 時，才能使用此選項。</span><span class="sxs-lookup"><span data-stu-id="5adf6-133">This option is only available if you have selected **Basic** or **Forms Authentication**.</span></span>  
  
 <span data-ttu-id="5adf6-134">**密碼**</span><span class="sxs-lookup"><span data-stu-id="5adf6-134">**Password**</span></span>  
 <span data-ttu-id="5adf6-135">請輸入使用者名稱的密碼。</span><span class="sxs-lookup"><span data-stu-id="5adf6-135">Enter the password for the user name.</span></span> <span data-ttu-id="5adf6-136">唯有選取 **[基本驗證]** 或 **[表單驗證]** 時，才能編輯此選項。</span><span class="sxs-lookup"><span data-stu-id="5adf6-136">This option is only editable if you have selected **Basic** or **Forms Authentication**.</span></span>  
  
 <span data-ttu-id="5adf6-137">**記住密碼**</span><span class="sxs-lookup"><span data-stu-id="5adf6-137">**Remember password**</span></span>  
 <span data-ttu-id="5adf6-138">請儲存您輸入的密碼。</span><span class="sxs-lookup"><span data-stu-id="5adf6-138">Store the password you have entered.</span></span> <span data-ttu-id="5adf6-139">您必須按一下 [選項]\*\*\*\* 才會顯示此選項，而且只有在選取使用 [基本]\*\*\*\* 或 [表單驗證]\*\*\*\* 進行連線時，才可編輯此選項。</span><span class="sxs-lookup"><span data-stu-id="5adf6-139">This option is only displayed if you click **Options**, and it is only editable if you have selected to connect using **Basic** or **Forms Authentication**.</span></span>  
  
 <span data-ttu-id="5adf6-140">**[連接]**</span><span class="sxs-lookup"><span data-stu-id="5adf6-140">**Connect**</span></span>  
 <span data-ttu-id="5adf6-141">連接到選取的伺服器。</span><span class="sxs-lookup"><span data-stu-id="5adf6-141">Connect to the selected server.</span></span>  
  
 <span data-ttu-id="5adf6-142">**選項**</span><span class="sxs-lookup"><span data-stu-id="5adf6-142">**Options**</span></span>  
 <span data-ttu-id="5adf6-143">顯示其他伺服器連接選項，例如記住密碼。</span><span class="sxs-lookup"><span data-stu-id="5adf6-143">Display additional server connection options, such as remembering the password.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="5adf6-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5adf6-144">See Also</span></span>  
 <span data-ttu-id="5adf6-145">[&#40;SSRS Configuration Manager 設定報表伺服器資料庫連接&#41;](../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md) </span><span class="sxs-lookup"><span data-stu-id="5adf6-145">[Configure a Report Server Database Connection  &#40;SSRS Configuration Manager&#41;](../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md) </span></span>  
 <span data-ttu-id="5adf6-146">[連接到 Management Studio 中的報表伺服器](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md) </span><span class="sxs-lookup"><span data-stu-id="5adf6-146">[Connect to a Report Server in Management Studio](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md) </span></span>  
 [<span data-ttu-id="5adf6-147">報表伺服器的驗證</span><span class="sxs-lookup"><span data-stu-id="5adf6-147">Authentication with the Report Server</span></span>](../reporting-services/security/authentication-with-the-report-server.md)  
  
  