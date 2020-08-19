---
title: PowerPivot 健全狀況規則-設定 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a01e63e6-97dc-43e5-ad12-ae6580afc606
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2c16db9ca1ba0e66402f5c157b44a38c45eb0852
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87703314"
---
# <a name="powerpivot-health-rules---configure"></a><span data-ttu-id="76768-102">PowerPivot 健全狀況規則 - 設定</span><span class="sxs-lookup"><span data-stu-id="76768-102">PowerPivot Health Rules - Configure</span></span>
  <span data-ttu-id="76768-103">PowerPivot for SharePoint 包含的 SharePoint 健全狀況規則可幫助您監控及修復伺服器可用性與組態問題。</span><span class="sxs-lookup"><span data-stu-id="76768-103">PowerPivot for SharePoint includes SharePoint health rules that help you monitor and remedy server availability and configuration problems.</span></span> <span data-ttu-id="76768-104">套用至 PowerPivot for SharePoint 的健全狀況規則會出現在 [檢閱規則定義] 頁面中。</span><span class="sxs-lookup"><span data-stu-id="76768-104">Health rules that apply to PowerPivot for SharePoint appear in the Review rule definitions page.</span></span>  
  
 <span data-ttu-id="76768-105">健全狀況規則可以早期偵測最終可能導致服務中斷的伺服器問題。</span><span class="sxs-lookup"><span data-stu-id="76768-105">Health rules provide early detection of server problems that could eventually result in service disruptions.</span></span> <span data-ttu-id="76768-106">PowerPivot for SharePoint 提供數個規則來協助您在影響使用者之前，先識別並修正問題。</span><span class="sxs-lookup"><span data-stu-id="76768-106">PowerPivot for SharePoint provides a number of rules to help you identify and fix problems before they impact your users.</span></span> <span data-ttu-id="76768-107">您可以自訂這些規則中的多個規則，以納入部署的唯一特性。</span><span class="sxs-lookup"><span data-stu-id="76768-107">You can customize many of these rules to fit the unique characteristics of your deployment.</span></span> <span data-ttu-id="76768-108">例如，如果您想要更多時間來處理磁碟空間的警告，可以將可用磁碟空間百分比從 5% 提高到 10%，讓您可以提前收到警告。</span><span class="sxs-lookup"><span data-stu-id="76768-108">For example, if you want more time to address warnings about disk space, you could raise the available disk space percentage from 5% to 10% so that you get the warning earlier.</span></span>  
  
 <span data-ttu-id="76768-109">可以自訂的規則是報告資源耗用或伺服器可用性的規則。</span><span class="sxs-lookup"><span data-stu-id="76768-109">Rules that can be customized are those that report on resource consumption or server availability.</span></span> <span data-ttu-id="76768-110">在這些領域中，自訂相當有協助，因為基礎系統功能在不同的伺服器和部署拓撲中，有相當大的不同。</span><span class="sxs-lookup"><span data-stu-id="76768-110">Customization is helpful in these areas because underlying system capacity varies widely across different servers and deployment topologies.</span></span> <span data-ttu-id="76768-111">相較之下，沒有任何自訂可用於識別伺服器組態或安全性問題的規則。</span><span class="sxs-lookup"><span data-stu-id="76768-111">In contrast, no customization is available for rules that identify server configuration or security issues.</span></span> <span data-ttu-id="76768-112">那些規則會跨所有安裝，統一套用。</span><span class="sxs-lookup"><span data-stu-id="76768-112">Those rules are intended to be applied uniformly across all installations.</span></span>  
  
