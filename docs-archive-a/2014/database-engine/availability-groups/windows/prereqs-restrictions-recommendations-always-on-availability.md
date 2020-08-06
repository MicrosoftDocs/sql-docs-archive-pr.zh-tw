---
title: AlwaysOn 可用性群組 (SQL Server) 的必要條件、限制和建議 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], WSFC clusters
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], prerequisites and restrictions
- Availability Groups [SQL Server], Failover Cluster Instances
- Availability Groups [SQL Server], databases
- Availability Groups [SQL Server]
ms.assetid: edbab896-42bb-4d17-8d75-e92ca11f7abb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 078f38058c612037a8013f7955349e94d6db610e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707910"
---
# <a name="prerequisites-restrictions-and-recommendations-for-alwayson-availability-groups-sql-server"></a>AlwaysOn 可用性群組的必要條件、限制和建議 (SQL Server)
  此主題描述部署 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]的考量，包括對於主機電腦、Windows Server 容錯移轉叢集 (WSFC) 叢集、伺服器執行個體和可用性群組的必要條件、限制和建議。 它也會指出這些元件的安全性考量和必要權限 (如果有的話)。  
  
> [!IMPORTANT]  
>  在您部署 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]之前，我們強烈建議您先閱讀本主題的每一節。  
  
 
  
##  <a name="net-hotfixes-that-support-alwayson-availability-groups"></a><a name="DotNetHotfixes"></a>支援 AlwaysOn 可用性群組的 .NET 修補程式  
 根據 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 您將搭配使用的元件和功能 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 而定，您可能需要安裝下表中識別的其他 .net 修補程式。 您可以依照任何順序安裝 Hotfix。  
  
||相依功能|Hotfix|連結|  
|------|-----------------------|------------|----------|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]|.NET 3.5 SP1 的修復程式新增了讀取意圖、readonly 和 multisubnetfailover AlwaysOn 功能的 SQL 用戶端支援。 每一部 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 報表伺服器上都需要安裝這個 Hotfix。|KB 2654347： [.net 3.5 SP1 的修補程式，可加入 AlwaysOn 功能的支援](https://go.microsoft.com/fwlink/?LinkId=242896)|  
  
##  <a name="windows-system-requirements-and-recommendations"></a><a name="SystemReqsForAOAG"></a>Windows 系統需求和建議  
  
  
###  <a name="checklist-requirements-windows-system"></a><a name="SystemRequirements"></a> 檢查清單：需求 (Windows 系統)  
 若要支援 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 功能，請確定要參與一個或多個可用性群組的每部電腦都符合下列基礎需求：  
  
||需求|連結|  
|------|-----------------|----------|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|確定系統不是網域控制站。|網域控制站不支援可用性群組。|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|確定每部電腦都是執行 x86 (非 WOW64) 或 x64 Windows Server 2008 (含) 以後版本。|WOW64 (Windows 64 位元上的 Windows 32 位元) 不支援 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]。|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|確定每部電腦都是在 Windows Server 容錯移轉叢集 (WSFC) 叢集中的節點。|[SQL Server 的 Windows Server 容錯移轉叢集 &#40;WSFC&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|確定 WSFC 叢集包含足夠多的節點可支援您的可用性群組組態。|WSFC 節點只能裝載給定可用性群組的一個可用性複本。 在給定 WSFC 節點上，一個或多個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體可以裝載許多可用性群組的可用性複本。<br /><br /> 詢問您的資料庫管理員，計畫中可用性群組的可用性複本支援需要多少 WSFC 節點。<br /><br /> [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)。|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|確定 WSFC 叢集中的每個節點上都安裝了所有適用的 Windows Hotfix。|** \* \* 重要 \* 事項 \* ：** 在部署的 WSFC 叢集節點上，需要或建議使用一些修補程式 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 。 如需詳細資訊，請參閱本節稍後的[支援 AlwaysOn 可用性群組的 Windows Hotfix (Windows 系統)](#WinHotfixes)。|  
  
> [!IMPORTANT]  
>  還要確定您的環境已正確設定為連接到可用性群組。 如需詳細資訊，請參閱[AlwaysOn Client Connectivity (SQL Server) ](always-on-client-connectivity-sql-server.md)。  
  
####  <a name="windows-hotfixes-that-support-alwayson-availability-groups-windows-system"></a><a name="WinHotfixes"></a>支援 AlwaysOn 可用性群組 (Windows 系統) 的 windows 修補程式  
 根據您的叢集拓撲，許多其他 Windows Server 2008 Service Pack 2 (SP2) 或 Windows Server 2008 R2 可能適用於支援 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]。 下表將識別這些 Hotfix。 您可以依照任何順序安裝這些 Hotfix。  
  
