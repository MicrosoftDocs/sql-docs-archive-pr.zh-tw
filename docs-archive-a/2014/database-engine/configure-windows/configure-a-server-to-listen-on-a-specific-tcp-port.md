---
title: 設定伺服器接聽特定 TCP 通訊埠 (SQL Server 組態管理員) |Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- fixed port
- static ports
- ports [SQL Server], assigning numbers
- assigning port numbers
- dynamic ports [SQL Server]
- TCP/IP [SQL Server], port numbers
ms.assetid: 2276a5ed-ae3f-4855-96d8-f5bf01890640
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4feb740910c65580e8ea3170d03481e6cb628860
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585597"
---
# <a name="configure-a-server-to-listen-on-a-specific-tcp-port-sql-server-configuration-manager"></a>設定伺服器接聽特定 TCP 通訊埠 (SQL Server 組態管理員)
  此主題描述如何使用 SQL Server 組態管理員，將 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體設定為在特定固定通訊埠上接聽。 當啟用時，預設的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體會在 TCP 通訊埠 1433 上接聽。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 的具名執行個體是針對動態通訊埠所設定。 這表示，當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務啟動時，它們會選取可用的通訊埠。 透過防火牆連接到具名執行個體時，設定 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 接聽特定通訊埠，如此才能在防火牆中開啟適當的通訊埠。  
  
 如需預設 Windows 防火牆設定的詳細資訊以及影響 Database Engine、Analysis Services、Reporting Services 和 Integration Services 之 TCP 通訊埠的描述，請參閱 [設定 Windows 防火牆以允許 SQL Server 存取](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
> [!TIP]  
>  選取通訊埠編號時，請參閱 [http://www.iana.org/assignments/port-numbers](http://www.iana.org/assignments/port-numbers)，以取得指派給特定應用程式的通訊埠編號清單。 選取未指派的通訊埠編號。 如需詳細資訊，請參閱 [The default dynamic port range for TCP/IP has changed in Windows Vista and in Windows Server 2008](https://support.microsoft.com/kb/929851)(在 Windows Vista 和 Windows Server 2008 中，TCP/IP 的預設動態通訊埠範圍已變更)。  
  
> [!WARNING]  
>  資料庫引擎會在重新啟動之後開始接聽新的通訊埠。 不過， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務會監視登錄，並在組態變更時回報新的通訊埠編號，即使資料庫引擎可能不會用到亦然。 重新啟動資料庫引擎可確保一致性並避免連接失敗。  
  
 **本主題內容**  
  
-   **若要使用下列項目，將伺服器設定為在特定 TCP 通訊埠上接聽：**  
  
     [SQL Server 組態管理員](#SSMSProcedure)  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> 使用 SQL Server 組態管理員  
  
#### <a name="to-assign-a-tcpip-port-number-to-the-sql-server-database-engine"></a>若要為 SQL Server Database Engine 指派 TCP/IP 通訊埠編號  
  
1.  在 [SQL Server 組態管理員] 的主控台窗格中，依序展開 [SQL Server 網路組態] 和 [\<instance name> 的通訊協定]，然後按兩下 [TCP/IP]。  
  
2.  在 [TCP/IP 內容] 對話方塊的 [IP 位址] 索引標籤上會出現數個 IP 位址，這些 IP 位址的格式是 **IP1**、**IP2** 到 **IPAll**。 其中一個是供回送介面卡的 IP 位址 127.0.0.1 使用。 同時會出現額外的 IP 位址代表電腦上的每個 IP 位址。 以滑鼠右鍵按一下每個位址，然後按一下 [屬性]**** 以識別要設定的 IP 位址。  
  
3.  如果 **[TCP 動態通訊埠]** 對話方塊包含 **0**，代表 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 正在接聽動態通訊埠，請將 0 刪除。  
  
4.  在 [IP_n_ 屬性]  區域方塊的 [TCP 通訊埠] 方塊中，鍵入您想要讓此 IP 位址接聽的連接埠號碼，然後按一下 [確定]。  
  
5.  在主控台窗格中，按一下 [SQL Server 服務]。  
  
6.  在 [詳細資料窗格] 中，以滑鼠右鍵按一下 [SQL Server (\<instance name>)] ，然後按一下 [重新啟動]，先停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 後再重新啟動。  
  
 設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接聽特定通訊埠之後，有三種方式可利用用戶端應用程式連接到特定通訊埠：  
  
-   執行伺服器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務，依名稱連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體。  
  
-   在用戶端上建立別名，指定通訊埠編號。  
  
-   設定用戶端使用自訂連接字串進行連接。  
  
## <a name="see-also"></a>另請參閱  
 [建立或刪除用戶端使用的伺服器別名 &#40;SQL Server 組態管理員&#41;](create-or-delete-a-server-alias-for-use-by-a-client.md)  
  
  