||  
|-|  
|<span data-ttu-id="76768-113">**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010</span><span class="sxs-lookup"><span data-stu-id="76768-113">**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010</span></span>|  
  
 <span data-ttu-id="76768-114">**注意** ：健全狀況規則設定是針對 SQL Server Analysis Services 執行個體和 PowerPivot 服務應用程式分別設定。</span><span class="sxs-lookup"><span data-stu-id="76768-114">**Note:** Health rule settings are configured separately for the SQL Server Analysis Services instance and the PowerPivot service application.</span></span> <span data-ttu-id="76768-115">請使用本主題的指示來設定每一個服務的健全狀況規則。</span><span class="sxs-lookup"><span data-stu-id="76768-115">Use the instructions in this topic to configure health rules for each service.</span></span> <span data-ttu-id="76768-116">如果是 SharePoint 2013 部署， [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 只會使用服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="76768-116">For a SharePoint 2013 deployment, [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] only uses the service application.</span></span> <span data-ttu-id="76768-117">因此， [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 會針對不同版本的 SharePoint 安裝不同組的健全狀況規則。</span><span class="sxs-lookup"><span data-stu-id="76768-117">Therefore [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] installs different sets of health rules for different versions of SharePoint.</span></span> <span data-ttu-id="76768-118">請參閱[健全狀況規則參考 &#40;PowerPivot for SharePoint&#41;](health-rules-reference-power-pivot-for-sharepoint.md)主題中的「版本」資料行，或者您可以執行下列 Windows PowerShell 命令來查看已安裝的規則。</span><span class="sxs-lookup"><span data-stu-id="76768-118">See the "version" column in the topic [Health Rules Reference &#40;PowerPivot for SharePoint&#41;](health-rules-reference-power-pivot-for-sharepoint.md), or you can run the following Windows PowerShell command to see the installed rules.</span></span>  
  
```powershell
Get-SPHealthAnalysisRule | Select name, enabled, summary | Where {$_.summary -like "*power*"}  | Format-Table -Property * -AutoSize | Out-Default  
```  
  
 <span data-ttu-id="76768-119">**本主題內容：**</span><span class="sxs-lookup"><span data-stu-id="76768-119">**In this topic:**</span></span>  
  
 [<span data-ttu-id="76768-120">檢視 PowerPivot 健全狀況規則</span><span class="sxs-lookup"><span data-stu-id="76768-120">View PowerPivot health rules</span></span>](#bkmk_view)  
  
 [<span data-ttu-id="76768-121">設定用於評估伺服器穩定性的健全狀況規則 (SQL Server Analysis Services)</span><span class="sxs-lookup"><span data-stu-id="76768-121">Configure health rules used to evaluate server stability (SQL Server Analysis Services)</span></span>](#bkmk_HR_SSAS)  
  
 [<span data-ttu-id="76768-122">設定用於評估應用程式穩定性的健全狀況規則 (PowerPivot 服務應用程式)</span><span class="sxs-lookup"><span data-stu-id="76768-122">Configure health rules used to evaluate application stability (PowerPivot Service Application)</span></span>](#bkmk_evaluate_application_stability)  
  
## <a name="prerequisites"></a><span data-ttu-id="76768-123">必要條件</span><span class="sxs-lookup"><span data-stu-id="76768-123">Prerequisites</span></span>  
 <span data-ttu-id="76768-124">您必須是服務應用程式管理員，才能變更 Analysis Services 執行個體與 PowerPivot 服務應用程式的組態屬性。</span><span class="sxs-lookup"><span data-stu-id="76768-124">You must be a service application administrator to change configuration properties of the Analysis Services instance and of the PowerPivot service application.</span></span>  
  
##  <a name="view-powerpivot-health-rules"></a><a name="bkmk_view"></a><span data-ttu-id="76768-125">View PowerPivot 健全狀況規則</span><span class="sxs-lookup"><span data-stu-id="76768-125">View PowerPivot health rules</span></span>  
  
1.  <span data-ttu-id="76768-126">在 SharePoint 管理中心按一下 **[監視]**，然後在 **[狀況分析器]** 區段中按一下 **[檢閱規則定義]**。</span><span class="sxs-lookup"><span data-stu-id="76768-126">In SharePoint Central Administration, click **Monitoring**, and in the **Health Analyzer** section, click **Review rule definitions**.</span></span>  
  
2.  <span data-ttu-id="76768-127">在 [組態] 區段中，尋找前置詞為 **PowerPivot:** 的規則。</span><span class="sxs-lookup"><span data-stu-id="76768-127">In the Configuration section, find the rules that have the **PowerPivot:** prefix.</span></span> <span data-ttu-id="76768-128">擁有此前置詞的所有 PowerPivot 相關健全狀況規則可協助您區分 PowerPivot 健全狀況規則與內建的 SharePoint 規則。</span><span class="sxs-lookup"><span data-stu-id="76768-128">All PowerPivot-related health rules have this prefix to help you distinguish them from the built-in SharePoint rules.</span></span>  
  
 <span data-ttu-id="76768-129">偵測到問題時，這些規則將會出現在 **[檢閱問題與方案]** 頁面中。</span><span class="sxs-lookup"><span data-stu-id="76768-129">These rules will appear in the **Review problems and solutions** page when problems are detected.</span></span>  
  
 <span data-ttu-id="76768-130">如果您對於要立即調查的問題有疑問，可以手動執行規則檢查來找出是否有任何問題。</span><span class="sxs-lookup"><span data-stu-id="76768-130">If you suspect a problem that you want to investigate immediately, you can run a rule check manually to find out if there is an issue.</span></span>  
  
 <span data-ttu-id="76768-131">若要這樣做，請按一下此規則來開啟其規則定義，然後在功能區中按一下 **[立即執行]** 。</span><span class="sxs-lookup"><span data-stu-id="76768-131">To do this, click the rule to open its rule definition, and then click **Run Now** in the ribbon.</span></span> <span data-ttu-id="76768-132">按一下 **[關閉]** 回到 **[檢閱問題與方案]** 頁面來檢視報表。</span><span class="sxs-lookup"><span data-stu-id="76768-132">Click **Close** to go back to the **Review problems and solutions** page to view the report.</span></span> <span data-ttu-id="76768-133">如果此規則偵測到問題，則頁面上會報告警告或錯誤。</span><span class="sxs-lookup"><span data-stu-id="76768-133">If the rule detected a problem, a warning or error will be reported on the page.</span></span> <span data-ttu-id="76768-134">在某些情況下，可能需要幾分鐘的時間才會出現錯誤或警告。</span><span class="sxs-lookup"><span data-stu-id="76768-134">In some cases, it can take a few minutes before the error or warning will appear.</span></span>  
  
##  <a name="configure-health-rules-used-to-evaluate-server-stability-sql-server-analysis-services"></a><a name="bkmk_HR_SSAS"></a><span data-ttu-id="76768-135">設定用來評估伺服器穩定性的健全狀況規則 (SQL Server Analysis Services) </span><span class="sxs-lookup"><span data-stu-id="76768-135">Configure health rules used to evaluate server stability (SQL Server Analysis Services)</span></span>  
 <span data-ttu-id="76768-136">Analysis Services 執行個體包括可偵測系統層級 (快取用途的 CPU、記憶體與磁碟空間) 問題的健全狀況規則。</span><span class="sxs-lookup"><span data-stu-id="76768-136">The Analysis Services instance includes health rules that detect problems at the system level (CPU, memory, and disk space used for caching purposes).</span></span> <span data-ttu-id="76768-137">請使用下列指示來修改可觸發健全狀況規則的臨界值。</span><span class="sxs-lookup"><span data-stu-id="76768-137">Use the following instructions to modify thresholds that trigger specific health rules.</span></span>  
  
1.  <span data-ttu-id="76768-138">在 SharePoint 管理中心內，按一下 **[系統設定]** 區段中的 **[管理伺服器上的服務]**。</span><span class="sxs-lookup"><span data-stu-id="76768-138">In SharePoint Central Administration, in the **System Settings** section, click **Manage services on server**.</span></span>  
  
2.  <span data-ttu-id="76768-139">在頁面頂端，擁有 Analysis Services 執行個體的 SharePoint 伺服器陣列中選取伺服器 (在下圖中，伺服器名稱為 AW-SRV033)。</span><span class="sxs-lookup"><span data-stu-id="76768-139">At the top of the page, select the server in your SharePoint farm that has an instance of Analysis Services (in the following illustration, the server name is AW-SRV033).</span></span> <span data-ttu-id="76768-140">**[SQL Server Analysis Services]** 將會出現在服務清單中。</span><span class="sxs-lookup"><span data-stu-id="76768-140">**SQL Server Analysis Services** will appear in the list of services.</span></span>  
  
     <span data-ttu-id="76768-141">![管理伺服器上的服務頁面的螢幕擷取畫面](../media/ssas-centraladmin-servicesonserver.gif "管理伺服器上的服務頁面的螢幕擷取畫面")</span><span class="sxs-lookup"><span data-stu-id="76768-141">![Screenshot of Manage Services on Server page](../media/ssas-centraladmin-servicesonserver.gif "Screenshot of Manage Services on Server page")</span></span>  
  
3.  <span data-ttu-id="76768-142">按一下 **[SQL Server Analysis Services]**。</span><span class="sxs-lookup"><span data-stu-id="76768-142">Click **SQL Server Analysis Services**.</span></span>  
  
4.  <span data-ttu-id="76768-143">在 [健全狀況規則設定] 中的服務屬性頁上，修改下列設定：</span><span class="sxs-lookup"><span data-stu-id="76768-143">In the service property pages, in Health Rule Settings, modify the following settings:</span></span>  
  
     <span data-ttu-id="76768-144">CPU 資源配置不足 (預設為 80%)</span><span class="sxs-lookup"><span data-stu-id="76768-144">Insufficient CPU Resource Allocation (default is 80%)</span></span>  
     <span data-ttu-id="76768-145">如果 Analysis Services 伺服器處理序 (msmdsrv.exe) 使用的 CPU 資源在 4 個小時期間超過或等於 80% (如 [資料收集間隔] 設定所指定)，就會觸發這個健全狀況規則。</span><span class="sxs-lookup"><span data-stu-id="76768-145">This health rule is triggered if the CPU resources used by Analysis Services server process (msmdsrv.exe) remains at or above 80% over a 4 hour period (as specified through the Data Collection Interval setting).</span></span>  
  
     <span data-ttu-id="76768-146">此組態設定會對應到 **[檢閱問題與方案]** 頁面上的以下規則定義： **[PowerPivot: Analysis Services 的 CPU 資源不足，無法執行要求的作業]**。</span><span class="sxs-lookup"><span data-stu-id="76768-146">This configuration setting corresponds to the following rule definition on the **Review problems and solutions** page: **PowerPivot: Analysis Services does not have sufficient CPU resources to perform requested operations.**</span></span>  
  
     <span data-ttu-id="76768-147">系統的 CPU 資源不足 (預設為 90%)</span><span class="sxs-lookup"><span data-stu-id="76768-147">Insufficient CPU Resources on the System (default is 90%)</span></span>  
     <span data-ttu-id="76768-148">如果伺服器的 CPU 資源在 4 個小時的期間內大於或等於 90% (如 [資料收集間隔] 設定所指定)，就會觸發這個健全狀況規則。</span><span class="sxs-lookup"><span data-stu-id="76768-148">This health rule is triggered if CPU resources for the server remain at or above 90% over a 4 hour period (as specified through the Data Collection Interval setting).</span></span> <span data-ttu-id="76768-149">整體 CPU 使用量會以健全狀態為基礎之負載平衡演算法的一部分來衡量，以伺服器健全狀態量值的形式監視 CPU 使用量。</span><span class="sxs-lookup"><span data-stu-id="76768-149">Overall CPU utilization is measured as part of the health-based load balancing algorithm that monitors CPU usage as a measure of server health.</span></span>  
  
     <span data-ttu-id="76768-150">此組態設定會對應到 **[檢閱問題與方案]** 頁面上的以下規則定義： **[PowerPivot: 整體 CPU 使用率太高]**。</span><span class="sxs-lookup"><span data-stu-id="76768-150">This configuration setting corresponds to the following rule definition on the **Review problems and solutions** page: **PowerPivot: Overall CPU usage is too high.**</span></span>  
  
     <span data-ttu-id="76768-151">記憶體臨界值不足 (預設為 5%)</span><span class="sxs-lookup"><span data-stu-id="76768-151">Insufficient Memory Threshold (default is 5%)</span></span>  
     <span data-ttu-id="76768-152">在 SharePoint 應用程式伺服器上，SQL Server Analysis Services 執行個體應該一律擁有永遠是未使用的少量保留記憶體。</span><span class="sxs-lookup"><span data-stu-id="76768-152">On a SharePoint application server, a SQL Server Analysis Services instance should always have a small amount of memory in reserve that is always unused.</span></span> <span data-ttu-id="76768-153">由於伺服器對於大部分的作業都會繫結記憶體，如果此伺服器一直都沒有執行到上限，則運作狀況會最好。</span><span class="sxs-lookup"><span data-stu-id="76768-153">Because the server is memory-bound for the majority of its operations, the server runs best if it does not run all the way to the upper limit.</span></span> <span data-ttu-id="76768-154">5% 的未使用記憶體會計算為配置給 Analysis Services 之記憶體的百分比。</span><span class="sxs-lookup"><span data-stu-id="76768-154">The 5% of unused memory is calculated as a percentage of memory allocated to Analysis Services.</span></span> <span data-ttu-id="76768-155">例如，如果您的總記憶體為 200 GB，並將 80% 的記憶體 (或 160 GB) 配置給 Analysis Services，則 5% 的未使用記憶體為 160 GB 的 5% (或 8 GB)。</span><span class="sxs-lookup"><span data-stu-id="76768-155">For example, if you have 200 GB of total memory, and Analysis Services is allocated 80% of that (or 160 GB), then the 5% of unused memory is 5% of 160 GB (or 8 GB).</span></span>  
  
     <span data-ttu-id="76768-156">此組態設定會對應到 **[檢閱問題與方案]** 頁面上的以下規則定義： **[PowerPivot: Analysis Services 的記憶體不足，無法執行要求的作業]**。</span><span class="sxs-lookup"><span data-stu-id="76768-156">This configuration setting corresponds to the following rule definition on the **Review problems and solutions** page: **PowerPivot: Analysis Services does not have sufficient memory to perform requested operations.**</span></span>  
  
     <span data-ttu-id="76768-157">最大連接數目 (預設為 100)</span><span class="sxs-lookup"><span data-stu-id="76768-157">Maximum Number of Connections (default is 100)</span></span>  
     <span data-ttu-id="76768-158">如果 Analysis Services 執行個體的連接數目在 4 個小時的期間超過或等於 100 個連接 (如 [資料收集間隔] 設定所指定)，就會觸發這個健全狀況規則。</span><span class="sxs-lookup"><span data-stu-id="76768-158">This health rule is triggered if the number of connections to the Analysis Services instance remains at or above 100 connections over a 4 hour period (as specified through the Data Collection Interval setting).</span></span> <span data-ttu-id="76768-159">這個預設值為任意值 (而不是根據伺服器的硬體規格或使用者活動)，所以您可能會根據您的環境中的伺服器容量和使用者活動來提高或降低此值。</span><span class="sxs-lookup"><span data-stu-id="76768-159">This default value is arbitrary (it is not based on the hardware specifications of your server or on user activity) so you might raise or lower the value depending on the server capacity and user activity in your environment.</span></span>  
  
     <span data-ttu-id="76768-160">此組態設定會對應到 **[檢閱問題與方案]** 頁面上的以下規則定義： **[PowerPivot: 連接數目太多表示要部署更多的伺服器才能處理目前的負載]**。</span><span class="sxs-lookup"><span data-stu-id="76768-160">This configuration setting corresponds to the following rule definition on the **Review problems and solutions** page: **PowerPivot: The high number of connections indicates that more servers should be deployed to handle the current load.**</span></span>  
  
     <span data-ttu-id="76768-161">磁碟空間不足 (預設為 5%)</span><span class="sxs-lookup"><span data-stu-id="76768-161">Insufficient Disk Space (default is 5%)</span></span>  
     <span data-ttu-id="76768-162">每次要求資料庫時，都會使用磁碟空間來快取 PowerPivot 資料。</span><span class="sxs-lookup"><span data-stu-id="76768-162">Disk space is used to cache PowerPivot data each time a database is requested.</span></span> <span data-ttu-id="76768-163">當磁碟空間不足時，這個規則會讓您知道這個狀況。</span><span class="sxs-lookup"><span data-stu-id="76768-163">This rule lets you know when disk space is running low.</span></span> <span data-ttu-id="76768-164">根據預設，當備份資料夾所在之磁碟機上的磁碟空間低於 5% 時，便會觸發此健全狀況規則。</span><span class="sxs-lookup"><span data-stu-id="76768-164">By default, this health rule is triggered when disk space is less than 5% on the disk drive where the backup folder is located.</span></span> <span data-ttu-id="76768-165">如需磁片使用量的詳細資訊，請參閱[設定磁碟空間使用量 &#40;PowerPivot for SharePoint&#41;](configure-disk-space-usage-power-pivot-for-sharepoint.md)。</span><span class="sxs-lookup"><span data-stu-id="76768-165">For more information about disk usage, see [Configure Disk Space Usage &#40;PowerPivot for SharePoint&#41;](configure-disk-space-usage-power-pivot-for-sharepoint.md).</span></span>  
  
     <span data-ttu-id="76768-166">此組態設定會對應到 **[檢閱問題與方案]** 頁面上的以下規則定義： **[PowerPivot: PowerPivot 資料快取所在之磁碟機上的磁碟空間不足]**。</span><span class="sxs-lookup"><span data-stu-id="76768-166">This configuration setting corresponds to the following rule definition on the **Review problems and solutions** page: **PowerPivot: Disk space is running low on the drive where PowerPivot data is cached.**</span></span>  
  
     <span data-ttu-id="76768-167">資料收集間隔 (小時)</span><span class="sxs-lookup"><span data-stu-id="76768-167">Data Collection Interval (in hours)</span></span>  
     <span data-ttu-id="76768-168">您可以指定資料收集期間，該期間用來計算觸發健全狀況規則所使用的數字。</span><span class="sxs-lookup"><span data-stu-id="76768-168">You can specify the data collection period used for calculating the numbers used for triggering health rules.</span></span> <span data-ttu-id="76768-169">雖然系統會持續受到監控，但是用來觸發健全狀況規則警告的臨界值會使用一段預先定義之間隔內所產生的資料來計算。</span><span class="sxs-lookup"><span data-stu-id="76768-169">Although the system is monitored constantly, the thresholds used to trigger health rule warnings are calculated using data that was generated over a predefined interval.</span></span> <span data-ttu-id="76768-170">預設間隔是 4 小時。</span><span class="sxs-lookup"><span data-stu-id="76768-170">The default interval is 4 hours.</span></span> <span data-ttu-id="76768-171">伺服器會擷取過去 4 小時所收集的系統和使用量資料，以評估使用者連接數目、磁碟空間使用量以及 CPU 和記憶體使用率。</span><span class="sxs-lookup"><span data-stu-id="76768-171">The server retrieves system and usage data collected over the previous 4 hours to evaluate the number of user connections, disk space usage, and CPU and memory utilization rates.</span></span>  
  
##  <a name="configure-health-rules-used-to-evaluate-application-stability-powerpivot-service-application"></a><a name="bkmk_evaluate_application_stability"></a><span data-ttu-id="76768-172">設定用於評估應用程式穩定性的健全狀況規則 (PowerPivot 服務應用程式) </span><span class="sxs-lookup"><span data-stu-id="76768-172">Configure health rules used to evaluate application stability (PowerPivot Service Application)</span></span>  
  
1.  <span data-ttu-id="76768-173">在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]** 。</span><span class="sxs-lookup"><span data-stu-id="76768-173">In Central Administration, in Application Management, click **Manage service applications**.</span></span>  
  
2.  <span data-ttu-id="76768-174">在 [服務應用程式] 頁面中，按一下 **[預設的 PowerPivot 服務應用程式]**。</span><span class="sxs-lookup"><span data-stu-id="76768-174">In the Service Applications page, click **Default PowerPivot Service Application**.</span></span>  
  
     <span data-ttu-id="76768-175">![ManageService 應用程式頁面的螢幕擷取畫面](../media/ssas-centraladmin-app.gif "ManageService 應用程式頁面的螢幕擷取畫面")</span><span class="sxs-lookup"><span data-stu-id="76768-175">![Screenshot of ManageService Application page](../media/ssas-centraladmin-app.gif "Screenshot of ManageService Application page")</span></span>  
  
3.  <span data-ttu-id="76768-176">隨即出現 PowerPivot 管理儀表板。</span><span class="sxs-lookup"><span data-stu-id="76768-176">The PowerPivot Management Dashboard appears.</span></span> <span data-ttu-id="76768-177">在 **[動作]** 清單中，按一下 **[設定服務應用程式設定]** ，以開啟服務應用程式設定頁面。</span><span class="sxs-lookup"><span data-stu-id="76768-177">Click the **Configure service application settings** in the **Actions** list to open the service application settings page.</span></span>  
  
     <span data-ttu-id="76768-178">![儀表板的螢幕擷取畫面，焦點在動作清單上](../media/ssas-centraladmin-actionslist.gif "儀表板的螢幕擷取畫面，焦點在動作清單上")</span><span class="sxs-lookup"><span data-stu-id="76768-178">![Screenshot of dashboard, focus on Actions list](../media/ssas-centraladmin-actionslist.gif "Screenshot of dashboard, focus on Actions list")</span></span>  
  
4.  <span data-ttu-id="76768-179">在 [健全狀況規則設定] 中，修改下列設定：</span><span class="sxs-lookup"><span data-stu-id="76768-179">In Health Rule Settings, modify the following settings:</span></span>  
  
     <span data-ttu-id="76768-180">連接負載比率 (預設為 20%)</span><span class="sxs-lookup"><span data-stu-id="76768-180">Load to Connection Ratio (default is 20%)</span></span>  
     <span data-ttu-id="76768-181">如果載入事件數目相對於連接事件數目而言較高，則會觸發這個健全狀況規則，發出伺服器可能卸載資料庫太快的訊號，或減少快取設定太極端的訊號。</span><span class="sxs-lookup"><span data-stu-id="76768-181">This health rule is triggered if the number of load events is high relative to the number of connection events, signaling that the server might be unloading databases too quickly, or that cache reduction settings are too aggressive.</span></span>  
  
     <span data-ttu-id="76768-182">此組態設定會對應到 **[檢閱問題與方案]** 頁面上的以下規則定義： **[PowerPivot: 連接的載入事件的比率過高]**。</span><span class="sxs-lookup"><span data-stu-id="76768-182">This configuration setting corresponds to the following rule definition on the **Review problems and solutions** page: **PowerPivot: The ratio of load events to connections is too high.**</span></span>  
  
     <span data-ttu-id="76768-183">資料收集間隔 (預設為 4 小時)</span><span class="sxs-lookup"><span data-stu-id="76768-183">Data Collection Interval (default is 4 hours)</span></span>  
     <span data-ttu-id="76768-184">您可以指定資料收集期間，該期間用來計算觸發健全狀況規則所使用的數字。</span><span class="sxs-lookup"><span data-stu-id="76768-184">You can specify the data collection period used for calculating the numbers used for triggering health rules.</span></span> <span data-ttu-id="76768-185">雖然系統會持續受到監控，但是用來觸發健全狀況規則警告的臨界值會使用一段預先定義之間隔內所產生的資料來計算。</span><span class="sxs-lookup"><span data-stu-id="76768-185">Although the system is monitored constantly, the thresholds used to trigger health rule warnings are calculated using data that was generated over a predefined interval.</span></span> <span data-ttu-id="76768-186">預設間隔是 4 小時。</span><span class="sxs-lookup"><span data-stu-id="76768-186">The default interval is 4 hours.</span></span> <span data-ttu-id="76768-187">伺服器會擷取過去 4 小時所收集的系統和使用量資料，以評估收集負載比率。</span><span class="sxs-lookup"><span data-stu-id="76768-187">The server retrieves system and usage data collected over the previous 4 hours to evaluate the load to collection ratio.</span></span>  
  
     <span data-ttu-id="76768-188">檢查 PowerPivot Management Dashboard.xlsx 檔案的更新 (預設為 5 天)</span><span class="sxs-lookup"><span data-stu-id="76768-188">Check for Updates to PowerPivot Management Dashboard.xlsx (default is 5 days)</span></span>  
     <span data-ttu-id="76768-189">PowerPivot Management Dashboard.xlsx 檔案是 PowerPivot 管理儀表板中的報表所使用的資料來源。</span><span class="sxs-lookup"><span data-stu-id="76768-189">The PowerPivot Management Dashboard.xlsx file is a data source used by reports in PowerPivot Management Dashboard.</span></span> <span data-ttu-id="76768-190">在預設伺服器組態中，此 .xlsx 檔每天都會重新整理 (使用 SharePoint 和 PowerPivot 系統服務所收集的使用量資料)。</span><span class="sxs-lookup"><span data-stu-id="76768-190">In a default server configuration, the .xlsx file is refreshed daily, using usage data collected by SharePoint and the PowerPivot System Service.</span></span> <span data-ttu-id="76768-191">萬一未更新此檔案，健全狀況規則會將它報告為問題。</span><span class="sxs-lookup"><span data-stu-id="76768-191">In event the file is not updated, a health rule reports it as a problem.</span></span> <span data-ttu-id="76768-192">根據預設，如果此檔案的時間戳記長達 5 天都未變更，則會觸發此規則。</span><span class="sxs-lookup"><span data-stu-id="76768-192">By default, the rule is triggered if the timestamp of the file has not changed for 5 days.</span></span>  
  
     <span data-ttu-id="76768-193">如需使用方式資料收集的詳細資訊，請參閱[設定 &#40;PowerPivot for SharePoint 的使用量資料收集](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)。</span><span class="sxs-lookup"><span data-stu-id="76768-193">For more information about usage data collection, see [Configure Usage Data Collection for &#40;PowerPivot for SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).</span></span>  
  
     <span data-ttu-id="76768-194">此組態設定會對應到 **[檢閱問題與方案]** 頁面上的以下規則定義： **[PowerPivot: 使用量資料並未以預期的頻率更新]**。</span><span class="sxs-lookup"><span data-stu-id="76768-194">This configuration setting corresponds to the following rule definition on the **Review problems and solutions** page: **PowerPivot: Usage data is not getting updated at the expected frequency.**</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="76768-195">另請參閱</span><span class="sxs-lookup"><span data-stu-id="76768-195">See Also</span></span>  
 <span data-ttu-id="76768-196">[設定磁碟空間使用量 &#40;PowerPivot for SharePoint&#41;](configure-disk-space-usage-power-pivot-for-sharepoint.md) </span><span class="sxs-lookup"><span data-stu-id="76768-196">[Configure Disk Space Usage &#40;PowerPivot for SharePoint&#41;](configure-disk-space-usage-power-pivot-for-sharepoint.md) </span></span>  
 [<span data-ttu-id="76768-197">PowerPivot 管理儀表板和使用量資料</span><span class="sxs-lookup"><span data-stu-id="76768-197">PowerPivot Management Dashboard and Usage Data</span></span>](power-pivot-management-dashboard-and-usage-data.md)  