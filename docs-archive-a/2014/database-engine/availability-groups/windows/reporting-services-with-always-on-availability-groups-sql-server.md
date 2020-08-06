---
title: 具有 AlwaysOn 可用性群組 (SQL Server) 的 Reporting Services |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: edeb5c75-fb13-467e-873a-ab3aad88ab72
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: dcaafcf3cac177ccad4a4b7712bda04a1fc932a8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707902"
---
# <a name="reporting-services-with-alwayson-availability-groups-sql-server"></a>Reporting Services 與 AlwaysOn 可用性群組 (SQL Server)
  本主題包含將 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)][!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 設定為使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)](AG) 的相關資訊。 使用 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 的三種案例包括報表資料來源的資料庫、報表伺服器資料庫以及報表設計。 這三種案例的支援功能和必要組態有所不同。

 使用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 搭配 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料來源的主要優點是能夠運用可讀取的次要複本做為報表資料來源，同時次要複本可針對主要資料庫提供容錯移轉。

 如需有關的一般資訊 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] ，請參閱[SQL Server 2012 (https://msdn.microsoft.com/sqlserver/gg508768) 的 AlwaysOn 常見問題](https://msdn.microsoft.com/sqlserver/gg508768)。

 

##  <a name="requirements-for-using-reporting-services-and-alwayson-availability-groups"></a><a name="bkmk_requirements"></a>使用 Reporting Services 和 AlwaysOn 可用性群組的需求
 若要搭配使用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ，您必須下載並安裝 .net 3.5 SP1 的修補程式。 此 Hotfix 會加入 SQL 用戶端對於 AG 功能的支援，以及連接字串屬性 **ApplicationIntent** 和 **MultiSubnetFailover**的支援。 如果裝載報表伺服器的每部電腦沒有安裝此 Hotfix，則嘗試預覽報表的使用者將會看見類似下面的錯誤訊息，而且該錯誤訊息將寫入報表伺服器追蹤記錄：

> **錯誤訊息：** 「不支援關鍵字 'applicationintent'」

 當您在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 連接字串中加入其中一個 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 屬性，但是伺服器無法辨識該屬性時，就會出現此訊息。 如果報表伺服器已啟用遠端錯誤，當您在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 使用者介面中按一下 [測試連線] 按鈕以及預覽報表時，就會看見上述錯誤訊息。

 如需有關必要 Hotfix 的詳細資訊，請參閱 [KB 2654347：此 Hotfix 可將 AlwaysOn 功能的支援加入 .Net 3.5 SP1](https://go.microsoft.com/fwlink/?LinkId=242896)。

 如需其他 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 需求的資訊，請參閱 [AlwaysOn 可用性群組的必要條件、限制和建議 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)。

> [!NOTE]
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 功能不支援 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 組態檔，例如 **RSreportserver.config**。 如果您對其中一個報表伺服器的組態檔進行手動變更，就必須手動更新複本。

##  <a name="report-data-sources-and-availability-groups"></a><a name="bkmk_reportdatasources"></a> 報表資料來源和可用性群組
 以 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 為基礎之 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 資料來源的行為可能會因系統管理員設定 AG 環境的方式而異。

 若要針對報表資料來源使用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] ，您必須將報表資料來源連接字串設定為使用可用性群組的 *「接聽程式 DNS 名稱」* (Listener DNS Name)。 支援的資料來源如下：

-   使用 SQL Native Client 的 ODBC 資料來源。

-   SQL 用戶端 (已將 .Net Hotfix 套用至報表伺服器)。

 連接字串也可以包含新的 AlwaysOn 連接屬性，以便將報表查詢要求設定為使用唯讀報表的次要複本。 將次要複本用於報表要求可降低讀寫主要複本的負載。 下圖是三個複本 AG 組態的範例，其中 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料來源連接字串已經使用 ApplicationIntent=ReadOnly 進行設定。 在此範例中，報表查詢要求會傳送至次要複本而非主要複本。

 ![使用 AG 群組的 SSRS 資料來源](../../media/rs-alwayson-basic.gif "使用 AG 群組的 SSRS 資料來源")

 下面是連接字串範例，其中 [AvailabilityGroupListenerName] 是建立複本時所設定的 **Listener DNS Name** ：

 `Data Source=[AvailabilityGroupListenerName];Initial Catalog = AdventureWorks2008R2; ApplicationIntent=ReadOnly`

 **使用者介面中的** [測試連接] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 按鈕將會驗證是否能夠建立連接，但是不會驗證 AG 組態。 例如，如果您在不屬於 AG 一部分之伺服器的連接字串中加入 ApplicationIntent，系統就會忽略額外的參數，而且 **[測試連接]** 按鈕只會驗證是否能夠建立指定之伺服器的連接。

 報表的建立和發行方式將會決定您可以編輯連接字串的位置：

-   **原生模式：** 您可以針對已經發行至原生模式報表伺服器的共用資料來源和報表使用報表管理員。

-   **SharePoint 模式：** 您可以針對已經發行至 SharePoint 伺服器的報表使用文件庫中的 SharePoint 設定頁面。

-   **報表設計：** 您可以在建立新報表時使用 [!INCLUDE[ssRBDenali](../../../includes/ssrbdenali-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]。 如需詳細資訊，請參閱本主題的＜報表設計＞一節。

 **其他資源：**

-   [管理報表資料來源](../../../reporting-services/report-data/manage-report-data-sources.md)

-   如需有關可用之連接字串屬性的詳細資訊，請參閱＜ [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)＞。

-   如需有關可用性群組接聽程式的詳細資訊，請參閱[建立或設定可用性群組接聽程式 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)。

 **考量因素：** 接收來自主要複本的資料變更時，次要複本通常會發生延遲。 下列因素可能會影響主要與次要複本之間的更新延遲：

-   次要複本的數目。 延遲會隨著加入至組態的每個次要複本而增加。

-   主要與次要複本之間的地理位置和距離。 例如，如果次要複本與主要複本位於不同的資料中心，其延遲通常會比次要複本與主要複本位於相同建築物的延遲要長。

-   每個複本之可用性模式的組態。 可用性模式會決定在次要複本將交易寫入磁碟之前，主要複本是否要等候認可資料庫上的交易。 如需詳細資訊，請參閱[AlwaysOn 可用性群組 &#40;SQL Server&#41;總覽](overview-of-always-on-availability-groups-sql-server.md)的「可用性模式」一節。

 使用唯讀次要複本做為 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料來源時，請務必確定資料更新延遲符合報表使用者的需求。

##  <a name="report-design-and-availability-groups"></a><a name="bkmk_reportdesign"></a> 報表設計和可用性群組
 在 [!INCLUDE[ssRBDenali](../../../includes/ssrbdenali-md.md)] 中設計報表或在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中設計報表專案時，使用者可以將報表資料來源連接字串設定為包含 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]所提供的新連接屬性。 新連接屬性的支援主要取決於使用者預覽報表的位置。

-   **本機預覽：** [!INCLUDE[ssRBDenali](../../../includes/ssrbdenali-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 會使用 .Net Framework 4.0 並且支援 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 連接字串屬性。

-   **遠端或伺服器模式預覽：** 如果將報表發行至報表伺服器或在 [!INCLUDE[ssRBDenali](../../../includes/ssrbdenali-md.md)] 中使用預覽功能之後，您看見類似下面的錯誤，就表示您正在根據報表伺服器預覽報表，而且報表伺服器尚未安裝 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 的 .Net Framework 3.5 SP1 Hotfix。

> **錯誤訊息：** 「不支援關鍵字 'applicationintent'」

##  <a name="report-server-databases-and-availability-groups"></a><a name="bkmk_reportserverdatabases"></a> 報表伺服器資料庫和可用性群組
 Reporting Services 對於使用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 搭配報表伺服器資料庫提供有限的支援。 您可以在 AG 中將報表伺服器資料庫設定為複本的一部分，但在容錯移轉時， [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 不會自動為報表伺服器資料庫使用不同的複本。

 您必須使用手動操作或自訂自動化指令碼，才能完成容錯移轉和復原。 完成這些動作之前，報表伺服器的某些功能可能會在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 容錯移轉之後無法正確運作。

> [!NOTE]
>  針對報表伺服器資料庫規劃容錯移轉和災害復原時，建議您一定要備份報表伺服器加密金鑰的複本。

###  <a name="differences-between-sharepoint-native-mode"></a><a name="bkmk_differences_in_server_mode"></a> SharePoint 原生模式之間的差異
 本節將摘要說明 SharePoint 模式及原生模式報表伺服器與 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]互動的方式差異。

 SharePoint 報表伺服器會為您所建立的每個 **服務應用程式建立** 3 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 個資料庫。 當您建立服務應用程式時，會在 SharePoint 管理中心內設定 SharePoint 模式報表伺服器資料庫的連接。 資料庫的預設名稱包含關聯到服務應用程式的 GUID。 以下是 SharePoint 模式報表伺服器的範例資料庫名稱：

-   ReportingService_85c08ac3c8e64d3cb400ad06ed5da5d6

-   ReportingService_85c08ac3c8e64d3cb400ad06ed5da5d6TempDB

-   ReportingService_85c08ac3c8e64d3cb400ad06ed5da5d6_Alerting

 原生模式報表伺服器會使用 **2** 個資料庫。 以下是原生模式報表伺服器的範例資料庫名稱：

-   ReportServer

-   ReportServerTempDB

 原生模式不支援或使用警示資料庫及相關功能。 您可以在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 組態管理員中設定原生模式報表伺服器。 若是 SharePoint 模式，您可以將服務應用程式資料庫名稱設定為您在 SharePoint 設定過程中建立的「用戶端存取點」的名稱。 如需使用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 來設定 SharePoint 的詳細資訊，請參閱 [Configure and manage SQL Server availability groups for SharePoint Server (https://go.microsoft.com/fwlink/?LinkId=245165)](https://go.microsoft.com/fwlink/?LinkId=245165) (設定及管理 SharePoint Server 的 SQL Server 可用性群組)。

> [!NOTE]
>  SharePoint 模式報表伺服器會在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 服務應用程式資料庫與 SharePoint 內容資料庫之間使用同步處理程序。 請務必一起維護報表伺服器資料庫和內容資料庫。 您應該考慮將它們設定在相同的可用性群組中，以便一起容錯移轉和復原。 請考慮下列案例：
> 
>  -   您還原或容錯移轉至內容資料庫的複本，但是該資料庫尚未收到報表伺服器資料庫已經收到的相同近期更新。
> -   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 同步處理程序將會偵測到內容資料庫與報表伺服器資料庫的項目清單之間存在差異。
> -   同步處理程序將會刪除或更新內容資料庫中的項目。

###  <a name="prepare-report-server-databases-for-availability-groups"></a><a name="bkmk_prepare_databases"></a> 針對可用性群組準備報表伺服器資料庫
 下面是準備將報表伺服器資料庫加入至 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]的基本步驟：

-   建立您的可用性群組並且設定 *「接聽程式 DNS 名稱」* (Listener DNS Name)。

-   **主要複本：** 將報表伺服器資料庫設定為單一可用性群組的一部分，並且建立包含所有報表伺服器資料庫的主要複本。

-   **次要複本：** 建立一或多個次要複本。 將資料庫從主要複本複製到次要複本的常見方法是使用 'RESTORE WITH NORECOVERY'，將資料庫還原至每個次要複本。 如需建立次要複本以及驗證資料同步處理是否運作的詳細資訊，請參閱[於 AlwaysOn 次要資料庫啟動資料移動 &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)。

-   **報表伺服器認證：** 您必須在次要與主要複本上建立適當的報表伺服器認證。 確切步驟主要取決於您在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 環境中使用的驗證類型：Windows [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 服務帳戶、Windows 使用者帳戶或 SQL Server 驗證。 如需詳細資訊，請參閱[設定報表伺服器資料庫連接 &#40;SSRS 組態管理員&#41;](../../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)

-   將資料庫連接更新為使用接聽程式 DNS 名稱。 若為原生模式報表伺服器，請在 **組態管理員中變更** [報表伺服器資料庫名稱] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 。 若為 SharePoint 模式，請為 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 服務應用程式變更 [資料庫伺服器名稱]。

###  <a name="steps-to-complete-disaster-recovery-of-report-server-databases"></a><a name="bkmk_steps_to_complete_failover"></a> 完成報表伺服器資料庫之災害復原的步驟
 您必須在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 容錯移轉至次要複本之後完成下列步驟：

1.  停止裝載 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料庫之主要資料庫引擎所使用的 SQL 代理程式服務執行個體。

2.  在成為新主要複本的電腦上啟動 SQL 代理程式服務。

3.  停止報表伺服器服務。

     如果報表伺服器處於原生模式，請使用 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 組態管理員來停止報表伺服器 Windows 伺服器。

     如果報表伺服器設定為 SharePoint 模式，請在 SharePoint 管理中心內停止 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 共用服務。

4.  啟動報表伺服器服務或 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint 服務。

5.  確認報表可以根據新的主要複本執行。

###  <a name="report-server-behavior-when-a-failover-occurs"></a><a name="bkmk_failover_behavior"></a> 進行容錯移轉時的報表伺服器行為
 當報表伺服器資料庫容錯移轉，而且您已經將報表伺服器環境更新為使用新的主要複本時，容錯移轉和復原程序會產生一些作業問題。 這些問題的影響會因下列條件而異：容錯移轉時的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 負載、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 容錯移轉至次要複本所需的時間長度，以及報表伺服器管理員將報表環境更新為使用新主要複本所需的時間長度。

-   由於重試邏輯以及報表伺服器無法在容錯移轉期間將排程的工作標記為已完成，因此背景處理的執行可能會發生一次以上。

-   通常已經觸發要在容錯移轉期間執行的背景處理執行將不會發生，因為 SQL Server Agent 無法將資料寫入報表伺服器資料庫中，而且這項資料不會同步處理至新的主要複本。

-   在資料庫容錯移轉完成而且報表伺服器服務重新啟動之後，系統將會自動重新建立 SQL Server Agent 作業。 在建立 SQL 代理程式作業之前，系統將不會處理任何與 SQL Server Agent 作業相關聯的背景執行。 這包括 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 訂閱、排程和快照集。

## <a name="see-also"></a>另請參閱
 [SQL Server Native Client 支援高可用性、嚴重損壞修復](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md) [AlwaysOn 可用性群組 (SQL Server) ](always-on-availability-groups-sql-server.md)消費者入門搭配[AlwaysOn 可用性群組](getting-started-with-always-on-availability-groups-sql-server.md)&#40;SQL Server&#41;[使用連接字串關鍵字搭配 SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) SQL Server Native Client[支援高可用性](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)的[用戶端連接存取](about-client-connection-access-to-availability-replicas-sql-server.md)、嚴重損壞修復 &#40;SQL Server&#41;


