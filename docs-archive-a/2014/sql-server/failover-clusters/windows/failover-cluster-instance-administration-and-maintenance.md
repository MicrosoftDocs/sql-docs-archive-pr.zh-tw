---
title: 容錯移轉叢集執行個體管理及維護 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- user accounts [SQL Server], failover clustering
- clusters [SQL Server], maintaining
- nodes [Faillover Clustering]
- failover clustering [SQL Server], maintaining
- adding nodes
- virtual servers [SQL Server], removing nodes
- clustered instance of SQL Server
- nodes [Faillover Clustering], removing
- nodes [Faillover Clustering], adding
- service accounts [SQL Server]
- removing nodes
- virtual servers [SQL Server], adding nodes
ms.assetid: 2d5c63e9-8061-45c3-94db-8dd3100b8a91
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 059d052402a1ad486c28a211585022bd67bcf3d2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595569"
---
# <a name="failover-cluster-instance-administration-and-maintenance"></a>容錯移轉叢集執行個體管理及維護
  從現有 AlwaysOn 容錯移轉叢集執行個體 (FCI) 中加入或移除節點這類的維護工作是使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式來完成。 其他管理工作 (例如變更 IP 位址資源、從特定 FCI 案例復原) 則是使用容錯移轉叢集管理員嵌入式管理單元 (Windows Server 容錯移轉叢集 (WSFC) 服務的嵌入式管理單元) 來完成。  
  
## <a name="maintaining-a-failover-cluster-instance"></a>維護容錯移轉叢集執行個體  
 安裝 FCI 之後，您可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式變更或修復該叢集。 例如，您可以將額外的節點新增到 FCI、執行 FCI 做為獨立的執行個體，或從 FCI 組態中移除節點。  
  
### <a name="adding-a-node-to-an-existing-failover-cluster-instance"></a>將節點加入現有的容錯移轉叢集執行個體  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式提供維護現有 FCI 的選項。 如果選擇這個選項，則可以在要加入 FCI 的電腦上執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式，將其他的節點加入 FCI。 如需詳細資訊，請參閱[建立新的 SQL Server 容錯移轉叢集 &#40;Setup&#41;](../install/create-a-new-sql-server-failover-cluster-setup.md) 和[在 SQL Server 容錯移轉叢集中加入或移除節點 &#40;Setup&#41;](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)。  
  
### <a name="removing-a-node-from-an-existing-failover-cluster-instance"></a>從現有的容錯移轉叢集執行個體移除節點  
 您可以在要從 FCI 移除的電腦上執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式，以從 FCI 移除節點。 FCI 內的每個節點都視為與 FCI 上其他節點無相依性的對等，而您可以將任何節點移除。 損毀的節點即使無法使用也可移除，而且移除程序將不會從無法使用的節點中解除安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 二進位編碼檔案。 已移除的節點可以隨時再加入 FCI。 如需詳細資訊，請參閱[在 SQL Server 容錯移轉叢集中新增或移除節點 &#40;安裝程式&#41;](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)。  
  
### <a name="changing-service-accounts"></a>變更服務帳戶  
 當 FCI 節點關閉或離線時，您不可以變更任何 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務帳戶的密碼。 如果您變更了帳戶密碼，就必須在所有的節點都恢復連線工作時，使用「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 組態管理員」重新設定密碼。  
  
 如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的服務帳戶並不是叢集中的系統管理員，就無法刪除叢集中任何節點的管理共用。 叢集中的管理共用必須可供使用， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 才能運作。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務帳戶與 WSFC 服務帳戶請不要使用相同的帳戶。 如果變更 WSFC 服務帳戶的密碼， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝將會失敗。  
  
 在 [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]上，服務 SID 用於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務帳戶。 如需詳細資訊，請參閱 [設定 Windows 服務帳戶與權限](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)預覽版本升級問題的解答。  
  
## <a name="administering-a-failover-cluster-instance"></a>管理容錯移轉叢集執行個體  
  
|工作描述|主題連結|  
|----------------------|----------------|  
|描述如何加入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資源的相依性。|[加入 SQL Server 資源的相依性](add-dependencies-to-a-sql-server-resource.md)|  
|Kerberos 是一種網路驗證通訊協定，可為用戶端/伺服器應用程式提供強大的驗證功能。 Kerberos 可做為交互操作的基礎，並且協助提升整個企業的網路驗證安全性。 您可以將 Kerberos 驗證搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 獨立執行個體或搭配 AlwaysOn FCI 使用。|[註冊 Kerberos 連接的服務主體名稱](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)。|  
|提供描述如何啟用 Kerberos 驗證之內容的連結||  
|描述用以從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集失敗中復原的程序。|[從容錯移轉叢集實例失敗復原](recover-from-failover-cluster-instance-failure.md)|  
|描述用於變更 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體之 IP 位址資源的程序。|[變更容錯移轉叢集執行個體的 IP 位址](change-the-ip-address-of-a-failover-cluster-instance.md)|  
  
## <a name="see-also"></a>另請參閱  
 [設定 HealthCheckTimeout 屬性設定](configure-healthchecktimeout-property-settings.md)   
 [設定 FailureConditionLevel 屬性設定](configure-failureconditionlevel-property-settings.md)   
 [檢視及閱讀容錯移轉叢集執行個體診斷記錄檔](view-and-read-failover-cluster-instance-diagnostics-log.md)  
  
  
