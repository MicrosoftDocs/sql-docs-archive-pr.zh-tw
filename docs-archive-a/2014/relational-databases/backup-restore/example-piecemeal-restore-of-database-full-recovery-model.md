---
title: 範例：分次還原資料庫 (完整復原模式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- piecemeal restores [SQL Server], full recovery model
- restore sequences [SQL Server], piecemeal
ms.assetid: 0a84892d-2f7a-4e77-b2d0-d68b95595210
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5cfccccdbdc0c4fb3b189ee0a9fa3aeaf426578b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87704206"
---
# <a name="example-piecemeal-restore-of-database-full-recovery-model"></a>範例：分次還原資料庫 (完整復原模式)
  分次還原順序會在檔案群組層級，分階段地還原與復原資料庫，從主要檔案群組開始，然後才是所有可讀寫的次要檔案群組。  
  
 在此範例中，資料庫 `adb` 是在損毀之後還原至新的電腦。 資料庫使用完整復原模式，因此開始還原之前，必須對資料庫進行結尾記錄備份。 在損毀之前，所有檔案群組都在線上。 檔案群組 `B` 是唯讀的。 所有的次要檔案群組都必須還原，但是會依照重要性的高低順序來進行： `A` (最高)、 `C`，最後是 `B`。 這個範例有四個記錄備份，包括結尾記錄備份。  
  
## <a name="tail-log-backup"></a>結尾記錄備份  
 還原資料庫之前，資料庫管理員必須備份記錄的結尾。 因為資料庫已損毀，必須使用 NO_TRUNCATE 選項來建立結尾記錄備份：  
  
```  
BACKUP LOG adb TO tailLogBackup WITH NORECOVERY, NO_TRUNCATE  
```  
  
 結尾記錄備份是下列還原順序中套用的最後一個備份。  
  
## <a name="restore-sequences"></a>還原順序  
  
> [!NOTE]  
>  線上還原順序的語法和離線還原順序的語法相同。  
  
1.  部分還原主要與次要檔案群組 `A`。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='Primary' FROM backup1   
       WITH PARTIAL, NORECOVERY  
    RESTORE DATABASE adb FILEGROUP='A' FROM backup2   
       WITH NORECOVERY  
    RESTORE LOG adb FROM backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM backup4 WITH NORECOVERY  
    RESTORE LOG adb FROM backup5 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
2.  線上還原檔案群組 `C`。  
  
     此時，主要檔案群組和次要檔案群組 `A` 在線上。 檔案群組 `B` 與 `C` 的所有檔案已暫止復原，且檔案群組處於離線。  
  
     步驟 1 中最後一個 `RESTORE LOG` 陳述式的訊息指出因為無法使用檔案群組 `C` ，所以會延遲回復此檔案群組的交易。 一般作業可繼續進行，但在回復作業完成之前，這些交易會維持鎖定，且不會截斷記錄。  
  
     在第二個還原順序中，資料庫管理員會還原檔案群組 `C`：  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='C' FROM backup2a WITH NORECOVERY  
    RESTORE LOG adb FROM backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM backup4 WITH NORECOVERY  
    RESTORE LOG adb FROM backup5 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
     此時，主要與次要檔案群組 `A` 和 `C` 會在線上。 檔案群組 `B` 裡的檔案會保持復原暫止，而檔案群組為離線。 已解決延遲的交易，而且可以截斷記錄。  
  
3.  線上還原檔案群組 `B`。  
  
     在第三個還原順序中，資料庫管理員會還原檔案群組 `B`。 在檔案群組變成唯讀之後會進行檔案群組 `B` 的備份，因此不需要在復原期間將它向前復原。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup2b WITH RECOVERY  
    ```  
  
     所有檔案群組現在都已在線上。  
  
## <a name="additional-examples"></a>其他範例  
  
-   [範例：分次還原資料庫 &#40;簡單復原模式&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [範例：僅限於部分檔案群組的分次還原 &#40;簡單復原模式&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [範例：線上還原唯讀檔案 &#40;簡單復原模式&#41;](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [範例：僅限於部分檔案群組的分次還原 &#40;完整復原模式&#41;](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [範例：線上還原讀取/寫入檔案 &#40;完整復原模式&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [範例：線上還原唯讀檔案 &#40;完整復原模式&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [線上還原 &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [套用交易記錄備份 &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [分次還原 &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
