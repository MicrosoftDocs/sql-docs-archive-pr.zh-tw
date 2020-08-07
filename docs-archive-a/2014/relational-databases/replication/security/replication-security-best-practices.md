---
title: 複寫安全性最佳做法 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], best practices
- security [SQL Server replication], between domains
- authentication [SQL Server replication]
- Internet [SQL Server replication], security
ms.assetid: 1ab2635d-0992-4c99-b17d-041d02ec9a7c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8e5918bfed52a6ed1befd81d2fdb7910062060e6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584379"
---
# <a name="replication-security-best-practices"></a>複寫安全性最佳做法
  複寫會移動分散式環境中的資料，範圍從單一網域上的企業內部網路，乃至於存取未受信任網域之間以及網際網路上資料的應用程式。 因此，了解在這些不同環境下保護複寫連接安全的最佳方法相當重要。  
  
 下列資訊與所有環境中的複寫相關：  
  
-   使用業界標準方法加密複寫拓撲中各電腦之間的連接，例如虛擬私人網路 (Virtual Private Networks，VPN)、安全通訊端層 (Secure Sockets Layer，SSL) 或 IP 安全性 (IPSEC)。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。 如需有關透過網際網路使用 VPN 與 SSL 複寫資料的資訊，請參閱＜ [Securing Replication Over the Internet](securing-replication-over-the-internet.md)＞。  
  
     如果使用 SSL 保護複寫拓撲中電腦之間的連接，請將每個複寫代理程式的 **-EncryptionLevel** 參數值指定為 **1** 或 **2** (建議使用 **2** 值)。 值 **1** 會指定使用加密，但代理程式不會確認 SSL 伺服器憑證是否由受信任簽發者簽署；值 **2** 則會指定對憑證進行確認。 可於代理程式設定檔和命令列中指定代理程式參數。 如需詳細資訊，請參閱  
  
    -   [處理複寫代理程式設定檔](../agents/replication-agent-profiles.md)  
  
    -   [檢視並修改複寫代理程式命令提示字元參數 &#40;SQL Server Management Studio&#41;](../agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../concepts/replication-agent-executables-concepts.md)  
  
-   以不同的 Windows 帳戶執行各複寫代理程式，並針對所有複寫代理程式連接使用 Windows 驗證。 如需指定帳戶的詳細資訊，請參閱[管理複寫的登入與密碼](identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)。  
  
-   僅對各代理程式授與必要的權限。 如需詳細資訊，請參閱＜ [Replication Agent Security Model](replication-agent-security-model.md)＞的「代理程式所需的權限」一節。  
  
-   確定發行集存取清單 (PAL) 中包含所有「合併代理程式」及「散發代理程式」。 如需詳細資訊，請參閱[保護發行者](secure-the-publisher.md)。  
  
-   僅允許 PAL 中的帳戶擁有執行複寫工作所需的權限，以遵守最低權限原則。 切勿將登入加入至複寫不需要的任何固定伺服器角色。  
  
-   設定快照集共用，以允許所有「合併代理程式」和「散發代理程式」擁有讀取權限。 在發行集的快照集擁有參數化篩選的情況下，務必確認各資料夾已設定為僅允許存取適當的「合併代理程式」帳戶。  
  
-   設定快照集共用，以允許「快照集代理程式」擁有寫入權限。  
  
-   如果您使用提取訂閱，請使用網路共用，而非使用快照集資料夾的本機路徑。  
  
 如果您的複寫拓撲包含不是位於相同網域中的電腦，或包含位於彼此之間沒有信任關係之網域中的電腦，可針對代理程式建立的連接使用 Windows 驗證或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證 (如需網域的詳細資訊，請參閱 Windows 說明文件)。 基於安全性最佳做法，建議您使用 Windows 驗證。  
  
-   使用 Windows 驗證：  
  
    -   在適當的節點 (在各節點使用相同名稱和密碼) 為各代理程式加入本機 Windows 帳戶 (並非網域帳戶)。 例如，發送訂閱的散發代理程式在散發者端執行，並且建立至散發者與訂閱者的連接。 「散發代理程式」的 Windows 帳戶應加入至「散發者」和「訂閱者」。  
  
    -   確認指定的代理程式 (例如，訂閱的「散發代理程式」) 會在每部電腦上以相同的帳戶執行。  
  
-   使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證：  
  
    -   在適當的節點 (在各節點使用相同帳戶名稱和密碼) 為各代理程式加入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 帳戶。 例如，發送訂閱的散發代理程式在散發者端執行，並且建立至散發者與訂閱者的連接。 「散發代理程式」的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 帳戶應加入至「散發者」和「訂閱者」。  
  
    -   確認指定的代理程式 (例如，訂閱的「散發代理程式」) 會在每部電腦上以相同的帳戶建立連接。  
  
    -   在需要 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證的情況下，通常無法存取 UNC 快照集共用 (例如，存取可能遭到防火牆封鎖)。 在這種情況下，您可以透過檔案傳輸通訊協定 (FTP) 將快照集傳送至「訂閱者」。 如需詳細資訊，請參閱[透過 FTP 傳送快照集](../transfer-snapshots-through-ftp.md)。  
  
## <a name="see-also"></a>另請參閱  
 [啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [透過網際網路的複寫](../replication-over-the-internet.md)   
 [保護訂閱者](secure-the-subscriber.md)   
 [保護散發者](secure-the-distributor.md)   
 [保護發行者](secure-the-publisher.md)   
 [SQL Server 複寫安全性](view-and-modify-replication-security-settings.md)  
  
  
