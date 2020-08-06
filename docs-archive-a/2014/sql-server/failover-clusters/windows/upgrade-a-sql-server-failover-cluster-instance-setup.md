---
title: 升級 SQL Server 容錯移轉叢集執行個體 (安裝程式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], creating clusters
- clusters [SQL Server], creating
- failover clustering [SQL Server], upgrading
ms.assetid: ea8b7d66-e5a1-402f-9928-8f7310e84f5c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a45628055ee12f5d771c863dec7a3368cdae5940
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708109"
---
# <a name="upgrade-a-sql-server-failover-cluster-instance-setup"></a>升級 SQL Server 容錯移轉叢集執行個體 (安裝程式)
  您可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝精靈或命令提示字元，將 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 容錯移轉叢集升級為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集。  
  
 在容錯移轉叢集升級期間，停機時間僅包含容錯移轉時間以及執行升級指令碼所需的時間。 如果您遵循容錯移轉叢集輪流升級程序，就會將停機時間減到最少。 視您是否在容錯移轉叢集節點上設有所有必要元件而定，您可能會在安裝這些必要元件時造成額外的停機時間。 如需有關如何在升級期間將停機時間降至最低的詳細資訊，請參閱此頁面上的[升級容錯移轉叢集之前的最佳作法](#BestPractices)一節。  
  
 如需如何升級的詳細資訊，請參閱[支援的版本與版本升級](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)和[升級至 SQL Server 2014](../../../database-engine/install-windows/upgrade-sql-server.md)。  
  
 如需命令提示字元使用方式範例語法的詳細資訊，請參閱[從命令提示字元安裝 SQL Server 2014](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。  
  
## <a name="prerequisites"></a>Prerequisites  
 在開始之前，請檢閱以下重要資訊：  
  
-   [安裝容錯移轉叢集之前](../install/before-installing-failover-clustering.md)  
  
-   [使用 Upgrade Advisor 來準備升級](../../install/use-upgrade-advisor-to-prepare-for-upgrades.md)。  
  
-   [升級 Database Engine](../../../database-engine/install-windows/upgrade-database-engine.md)  
  
-   安裝程式會在叢集作業系統上安裝 .NET Framework 4.0。 若要盡量縮短任何可能的停機時間，您可以考慮在執行安裝程式前先安裝 .NET Framework 4.0。  
  
-   若要確定 Visual Studio 元件可以正確安裝， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 需要安裝更新。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式會檢查此更新的狀態，然後需要您下載並安裝更新才能繼續安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 若要避免 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式期間的中斷，您可以先下載並安裝更新，然後執行如下所述的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式 (或安裝 Windows Update 上可用 .NET 3.5 SP1 的所有更新)：  
  
     如果您將安裝 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 在 Windows Server 2008 SP2 作業系統的電腦上，您可以從[這裡](https://go.microsoft.com/fwlink/?LinkId=198093)取得所需的更新  
  
     如果您將 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 安裝在 [!INCLUDE[win7](../../../includes/win7-md.md)] SP1 或 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] SP1 作業系統的電腦上，則已包含此更新。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式不再安裝 .NET Framework 3.5 SP1，但是在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 上安裝 [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] 時，可能會需要 .NET Framework 3.5 SP1。 如需詳細資訊，請參閱 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] [版本](https://go.microsoft.com/fwlink/?LinkId=296445)資訊。  
  
-   若是本機安裝，您必須以管理員身分執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，則必須使用對遠端共用位置具有讀取權限的網域帳戶。  
  
-   若要將實例升級 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 為 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 容錯移轉叢集，要升級的實例必須是容錯移轉叢集。  
  
     若要將獨立的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體移動到 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 容錯移轉叢集，請安裝新的 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 容錯移轉叢集，然後利用「複製資料庫精靈」，從獨立的執行個體移轉使用者資料庫。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="rolling-upgrades"></a>輪流升級  
 若要將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集升級為 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]，您必須在每個容錯移轉叢集節點上使用升級動作來執行安裝程式 (從被動節點開始，一次一個)。 當您升級每個節點時，它就不會包含在容錯移轉叢集的可能擁有者中。 如果發生非預期的容錯移轉，在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式將叢集資源群組擁有權移至升級的節點之前，升級的節點不會參與容錯移轉。  
  
 根據預設，安裝程式會自動決定容錯移轉至升級節點的時機。 這個時機會取決於容錯移轉叢集執行個體中的節點總數以及已經升級的節點數目而定。 如果半數以上的節點都已經升級，當您在下一個節點上執行升級時，安裝程式就會導致系統容錯移轉至升級的節點。 容錯移轉至升級的節點之後，叢集群組就會移至升級的節點。 系統會將所有升級的節點都放置在可能擁有者的清單中，並從可能擁有者的清單中移除尚未升級的所有節點。 當您升級其餘每個節點時，它就會加入至容錯移轉叢集的可能擁有者。  
  
 這個程序會導致停機時間僅會包含整個容錯移轉叢集升級期間的單一容錯移轉時間和資料庫升級指令碼執行時間。  
  
 若要在升級程序期間控制叢集節點的容錯移轉行為，請從命令提示字元執行升級作業，然後使用 /FAILOVERCLUSTERROLLOWNERSHIP 參數。 如需詳細資訊，請參閱[從命令提示字元安裝 SQL Server 2014](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。  
  
 **注意**如果有單一節點容錯移轉叢集， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式會讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資源群組離線。  
  
## <a name="considerations-when-upgrading-from-ssversion2005"></a>從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 升級時的考量  
 如果您為叢集安全性原則指定了網域群組，就無法在 [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)] 上指定服務 SID。 如果您想要使用服務 SID，則需要執行並存升級。  
  
 當您選取 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 進行升級時，全文檢索搜尋會包含在安裝程式中，不論它是否已在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中安裝。  
  
 如果已在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中啟用全文檢索搜尋，安裝程式會重建全文檢索搜尋目錄，不論可供您使用的選項為何。  
  
## <a name="upgrading-to-a-sssql14-multi-subnet-failover-cluster"></a>升級至 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 多重子網路容錯移轉叢集  
 可能的升級案例有兩種：  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集目前設定在單一子網路上：您必須先啟動安裝程式，並遵循升級程序進行，以將現有叢集升級至 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]。 在完成升級現有的容錯移轉叢集之後，使用 AddNode 功能，以加入位在不同子網路上的節點。 請確認叢集網路組態頁面中的 IP 位址資源相依性已變更為 OR。 您現在已擁有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 多重子網路容錯移轉叢集。  
  
