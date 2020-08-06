---
title: 使用 IPv6 連接 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Internet Protocol
- IPv4
- IPv6
ms.assetid: 2669098c-f5f1-43da-aec6-e91003ac89f6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0f2ecd605f67446fade262cfe795f344dfb165c0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87704586"
---
# <a name="connecting-using-ipv6"></a>使用 IPv6 連接
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 完整支援網際網路通訊協定第 4 版 (IPv4) 與網際網路通訊協定第 6 版 (IPv6)。 當 Windows 是設定為 IPv6 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，元件會自動辨識 IPv6 的存在性。 不需要特殊的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態。  
  
 支援包括但不限於下列各項：  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 和其他伺服器元件可同時接聽 IPv4 和 IPv6 位址。 當 IPv4 和 IPv6 都出現時，您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員，來設定 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 只接聽 IPv4 位址或 IPv6 位址。  
  
-   當支援 IPv4 和 IPv6 的電腦上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務是在 IPv4 位址上接受查詢時，它的回應是將 IPv4 位址及第一個 IPv4 TCP 通訊埠列在其清單中。 在 IPv6 位址上接受查詢時，它的回應是將 IPv6 位址及第一個 IPv6 TCP 通訊埠列在其清單中。 若要避免不一致，我們建議 IPv4 和 IPv6 接聽程式設定為接聽相同通訊埠。  
  
-   像 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員之類的工具接受 IPv4 和 IPv6 格式的 IP 位址。 在大多數情況下，如果 \<*computer_name*> \\ < 使用伺服器主機名稱或完整功能變數名稱 (FQDN) 來指定*instance_name*>，則不需要修改連接字串。 如果伺服器電腦有 IPv4 和 IPv6，其主機名稱或 FQDN 將解析成多個 IP 位址，包括至少一個 IPv4 位址及多個 IPv6 位址。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 嘗試依照從 TCP/IP 接收的順序來使用這些 IP 位址建立連線，以及使用第一個成功的連線。 由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 無法預測順序，因此，這應該被視為隨機順序。 如果 IPv4 和 IPv6 位址都出現，則先嘗試使用 IPv4 位址。 此邏輯對 ODBC、OLE DB 或 ADO.NET 的使用者是透明化的。  
  
    > [!NOTE]  
    >  如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 未接聽 IPv4，在嘗試使用 IPv6 位址之前，嘗試建立的 IPv4 連接必須等到逾時。 若要避免發生此情形，請直接連接到 IPv6 IP 位址，或在具有 IPv6 位址的用戶端上設定別名。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)  
  
  
