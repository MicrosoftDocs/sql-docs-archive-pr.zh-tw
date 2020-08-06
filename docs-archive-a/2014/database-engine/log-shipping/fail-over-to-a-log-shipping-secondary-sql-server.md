---
title: 容錯移轉至記錄傳送次要 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- primary databases [SQL Server]
- secondary data files [SQL Server], manual fail over
- log shipping [SQL Server], failover
- failover [SQL Server], log shipping
ms.assetid: edfe5d59-4287-49c1-96c9-dd56212027bc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 164e2809e4eff5a14ef54124df7c7ca9077793ba
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87703250"
---
# <a name="fail-over-to-a-log-shipping-secondary-sql-server"></a>容錯移轉至記錄傳送次要 (SQL Server)
  如果主要伺服器執行個體失敗或需要維護，則容錯移轉至記錄傳送次要十分有用。  
  
## <a name="preparing-for-a-controlled-failover"></a>準備控制的容錯移轉  
 一般而言，因為主要資料庫的最新備份作業後仍會繼續更新該主要資料庫，所以主要和次要資料庫並不同步。 而且，在某些情況下，最近的交易記錄備份尚未複製到次要伺服器執行個體，或某些複製的記錄備份可能仍未套用至次要資料庫。 建議您，如果可能，請使用主要資料庫開始同步處理所有次要資料庫。  
  
 如需記錄傳送作業的相關資訊，請參閱 [關於記錄傳送 &#40;SQL Server&#41;](about-log-shipping-sql-server.md)。  
  
## <a name="failing-over"></a>容錯移轉  
 若要容錯移轉至次要資料庫：  
  
1.  將任何未複製的備份檔從備份共用複製到每個次要伺服器的複製目的資料夾。  
  
2.  依序將任何未套用的交易記錄備份套用到每個次要資料庫。 如需詳細資訊，請參閱[套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)。  
  
3.  如果可存取主要資料庫，則請備份使用中交易記錄，並將記錄備份套用到次要資料庫。  
  
     如果原始主要伺服器執行個體未損毀，請使用 WITH NORECOVERY 來備份主要資料庫的交易記錄結尾。 這樣會讓資料庫維持在還原中的狀態，所以無法提供給使用者使用。 最後，您將可從取代主要資料庫套用交易記錄備份，以向前復原這個資料庫。  
  
     如需詳細資訊，請參閱[套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)。  
  
4.  在同步處理次要伺服器後，您就可以透過復原次要資料庫並將用戶端重新導向至該伺服器執行個體，藉以容錯移轉至偏好的伺服器。 復原會讓資料庫進入一致狀態，並使其連線。  
  
    > [!NOTE]  
    >  當您讓次要資料庫可以使用時，就應該確保其中繼資料與原始主要資料庫的中繼資料一致。 如需詳細資訊，請參閱 [在另一個伺服器執行個體上提供可用的資料庫時，管理中繼資料 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)。  
  
5.  在復原次要資料庫後，您可以將它重新設定為當做其他次要資料庫的主要資料庫使用。  
  
     如果沒有其他次要資料庫可用，請參閱[設定記錄傳送 &#40;SQL Server&#41;](configure-log-shipping-sql-server.md)。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
  
-   [變更主要與次要記錄傳送伺服器間的角色 &#40;SQL Server&#41;](change-roles-between-primary-and-secondary-log-shipping-servers-sql-server.md)  
  
-   [角色切換後針對登入和作業進行管理 &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [記錄傳送資料表與預存程序](log-shipping-tables-and-stored-procedures.md)   
 [關於記錄傳送 &#40;SQL Server&#41;](about-log-shipping-sql-server.md)   
 [結尾記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)  
  
  
