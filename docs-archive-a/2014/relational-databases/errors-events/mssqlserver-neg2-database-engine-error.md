---
title: MSSQLSERVER_-2 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "2"
helpviewer_keywords:
- -2 (Database Engine error)
ms.assetid: f37a7b7d-26e1-4b9e-bcb4-57f7805393d2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5d39b4a11387a60056bba3f87adffcb2653b60f2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87701221"
---
# <a name="mssqlserver_-2"></a>MSSQLSERVER_-2
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|-2|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱||  
|訊息文字|已超過逾時的設定。  在作業完成前就已超過逾時期間，或是伺服器沒有回應。 (Microsoft SQL Server，錯誤: -2)|   
  
## <a name="explanation"></a>說明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端無法連接到伺服器。 發生這個錯誤可能是因為伺服器上的防火牆拒絕連接。 
  
## <a name="user-action"></a>使用者動作  
 確定已將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 伺服器執行個體上的防火牆設定成接受連線。  
  
## <a name="see-also"></a>另請參閱  
 [設定 Windows 防火牆以允許 SQL Server 存取](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)   
 [設定資料庫引擎存取的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [設定用戶端通訊協定](../../database-engine/configure-windows/configure-client-protocols.md)   
 [網路通訊協定和網路程式庫](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [用戶端網路組態](../../database-engine/configure-windows/client-network-configuration.md)   
 [設定用戶端通訊協定](../../database-engine/configure-windows/configure-client-protocols.md)   
 [啟用或停用伺服器網路通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
