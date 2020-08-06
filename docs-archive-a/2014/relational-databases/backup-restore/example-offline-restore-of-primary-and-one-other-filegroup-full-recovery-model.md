---
title: 範例：離線還原主要和另一個檔案群組 (完整復原模式) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- offline restores [SQL Server]
- restore sequences [SQL Server], offline
ms.assetid: 7d6c50eb-dc84-4d66-855a-0b5f1bd89737
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6f845927fdd74fba476139fccbf9a5fa112d434e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599522"
---
# <a name="example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model"></a>範例：離線還原主要檔案群組與另一個檔案群組 (完整復原模式)
  本主題僅與在完整復原模式下，包含多個檔案群組的資料庫有關。  
  
 在此範例中，名為 `adb` 的資料庫包含三個檔案群組。 檔案群組 `A` 和 `C` 可讀取/寫入，而檔案群組 `B` 則是唯讀的。 主要檔案群組和檔案群組 `B` 損毀，但檔案群組 `A` 和 `C` 完整無缺。 在損毀之前，所有檔案群組都在線上。  
  
 資料庫管理員決定還原並復原主要檔案群組和檔案群組 `B`。 資料庫使用完整復原模式，因此開始還原之前，必須對資料庫進行結尾記錄備份。 當資料庫上線時，檔案群組 `A` 和 `C` 會自動回到線上。  
  
> [!NOTE]  
>  離線還原順序的步驟比唯讀檔案的線上還原步驟少。 如需範例，請參閱[範例：線上還原唯讀檔案 &#40;完整復原模式&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)。 但是在還原順序期間，整個資料庫都會離線。  
  
## <a name="tail-log-backup"></a>結尾記錄備份  
 還原資料庫之前，資料庫管理員必須備份記錄的結尾。 因為資料庫已損毀，必須使用 NO_TRUNCATE 選項來建立結尾記錄備份：  
  
```  
BACKUP LOG adb TO tailLogBackup   
   WITH NORECOVERY, NO_TRUNCATE  
```  
  
 結尾記錄備份是下列還原順序中套用的最後一個備份。  
  
## <a name="restore-sequence"></a>還原順序  
 為了還原主要檔案群組和檔案群組 `B`，資料庫管理員會使用不含 PARTIAL 選項的還原順序，如下所示：  
  
```  
RESTORE DATABASE adb FILEGROUP='Primary' FROM backup1   
WITH NORECOVERY  
RESTORE DATABASE adb FILEGROUP='B' FROM backup2   
WITH NORECOVERY  
RESTORE LOG adb FROM backup3 WITH NORECOVERY  
RESTORE LOG adb FROM backup4 WITH NORECOVERY  
RESTORE LOG adb FROM backup5 WITH NORECOVERY  
RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
```  
  
 未還原的檔案會自動回到線上。 接著，所有檔案群組都會回到線上狀態。  
  
## <a name="see-also"></a>另請參閱  
 [線上還原 &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [分次還原 &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)   
 [檔案還原 &#40;完整復原模式&#41;](file-restores-full-recovery-model.md)   
 [套用交易記錄備份 &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