2.  目前已使用延展 V-LAN 技術，將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集設定在多重子網路中：您必須先將現有的叢集升級到 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]。 由於延伸 V-LAN 技術會設定單一子網路網路，網路組態必須變更為多重子網路，而且要使用 Windows 容錯移轉叢集管理工具變更 IP 位址資源相依性，並將 IP 相依性變更為 OR。  
  
###  <a name="best-practices-before-upgrading-a-ssnoversion-failover-cluster"></a><a name="BestPractices"></a>升級容錯移轉叢集之前的最佳作法 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 若要排除重新啟動所產生的非預期停機時間，請在所有容錯移轉叢集節點上預先安裝 .NET Framework 4.0 的不必重新開機封裝，然後在叢集節點上執行升級。 下面是預先安裝必要元件的建議步驟：  
  
-   安裝 .NET 4.0 的不必重新開機封裝，並且只升級以被動節點開始的共用元件。 這樣會安裝 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 4.0、Windows Installer 4.5 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的支援檔案。  
  
-   視需要重新啟動一次或多次。  
  
-   容錯移轉至升級的節點。  
  
-   在剩餘的最後一個節點上升級共用的元件。  
  
 當您已經升級所有共用的元件而且已經安裝必要元件之後，請啟動容錯移轉叢集升級程序。 您必須在每個容錯移轉叢集節點上執行升級，從被動節點開始而且直到擁有叢集資源群組的節點為止。  
  
-   您無法將功能加入至現有的容錯移轉叢集。  
  
-   變更容錯移轉叢集的版本會受限於特定狀況。 如需詳細資訊，請參閱 [支援的版本與版本升級](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)。  
  
##  <a name="to-upgrade-a-ssnoversion-failover-cluster"></a><a name="UpgradeSteps"></a> 若要升級 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集  
  
#### <a name="to-upgrade-a-ssnoversion-failover-cluster"></a>若要升級 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集  
  
