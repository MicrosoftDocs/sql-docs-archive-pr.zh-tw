---
title: 手動容錯移轉資料庫鏡像工作階段 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- failover [SQL Server], database mirroring
- manual failover [SQL Server]
- database mirroring [SQL Server], failover
ms.assetid: 36218d61-b5f5-4194-905a-608e0e903db4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2c04ea4908ccbc4cfe4f6bb3606347dd444ef416
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592196"
---
# <a name="manually-fail-over-a-database-mirroring-session-transact-sql"></a>手動容錯移轉資料庫鏡像工作階段 (Transact-SQL)
  鏡像資料庫已同步處理時 (亦即，資料庫為 SYNCHRONIZED 狀態時)，資料庫擁有者可以初始化至鏡像伺服器的手動容錯移轉。 手動容錯移轉只能從主體伺服器中起始。  
  
### <a name="to-manually-fail-over-a-database-mirroring-session"></a>手動容錯移轉資料庫鏡像工作階段  
  
1.  連接到主體伺服器。  
  
2.  將資料庫內容設定為 **master** 資料庫：  
  
     `USE master;`  
  
3.  在主體伺服器上發出下列陳述式：  
  
     [ALTER DATABASE 資料庫名稱](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring) ** SET PARTNER FAILOVER，其中「資料庫名稱」** 是鏡像資料庫。  
  
     如此可將鏡像伺服器立即轉換為主體角色。  
  
 在先前的主體伺服器上，用戶端與資料庫的連接會中斷，進行中的交易則會回復。  
  
> [!NOTE]  
>  在容錯移轉發生時，凡是已利用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器準備好但尚未認可的交易，都會在資料庫完成容錯移轉後視為已中止。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE 資料庫鏡像 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [手動故障切換資料庫鏡像會話 &#40;SQL Server Management Studio&#41;](manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)   
 [資料庫鏡像工作階段期間的角色切換 &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)  
  
  
