---
title: SQL Server 連線所需的 CDC 設計工具權限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 80334de2-17c1-43c9-951e-21a9f864e9cb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0815a5d8f1cb66dee0d290a45166ebb395c8efa8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585525"
---
# <a name="sql-server-connection-required-permissions-for-the-cdc-designer"></a>SQL Server 連接所需的 CDC 設計工具權限
  CDC 設計工具主控台需要與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之間的連接資訊，才能執行工作。 本主題描述可以在 **[連接到 SQL Server]** 對話方塊中提供的資訊，以便設定與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的連接。  
  
 必要時會開啟 **[連接到 SQL Server]** 對話方塊，例如當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接資訊無法取得時，或是當資訊存在但是連接沒有必要的權限時。  
  
 下表描述需要連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的各種工作以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入/使用者的必要權限。  
  
|Task|最低權限|  
|----------|-------------------------|  
|使用關聯的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體檢視 CDC 服務和執行個體的清單。|`db_datareader` 角色|  
|啟動/停止 CDC 執行個體|`db_datareader` 和 `db_datawriter` 角色|  
|檢視 CDC 執行個體狀態。|`db_owner` 角色|  
|建立新的 Oracle CDC 執行個體資料庫。|`dbcreator` 固定伺服器角色|  
|建立新的 Oracle CDC 執行個體。|`db_datareader` 角色<br /><br /> `db_owner` 角色。|  
|取得部署指令碼。|`db_datareader` 和 `db_datawriter` 角色<br /><br /> `db_owner` 角色|  
|變更組態及加入/移除擷取執行個體。|`db_datareader` 和 `db_datawriter` 角色<br /><br /> `db_owner` 角色|  
  
## <a name="see-also"></a>另請參閱  
 [存取 CDC 設計工具主控台](access-the-cdc-designer-console.md)   
 [用來建立執行個體的 SQL Server 連接](sql-server-connection-for-instance-creation.md)  
  
  