1.  插入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝媒體，然後在根資料夾中，按兩下 Setup.exe。 若要從網路共用區進行安裝，請移到共用區上的根資料夾，然後按兩下 Setup.exe。 如果您之前未安裝必要元件，系統可能會要求您安裝。  
  
2.  > [!IMPORTANT]  
    >  如需步驟3和4的詳細資訊，請參閱[升級容錯移轉叢集之前的最佳作法](#BestPractices)一節。  
  
3.  安裝必要元件之後，安裝精靈會啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝中心。 若要升級現有的實例 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，請按一下 [**從、、或升級] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 。**  
  
4.  如果需要安裝程式支援檔案， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式就會安裝這些檔案。 如果系統指示您重新啟動電腦，請先重新啟動，然後再繼續進行。  
  
5.  系統組態檢查會在電腦上執行探索作業。 若要繼續，請[!INCLUDE[clickOK](../../../includes/clickok-md.md)]。  
  
6.  在 [產品金鑰] 頁面上，針對符合舊產品版本的新版本輸入 PID 金鑰。 例如，若要升級 Enterprise 容錯移轉叢集，您必須提供 [!INCLUDE[ssEnterprise](../../../includes/ssenterprise-md.md)]的 PID 金鑰。 選取 [下一步] 以繼續操作。 請注意，您針對容錯移轉叢集升級所使用的 PID 金鑰在相同 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的所有容錯移轉叢集節點之間必須一致。 如需詳細資訊，請參閱[SQL Server 2014 的版本和元件](../../editions-and-components-of-sql-server-2016.md)和[支援的版本與版本升級](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)。  
  
7.  在 [授權條款] 頁面上，閱讀授權合約，然後選取要接受授權條款和條件的核取方塊。 若要協助提升 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，您也可以啟用功能使用方式選項，並傳送報告給 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]。 **按 [下一步] 繼續**。 若要結束安裝程式，請按一下 **[取消]** 。  
  
8.  在 [選取執行個體] 頁面中，指定要升級為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]執行個體。 **按 [下一步] 繼續**。  
  
