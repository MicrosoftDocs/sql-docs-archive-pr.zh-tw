---
title: 設定原生模式報表伺服器向外延展部署 (SSRS Configuration Manager) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], deployments
- deploying [Reporting Services], scale-out deployment model
- scale-out deployments [Reporting Services]
ms.assetid: b30d0308-4d9b-4f85-9f83-dece4dcb2775
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6855769d36632ce60b7cf299291d58d5f136d120
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598750"
---
# <a name="configure-a-native-mode-report-server-scale-out-deployment-ssrs-configuration-manager"></a>設定原生模式報表伺服器向外延展部署 (SSRS 組態管理員)

  Reporting Services 原生模式支援向外延展部署模型，它可讓您在執行多個報表伺服器執行個體時共用單一報表伺服器資料庫。 向外延展部署是用來提高報表伺服器的延展性，以便處理更多的並行使用者及更大量的報表執行負載。 它也可以給特定伺服器專用，以處理互動式或已排程的報表。

 SharePoint 模式報表伺服器會利用 SharePoint 產品基礎結構進行相應放大。SharePoint 模式向外延展的執行方式是將其他 SharePoint 模式報表伺服器加入至 SharePoint 伺服器陣列。 如需 SharePoint 模式中向外延展的資訊，請參閱[將其他報表伺服器新增至伺服器陣列 &#40;SSRS 向外延展&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)。

 **向外延展部署是由以下項目所組成：**

-   共用單一報表伺服器資料庫的兩個或多個報表伺服器執行個體。

-   選擇性的網路負載平衡 (NLB) 叢集，以便將互動式使用者負載散佈在不同的報表伺服器執行個體之間。

 如果您在 NLB 叢集上設定 Reporting Services，您需要確定 NLB 虛擬伺服器名稱用於報表伺服器 URL 的組態中，而且伺服器設定為可共用相同的檢視狀態。

 Reporting Services 不會參與 Microsoft Cluster Services 叢集。 但是，您可以在屬於容錯移轉叢集之一部分的 Database Engine 執行個體上建立報表伺服器資料庫。

 **若要規劃、安裝及設定向外延展部署，請遵循以下步驟：**

-   如需有關如何安裝報表伺服器實例的指示，請參閱《線上叢書》中[的安裝 SQL Server 2014 &#40;安裝程式&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。

-   如果您打算在網路負載平衡 (NLB) 叢集上主控向外延展部署，您應該先設定 NLB 叢集，然後再設定向外延展部署。 如需詳細資訊，請參閱 [在網路負載平衡叢集上設定報表伺服器](../report-server/configure-a-report-server-on-a-network-load-balancing-cluster.md)。

-   如需如何共用報表伺服器資料庫以及將報表伺服器加入向外延展的指示，請檢閱本主題中的程序。

     下列程序說明如何設定兩個節點之報表伺服器的向外延展部署。 請重複本主題所述的步驟，將其他報表伺服器節點加入部署中。

    -   使用安裝程式可安裝將要加入向外延展部署的每一個報表伺服器執行個體。

         若要避免在將伺服器執行個體連接到共用資料庫時發生資料庫相容錯誤，請確定所有的執行個體都是相同的版本。 例如，如果您使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 報表伺服器執行個體來建立報表伺服器資料庫，則相同部署中的所有其他執行個體也都必須為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。

    -   使用 Reporting Services 組態管理員可將每一部報表伺服器連接到共用資料庫。 您一次只能連接並設定一個報表伺服器。

    -   使用 Reporting Services 組態工具可完成向外延展，其方式是將新的報表伺服器執行個體加入已經連接至報表伺服器資料庫的第一個報表伺服器執行個體。

### <a name="to-install-a-sql-server-instance-to-host-the-report-server-databases"></a>安裝 SQL Server 執行個體以便主控報表伺服器資料庫

1.  在即將主控報表伺服器資料庫的電腦上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 您至少要安裝 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。

2.  如有需要，請針對遠端連接啟用報表伺服器。 某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本預設並不會啟用遠端 TCP/IP 和具名管道連接。 若要確認是否允許遠端連接，請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員並檢視目標執行個體的網路組態設定。 如果遠端執行個體也是具名執行個體，請確認 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務已啟用，而且在目標伺服器上執行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務提供了用來連接具名執行個體的通訊埠編號。

### <a name="to-install-the-first-report-server-instance"></a>若要安裝第一個報表伺服器執行個體

1.  安裝屬於部署之一部分的第一個報表伺服器執行個體。 當您安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 時，請在 [報表伺服器安裝選項] 頁面上選擇 [安裝但不設定伺服器]**** 選項。

2.  啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具。

3.  設定報表伺服器 Web 服務 URL、報表管理員 URL 和報表伺服器資料庫。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的[設定報表伺服器 &#40;Reporting Services 原生模式&#41;](../report-server/configure-a-report-server-reporting-services-native-mode.md)。

4.  確認報表伺服器可運作。 如需詳細資訊，請參閱《 [線上叢書》的](../../reporting-services/install-windows/verify-a-reporting-services-installation.md) 驗證 Reporting Services 安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。

### <a name="to-install-and-configure-the-second-report-server-instance"></a>若要安裝和設定第二個報表伺服器執行個體

1.  執行安裝程式，將第二個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體安裝在另一部電腦上，或做為相同電腦上的具名執行個體。 當您安裝 Reporting Services 時，請在 [報表伺服器安裝選項] 頁面上選擇 [安裝但不設定伺服器]**** 選項。

2.  啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並連接到您剛才安裝的新執行個體。

3.  請將報表伺服器連接到您用於第一個報表伺服器執行個體的相同資料庫：

    1.  按一下 [**資料庫**] 以開啟 [資料庫] 頁面。

    2.  按一下 **[變更資料庫]**。

    3.  按一下 **[選擇現有報表伺服器資料庫]**。

    4.  輸入主控您要使用之報表伺服器資料庫的 SQL Server Database Engine 執行個體的伺服器名稱。 這必須是您在先前的指示集內所連接的相同伺服器。

    5.  按一下 [**測試連接**]，然後按 **[下一步]**。

    6.  在 [**報表伺服器資料庫**] 中，選取您為第一部報表伺服器所建立的資料庫，然後按 **[下一步]**。 預設名稱為 ReportServer。 請勿選取 ReportServerTempDB，因為它只能在處理報表時用來儲存暫存資料。 如果資料庫清單是空的，請重複前四個步驟來建立與伺服器的連接。

    7.  在 [認證] 頁面中，選取報表伺服器將用來連接到報表伺服器資料庫的帳戶類型和認證。 您可以使用與第一個報表伺服器執行個體相同的認證，或是不同的認證。 按 [下一步] 。

    8.  按一下 [**摘要**]，然後按一下 **[完成]**。

4.  設定報表伺服器 Web 服務 URL。 還不要測試 URL， 要等到報表伺服器加入向外延展部署之後，才會解析此 URL。

5.  設定報表管理員 URL。 還不要測試此 URL 或嘗試驗證部署。 要等到報表伺服器加入向外延展部署之後，報表伺服器才可以使用。

### <a name="to-join-the-second-report-server-instance-to-the-scale-out-deployment"></a>將第二個報表伺服器執行個體加入向外延展部署

1.  開啟 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並重新連接到第一個報表伺服器執行個體。 由於第一部報表伺服器已針對可回復的加密作業初始化，因此它可用來將其他報表伺服器執行個體加入向外延展部署中。

2.  按一下 [向外延展部署]****，開啟 [向外延展部署] 頁面。 您應該會看到兩個項目，一個項目適用於連接到報表伺服器資料庫的每一個報表伺服器執行個體。 第一個報表伺服器執行個體應該會加入， 第二部報表伺服器應該是「正在等候加入」。 如果您沒有看到類似於部署的項目，請確認您已連接到已設定及初始化來使用報表伺服器資料庫的第一部報表伺服器。

     ![[相應放大部署] 頁面的局部螢幕擷取畫面](../../../2014/sql-server/install/media/scaloutscreen.gif "[相應放大部署] 頁面的局部螢幕擷取畫面")

3.  在 [向外延展部署] 頁面上，選取正在等候加入部署的報表伺服器實例，然後按一下 [**新增伺服器**]。

    > [!NOTE]
    >  **問題：** 當您嘗試將 Reporting Services 報表伺服器實例加入向外延展部署時，可能會遇到類似「拒絕存取」的錯誤訊息。
    > 
    >  **因應措施** ：從第一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體備份 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 加密金鑰，然後將此金鑰還原到第二部 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器。 接著嘗試將第二部伺服器加入 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 向外延展部署。

4.  您現在應該能夠確認這兩個報表伺服器執行個體都可運作。 若要確認第二個執行個體，您可以使用 Reporting Services 組態工具連接到報表伺服器，然後按一下 [Web 服務 URL] 或 [報表管理員 URL]。

 如果您打算在負載平衡的伺服器叢集中執行報表伺服器，還需要其他組態。 如需詳細資訊，請參閱 [在網路負載平衡叢集上設定報表伺服器](../report-server/configure-a-report-server-on-a-network-load-balancing-cluster.md)。

## <a name="see-also"></a>另請參閱
 [設定服務帳戶 &#40;ssrs Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-service-account-ssrs-configuration-manager.md) [將 &#40;URL 設定為 ssrs Configuration Manager](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)&#41;[建立原生模式報表伺服器資料庫 &#40;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md) Ssrs Configuration Manager&#41;將報表[伺服器 Url 設定](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)&#40;ssrs [Configuration Manager&#41;將](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)[報表伺服器資料庫連接](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)&#40;ssrs Configuration Manager&#41;[管理 &#40;原生模式報表伺服器](../report-server/manage-a-reporting-services-native-mode-report-server.md)


