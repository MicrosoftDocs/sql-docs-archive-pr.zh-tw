---
title: 針對失敗的新增檔案作業進行疑難排解 (AlwaysOn 可用性群組) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- secondary databases [SQL Server], Availability Groups
- Availability Groups [SQL Server], troubleshooting
ms.assetid: 31ceaebf-864b-4dd0-9112-0d047b0316ad
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2551080c214f18473caa71a3e17797c34fcc943a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708630"
---
# <a name="troubleshoot-a-failed-add-file-operation-alwayson-availability-groups"></a>疑難排解失敗的加入檔案作業 (AlwaysOn 可用性群組)
  在某些 AlwaysOn 可用性群組部署中，在裝載主要複本的系統和裝載次要複本的系統之間會有檔案路徑差異。 如果加入檔案作業的檔案路徑不存在於次要複本，則加入檔案作業將會在主要資料庫上成功完成。 但是加入檔案作業會造成次要資料庫暫停。 而這又會導致次要複本進入 NOT SYNCHRONIZING 狀態。  
  
> [!NOTE]  
>  我們建議，給定次要資料庫的檔案路徑 (包括磁碟機代號) 盡可能與對應主要資料庫的路徑完全相同。  
  
## <a name="problem-resolution"></a>解決問題  
 若要解決此問題，資料庫擁有者必須完成以下步驟：  
  
1.  從可用性群組中移除次要資料庫。 如需詳細資訊，請參閱[將次要資料庫從可用性群組移除 &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)。  
  
2.  在現有次要資料庫上，使用 WITH NORECOVERY 和 WITH MOVE (指定裝載次要複本之伺服器執行個體上的檔案路徑)，將包含加入之檔案的檔案群組的完整備份還原到次要資料庫。 如需詳細資訊，請參閱[將資料庫還原到新位置 &#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)。  
  
3.  在主要伺服器上備份包含加入檔案作業的交易記錄，並且使用 WITH NORECOVERY 和 WITH MOVE 手動在次要資料庫上還原記錄備份。  
  
4.  透過使用 WITH NO RECOVERY 從主要資料庫還原任何其他未完成的記錄備份，準備次要資料庫重新加入可用性群組。  
  
5.  將次要資料庫重新加入可用性群組。 如需詳細資訊，請參閱 [將次要資料庫聯結至可用性群組 &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [針對可用性群組手動準備次要資料庫 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)   
 [孤立的使用者疑難排解 &#40;SQL Server&#41;](../../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)   
 [針對 AlwaysOn 可用性群組 Configuration &#40;SQL Server&#41;已刪除進行疑難排解](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