9. 在 [特徵選取] 頁面上，系統會預先選取要升級的功能。 當您選取功能名稱之後，每一個元件群組的描述就會出現在右窗格中。 請注意，您無法變更要升級的功能，而且您無法在升級作業期間加入功能。 若要在升級作業完成後將功能加入升級的實例 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] ，請參閱[將功能加入至 SQL Server 2014 的實例 &#40;安裝&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-setup.md)。  
  
     右窗格會顯示選取功能的必要條件。 SQL Server 安裝程式將會在這個程序稍後說明的安裝步驟期間安裝尚未安裝的必要條件。  
  
10. 在 [執行個體組態] 頁面上，系統會根據舊的執行個體自動填入欄位。 您可以選擇指定新的 InstanceID 值。  
  
     **執行個體識別碼** ：依預設，此執行個體名稱會當作執行個體識別碼使用。 這是用來識別 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體的安裝目錄和登錄機碼。 這是預設執行個體和具名執行個體的狀況。 如果是預設執行個體，執行個體名稱和執行個體識別碼將會是 MSSQLSERVER。 若要使用非預設的執行個體識別碼，請選取 [執行個體識別碼]**** 核取方塊並提供值。 如果您覆寫預設值，就必須針對在所有容錯移轉叢集節點上升級的執行個體指定相同的執行個體識別碼。 升級之執行個體的執行個體識別碼在這些節點之間必須相符。  
  
     偵測**到的實例和功能**-此方格會顯示執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式之電腦上的實例。 **按 [下一步] 繼續**。  
  
11. [磁碟空間需求] 頁面會計算您所指定之功能的所需磁碟空間，並且比較空間需求與執行安裝程式之電腦的可用磁碟空間。  
  
12. 在 [全文檢索搜尋升級] 頁面上，針對升級的資料庫指定升級選項。 如需詳細資訊，請參閱 [全文檢索搜尋升級選項](../../install/full-text-search-upgrade-options.md)。  
  
13. 在 **[錯誤報告]** 頁面上，指定您想要傳送給 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 的資訊，這可協助改善 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 錯誤報告選項預設為啟用。  
  
14. 在升級作業開始之前，系統組態檢查會執行一組額外的規則，以便使用您已指定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 功能來驗證電腦組態。  
  
15. [叢集升級報表] 頁面會顯示容錯移轉叢集執行個體中的節點清單以及每個節點上 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 元件的執行個體版本資訊。 它會顯示資料庫指令碼狀態和複寫指令碼狀態。 此外，它也會顯示當您按一下 [下一步]**** 時所進行之動作的參考用訊息。 根據已升級的容錯移轉叢集節點數目和節點總數，安裝程式會顯示當您按 **[下一步]** 時所發生的容錯移轉行為。 如果您尚未安裝必要元件，它也會發出可能產生不必要停機時間的警告。  
  
16. [準備升級] 頁面會顯示在安裝期間指定之安裝選項的樹狀檢視。 若要繼續，請按一下 **[升級]** 。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式會先安裝選取功能所需的必要條件，之後再進行功能安裝。  
  
17. 在升級期間，[進度] 頁面會提供狀態，好讓您可以在安裝程式進行時監視目前節點的升級進度。  
  
18. 升級目前的節點之後，[叢集升級報表] 頁面就會顯示所有容錯移轉叢集節點的升級狀態資訊、每個容錯移轉叢集節點的功能，以及其版本資訊。 請確認所顯示的版本資訊並且繼續進行其餘節點的升級作業。 如果發生容錯移轉至升級節點的行為，這也會出現在狀態頁面上。 您也可以在 Windows 叢集管理員工具中檢查，然後確認。  
  
19. 升級之後，[完成] 頁面會提供安裝和其他重要注意事項之摘要記錄檔的連結。 若要完成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程序，請按一下 **[關閉]** 。  
  
20. 如果指示您重新啟動電腦，請立刻執行。 當您完成安裝時，請務必閱讀安裝精靈所提供的訊息。 如需安裝程式記錄檔的詳細資訊，請參閱 [檢視與讀取 SQL Server 安裝程式記錄檔](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)。  
  
21. 若要完成升級程序，請在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集的所有其他節點上重複步驟 1 到 21。  
  
## <a name="to-upgrade-a-ssnoversion-multi-subnet-failover-cluster"></a>若要升級 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 多重子網路容錯移轉叢集  
  
#### <a name="to-upgrade-to-a-ssnoversion-multi-subnet-failover-cluster-existing-ssnoversion-cluster-is-a-non-multi-subnet-cluster"></a>若要升級到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 多重子網路容錯移轉叢集 (現有的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 叢集為非多重子網路叢集)。  
  
1.  遵循上面的[升級 SQL Server 容錯移轉](#UpgradeSteps)叢集一節中所述的步驟1到24，將您的叢集升級至 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 。  
  
2.  使用 AddNode 安裝程式動作將節點加入到不同的子網路，並在 [叢集網路組態]**** 頁面確認 IP 位址資源相依性為 OR。 如需詳細資訊，請參閱[在 SQL Server 容錯移轉叢集中新增或移除節點 &#40;安裝程式&#41;](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)。  
  
#### <a name="to-upgrade-a-multi-subnet-cluster-currently-using-stretch-v-lan"></a>若要升級目前使用延展 V-Lan 的多重子網路叢集。  
  
1.  遵循上面的[升級 SQL Server 容錯移轉](#UpgradeSteps)叢集一節中所述的步驟1到24，將您的叢集升級至 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 。  
  
2.  變更網路設定，將遠端節點移到不同的子網路。  
  
3.  使用 Windows 容錯移轉叢集管理工具，為新的子網路加入新的 IP 位址，並將 IP 位址資源相依性設定為 OR。  
  
## <a name="next-steps"></a>後續步驟  
 在升級為 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]之後，請完成下列工作：  
  
-   註冊伺服器  
  
     升級會移除先前 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的登錄設定。 在升級之後，您必須重新註冊伺服器。  
  
-   更新統計資料  
  
     若要協助最佳化查詢效能，我們建議您在升級之後，更新所有資料庫的統計資料。 請使用 **sp_updatestats** 預存程序來更新 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中使用者定義資料表的統計資料。  
  
-   設定新的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝。  
  
     為了減少系統的可攻擊介面區， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以選擇性地安裝和啟用主要服務和功能。 如需有關介面區組態的詳細資訊，請參閱這一版的讀我檔案。  
  
## <a name="see-also"></a>另請參閱  
 [從命令提示字元安裝 SQL Server 2014](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [檢視與讀取 SQL Server 安裝程式記錄檔](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
