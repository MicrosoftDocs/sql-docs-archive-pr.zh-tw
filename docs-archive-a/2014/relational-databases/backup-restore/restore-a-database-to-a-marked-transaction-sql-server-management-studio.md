---
title: 還原資料庫至標示的交易 (SQL Server Management Studio) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restoretlog.markedtransaction.f1
helpviewer_keywords:
- database restores [SQL Server], marked transactions
- restoring databases [SQL Server], marked transactions
- marked transactions [SQL Server], restoring
ms.assetid: 8f0ea144-1819-4832-905f-e5d0f49b066b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8de9ef5bed389f020f14e60ccd99f39698e7110f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598469"
---
# <a name="restore-a-database-to-a-marked-transaction-sql-server-management-studio"></a>還原資料庫至標示的異動 (SQL Server Management Studio)
  當資料庫處於還原中狀態時，您可以利用 [還原交易記錄]  對話方塊，將資料庫還原成可用記錄備份中標示的交易。  
  
> [!NOTE]  
>  如需詳細資訊，請參閱[使用標示的交易以一致的方式復原相關資料庫 &#40;完整復原模式&#41;](use-marked-transactions-to-recover-related-databases-consistently.md) 和[復原包含標示之交易的相關資料庫](recovery-of-related-databases-that-contain-marked-transaction.md)。  
  
### <a name="to-restore-a-marked-transaction"></a>若要還原標示的交易  
  
1.  連線到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體之後，在物件總管中按一下伺服器名稱，以展開伺服器樹狀目錄。  
  
2.  展開 **[資料庫]** ，然後視資料庫而定，選取使用者資料庫，或者展開 **[系統資料庫]** 並選取一個系統資料庫。  
  
3.  以滑鼠右鍵按一下資料庫，指向 [工作]  ，然後按一下 [還原]  。  
  
4.  按一下 [交易記錄]  ，這會開啟 [還原交易記錄]  對話方塊。  
  
5.  在 [一般]  頁面的 [還原至]  區段中，選取 [標示的交易]  ，這會開啟 [選取標示的交易]  對話方塊。 這個對話方塊會顯示一個方格，其中列出在選取的交易記錄備份中，可用之標示的交易。  
  
     依預設，會還原到標示的交易，但是不含該交易。 若也要還原標示的交易，請選取 **[包含標示的交易]** 。  
  
     下表列出方格的各資料行標頭，並描述各標頭的值。  
  
    |頁首|值|  
    |------------|-----------|  
    |\<blank>|顯示選取標示的核取方塊。|  
    |**交易標示**|在認可交易時，由使用者所指定之標示交易的名稱。|  
    |**日期**|認可交易的日期和時間。 交易日期和時間是依照 **msdbgmarkhistory** 資料表中記錄的顯示，而非依照用戶端電腦的日期和時間。|  
    |**說明**|在認可交易時，由使用者所指定之標示交易的描述 (如果有的話)。|  
    |**LSN**|標示之交易的記錄序號。|  
    |**Database**|認可標示的交易之資料庫的名稱。|  
    |**使用者名稱**|認可標示的交易之資料庫使用者的名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [還原資料庫備份 &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)   
 [還原交易記錄備份 &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)  
  
  