||適用於 Windows 2008 SP2|適用於 Windows 2008 R2 SP1|包含在 Windows 2012 中|若要支援 .。。|Hotfix|連結|  
|------|---------------------------------|------------------------------------|------------------------------|-----------------|------------|----------|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|是|是|是|**設定最佳的 WSFC 仲裁**|在每個 WSFC 節點上，確定已經安裝了知識庫文件 2494036 中所述的 Hotfix。<br /><br /> 此 Hotfix 支援使用非自動容錯移轉目標來設定最佳仲裁。 此功能使您可以選取投票的節點，藉此改善多網站叢集。|KB 2494036：  [此 Hotfix 可讓您設定在 Windows Server 2008 和 Windows Server 2008 R2 中沒有仲裁投票的叢集節點](https://support.microsoft.com/kb/2494036)(機器翻譯)<br /><br /> 如需仲裁投票的相關資訊，請參閱 [WSFC 仲裁模式和投票組態 &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|是|是|是|**更有效率地使用網路頻寬**|在每個 WSFC 節點上，確定已經安裝了知識庫文件 2616514 中所述的 Hotfix。<br /><br /> 如果沒有這個 Hotfix，叢集服務就會在叢集節點之間傳送不必要的登錄通知。 這種行為會限制網路頻寬，而這對 [!INCLUDE[ssHADRc](../../../includes/sshadrc-md.md)]會造成嚴重問題。|KB 2616514：  [叢集服務會在 Windows Server 2008 或 Windows Server 2008 R2 的叢集節點之間傳送不必要的登錄機碼變更通知](https://support.microsoft.com/kb/2616514)(機器翻譯)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")||是|不適用|**並非所有 WSFC 節點皆可在磁碟上進行 VPD 儲存測試**|如果 WSFC 節點正在執行 Windows Server 2008 R2 Service Pack 1 (SP1)，而且「驗證 SCSI 裝置重要產品資料 (VPD)」儲存測試在已上線但並非 WSFC 叢集中的所有節點都可使用的磁碟上不正確地執行之後失敗，請安裝知識庫文件 2531907 中所述的 Hotfix。<br /><br /> 此 Hotfix 可排除在磁碟已上線時驗證報告中不正確的警告或錯誤。|KB 2531907：[Validate SCSI Device Vital Product Data (VPD) test fails after you install Windows Server 2008 R2 SP1](https://support.microsoft.com/kb/2531907) (在您安裝 Windows Server 2008 R2 SP1 之後，驗證 SCSI 裝置重要產品資料 (VPD) 測試失敗)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")||是|是|**更快容錯移轉至本機複本**|若 WSFC 節點執行 Windows Server 2008 R2 Service Pack 1 (SP1)，請確定已經安裝了知識庫文件 2687741 中所述的下列 Hotfix。<br /><br /> 此 Hotfix 可以提升 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 容錯移轉至本機複本的效能。|KB 2687741：  [此 Windows Server 2008 R2 Hotfix 可提升 SQL Server 2012 之「AlwaysOn 可用性群組」功能的效能](https://support.microsoft.com/KB/2687741)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|是|是|是|**非對稱式儲存體-適用于容錯移轉叢集實例 (Fci) **|如果任何容錯移轉叢集執行個體 (FCI) 都將啟用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，請安裝 Windows Server 2008 Hotfix 976097。<br /><br /> 此修補程式可讓「容錯移轉叢集管理」 Microsoft Management Console (MMC) 嵌入式管理單元支援只能在部分 WSFC 節點上使用的非對稱式儲存體共用磁片。|KB 976097：[Hotfix to add support for asymmetric storages to the Failover Cluster Management MMC snap-in for a failover cluster that is running Windows Server 2008 or Windows Server 2008 R2](https://support.microsoft.com/kb/976097) (對於執行 Windows Server 2008 或 Windows Server 2008 R2 之容錯移轉叢集的容錯移轉叢集管理 MMC 嵌入式管理單元，Hotfix 新增非對稱儲存支援)<br /><br /> [AlwaysOn 架構指南：使用容錯移轉叢集執行個體和可用性群組，建立高可用性和災害復原方案](https://technet.microsoft.com/library/jj215886.aspx)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|是|是|不適用|** (IPsec) 的網際網路通訊協定安全性**|如果您的環境使用 IPsec 連接，當用戶端電腦重新建立虛擬網路名稱的 IPsec 連接 (在本文中，連接至可用性群組接聽程式) 時，您會遇到長時間的延遲 (大約二或三分鐘)。 如果您使用 IPsec 連接，我們建議您檢閱知識庫文件 (KB 980915) 中詳述的特定案例。|KB 980915：  [當您從執行 Windows Server 2003、Windows Vista、Windows Server 2008、Windows 7 或 Windows Server 2008 R2 的電腦重新連接 IPSec 連接時發生長時間延遲](https://support.microsoft.com/kb/980915)(機器翻譯)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|是|是|是|**Ipv4**|如果您使用 IPv6，我們建議您根據自己的 Windows Server 作業系統，檢閱知識庫文件 2578103 或 2578113 中詳述的特定案例。<br /><br /> 如果您的 Windows Server 拓撲使用 IP 第 6 版 (IPv6)，WSFC 叢集服務大約需要 30 秒來容錯移轉 IPv6 IP 位址。 這會導致用戶端大約等候 30 秒，然後再重新連接到 IPv6 IP 位址。|KB 2578103 (Windows Server 2008)：[The Cluster service takes about 30 seconds to fail over IPv6 IP addresses in Windows Server 2008](https://support.microsoft.com/kb/2578103) (叢集服務大約需要 30 秒時間容錯移轉 Windows Server 2008 中的 IPv6 IP 位址)<br /><br /> KB 2578113 (Windows Server 2008 R2)：**Windows Server 2008 R2：** [The Cluster service takes about 30 seconds to fail over IPv6 IP addresses in Windows Server 2008 R2](https://support.microsoft.com/kb/2578113) (叢集服務大約需要 30 秒時間容錯移轉 Windows Server 2008 R2 中的 IPv6 IP 位址)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|是|是|是|**叢集和應用程式伺服器之間沒有路由器**|如果容錯移轉叢集與應用程式伺服器之間不存在任何路由器，叢集服務就會緩慢地容錯移轉網路相關資源。 在可用性群組容錯移轉之後，這會延遲用戶端重新連接。 如果路由器不存在，我們建議您檢閱知識庫文件 2582281 中詳述的特定案例並安裝 Hotfix (如果適用於環境的話)。|KB 2582281：  [如果叢集與應用程式伺服器之間不存在任何路由器，就會緩慢地進行容錯移轉作業](https://support.microsoft.com/kb/2582281)(機器翻譯)|  
  
###  <a name="recommendations-for-computers-that-host-availability-replicas-windows-system"></a><a name="ComputerRecommendations"></a> 對裝載可用性複本之電腦的建議 (Windows 系統)  
  
-   **可比較的系統：** 對於指定的可用性群組而言，所有可用性複本都應該在可處理相同工作負載的可相比系統上執行。  
  
-   **專用的網路介面卡：** 為達最佳效能，請針對 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 使用專用的網路介面卡 (NIC)。  
  
-   **足夠的磁碟空間：** 伺服器執行個體裝載可用性複本的每部電腦都必須擁有足夠的磁碟空間，才能容納可用性群組中的所有資料庫。 請牢記，當主要資料庫成長時，其對應的次要資料庫也會成長相同的數量。  
  
###  <a name="permissions-windows-system"></a><a name="PermissionsWindows"></a> 權限 (Windows 系統)  
 若要管理 WSFC 叢集，使用者必須是每個叢集節點上的系統管理員。  
  
 如需管理叢集之帳戶的詳細資訊，請參閱[附錄 A：容錯移轉叢集需求](https://technet.microsoft.com/library/dd197454\(WS.10\).aspx)。  
  
###  <a name="related-tasks-windows-system"></a><a name="RelatedTasksWindows"></a> 相關工作 (Windows 系統)  
  
|Task|連結|  
|----------|----------|  
|設定 HostRecordTTL 值。|[變更 HostRecordTTL (使用 Windows PowerShell)](#ChangeHostRecordTTLps)|  
  
####  <a name="change-the-hostrecordttl-using-windows-powershell"></a><a name="ChangeHostRecordTTLps"></a> 變更 HostRecordTTL (使用 Windows PowerShell)  
  
1.  透過 **[以系統管理員身分執行]** 開啟 PowerShell 視窗。  
  
2.  匯入 FailoverClusters 模組。  
  
3.  使用 `Get-ClusterResource` 指令程式尋找網路名稱資源，然後使用 `Set-ClusterParameter` 指令程式設定 `HostRecordTTL` 值，如下所示：  
  
     Get-ClusterResource " *\<NetworkResourceName>* " | Set-ClusterParameter HostRecordTTL *\<TimeInSeconds>*  
  
     下列 PowerShell 範例會針對名為 "`SQL Network Name (SQL35)`" 的網路名稱資源將 HostRecordTTL 設定為 300 秒。  
  
    ```powershell
    Import-Module FailoverClusters  
  
    $nameResource = "SQL Network Name (SQL35)"  
    Get-ClusterResource $nameResource | Set-ClusterParameter ClusterParameter HostRecordTTL 300  
    ```  
  
    > [!TIP]  
    >  每次開啟新的 PowerShell 視窗時，都需要匯入 `FailoverClusters` 模組。  
  
##### <a name="related-content-powershell"></a>相關內容 (PowerShell)  
  
-   [Clustering and High-Availability](https://techcommunity.microsoft.com/t5/failover-clustering/bg-p/FailoverClustering) (叢集和高可用性 - 容錯移轉叢集和網路負載平衡團隊部落格)  
  
-   [在容錯移轉叢集上開始使用 Windows PowerShell](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [叢集資源命令和對等的 Windows PowerShell 指令程式](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
###  <a name="related-content-windows-system"></a><a name="RelatedContentWS"></a> 相關內容 (Windows 系統)  
  
-   [在多網站容錯移轉叢集中設定 DNS 設定](https://technet.microsoft.com/library/dd197562\(WS.10\).aspx)  
  
-   [網路名稱資源的 DNS 註冊](https://techcommunity.microsoft.com/t5/failover-clustering/dns-registration-with-the-network-name-resource/ba-p/371482)  
  
-   [Windows 2008 R2 容錯移轉多站台叢集](https://kiruba4u.blogspot.com/2012/03/failover-clustering-in-windows-server.html)  
  
##  <a name="sql-server-instance-prerequisites-and-restrictions"></a><a name="ServerInstance"></a> SQL Server 執行個體的必要條件和限制  
 每個可用性群組都需要 *執行個體所裝載的一組容錯移轉夥伴，稱為*「可用性複本」 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)](Availability Replica)。 給定的伺服器執行個體可以是「獨立執行個體」或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]「容錯移傳叢集執行個體」 (FCI)。  
  
 
  
###  <a name="checklist-prerequisites-server-instance"></a><a name="PrerequisitesSI"></a> 檢查清單：必要條件 (伺服器執行個體)  
  
||必要條件|連結|  
|-|------------------|-----------|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|主機電腦必須是 Windows Server 容錯移轉叢集 (WSFC) 節點。 裝載給定可用性群組之可用性複本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體，必須位於單一 WSFC 叢集的不同節點上。 唯一的例外狀況是在移轉至另一個 WSFC 叢集期間，可用性群組可以暫時跨兩個叢集。|[SQL Server 的 Windows Server 容錯移轉叢集 &#40;WSFC&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)<br /><br /> [容錯移轉叢集和 AlwaysOn 可用性群組 &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|若要讓可用性群組使用 Kerberos：<br /><br /> 裝載可用性群組之可用性複本的所有伺服器執行個體都必須使用相同的 SQL Server 服務帳戶。<br /><br /> 網域管理員需要針對可用性群組接聽程式之虛擬網路名稱 (VNN) 的 SQL Server 服務帳戶，在 Active Directory 中手動註冊伺服器主體名稱 (SPN)。 如果對 SQL Server 服務帳戶以外的帳戶註冊 SPN，驗證會失敗。<br /><br /> **\*\* 重要 \*\*** 如果您變更 SQL Server 服務帳戶，網域管理員需要手動重新註冊 SPN。|[註冊 Kerberos 連接的服務主體名稱](../../configure-windows/register-a-service-principal-name-for-kerberos-connections.md)<br /><br /> **簡短說明：**<br /><br /> Kerberos 和 SPN 強制執行相互驗證。 SPN 對應到啟動 SQL Server 服務的 Windows 帳戶。 如果不正確地註冊 SPN 或註冊作業失敗，則 Windows 安全層無法判斷與 SPN 相關聯的帳戶，也無法使用 Kerberos 驗證。<br /><br /> 注意:NTLM 沒有此需求。|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|如果您計劃使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體 (FCI) 來裝載可用性複本，請務必了解 FCI 限制且符合 FCI 需求。|[使用 SQL Server 容錯移轉叢集執行個體 (FCI) 裝載可用性複本的必要條件和限制](#FciArLimitations) (本主題稍後)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|每個伺服器執行個體都必須執行 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]Enterprise Edition。|[SQL Server 2014 各版本所支援的功能](../../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|裝載可用性群組之可用性複本的所有伺服器執行個體都必須使用相同的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 定序。|[設定或變更伺服器定序](../../../relational-databases/collations/set-or-change-the-server-collation.md)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|在將要裝載任何可用性群組之可用性複本的每個伺服器執行個體上，啟用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 功能。 在給定的電腦上，只要 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 安裝有支援，您就可以對多個伺服器執行個體啟用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。|[啟用和停用 AlwaysOn 可用性群組 &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)<br /><br /> 重要如果您刪除並重新建立 WSFC 叢集，則必須在** \* 原始 WSFC 叢集上已啟用的每個伺服器實例上，停用並重新啟用此功能。 \* \* \* ** [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|每一個伺服器執行個體都需要資料庫鏡像端點。 請注意，伺服器執行個體上的所有可用性複本、資料庫鏡像夥伴和見證都會共用此端點。<br /><br /> 如果您選取來裝載可用性複本的伺服器執行個體在網域使用者帳戶下執行，而且還沒有資料庫鏡像端點， [新增可用性群組精靈](use-the-availability-group-wizard-sql-server-management-studio.md) (或 [新增複本至可用性群組精靈](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)) 可以建立端點並授與伺服器執行個體服務帳戶 CONNECT 權限。 但是，如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務是以內建帳戶 (例如本機系統、本機服務或網路服務) 或非網域帳戶的身分執行，您就必須將憑證用於端點驗證，而且精靈無法在此伺服器執行個體上建立資料庫鏡像端點。 在此情況下，我們建議您先手動建立資料庫鏡像端點，然後再啟動精靈。<br /><br /> **\*\* 安全性注意事項 \*\***[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 的傳輸安全性與資料庫鏡像相同。|[資料庫鏡像端點 &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)<br /><br /> [資料庫鏡像和 AlwaysOn 可用性群組的傳輸安全性 &#40;SQL Server&#41;](../../database-mirroring/transport-security-database-mirroring-always-on-availability.md)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|如果使用 FILESTREAM 的任何資料庫將要加入至可用性群組，請確定即將裝載可用性群組之可用性複本的每個伺服器執行個體都啟用了 FILESTREAM。|[啟用及設定 FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|如果任何自主資料庫將要加入至可用性群組，請確定在即將裝載可用性群組之可用性複本的每個伺服器執行個體，`contained database authentication` 伺服器選項都設為 `1`。|[自主資料庫驗證伺服器組態選項](../../configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [伺服器組態選項 &#40;SQL Server&#41;](../../configure-windows/server-configuration-options-sql-server.md)|  
  
###  <a name="thread-usage-by-availability-groups"></a><a name="ThreadUsage"></a> 可用性群組的執行緒使用量  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 有下列工作者執行緒的需求：  
  
-   在閒置的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體上， [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 使用 0 個執行緒。  
  
-   可用性群組使用之執行緒的最大數目是伺服器執行緒最大數目的設定值 ('`max worker threads`') 減 40。  
  
-   裝載在給定伺服器執行個體上的可用性複本共用單一執行緒集區。  
  
     視需要共用執行緒，如下所示：  
  
    -   一般而言，有 3-10 個共用的執行緒，但這個數目會根據主要複本的工作負載而增加。  
  
    -   如果給定的執行緒已經閒置一段時間，它會釋放回一般 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行緒集區。 一般而言，非使用中的執行緒在 ~15 秒非使用狀態之後釋出。 不過，根據上一個活動，閒置執行緒可能會保留更久。  
  
-   此外，可用性群組也使用不共用的執行緒，如下所示：  
  
    -   每個主要複本會針對每個主要資料庫使用 1 個記錄檔擷取執行緒。 此外，它會針對每個次要資料庫使用 1 個記錄檔傳送執行緒。 記錄檔傳送執行緒在 ~15 秒非使用狀態之後釋出。  
  
    -   每個次要複本會針對每個次要資料庫使用 1 個重做執行緒。 重做傳送執行緒在 ~15 秒非使用狀態之後釋出。  
  
    -   次要複本上的備份會在備份作業的持續時間內保留主要複本上的執行緒。  
  
 如需詳細資訊，請參閱 [AlwaysON - HADRON 學習系列：資料庫啟用 HADRON 時背景工作集區的使用方式](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx) (CSS [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 工程師部落格)。  
  
###  <a name="permissions-server-instance"></a><a name="PermissionsSI"></a> 權限 (伺服器執行個體)  
  
|Task|必要權限|  
|----------|--------------------------|  
|建立資料庫鏡像端點|需要 CREATE ENDPOINT 權限或 **系統管理員 (sysadmin)** 固定伺服器角色的成員資格。  也需要 CONTROL ON ENDPOINT 權限。 如需詳細資訊，請參閱 [GRANT 端點權限 &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql)。|  
|啟用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]|需要本機電腦的 **Administrator** 群組成員資格和 WSFC 叢集的完整控制。|  
  
###  <a name="related-tasks-server-instance"></a><a name="RelatedTasksSI"></a> 相關工作 (伺服器執行個體)  
  
|Task|主題|  
|----------|-----------|  
|判斷資料庫鏡像端點是否存在|[sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)|  
|建立資料庫鏡像端點 (如果尚未存在)|[建立 Windows 驗證的資料庫鏡像端點 &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)<br /><br /> [使用資料庫鏡像端點憑證 &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)<br /><br /> [建立 AlwaysOn 可用性群組 &#40;SQL Server PowerShell 的資料庫鏡像端點&#41;](database-mirroring-always-on-availability-groups-powershell.md)|  
|啟用 AlwaysOn 可用性群組|[啟用和停用 AlwaysOn 可用性群組 &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)|  
  
###  <a name="related-content-server-instance"></a><a name="RelatedContentSI"></a> 相關內容 (伺服器執行個體)  
  
-   [AlwaysON - HADRON 學習系列：具備 HADRON 功能之資料庫的工作者集區使用方式](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
##  <a name="network-connectivity-recommendations"></a><a name="NetworkConnect"></a> 網路連線建議  
 我們強烈建議您針對 WSFC 叢集成員之間的通訊及可用性複本之間的通訊使用相同的網路連結。  使用不同的網路連結時，部分連結失敗 (或甚至間歇性失敗) 可能會發生意外的行為。  
  
 例如，如果希望可用性群組支援自動容錯移轉，則屬於自動容錯移轉夥伴的次要複本必須處於 SYNCHRONIZED 狀態。 如果此次要複本的網路連結失敗 (或甚至間歇性失敗)，此複本會進入 UNSYNCHRONIZED 狀態，而且要等到還原連結之後才會開始重新同步處理。 如果 WSFC 叢集在次要複本未同步處理時要求自動容錯移轉，則不會發生自動容錯移轉。  
  
##  <a name="client-connectivity-support"></a><a name="ClientConnSupport"></a> 用戶端連接性支援  
 如需有關 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 用戶端連線支援的詳細資訊，請參閱[AlwaysOn client connectivity (SQL Server) ](always-on-client-connectivity-sql-server.md)。  
  
##  <a name="prerequisites-and-restrictions-for-using-a-sql-server-failover-cluster-instance-fci-to-host-an-availability-replica"></a><a name="FciArLimitations"></a> 使用 SQL Server 容錯移轉叢集執行個體 (FCI) 裝載可用性複本的必要條件和限制  
 
  
###  <a name="restrictions-fcis"></a><a name="RestrictionsFCI"></a> 限制 (FCI)  
  
> [!NOTE]  
>  從 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 開始，AlwaysOn 容錯移轉叢集執行個體在 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] 和 [!INCLUDE[win8srv](../../../includes/win8srv-md.md)] 中都支援叢集共用磁碟區 (CSV)。 如需有關 CSV 的詳細資訊，請參閱 [了解容錯移轉叢集的叢集共用磁碟區](https://technet.microsoft.com/library/dd759255.aspx)。  
  
-   **FCI 的叢集節點只能針對給定的可用性群組裝載一個複本：**  如果您在 FCI 上加入可用性複本，則可能是 FCI 擁有者的 WSFC 叢集節點將無法針對相同的可用性群組裝載另一個複本。  
  
     此外，其他每個複本都必須由相同 WSFC 叢集中之不同 WSFC 節點上的 SQL Server 2012 執行個體裝載。 唯一的例外狀況是在移轉至另一個 WSFC 叢集期間，可用性群組可以暫時跨兩個叢集。  
  
-   **FCI 不支援依照可用性群組自動容錯移轉：** FCI 不支援依照可用性群組進行自動容錯移轉，因此任何由 FCI 裝載的可用性複本只能設定為手動容錯移轉。  
  
-   **變更 FCI 網路名稱：** 如果您需要對裝載可用性複本的 FCI 變更網路名稱，則需要從其可用性群組移除複本，然後將複本重新新增至可用性群組。 您無法移除主要複本，因此如果要對裝載可用性複本的 FCI 重新命名，應該容錯移轉至次要複本，然後移除先前的主要複本並重新加回。 請注意重新命名 FCI 可能改變其資料庫鏡像端點的 URL。 當您加入複本時，請務必指定目前端點的 URL。  
  
###  <a name="checklist-prerequisites-fcis"></a><a name="PrerequisitesFCI"></a> 檢查清單：必要條件 (FCI)  
  
||必要條件|連結|  
|-|------------------|----------|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|使用 FCI 裝載可用性複本之前，請先確定系統管理員已安裝知識庫文件 KB 976097 中所述的 Windows Server 2008 Hotfix。 此修補程式可讓「容錯移轉叢集管理」 Microsoft Management Console (MMC) 嵌入式管理單元支援只能在部分 WSFC 節點上使用的非對稱式儲存體共用磁片。|KB 976097：[Hotfix to add support for asymmetric storages to the Failover Cluster Management MMC snap-in for a failover cluster that is running Windows Server 2008 or Windows Server 2008 R2](https://support.microsoft.com/kb/976097) (對於執行 Windows Server 2008 或 Windows Server 2008 R2 之容錯移轉叢集的容錯移轉叢集管理 MMC 嵌入式管理單元，Hotfix 新增非對稱儲存支援)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|依照標準 SQL Server 容錯移轉叢集執行個體安裝，確定每個 SQL Server 容錯移轉叢集執行個體 (FCI) 都擁有必要的共用儲存體。||  
  
###  <a name="related-tasks-fcis"></a><a name="RelatedTasksFCIs"></a> 相關工作 (FCI)  
  
|Task|主題|  
|----------|-----------|  
|安裝 SQL Server 容錯移轉叢集|[建立新的 SQL Server 容錯移轉叢集 &#40;安裝程式&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|現有 SQL Server 容錯移轉叢集的就地升級|[升級 SQL Server 容錯移轉叢集執行個體 &#40;安裝程式&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)|  
|維護現有 SQL Server 容錯移轉叢集|[在 SQL Server 容錯移轉叢集中新增或移除節點 &#40;安裝程式&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
  
###  <a name="related-content-fcis"></a><a name="RelatedContentFCIs"></a> 相關內容 (FCIs)  
  
-   [容錯移轉叢集和 AlwaysOn 可用性群組 &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)  
  
-   [AlwaysOn 架構指南：使用容錯移轉叢集執行個體和可用性群組，建立高可用性和災害復原方案](https://technet.microsoft.com/library/jj215886.aspx)  
  
##  <a name="availability-group-prerequisites-and-restrictions"></a><a name="PrerequisitesForAGs"></a> 可用性群組的必要條件和限制  

  
###  <a name="restrictions-availability-groups"></a><a name="RestrictionsAG"></a> 限制 (可用性群組)  
  
-   **可用性複本必須由一個 WSFC 叢集中的不同節點所裝載**  ：對於給定的可用性群組而言，可用性複本必須由在相同 WSFC 叢集中不同節點上執行的伺服器執行個體所裝載。 唯一的例外狀況是在移轉至另一個 WSFC 叢集期間，可用性群組可以暫時跨兩個叢集。  
  
    > [!NOTE]  
    >  同一部實體電腦上的虛擬機器可各自裝載相同可用性群組的可用性複本，因為每部虛擬機器都會當做個別的電腦。  
  
-   **唯一的可用性群組名稱**  ：每個可用性群組名稱在 WSFC 叢集上都必須是唯一的。 可用性群組名稱的最大長度為 128 個字元。  
  
-   **可用性複本：** 每個可用性群組都支援一個主要複本和最多八個次要複本。 所有複本都可以在非同步認可模式下執行，或其中多達三個複本可以在同步認可模式下執行 (一個主要複本並且包含兩個同步次要複本)。  
  
-   **每一部電腦之可用性群組和可用性資料庫的最大數量：** 您可以放到電腦的資料庫和可用性群組 (VM 或實體) 的實際數量取決於硬體和工作負載，但沒有強制執行的限制。 Microsoft 對每部實體電腦 10 AG 和 100 DB 進行過廣泛測試。 超載系統的徵狀包括 (但不限於) 工作者執行緒耗盡、AlwaysOn 系統檢視和 DMV 的回應時間緩慢，及/或停止的發送器系統傾印。 請確實透過類似實際執行的工作負載徹底測試您的環境，確保其能夠在應用程式 SLA 範圍內處理尖峰工作負載容量。 在考量 SLA 的情況下，務必考慮失敗情況下的負載，以及預期的回應時間。  
  
-   **請勿使用容錯移轉叢集管理員來操作可用性群組：**  
  
     例如：  
  
    -   不要變更任何可用性群組屬性，例如可能的擁有者。  
  
    -   不要使用容錯移轉叢集管理員進行可用性群組的容錯移轉。 您必須使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]。  
  
###  <a name="prerequisites-availability-groups"></a><a name="RequirementsAG"></a> 必要條件 (可用性群組)  
 在建立或重新設定可用性群組組態時，請務必遵守下列需求。  
  
||必要條件|描述|  
|-|------------------|-----------------|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|如果您計劃使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體 (FCI) 來裝載可用性複本，請務必了解 FCI 限制且符合 FCI 需求。|[使用 SQL Server 容錯移轉叢集執行個體 (FCI) 裝載可用性複本的必要條件和限制](#FciArLimitations) (本主題稍早所述)|  
  
###  <a name="security-availability-groups"></a><a name="SecurityAG"></a> 安全性 (可用性群組)  
  
-   安全性是從 Windows Server 容錯移轉叢集 (WSFC) 叢集繼承。 在整個 WSFC 叢集 API 的資料粒度，WSFC 提供了兩個層級的使用者安全性：  
  
    -   唯讀存取  
  
    -   完整控制  
  
         [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 需要完整控制，而於 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 執行個體上啟用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，可使其對 WSFC 叢集有完整控制 (透過服務 SID).  
  
         不能在 WSFC 容錯移轉叢集管理員直接加入或移除伺服器執行個體的安全性。 若要管理 WSFC 安全性工作階段，請使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 組態管理員或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的 WMI 對等工具。  
  
-   每個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體都必須有權限可存取登錄、叢集等項目。  
  
-   我們建議您針對裝載 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 可用性複本的伺服器執行個體之間的連接使用加密。  
  
#### <a name="permissions-availability-groups"></a>權限 (可用性群組)  
  
|Task|必要權限|  
|----------|--------------------------|  
|建立可用性群組|需要 **系統管理員 (sysadmin)** 固定伺服器角色的成員資格，以及 CREATE AVAILABILITY GROUP 伺服器權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。|  
|改變可用性群組|需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。<br /><br /> 此外，將資料庫聯結至可用性群組需要 **db_owner** 固定資料庫角色的成員資格。|  
|卸除/刪除可用性群組|需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。 若要卸除本機複本位置所未裝載的可用性群組，您需要該可用性群組的 CONTROL SERVER 權限或 CONTROL 權限。|  
  
###  <a name="related-tasks-availability-groups"></a><a name="RelatedTasksAGs"></a> 相關工作 (可用性群組)  
  
|Task|主題|  
|----------|-----------|  
|建立可用性群組|[使用可用性群組 (新增可用性群組精靈)](use-the-availability-group-wizard-sql-server-management-studio.md)<br /><br /> [建立可用性群組 (Transact-SQL)](create-an-availability-group-transact-sql.md)<br /><br /> [建立可用性群組 (SQL Server PowerShell)](../../../powershell/sql-server-powershell.md)<br /><br /> [在新增或修改可用性複本時指定端點 URL &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)|  
|修改可用性複本的數目|[將次要複本加入至可用性群組 &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [將次要複本聯結至可用性群組 &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [將次要複本從可用性群組移除 &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)|  
|建立可用性群組接聽程式|[建立或設定可用性群組接聽程式 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)|  
|卸除可用性群組|[移除可用性群組 &#40;SQL Server&#41;](remove-an-availability-group-sql-server.md)|  
  
##  <a name="availability-database-prerequisites-and-restrictions"></a><a name="PrerequisitesForDbs"></a> 可用性資料庫的必要條件和限制  
 資料庫必須符合下列必要條件和限制，才適合加入至可用性群組。  
  
 
  
###  <a name="checklist-requirements-availability-databases"></a><a name="RequirementsDb"></a> 檢查清單：需求 (可用性資料庫)  
 資料庫必須擁有下列資格，才能加入至可用性群組：  
  
||需求|連結|  
|-|------------------|----------|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|必須是使用者資料庫。 系統資料庫不得屬於可用性群組。||  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|位於建立可用性群組的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上，而且伺服器執行個體能夠存取它。||  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|必須是讀取/寫入資料庫。 唯讀資料庫不得加入至可用性群組。|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**is_read_only** = 0)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|必須是多使用者資料庫。|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**user_access** = 0)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|不使用 AUTO_CLOSE。|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**is_auto_close_on** = 0)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|使用完整復原模式 (也稱為完整復原模式)。|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**recovery_model** = 1)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|至少擁有一個完整資料庫備份。<br /><br /> 注意:將資料庫設為完整復原模式之後，需要完整備份以起始完整復原記錄檔鏈結。|[建立完整資料庫備份 &#40;SQL Server&#41;](../../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|不屬於任何現有的可用性群組。|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**group_database_id** = NULL)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|並未設定資料庫鏡像。|[sys.database_mirroring](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql) (如果資料庫未參與鏡像，前置詞為 "mirroring_" 的所有資料行都是 NULL)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|將使用 FILESTREAM 的資料庫加入至可用性群組之前，請確定 (將要) 裝載可用性群組之可用性複本的每個伺服器執行個體都啟用了 FILESTREAM。|[啟用及設定 FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|![核取方塊](../../media/checkboxemptycenterxtraspacetopandright.gif "核取方塊")|將自主資料庫加入至可用性群組之前，請確定在 (將要) 裝載可用性群組之可用性複本的每個伺服器執行個體，`contained database authentication` 伺服器選項都設為 `1`。|[自主資料庫驗證伺服器組態選項](../../configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [伺服器組態選項 &#40;SQL Server&#41;](../../configure-windows/server-configuration-options-sql-server.md)|  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]可搭配任何支援的資料庫相容性層級使用。  
  
###  <a name="restrictions-availability-databases"></a><a name="RestrictionsDb"></a> 限制 (可用性資料庫)  
  
-   如果次要資料庫的檔案路徑 (包括磁碟機代號) 不同於對應主要資料庫的路徑，下列限制適用：  
  
    -   **[!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]/[!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)]：** 不支援 [完整] 選項 (在[選取初始資料同步處理頁面](select-initial-data-synchronization-page-always-on-availability-group-wizards.md))，  
  
    -   **RESTORE WITH MOVE：** 若要建立次要資料庫，在裝載次要複本的每個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上，資料庫檔案必須是 RESTORED WITH MOVE。  
  
    -   **對新增檔案作業的影響：** 在次要資料庫上，對主要複本稍後的新增檔案作業可能會失敗。 此失敗可能導致次要資料庫暫停。 而這又會導致次要複本進入 NOT SYNCHRONIZING 狀態。  
  
        > [!NOTE]  
        >  如需回應失敗之新增檔案作業的相關資訊，請參閱[疑難排解失敗的新增檔案作業 &#40;AlwaysOn 可用性群組&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)。  
  
-   您無法卸除目前屬於可用性群組的資料庫。  
  
###  <a name="follow-up-for-tde-protected-databases"></a><a name="TDEdbs"></a> 追蹤 TDE 保護的資料庫  
 如果您使用透明資料加密 (TDE)，用來建立及解密其他金鑰的憑證或非對稱金鑰在裝載可用性群組之可用性複本的每一個伺服器執行個體上都必須相同。 如需詳細資訊，請參閱 [將 TDE 保護的資料庫移至另一個 SQL Server](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)。  
  
###  <a name="permissions-availability-databases"></a><a name="PermissionsDbs"></a> 權限 (可用性資料庫)  
 需要資料庫的 ALTER 權限。  
  
###  <a name="related-tasks-availability-databases"></a><a name="RelatedTasksADb"></a> 相關工作 (可用性資料庫)  
  
|Task|主題|  
|----------|-----------|  
|準備次要資料庫 (手動)|[針對可用性群組手動準備次要資料庫 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)|  
|將次要資料庫聯結至可用性群組 (手動)|[將次要資料庫聯結至可用性群組 &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)|  
|修改可用性資料庫的數目|[將資料庫加入至可用性群組 &#40;SQL Server&#41;](availability-group-add-a-database.md)<br /><br /> [將次要資料庫從可用性群組移除 &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)<br /><br /> [將主要資料庫從可用性群組移除 &#40;SQL Server&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)|  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 相關內容  
  
-   [Microsoft SQL Server AlwaysOn 高可用性和災害復原方案指南](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [SQL Server AlwaysOn 團隊部落格：官方 SQL Server AlwaysOn 團隊部落格](https://blogs.msdn.com/b/sqlalwayson/)  
  
-   [AlwaysON - HADRON 學習系列：具備 HADRON 功能之資料庫的工作者集區使用方式](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [容錯移轉叢集和 AlwaysOn 可用性群組 &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 用戶端連接性 (SQL Server)](always-on-client-connectivity-sql-server.md)  
  
  
